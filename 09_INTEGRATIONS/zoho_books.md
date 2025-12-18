# Zoho Books Integration Runbook

This document describes the integration with Zoho Books, which is used for invoicing and accounting.

## 1. Relationship with Zoho Billing

Zoho Books is tightly integrated with Zoho Billing. When a subscription in Zoho Billing generates an invoice, that invoice is automatically created in Zoho Books. This ensures that all billing and revenue data is accurately reflected in the accounting system.

## 2. Role of the Platform

The platform's role in relation to Zoho Books is primarily to:

-   Ensure that customer and subscription data is accurately passed to Zoho Billing, which then populates Zoho Books.
-   Provide a UI for customers to view their invoice history. This is done by fetching invoice data from the Zoho Books API.
-   Handle any necessary adjustments or credit notes, which are created in Zoho Books via the API and then reconciled with the customer's subscription in Zoho Billing.

## 3. API Integration

-   **Authentication**: The same OAuth 2.0 credentials used for Zoho Billing can be used to access the Zoho Books API, provided the necessary scopes (e.g., `ZohoBooks.invoices.READ`) were requested.
-   **Endpoints**: The primary endpoints used will be for fetching invoices and creating credit notes.

## 4. Invoice Viewing

When a user views their billing history in the platform, the application will:

1.  Fetch the list of invoices for the corresponding customer from the Zoho Books API.
2.  Display the key details of each invoice (date, amount, status).
3.  Provide a link to download the PDF version of the invoice, which is also retrieved from the Zoho Books API.
