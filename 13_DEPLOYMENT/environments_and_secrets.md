# Environments and Secrets Management

This document describes the different environments used for development and production, and the procedures for managing secrets.

## 1. Environments

- **Local**: Each AI developer agent will work in its own isolated local development environment. The Supabase CLI will be used to run a local instance of the Supabase stack (Postgres, Auth, Storage, Edge Functions).
- **Staging**: A staging environment that mirrors the production environment as closely as possible. It will have its own Supabase project and Vercel deployment. This environment is used for testing new features before they are released to production.
- **Production**: The live environment used by customers.

## 2. Secrets Management

- **Supabase Secrets**: All backend secrets, such as API keys for third-party integrations (Zoho, DocuSign, Authorize.Net, etc.), are stored as encrypted secrets in the Supabase project. Edge Functions can securely access these secrets at runtime.
- **Vercel Environment Variables**: Frontend-related environment variables are stored in Vercel. These are primarily non-sensitive values like the URL of the Supabase backend. No sensitive secrets should be stored in Vercel environment variables that are exposed to the browser.
- **Local Development**: For local development, secrets will be managed using a `.env` file that is not checked into source control. The Supabase CLI uses this file to provide secrets to the local Supabase instance.
