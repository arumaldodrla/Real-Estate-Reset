# Authorize.Net Integration Runbook

This document details the integration with Authorize.Net for credit card processing.

## 1. Primary Integration via Zoho Billing

- **Default Approach**: The primary method for processing payments is through the integration between Zoho Billing and Authorize.Net. The platform initiates payment actions (e.g., creating a subscription, processing an invoice) via the Zoho Billing API, and Zoho Billing handles the communication with Authorize.Net.
- **Benefits**: This approach simplifies PCI compliance, as the platform does not directly handle or store sensitive credit card information.

## 2. Optional Direct Integration

- **Use Case**: A direct integration with Authorize.Net may be implemented for specific use cases not supported by the Zoho Billing integration, or as a future enhancement.
- **Implementation**: If a direct integration is built, it must use Authorize.Net's Accept.js or Accept Hosted solution to ensure that sensitive cardholder data is not transmitted through the platform's servers, thus maintaining PCI compliance.
- **Feature Flag**: The direct integration will be controlled by a feature flag.

## 3. API Credentials

- **Authorize.Net**: The integration requires an API Login ID and a Transaction Key from the Authorize.Net Merchant Interface. These are stored securely in Supabase Secrets.
- **Zoho Billing**: The connection between Zoho Billing and Authorize.Net is configured within the Zoho Billing settings.

## 4. Reconciliation

- Regardless of the integration method, the platform must have a reconciliation process to ensure that the subscription and invoice status in the platform's database matches the state in Zoho Billing and Zoho Books.
- Webhooks from Zoho Billing will be used to receive real-time updates on payment status.
