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
