# Deploying Matenote to Coolify

This guide details how to deploy your Next.js application to your self-hosted Coolify instance.

## Prerequisites
-   Your code is pushed to a Git repository (GitHub/GitLab/etc).
-   You have access to your Coolify dashboard.

## Step 1: Create a New Service
1.  Go to your project in Coolify.
2.  Click **"+ New"**.
3.  Select **"Git Repository"** (Public or Private).
4.  Select your repository and branch (e.g., `main`).

## Step 2: Configuration
Coolify should automatically detect that this is a Docker-based project because of the `Dockerfile` we added.

### Build Pack
-   Ensure **Build Pack** is set to **Docker File**.
-   **Docker File Location**: `/Dockerfile` (default).

### Environment Variables
You need to add your secrets. Go to the **Environment Variables** tab and add:
-   `NEXT_PUBLIC_API_URL`: Your backend URL.
-   `NEXT_PUBLIC_SUPABASE_URL`: Your Supabase URL.
-   `NEXT_PUBLIC_SUPABASE_ANON_KEY`: Your Supabase Anon Key.
-   Any other secrets from your `.env.local` file.

**Note:** Since this is a client-side heavy app, variables starting with `NEXT_PUBLIC_` are baked into the build. If you change them, you must **Redeploy**.

## Step 3: Domains
1.  Go to the **Service Configuration** (Settings).
2.  In **Domains**, add the domain you want to use (e.g., `https://app.mydomain.com`).
3.  Coolify will automatically handle SSL certificates for you.

## Step 4: Deploy
1.  Click **Deploy** at the top right.
2.  Watch the specific "Build Logs".
3.  Once finished, your status should turn **Healthy** (green).

## Troubleshooting
-   **"Command not found"**: Ensure the Base Directory is set to `/` (or root).
-   **Public Vars Missing**: Remember that `NEXT_PUBLIC` vars are needed at *build time*. Ensure they are set in the Coolify "Secrets" or "Environment Variables" section before clicking Deploy.
