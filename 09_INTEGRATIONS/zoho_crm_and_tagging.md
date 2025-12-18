# Zoho CRM and Tagging Integration Runbook

This document outlines the integration with Zoho CRM, which serves as the central repository for all customer data.

## 1. Data Flow

- **Unidirectional Sync**: The data flow is primarily one-way: from the platform to Zoho CRM. The platform is the system of engagement, and Zoho CRM is the system of record for customer information.
- **Events**: Key events in the customer lifecycle within the platform trigger updates in Zoho CRM.

## 2. Core Workflows

- **New User Signup**: When a new user signs up for a trial, a new **Contact** and **Account** are created in Zoho CRM.
- **Subscription Activation**: When a user subscribes to a paid plan, a **Deal** is created and associated with their account. The deal is updated as the subscription progresses through its lifecycle.
- **Customer Data Updates**: Any changes to the user's profile in the platform are synced to the corresponding contact in Zoho CRM.

## 3. Tagging Taxonomy

A crucial part of the Zoho CRM integration is a well-defined tagging taxonomy. Tags are used to segment customers and to drive automated workflows within the Zoho ecosystem. The following tagging structure will be implemented:

- **Lifecycle Stage**: `lifecycle-trial`, `lifecycle-active`, `lifecycle-churned`
- **Plan Tier**: `plan-base`, `plan-plus`, `plan-pro`
- **Lead Source**: `source-website`, `source-whatsapp`, `source-referral`
- **Compliance Flags**: `compliance-gdpr`, `compliance-ccpa`

## 4. API Integration

- **Authentication**: The integration uses the same OAuth 2.0 credentials as the other Zoho services.
- **Endpoints**: The integration will use the Zoho CRM API to create and update contacts, accounts, and deals, and to manage tags.

## 5. Canonical ID Mapping

To ensure data integrity, the platform will maintain a mapping of its internal user ID to the Zoho CRM `contact_id` and `account_id`. This mapping is essential for all cross-system workflows, such as creating a Zoho Desk ticket for a CRM contact.
