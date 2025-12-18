# Threat Model

This document outlines the threat model for the Real Estate Transaction Coordinator + Agent CRM platform, following the STRIDE methodology.

## STRIDE Threat Model

| Threat Category | Description | Scenario | Mitigation | 
|---|---|---|---|
| **Spoofing** | An attacker impersonates a legitimate user or system component. | An attacker spoofs the identity of an agent to gain access to their data. | - Strong authentication (Supabase Auth with MFA)
- RLS policies to enforce data access rules | 
| **Tampering** | An attacker modifies data in transit or at rest. | An attacker intercepts and modifies a document being sent for signature. | - TLS for all data in transit
- Digital signatures on documents (DocuSign)
- Immutable audit logs | 
| **Repudiation** | An attacker denies having performed an action. | An agent denies having sent a document or approved a change. | - Comprehensive and immutable audit logs for all key actions
- Digital signatures with a clear audit trail (DocuSign) | 
| **Information Disclosure** | An attacker gains access to sensitive information. | A vulnerability in an Edge Function exposes customer PII from the chatbot conversations. | - RLS to enforce data isolation
- Encryption of sensitive data at rest and in transit
- Principle of least privilege for all system components
- Regular vulnerability scanning | 
| **Denial of Service (DoS)** | An attacker makes a system or service unavailable to legitimate users. | An attacker floods the chatbot webhook with requests, overwhelming the system. | - Rate limiting on all public-facing API endpoints and webhooks
- Auto-scaling infrastructure (Vercel and Supabase)
- Web Application Firewall (WAF) | 
| **Elevation of Privilege** | An attacker gains higher-level permissions than they are authorized for. | A user finds a flaw in the RLS policies that allows them to access data from another team. | - Rigorous testing of RLS policies
- Regular security code reviews
- Principle of least privilege | 
