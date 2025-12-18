# Real Estate Transaction Coordinator + Agent CRM - Documentation Pack

**Version:** 2.0
**Date:** December 18, 2025

## Introduction

Welcome to the complete technical design and implementation specification for the Real Estate Transaction Coordinator + Agent CRM platform. This documentation pack is intended for the AI developer agents at Google Antigravity who will be responsible for building, deploying, and maintaining the platform.

This is a living document that will be updated as the project evolves. It is the single source of truth for all technical aspects of the platform.

## How to Use This Documentation

This documentation is organized into a series of files, each covering a specific aspect of the system. It is recommended to start with this README and then proceed to the other documents as needed. The file structure is designed to be logical and easy to navigate.

## Core Principles

The development of this platform is guided by the following core principles:

-   **Automation First**: All customer-facing flows must be fully automated.
-   **Human-Governed Evolution**: Major changes require human review and approval.
-   **Compliance by Design**: The architecture must support SOC 2, ISO 27001, GDPR, and other relevant regulations from day one.
-   **Positive, Detail-Oriented UX**: The platform should provide a calm, clear, and low-friction user experience.
-   **Least Privilege & Defense-in-Depth**: Every component runs with the minimum necessary permissions.
-   **Jurisdiction & Regulation Awareness**: The AI agent must understand and respect local laws and regulations.

## Documentation Index

### Core Specifications
*   [00_README.md](00_README.md): This file, providing an overview and index of the documentation pack.
*   [01_PRD.md](01_PRD.md): The Product Requirements Document, which outlines the functional and non-functional requirements of the platform.
*   [03_SYSTEM_ARCHITECTURE.md](03_SYSTEM_ARCHITECTURE.md): A high-level overview of the system architecture.
*   [06_DATABASE_SCHEMA.md](06_DATABASE_SCHEMA.md): The complete database schema.
*   [07_RLS_AND_AUTHZ.md](07_RLS_AND_AUTHZ.md): Row-Level Security (RLS) and authorization model.
*   [08_API_SPEC_OPENAPI.yaml](08_API_SPEC_OPENAPI.yaml): The OpenAPI specification for all internal and external APIs.

### Integrations
*   [09_INTEGRATIONS/authorize_net.md](09_INTEGRATIONS/authorize_net.md): Authorize.Net Integration Runbook
*   [09_INTEGRATIONS/docusign.md](09_INTEGRATIONS/docusign.md): DocuSign Integration Runbook
*   [09_INTEGRATIONS/email_gmail_outlook.md](09_INTEGRATIONS/email_gmail_outlook.md): Email (Gmail/Outlook) Integration Runbook
*   [09_INTEGRATIONS/facebook_messenger.md](09_INTEGRATIONS/facebook_messenger.md): Facebook Messenger & Instagram DM Integration Runbook
*   [09_INTEGRATIONS/listing_apis_and_aggregators.md](09_INTEGRATIONS/listing_apis_and_aggregators.md): Listing APIs and Aggregators Integration Runbook
*   [09_INTEGRATIONS/payments_and_reconciliation.md](09_INTEGRATIONS/payments_and_reconciliation.md): Payments and Reconciliation Runbook
*   [09_INTEGRATIONS/rets_mls.md](09_INTEGRATIONS/rets_mls.md): MLS Integration (RETS) Runbook
*   [09_INTEGRATIONS/sendgrid.md](09_INTEGRATIONS/sendgrid.md): SendGrid Integration Runbook
*   [09_INTEGRATIONS/website_widget.md](09_INTEGRATIONS/website_widget.md): Website Widget Integration Runbook
*   [09_INTEGRATIONS/whatsapp_meta.md](09_INTEGRATIONS/whatsapp_meta.md): WhatsApp Business API (Native Meta) Integration Runbook
*   [09_INTEGRATIONS/whatsapp_twilio_fallback.md](09_INTEGRATIONS/whatsapp_twilio_fallback.md): WhatsApp Business API (Twilio Fallback) Integration Runbook
*   [09_INTEGRATIONS/zoho_billing.md](09_INTEGRATIONS/zoho_billing.md): Zoho Billing Integration Runbook
*   [09_INTEGRATIONS/zoho_books.md](09_INTEGRATIONS/zoho_books.md): Zoho Books Integration Runbook
*   [09_INTEGRATIONS/zoho_crm_and_tagging.md](09_INTEGRATIONS/zoho_crm_and_tagging.md): Zoho CRM and Tagging Integration Runbook
*   [09_INTEGRATIONS/zoho_desk_ticketing.md](09_INTEGRATIONS/zoho_desk_ticketing.md): Zoho Desk Ticketing Integration Runbook

