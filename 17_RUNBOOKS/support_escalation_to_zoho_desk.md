# Support Escalation to Zoho Desk Runbook

This document outlines the process for handling support escalations from the AI Support Agent to the human support team via Zoho Desk.

## 1. Escalation Triggers

The AI Support Agent will escalate a conversation to a human agent under the following conditions:

-   The user explicitly requests to speak to a human (e.g., "talk to a person," "I need more help").
-   The AI agent fails to understand the user's query after multiple attempts.
-   The user is expressing a high level of frustration or anger.
-   The user's issue is outside the scope of the AI agent's knowledge base (e.g., a complex billing issue, a legal question).

## 2. Escalation Process

```mermaid
sequenceDiagram
    participant User
    participant AISupportAgent as AI Support Agent
    participant AutomationAgent as Lifecycle Automation Agent
    participant ZohoDesk as Zoho Desk API

    User->>AISupportAgent: Expresses need for human help
    AISupportAgent->>AISupportAgent: Identifies escalation trigger
    AISupportAgent->>User: "I'm creating a ticket for our human support team."
    AISupportAgent->>AutomationAgent: Initiate escalation with conversation context
    AutomationAgent->>AutomationAgent: Retrieve user's Zoho Contact ID
    AutomationAgent->>ZohoDesk: Create Ticket (POST /api/v1/tickets)
    ZohoDesk-->>AutomationAgent: Return new ticket ID
    AutomationAgent-->>AISupportAgent: Confirm ticket creation
    AISupportAgent->>User: "Your ticket number is #12345. Our team will be in touch."
```

## 3. Data Integrity

-   **Full Context**: It is critical that the full context of the conversation with the AI agent is included in the Zoho Desk ticket description. This allows the human agent to understand the issue without asking the user to repeat themselves.
-   **Contact Association**: The ticket must be correctly associated with the user's contact record in Zoho CRM. This is achieved by using the canonical ID mapping to find the user's `zoho_contact_id`.

## 4. Monitoring

-   The number of escalations to Zoho Desk is a key metric for the performance of the AI Support Agent. A high escalation rate may indicate that the AI agent's knowledge base needs to be improved or that there are recurring issues with the platform.
