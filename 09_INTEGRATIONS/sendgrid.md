# SendGrid Integration Runbook

This document outlines the integration with SendGrid for sending transactional emails.

## 1. Purpose

SendGrid is used to reliably send transactional emails to users, such as:

- Welcome emails
- Password reset instructions
- Notifications and reminders
- Invoices and billing alerts

## 2. Setup

1.  **SendGrid Account**: A SendGrid account is required.
2.  **API Key**: A SendGrid API key with mail-sending permissions is generated and stored securely in Supabase Secrets (`SENDGRID_API_KEY`).
3.  **Verified Sender**: The domain used for sending emails must be verified with SendGrid to ensure high deliverability.

## 3. Implementation

-   A helper function or service is created that abstracts the SendGrid API.
-   This function is used throughout the application wherever a transactional email needs to be sent.
-   Dynamic templates in SendGrid can be used for creating visually rich and personalized emails.

## 4. Webhooks

SendGrid webhooks can be configured to receive real-time feedback on email delivery, bounces, and opens. This data can be used for analytics and to improve email deliverability.

-   **Webhook URL**: A Supabase Edge Function is created to handle incoming webhook events from SendGrid.
-   **Events**: The platform can subscribe to events like `delivered`, `bounced`, `spam_report`, and `open`.
