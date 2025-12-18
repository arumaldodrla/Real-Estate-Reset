# Listing APIs and Aggregators Integration Runbook

This document covers the integration with third-party property listing APIs (e.g., Zillow, Redfin) and data aggregators.

## 1. Strategy

Direct access to APIs from major listing portals like Zillow and Redfin can be restricted. The integration strategy is as follows:

1.  **Prioritize Official APIs**: If a portal offers an official, supported API for property listings, it will be the preferred method of integration.
2.  **Use Third-Party Aggregators**: If an official API is not available, use a data aggregator service (e.g., RealtyMole, Bright MLS) that provides a unified API for listings from multiple sources.
3.  **Compliant Scraping as a Last Resort**: Web scraping will only be considered if it is done through a partner who ensures compliance with the portal's Terms of Service, and this approach will be documented and reviewed for legal and ethical implications.

## 2. Sync Process

The process for syncing from these APIs is similar to the RETS integration:

-   A Supabase Scheduled Function (`property_api_sync_worker`) runs periodically.
-   The function calls the relevant API, fetching new or updated listings based on the agent's configured geographic focus.
-   The data is normalized and inserted or updated in the `properties` table, with the `source` column indicating the origin (e.g., 'zillow', 'realtymole').
-   The property is then passed to the enrichment and embedding services.

## 3. Configuration

-   Agents can configure which sources they want to sync from in their settings.
-   API keys for each service are stored securely in Supabase Secrets.

## 4. Note on API Availability

The availability and terms of these APIs can change. The integration must be designed to be resilient to these changes, with clear error handling and logging to detect when an API is no longer available.
