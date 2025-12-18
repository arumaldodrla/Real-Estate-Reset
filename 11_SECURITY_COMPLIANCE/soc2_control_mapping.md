# SOC 2 Control Mapping

This document maps the platform's security and operational controls to the Trust Services Criteria for SOC 2. It is intended to be a living document that will be updated as the platform evolves and undergoes formal SOC 2 audits.

## Control Mapping

| Trust Service Criteria | Criteria | Platform Control | Implementation Evidence |
|---|---|---|---|
| **Security** | CC1.1 - The entity has established a governance structure that provides oversight and accountability for the security program. | The platform has a defined security governance structure with clear roles and responsibilities. | - This documentation pack (specifically the Security & Compliance section)
- Defined roles for security oversight | 
| **Security** | CC6.1 - The entity has established logical access security measures to protect against unauthorized access. | - Role-Based Access Control (RBAC) is implemented via Supabase Auth.
- Multi-Factor Authentication (MFA) is enforced.
- Row-Level Security (RLS) policies are used to enforce data isolation. | - `07_RLS_AND_AUTHZ.md`
- Supabase Auth configuration
- RLS policies in the database schema | 
| **Security** | CC6.6 - The entity has established procedures to prevent or detect and act upon unauthorized or inappropriate use of the system. | - All key actions are logged to an immutable audit trail.
- Alerts are configured for suspicious activities. | - `audit_logs` table schema
- Alerting rules in the observability platform | 
| **Security** | CC7.1 - The entity has established procedures to protect against malware, viruses, and other malicious software. | - All code is scanned for vulnerabilities before deployment.
- The platform runs on a managed infrastructure (Vercel, Supabase) that includes protections against common threats. | - CI/CD pipeline configuration with vulnerability scanning step
- Vercel and Supabase security documentation | 
| **Availability** | A1.1 - The entity has established a process to manage the availability of the system and has established service-level agreements (SLAs) with its customers. | - The platform has a target uptime of 99.5%.
- The infrastructure is designed for high availability with auto-scaling and redundancy. | - `14_OBSERVABILITY/slos.md`
- Vercel and Supabase architecture documentation | 
| **Availability** | A1.2 - The entity has established procedures to protect against service disruptions due to system failures. | - The platform has a disaster recovery plan and a rollback strategy for deployments.
- Regular backups of the database are taken. | - `13_DEPLOYMENT/rollback_strategy.md`
- Supabase backup configuration | 
| **Confidentiality** | C1.1 - The entity has established procedures to identify and protect confidential information. | - Data is classified into Public, Internal, and Confidential categories.
- Confidential data is encrypted at rest and in transit.
- PII is handled with specific minimization techniques (e.g., hashing). | - `11_SECURITY_COMPLIANCE/security_baseline.md`
- Database schema showing encryption
- Code implementing PII hashing | 
| **Confidentiality** | C1.2 - The entity has established procedures to prevent the unauthorized disclosure of confidential information. | - RLS policies and RBAC are used to restrict access to confidential information.
- All employees and contractors are subject to confidentiality agreements. | - `07_RLS_AND_AUTHZ.md`
- HR records ofnboarding procedures | 
