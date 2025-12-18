# Repository Structure

This document outlines the recommended repository structure for the project. The structure is designed to be logical and to support the development workflow of the AI agents.

```
/
├── frontend/         # Refine/React frontend application
│   ├── src/
│   │   ├── components/ # Reusable React components
│   │   ├── pages/      # Application pages
│   │   ├── hooks/      # Custom React hooks
│   │   └── ...
│   └── package.json
├── supabase/         # Supabase project configuration
│   ├── migrations/   # Database migrations
│   ├── functions/    # Edge Functions
│   │   ├── whatsapp-webhook/
│   │   ├── facebook-webhook/
│   │   ├── rets-sync-worker/
│   │   └── ...
│   └── config.toml
├── docs/             # Project documentation (this pack)
└── ...
```

## Frontend

The `frontend` directory contains the React application built with the Refine framework. It includes all the UI components, pages, and logic for the user-facing application.

## Supabase

The `supabase` directory contains all the configuration for the Supabase project, including:

-   **Migrations**: The `migrations` directory contains the SQL files for database schema changes. The Supabase CLI is used to manage and apply these migrations.
-   **Functions**: The `functions` directory contains the source code for the Supabase Edge Functions, which are used for backend logic, webhooks, and scheduled jobs.

## Documentation

The `docs` directory contains the complete documentation pack for the project, including the files you are currently reading.
