# Integration Failures Runbook

This document provides a guide for diagnosing and resolving common failures with third-party integrations.

## 1. General Troubleshooting Steps

1.  **Check the Logs**: The first step for any integration failure is to check the logs in the observability platform. Look for error messages, status codes, and trace IDs related to the failing integration.
2.  **Check the External Service Status**: Check the status page of the third-party service (e.g., Supabase, Vercel, Zoho, DocuSign) to see if they are experiencing a system-wide outage.
3.  **Verify API Credentials**: Ensure that the API keys and other credentials for the service are correct and have not expired.

## 2. Specific Integration Scenarios

### MLS/RETS Sync Failure

-   **Symptom**: Properties are not being updated from an MLS provider.
-   **Diagnosis**:
    -   Check the logs for the `rets_sync_worker` function for error messages.
    -   Common errors include authentication failures (invalid credentials) or network connectivity issues.
-   **Resolution**:
    -   If it is an authentication failure, work with the brokerage admin to verify and update their RETS credentials.
    -   If it is a network issue, check the Supabase network status and the RETS server's availability.

### WhatsApp/Facebook Message Delivery Failure

-   **Symptom**: Messages are not being sent or received via WhatsApp or Facebook Messenger.
-   **Diagnosis**:
    -   Check the `message_queue` table for messages with a `failed` status.
    -   Check the logs for the `whatsapp-webhook` or `facebook-webhook` functions for errors.
    -   Check the Meta Business Suite for any alerts or issues with the WhatsApp Business Account or Facebook Page.
-   **Resolution**:
    -   Common issues include an expired access token, incorrect webhook configuration, or a violation of the platform's policies.
    -   Follow the error messages in the logs and the guidance in the Meta developer documentation to resolve the issue.

### Zoho API Failures

-   **Symptom**: Customer data is not being synced to Zoho CRM, or subscriptions are not being created in Zoho Billing.
-   **Diagnosis**:
    -   Check the logs for the relevant Edge Function (e.g., `create-zoho-contact`) for API error responses from Zoho.
-   **Resolution**:
    -   Common errors include invalid OAuth tokens, incorrect API endpoint usage, or data validation errors.
    -   Refresh the OAuth token if it has expired.
    -   Consult the Zoho API documentation to correct any issues with the API request.