### AI System
*   [10_AI_SYSTEM/ai_overview.md](10_AI_SYSTEM/ai_overview.md): An overview of the AI architecture.
*   [10_AI_SYSTEM/lifecycle_automation_agent.md](10_AI_SYSTEM/lifecycle_automation_agent.md): Lifecycle Automation Agent
*   [10_AI_SYSTEM/prompt_library.md](10_AI_SYSTEM/prompt_library.md): A complete prompt library for all agents.

### Security & Compliance
*   [11_SECURITY_COMPLIANCE/fair_housing_and_nondiscrimination.md](11_SECURITY_COMPLIANCE/fair_housing_and_nondiscrimination.md): Fair Housing and Nondiscrimination Policy
*   [11_SECURITY_COMPLIANCE/gdpr_and_data_subject_rights.md](11_SECURITY_COMPLIANCE/gdpr_and_data_subject_rights.md): GDPR and Data Subject Rights
*   [11_SECURITY_COMPLIANCE/iso27001_mapping.md](11_SECURITY_COMPLIANCE/iso27001_mapping.md): ISO 27001 Control Mapping
*   [11_SECURITY_COMPLIANCE/security_baseline.md](11_SECURITY_COMPLIANCE/security_baseline.md): A threat model, security baseline.
*   [11_SECURITY_COMPLIANCE/soc2_control_mapping.md](11_SECURITY_COMPLIANCE/soc2_control_mapping.md): Control mappings for SOC 2.
*   [11_SECURITY_COMPLIANCE/threat_model.md](11_SECURITY_COMPLIANCE/threat_model.md): Threat Model

### Development & Deployment
*   [12_DEV_GUIDES/local_setup.md](12_DEV_GUIDES/local_setup.md): Guides for local setup.
*   [12_DEV_GUIDES/repo_structure.md](12_DEV_GUIDES/repo_structure.md): Repository structure.
*   [13_DEPLOYMENT/environments_and_secrets.md](13_DEPLOYMENT/environments_and_secrets.md): Environments and Secrets Management
*   [13_DEPLOYMENT/rollback_strategy.md](13_DEPLOYMENT/rollback_strategy.md): Rollback Strategy
*   [13_DEPLOYMENT/supabase_migrations.md](13_DEPLOYMENT/supabase_migrations.md): Supabase Migrations Guide
*   [13_DEPLOYMENT/vercel_deploy.md](13_DEPLOYMENT/vercel_deploy.md): Vercel Deployment Guide

### Roadmap & Runbooks
*   [16_ROADMAP/phased_rollout_plan.md](16_ROADMAP/phased_rollout_plan.md): Phased Rollout Plan
*   [17_RUNBOOKS/integration_failures.md](17_RUNBOOKS/integration_failures.md): Integration Failures Runbook
*   [17_RUNBOOKS/ops_daily_weekly.md](17_RUNBOOKS/ops_daily_weekly.md): Daily and Weekly Operations Runbook
*   [17_RUNBOOKS/self_check_self_heal.md](17_RUNBOOKS/self_check_self_heal.md): Self-Check and Self-Heal Runbook
*   [17_RUNBOOKS/support_escalation_to_zoho_desk.md](17_RUNBOOKS/support_escalation_to_zoho_desk.md): Support Escalation to Zoho Desk Runbook
