# Self-Check and Self-Heal Runbook

This document describes the platform's automated self-check and self-healing capabilities, designed to ensure system stability and to automatically resolve minor issues without human intervention.

## 1. Weekly Self-Check

A Supabase Scheduled Function (`weekly_self_check`) runs once a week to perform a comprehensive health check of the system. The results of the check are logged, and alerts are sent for any issues that require manual review.

### Checks Performed:

- **Property Data Freshness**: Verifies that all active MLS and API property syncs have run successfully within the last 7 days.
- **Embedding Quality**: Samples a random set of properties to ensure that their vector embeddings are valid and non-zero. If any embeddings are missing, it triggers a job to regenerate them.
- **Regulation Database Sync**: Checks that the `regulations` table has entries for all jurisdictions where agents are currently operating. It flags any new jurisdictions that have been added but do not yet have corresponding regulation data.
- **AI Model Availability**: Makes a simple test call to the configured LLM APIs (Gemini/Claude) to verify connectivity.
- **Channel Health**: Performs a basic health check on the communication channels:
    - Attempts to send a test message via a test WhatsApp account.
    - Verifies that the Facebook and Instagram webhooks are responsive.
    - Checks that the website widget's JavaScript asset is loading correctly.

## 2. Self-Healing Actions

The system is authorized to perform a limited set of self-healing actions for minor issues.

- **Retry Failed Jobs**: Simple, transient failures in jobs like property enrichment or embedding generation will be automatically retried with an exponential backoff.
- **Regenerate Missing Embeddings**: If the self-check finds properties with missing embeddings, it will automatically queue them for regeneration.

## 3. Prohibited Self-Healing Actions

To ensure system stability and to adhere to the principle of human-governed evolution, the system is **prohibited** from taking the following self-healing actions:

- **Modifying Database Schema**: Any changes to the database schema must be done through a formal migration process by a developer agent.
- **Changing RLS Policies**: Any changes to Row-Level Security policies must be done manually.
- **Updating Production Code**: The system cannot modify its own code.
- **Making Major Configuration Changes**: Any significant changes to system configuration (e.g., switching the primary LLM provider) require human approval.
