# Daily and Weekly Operations Runbook

This document outlines the daily and weekly operational tasks required to maintain the health and performance of the platform. Many of these tasks are designed to be automated.

## 1. Daily Operations

### Automated Checks

- **Integration Health**: A scheduled job runs daily to check the status of all third-party integrations.
  - **MLS/RETS Sync**: Verify that all configured MLS syncs have completed successfully in the last 24 hours.
  - **API Sync**: Verify that all third-party listing API syncs have completed successfully.
  - **Zoho API**: Make a test call to the Zoho API to ensure connectivity.
  - **AI Model Availability**: Make a test call to the Gemini/Claude APIs.
- **Message Queue backlog**: Monitor the `message_queue` table for any messages that have been in a `pending` state for an unusually long time. Alert if the backlog exceeds a defined threshold.

### Manual Review

- **Failed Jobs**: Review any failed jobs from the previous day (e.g., RETS syncs, enrichment tasks) and manually retry them if necessary.
- **Support Escalations**: Review the new tickets created in Zoho Desk to identify any recurring issues or platform-wide problems.

## 2. Weekly Operations

### Automated Checks

- **Weekly Self-Check**: The comprehensive weekly self-check job runs, as defined in the `self_check_self_heal.md` runbook. This includes checks for data freshness, embedding quality, and regulation database sync.

### Manual Review

- **Performance Metrics**: Review the key performance indicators (KPIs) for the platform from the observability dashboards.
  - Chatbot response times
  - API endpoint latencies
  - Database query performance
- **Security and Compliance**: Review security logs and audit trails for any suspicious activity.
- **Chatbot Analytics**: Review the chatbot analytics dashboard to understand user query patterns, identify common points of failure, and look for opportunities to improve the AI's responses and intents.
