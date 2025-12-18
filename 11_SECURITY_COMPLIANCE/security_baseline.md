# Security Baseline

This document defines the minimum security controls and best practices that must be implemented across the platform.

## 1. Data Classification

- **Public**: General property listings, marketing materials.
- **Internal**: Agent/brokerage configs, chatbot rules, analytics.
- **Confidential**: Customer conversations, PII, transaction records, financial data.

## 2. Access Control

- **Least Privilege**: All users and system components must operate with the minimum level of permissions required to perform their functions.
- **Role-Based Access Control (RBAC)**: Access to data and functionality is controlled by the user's role (e.g., `agent`, `team_admin`).
- **Multi-Factor Authentication (MFA)**: MFA must be enforced for all users accessing the platform.

## 3. Data Protection

- **Encryption in Transit**: All network communication must be encrypted using TLS 1.2 or higher.
- **Encryption at Rest**: All sensitive data stored in the database must be encrypted.
- **PII Handling**: Personally Identifiable Information (PII) must be handled with extreme care. Customer identities in the chatbot system are to be hashed, and the system should never store sensitive information like social security numbers.

## 4. API Key Security

- **Isolation**: API keys for each integration must be stored securely in Supabase Secrets and isolated from each other.
- **Limited Scope**: Edge Functions that use API keys must run with the minimum necessary scope.
- **No Logging**: API keys must never be logged or exposed in error messages.

## 5. Secure Development

- **Code Reviews**: All code changes must be reviewed for security vulnerabilities before being merged.
- **Vulnerability Scanning**: The application and its dependencies must be regularly scanned for known vulnerabilities.
- **Secret Management**: All secrets (API keys, passwords, tokens) must be stored in a secure secret management system (Supabase Secrets, Vercel Environment Variables) and never hard-coded in the source code.
