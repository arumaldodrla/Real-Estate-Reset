# Local Development Setup

This guide provides step-by-step instructions for setting up a local development environment for the Real Estate AI Platform. Following these steps will ensure that AI developer agents can build, test, and contribute to the project in a consistent and reproducible manner.

## 1. Prerequisites

Before you begin, ensure you have the following tools installed on your system:

- **Git:** For version control.
- **Node.js:** Version 22.13.0 or later.
- **pnpm:** As the primary package manager for the frontend project.
- **Supabase CLI:** Version 1.100.0 or later for managing the local Supabase stack.
- **Docker:** Required by the Supabase CLI to run the local development environment.

## 2. Repository Setup

1.  **Clone the Repository:**

    ```bash
    git clone https://github.com/arumaldodrla/Real-Estate-Reset.git
    cd Real-Estate-Reset
    ```

2.  **Install Frontend Dependencies:**

    Navigate to the `frontend` directory and install the required Node.js packages using `pnpm`.

    ```bash
    cd frontend
    pnpm install
    ```

## 3. Supabase Local Environment

The Supabase CLI uses Docker to run the entire Supabase stack on your local machine, including the PostgreSQL database, GoTrue for authentication, and Edge Functions.

1.  **Start Supabase Services:**

    From the `supabase` directory, start the local Supabase environment.

    ```bash
    cd supabase
    supabase start
    ```

    This command will download the necessary Docker images and start the services. Once it's running, it will output the local Supabase URL, the database connection string, and the JWT secret.

2.  **Link the Project:**

    Link your local Supabase project to your remote Supabase project on the cloud.

    ```bash
    supabase link --project-ref <your-project-ref>
    ```

3.  **Apply Database Migrations:**

    Apply all the database migrations to your local PostgreSQL instance to set up the schema.

    ```bash
    supabase db reset
    ```

## 4. Environment Variables

Create a `.env.local` file in the `frontend` directory and add the following environment variables. You can get these values from the output of the `supabase start` command.

```
NEXT_PUBLIC_SUPABASE_URL=http://127.0.0.1:54321
NEXT_PUBLIC_SUPABASE_ANON_KEY=<your-anon-key>
```

## 5. Running the Application

Once the setup is complete, you can run the frontend and backend services.

1.  **Start the Frontend Development Server:**

    From the `frontend` directory, start the Vite development server.

    ```bash
    cd frontend
    pnpm dev
    ```

    The application will be available at `http://localhost:5173`.

2.  **Deploy Supabase Edge Functions:**

    From the `supabase` directory, deploy any changes to your local Edge Functions.

    ```bash
    cd supabase
    supabase functions deploy --no-verify-jwt
    ```

## 6. Development Workflow

-   **Making Database Changes:**
    1.  Create a new migration file: `supabase migration new <migration-name>`
    2.  Add your SQL changes to the new migration file.
    3.  Apply the migrations locally: `supabase db reset`
-   **Making Edge Function Changes:**
    1.  Modify the function code in the `supabase/functions` directory.
    2.  Deploy the changes: `supabase functions deploy --no-verify-jwt`

By following this guide, you will have a fully functional local development environment that mirrors the production setup, allowing for efficient and error-free development.
