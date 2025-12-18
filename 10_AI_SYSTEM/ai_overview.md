# AI System Overview

This document provides a high-level overview of the AI systems and components within the platform. The AI capabilities are central to the product's value proposition, powering everything from the customer-facing property recommendation agent to the internal support and automation agents.

## 1. Core AI Components

### AI Property Agent

-   **Purpose**: A customer-facing chatbot that provides property recommendations and market guidance.
-   **Technology**: Powered by a Large Language Model (LLM) such as Gemini or Claude, combined with a vector search over the property database (`pgvector`).
-   **Key Features**:
    -   Natural Language Understanding (NLU) of user queries.
    -   Semantic search for properties based on conversational input.
    -   Application of regulatory and jurisdictional filters to ensure compliant recommendations.
    -   Multi-channel deployment (WhatsApp, Facebook Messenger, Instagram DM, Website Widget).

### AI Support Agent

-   **Purpose**: An internal, coordinator-facing AI assistant that provides in-app support and access to a knowledge base.
-   **Technology**: An LLM-powered agent that is trained on the platform's documentation and can answer questions about its features and functionality.
-   **Key Features**:
    -   Context-aware assistance.
    -   Escalation path to a human support agent via Zoho Desk integration.

### Email/Document Intelligence

-   **Purpose**: To automate the processing of emails and documents related to real estate transactions.
-   **Technology**: Uses an LLM (Gemini or Claude) to classify emails and documents, and to extract key entities (dates, names, amounts).
-   **Key Features**:
    -   Automated document sorting and filing.
    -   Extraction of data to populate transaction fields and create deadlines.

## 2. AI Principles

-   **Human-in-the-Loop**: While the AI agents are designed to be autonomous, there are clear escalation paths for human intervention, particularly for complex or sensitive issues.
-   **Compliance by Design**: The AI systems are built with a strong emphasis on regulatory compliance, including fair housing laws and data privacy regulations.
-   **Transparency**: The AI agents are transparent about their capabilities and limitations, and they clearly disclose when a user is interacting with an AI.
