# Zoho Desk Ticketing Integration Runbook

This document describes the integration with Zoho Desk for managing customer support escalations.

## 1. Architectural Role

The primary support channel for users is the AI Support Agent within the platform. Human involvement is an exception path. When the AI agent determines it cannot resolve an issue, it must escalate the case by creating a ticket in Zoho Desk.

## 2. Workflow: AI to Human Escalation

1.  **Escalation Trigger**: The AI Support Agent identifies a situation that requires human intervention (e.g., a complex technical issue, a billing dispute, a user explicitly requesting to speak to a human).
2.  **Context Gathering**: The AI agent gathers the full context of the conversation, including the user's details, the history of the issue, and any troubleshooting steps already taken.
3.  **Ticket Creation**: The platform calls the Zoho Desk API to create a new ticket.
4.  **Data Population**: The API call populates the ticket with:
    -   **Contact**: The ticket is associated with the correct Zoho CRM contact by using the canonical ID mapping.
    -   **Subject**: A clear and concise summary of the issue.
    -   **Description**: The full conversational context and a summary of the problem.
    -   **Classification**: The ticket is categorized (e.g., "Billing," "Technical") and prioritized.
5.  **User Notification**: The user is informed that a support ticket has been created and that a human agent will follow up with them.

## 3. API Integration

-   **Authentication**: The integration uses the same OAuth 2.0 credentials as the other Zoho services, with the `ZohoDesk.tickets.CREATE` scope.
-   **Endpoint**: The `POST /api/v1/tickets` endpoint in the Zoho Desk API is used to create tickets.

## 4. Importance of Context

It is critical that the full context of the issue is passed to Zoho Desk. This prevents the human agent from having to ask the customer to repeat information, leading to a more efficient and positive support experience.
