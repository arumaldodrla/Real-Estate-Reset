# Supabase Migrations Guide

This document describes the process for managing and applying database migrations for the Supabase project.

## 1. Supabase CLI

The Supabase CLI is the primary tool for managing database migrations. It must be installed in the development environment.

## 2. Migration Workflow

1.  **Link Project**: The local repository is linked to the Supabase project using the `supabase link` command.
2.  **Create a New Migration**: To make a change to the database schema, a new migration file is created using the `supabase migration new` command. This creates a new SQL file in the `supabase/migrations` directory.
3.  **Write Migration SQL**: The developer writes the SQL statements for the schema change in the newly created migration file.
4.  **Apply Locally**: The migration is applied to the local database using the `supabase db reset` command, which resets the local database and applies all migrations.
5.  **Deploy to Production**: Once the migration has been tested locally and in staging, it is deployed to the production database by committing the migration file to the main branch and running `supabase migration up` from a CI/CD pipeline or manually.

## 3. Reversible Migrations

All migrations should be written to be reversible whenever possible. This means that for every `CREATE TABLE` statement, there should be a corresponding `DROP TABLE` statement (commented out or in a separate down migration file, depending on the chosen strategy). This is crucial for the rollback strategy.
