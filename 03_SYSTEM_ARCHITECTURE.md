# 03. System Architecture

This document provides a high-level overview of the system architecture using the C4 model. It includes context and container diagrams to illustrate the system's components and their interactions.

## C4 Model: Level 1 - System Context Diagram

This diagram shows the system in its environment, including the key user personas and external systems it interacts with.

```mermaid
C4Context
  title System Context Diagram for Real Estate AI Platform

  Person(tc, "Transaction Coordinator")
  Person(agent, "Real Estate Agent")
  Person(customer, "End Customer")
  Person(admin, "System Administrator")

  System_Ext(mls, "MLS (RETS)")
  System_Ext(listing_apis, "Listing APIs", "Zillow, Redfin, etc.")
  System_Ext(zoho, "Zoho Ecosystem", "CRM, Billing, Books, Desk")
  System_Ext(docusign, "DocuSign")
  System_Ext(authnet, "Authorize.Net")
  System_Ext(llm, "AI/LLM Services", "Gemini, Claude")
  System_Ext(social, "Social Messaging", "WhatsApp, Facebook, Instagram")

  System(platform, "Real Estate AI Platform", "The complete system")

  Rel(tc, platform, "Manages transactions and documents")
  Rel(agent, platform, "Manages CRM, properties, and chatbot config")
  Rel(customer, platform, "Interacts with AI Property Agent")
  Rel(admin, platform, "Administers and monitors the system")

  Rel(platform, mls, "Syncs property data via RETS")
  Rel(platform, listing_apis, "Syncs property data via APIs")
  Rel(platform, zoho, "Syncs customer, billing, and support data")
  Rel(platform, docusign, "Sends documents for eSignature")
  Rel(platform, authnet, "Processes payments via Zoho")
  Rel(platform, llm, "Powers AI agents and classification")
  Rel(platform, social, "Sends and receives messages")
```

## C4-Model: Level 2 - Container Diagram

This diagram zooms into the system, showing the high-level containers (applications and data stores) that make up the platform.

```mermaid
C4Container
  title Container Diagram for Real Estate AI Platform

  Person(tc, "Transaction Coordinator")
  Person(agent, "Real Estate Agent")
  Person(customer, "End Customer")

  System_Ext(mls, "MLS (RETS)")
  System_Ext(listing_apis, "Listing APIs")
  System_Ext(zoho, "Zoho Ecosystem")
  System_Ext(llm, "AI/LLM Services")
  System_Ext(social, "Social Messaging")

  System_Boundary(platform, "Real Estate AI Platform") {
    Container(frontend, "Frontend Web App", "React, Refine, Tailwind", "The user-facing application hosted on Vercel")
    ContainerDb(db, "Database", "Supabase PostgreSQL + pgvector", "Stores all core data, including properties, users, and conversations")
    Container(api, "Backend API", "Supabase Edge Functions", "Provides the core business logic, webhook handling, and integrations")
  }

  Rel(tc, frontend, "Uses")
  Rel(agent, frontend, "Uses")
  Rel(customer, social, "Sends/Receives Messages")

  Rel(frontend, api, "Makes API calls to", "HTTPS")
  Rel(api, db, "Reads from and writes to", "PostgreSQL Protocol")

  Rel(api, mls, "Syncs properties from")
  Rel(api, listing_apis, "Syncs properties from")
  Rel(api, zoho, "Syncs data with")
  Rel(api, llm, "Calls for AI capabilities")
  Rel(api, social, "Integrates with")
```


## C4-Model: Level 3 - Component Diagram (Backend API)

This diagram breaks down the `Backend API` container into its key components, which are implemented as Supabase Edge Functions.

```mermaid
C4Component
  title Component Diagram for Backend API

  Container(frontend, "Frontend Web App")
  ContainerDb(db, "Database")
  System_Ext(social, "Social Messaging APIs")
  System_Ext(llm, "AI/LLM Services")
  System_Ext(mls, "MLS/RETS Service")

  System_Boundary(api, "Backend API (Supabase Edge Functions)") {
    Component(auth_handler, "Auth Handler", "Deno/TypeScript", "Handles user authentication and JWT validation")
    Component(webhook_handler, "Webhook Handler", "Deno/TypeScript", "Receives incoming webhooks from social channels (WhatsApp, etc.)")
    Component(message_orchestrator, "Message Orchestrator", "Deno/TypeScript", "Routes incoming messages to the AI Property Agent")
    Component(ai_agent, "AI Property Agent", "Deno/TypeScript", "Processes queries, performs vector search, and generates responses")
    Component(property_ingestor, "Property Ingestor", "Deno/TypeScript", "Scheduled function to sync properties from MLS/APIs")
    Component(zoho_sync, "Zoho Sync", "Deno/TypeScript", "Syncs data with Zoho CRM, Billing, and Desk")
  }

  Rel(frontend, auth_handler, "Authenticates user")
  Rel(social, webhook_handler, "Sends incoming messages")
  Rel(webhook_handler, message_orchestrator, "Forwards message for processing")
  Rel(message_orchestrator, ai_agent, "Invokes agent to handle query")
  Rel(ai_agent, db, "Reads property data and vector embeddings")
  Rel(ai_agent, llm, "Calls for NLU and response generation")
  Rel(ai_agent, social, "Sends response back to user")
  Rel(property_ingestor, mls, "Fetches new listings")
  Rel(property_ingestor, db, "Writes property data and embeddings")
  Rel(api, zoho_sync, "Syncs data periodically")
```

## Sequence Diagram: AI Chatbot Interaction

This diagram illustrates the sequence of events when an end customer sends a message to the AI Property Agent.

```mermaid
sequenceDiagram
    participant C as End Customer
    participant SM as Social Messaging API
    participant WH as Webhook Handler
    participant MO as Message Orchestrator
    participant AIA as AI Property Agent
    participant DB as Database (Supabase)
    participant LLM as AI/LLM Service

    C->>SM: Sends message ("I'm looking for a 3-bed in Austin")
    SM->>WH: POST /webhook
    WH->>MO: Forward message
    MO->>AIA: ProcessQuery(message)
    AIA->>LLM: 1. Extract Intent & Entities
    LLM-->>AIA: { intent: 'property_search', entities: { beds: 3, city: 'Austin' } }
    AIA->>DB: 2. Vector Search for properties
    DB-->>AIA: Return matching properties
    AIA->>LLM: 3. Generate Response with properties & compliance notes
    LLM-->>AIA: Formatted response text
    AIA->>SM: Send reply message
    SM-->>C: Delivers message to customer
```
