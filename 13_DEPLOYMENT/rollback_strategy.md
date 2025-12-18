# Rollback Strategy

This document outlines the strategy for rolling back deployments in the event of a critical issue in production.

## 1. Frontend Application (Vercel)

- **Instant Rollbacks**: Vercel provides an easy, one-click rollback feature. From the Vercel dashboard, any previous deployment can be instantly promoted to production.
- **Procedure**:
    1. Identify the last known good deployment.
    2. From the Vercel project dashboard, select the good deployment and click "Promote to Production."

## 2. Backend (Supabase)

### Database Migrations

- **Reversible Migrations**: As described in the migrations guide, all database migrations should be written to be reversible.
- **Rollback Procedure**:
    1. Create a new migration that reverses the changes from the problematic migration.
    2. Apply this new migration to the production database.

### Edge Functions

- **Versioning**: While Supabase Edge Functions do not have a built-in versioning and rollback system as of this writing, the code for the functions is managed in Git.
- **Rollback Procedure**:
    1. Revert the commit that introduced the problematic change in the Edge Function code.
    2. Redeploy the functions using the `supabase functions deploy` command.

## 3. Hotfixes

For issues that can be fixed quickly, a hotfix is often preferable to a full rollback. A hotfix involves creating a new branch from the main branch, applying the fix, and deploying this new version to production. This approach minimizes downtime and avoids the potential data consistency issues that can arise from a database rollback.
