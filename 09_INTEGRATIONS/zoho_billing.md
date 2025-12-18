# Zoho Billing Integration Runbook

This document details the integration with Zoho Billing, which serves as the system of record for all subscription and billing-related activities.

## 1. Architectural Principle: Platform is Primary

A core principle of this architecture is that the platform owns the customer-facing user experience. Customers manage their subscriptions, view invoices, and update payment methods within the platform's UI. Zoho Billing is treated as a back-office service, orchestrated via its API.

## 2. Authentication

-   **OAuth 2.0**: The integration uses OAuth 2.0 to authenticate with the Zoho Billing API.
-   **API Credentials**: A Client ID and Client Secret are obtained from the Zoho API Console and stored securely in Supabase Secrets.
-   **Tokens**: Access and refresh tokens are managed and stored securely by the platform.

## 3. Core Workflows

### Subscription Management

-   **Create Subscription**: When a user subscribes to a plan in the platform's UI, a corresponding subscription is created in Zoho Billing via the API. This includes the customer details, the plan, and any addons.
-   **Update Subscription**: Plan changes (upgrades, downgrades, cancellations) made in the platform UI are synced to Zoho Billing.
-   **Payment Method**: When a user adds or updates their payment method, the platform uses the Zoho Billing API to create or update the payment source, ensuring that sensitive payment information is handled by Zoho and not stored on the platform.

### Invoice and Payment Processing

-   **Invoice Generation**: Zoho Billing automatically generates invoices based on the subscription cycle.
-   **Payment Collection**: Zoho Billing attempts to collect payment using the configured payment gateway (Authorize.Net).
-   **Webhook Notifications**: The platform subscribes to Zoho Billing webhooks to receive real-time updates on invoice and payment status (e.g., `invoice.created`, `payment.success`, `payment.failed`). These updates are used to keep the platform's database in sync and to trigger other workflows (e.g., dunning emails).

## 4. Data Synchronization

-   **Canonical IDs**: The platform maintains a mapping between its internal user and subscription IDs and the corresponding IDs in Zoho Billing (e.g., `customer_id`, `subscription_id`).
-   **Reconciliation**: A regular reconciliation job runs to ensure data consistency between the platform and Zoho Billing, correcting any discrepancies that may have occurred due to webhook failures or other issues.
