# Lifecycle Automation Agent

This document describes the design and function of the Lifecycle Automation Agent, a system-level AI agent responsible for orchestrating the entire customer lifecycle, from trial to churn, by integrating with the Zoho ecosystem.

## 1. Core Responsibility

The primary responsibility of the Lifecycle Automation Agent is to ensure that all customer lifecycle events that occur within the platform are accurately and immediately reflected in the Zoho back-office systems (CRM, Billing, Books, Desk). It acts as the central orchestrator for all customer operations automation.

## 2. Architectural Role

The agent is implemented as a collection of event-driven Supabase Edge Functions. These functions are triggered by specific events within the platform, such as a user signing up, subscribing to a plan, or requesting support.

## 3. Key Workflows

### New User Onboarding

1.  **Trigger**: A new user completes the signup process in the platform.
2.  **Action**: The agent is triggered.
3.  **Orchestration**:
    -   Creates a new **Contact** and **Account** in Zoho CRM.
    -   Applies the `lifecycle-trial` and `source-website` tags to the new contact.
    -   Stores the returned `zoho_contact_id` and `zoho_account_id` in the platform's database, mapping them to the platform's `user_id`.

### Trial to Paid Conversion

1.  **Trigger**: A user on a trial plan subscribes to a paid plan through the platform's billing UI.
2.  **Action**: The agent is triggered.
3.  **Orchestration**:
    -   Creates a new **Subscription** in Zoho Billing, associated with the customer's `zoho_contact_id`.
    -   Zoho Billing automatically creates the first **Invoice** in Zoho Books and attempts to process the payment via Authorize.Net.
    -   The agent updates the contact's tags in Zoho CRM, removing `lifecycle-trial` and adding `lifecycle-active` and the appropriate plan tag (e.g., `plan-pro`).
    -   The `zoho_subscription_id` is stored in the platform's database.

### Support Escalation

1.  **Trigger**: The AI Support Agent determines that an issue requires human intervention.
2.  **Action**: The AI Support Agent invokes the Lifecycle Automation Agent's support escalation function.
3.  **Orchestration**:
    -   The agent creates a new **Ticket** in Zoho Desk.
    -   The ticket is automatically associated with the correct Zoho CRM contact using the stored `zoho_contact_id`.
    -   The ticket description is populated with the full context of the user's conversation with the AI Support Agent.

## 4. Canonical ID Mapping

A critical component of this system is the `user_integrations` table (or similar) in the platform's database. This table maintains the mapping between the platform's internal `user_id` and the various IDs from the Zoho ecosystem.

| platform_user_id | zoho_contact_id | zoho_account_id | zoho_subscription_id |
|---|---|---|---|
| `uuid` | `string` | `string` | `string` |

This table is the single source of truth for cross-system identity and is essential for the correct functioning of all automation workflows.
