# DocuSign Integration Runbook

This document describes the integration with the DocuSign eSignature API for managing and tracking electronic signatures on transaction documents.

## 1. Architecture

The integration allows users to send documents for signature directly from the platform and to receive real-time status updates on the signature process. The core of the integration is built around the DocuSign eSignature REST API.

## 2. Authentication

-   **OAuth 2.0 JWT Grant**: For system-level integration (e.g., sending documents on behalf of the platform or a brokerage), the JWT Grant flow will be used for authentication. This avoids the need for user interaction to authenticate.
-   **OAuth 2.0 Authorization Code Grant**: For actions performed directly by a user (e.g., sending a document from their own DocuSign account), the Authorization Code Grant flow will be used, which involves a user consent screen.
-   **API Credentials**: The integration requires a DocuSign Integration Key (client ID), a private key for the JWT grant, and a client secret. These are stored securely in Supabase Secrets.

## 3. Core Flows

### Sending a Document for Signature

1.  The user selects a document and the recipients within the platform.
2.  The platform creates an **Envelope** using the DocuSign API. The envelope defines the document, the recipients, and the signing locations (tabs).
3.  DocuSign sends emails to the recipients with a link to sign the document.

### Tracking Signature Status

-   **DocuSign Connect**: A webhook service (DocuSign Connect) is used to receive real-time updates on the envelope status (e.g., `Sent`, `Delivered`, `Signed`, `Completed`).
-   **Webhook URL**: A Supabase Edge Function is configured as the webhook listener.
-   The platform updates the status of the document and the transaction based on the notifications received from DocuSign.

## 4. Implementation Details

-   **Templates**: The integration will support the use of DocuSign templates to standardize the signature process for common document types.
-   **Embedded Signing**: For a more seamless user experience, the platform can use DocuSign's embedded signing feature, which allows recipients to sign documents within an iframe in the application, rather than being redirected to the DocuSign website.
