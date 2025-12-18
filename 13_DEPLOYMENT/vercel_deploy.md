# Vercel Deployment Guide

This document provides a guide for deploying the frontend application to Vercel.

## 1. Project Configuration

- **Framework Preset**: The Vercel project will be configured with the "Vite" framework preset.
- **Build Command**: `npm run build`
- **Output Directory**: `dist`
- **Root Directory**: `frontend`

## 2. CI/CD Integration

- **Git Integration**: The Vercel project will be connected to the project's Git repository (e.g., on GitHub).
- **Automatic Deployments**: Vercel will be configured to automatically build and deploy the application whenever new commits are pushed to the main branch.
- **Preview Deployments**: For every pull request, Vercel will create a unique preview deployment. This allows for testing and reviewing changes in a live environment before they are merged into the main branch.

## 3. Environment Variables

- The Vercel project will be configured with the necessary environment variables, such as `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`, to connect to the Supabase backend.
- Separate environment variables will be configured for the staging and production environments.
