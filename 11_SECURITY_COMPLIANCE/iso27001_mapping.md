# ISO 27001 Control Mapping

This document maps the platform's security controls to the Annex A controls of the ISO/IEC 27001:2013 standard. This mapping is a starting point for a formal ISO 27001 certification process.

## Annex A Control Mapping

| Annex A Control | Control Objective | Platform Control | Implementation Evidence |
|---|---|---|---|
| **A.5.1.1** | Policies for information security | The platform has a comprehensive set of information security policies. | - This documentation pack, particularly the `11_SECURITY_COMPLIANCE` section. |
| **A.8.1.1** | Inventory of assets | An inventory of all information assets is maintained. | - The `03_SYSTEM_ARCHITECTURE.md` and `06_DATABASE_SCHEMA.md` documents serve as an inventory of key system and data assets. |
| **A.9.1.1** | Access control policy | A formal access control policy is in place. | - The `07_RLS_AND_AUTHZ.md` document defines the access control policy. |
| **A.9.2.3** | Management of privileged access rights | Access to privileged accounts is restricted and managed. | - Supabase roles and permissions are used to manage privileged access.
- Access to the Supabase project is restricted to authorized personnel. |
| **A.9.4.1** | Information access restriction | Access to information and application functions is restricted in accordance with the access control policy. | - RLS policies and RBAC are implemented to enforce access restrictions. |
| **A.10.1.1** | Policy on the use of cryptographic controls | A policy on the use of cryptography for protection of information has been developed and implemented. | - The `11_SECURITY_COMPLIANCE/security_baseline.md` document specifies the requirements for encryption at rest and in transit. |
| **A.12.1.2** | Protection against malware | Controls are in place to protect against malware. | - The platform is hosted on a managed infrastructure (Vercel, Supabase) that includes malware protection.
- All dependencies are scanned for vulnerabilities. |
| **A.14.1.1** | Information security requirements analysis and specification | Information security requirements are included in the requirements for new information systems or enhancements to existing information systems. | - The `01_PRD.md` includes non-functional requirements for security and compliance. |
| **A.14.2.1** | Secure development policy | Rules for the development of software and systems have been established and are applied to developments within the organization. | - The `12_DEV_GUIDES/coding_standards.md` document will define the secure coding standards. |
| **A.16.1.1** | Responsibilities and procedures | Management responsibilities and procedures have been established to ensure a quick, effective, and orderly response to information security incidents. | - The `11_SECURITY_COMPLIANCE/incident_response_runbook.md` will define the incident response procedures. |
