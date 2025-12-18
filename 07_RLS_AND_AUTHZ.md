# 07. Row-Level Security (RLS) and Authorization

This document outlines the Row-Level Security (RLS) policies and authorization model for the platform, ensuring multi-tenant data isolation and adherence to the principle of least privilege. All policies are implemented in Supabase using PostgreSQL's RLS capabilities.

## 7.1 Authorization Model

The platform uses a role-based access control (RBAC) model based on user roles within a team (tenancy).

- **`team_admin`**: Manages team settings, billing, and can view all data within their team.
- **`agent`**: A standard user who manages their own transactions, properties, and chatbot configurations. They can only access data associated with their `user_id` or `team_id`.
- **`system_admin`**: Internal administrative role with elevated privileges for system maintenance and support.

## 7.2 RLS Policies

RLS is enabled on all tables containing tenant data. The policies below are examples and should be adapted to the final data model.

A helper function `auth.uid()` is used to get the ID of the currently authenticated user, and a custom function `get_team_id(user_id)` can be created to retrieve the user's team ID.

### `properties` Table

**Requirement:** Users can access properties belonging to their team.

```sql
-- Enable RLS
ALTER TABLE properties ENABLE ROW LEVEL SECURITY;

-- Policy: Allow team members to view properties
CREATE POLICY "Allow team members to view properties" ON properties
FOR SELECT USING (
  team_id = (SELECT team_id FROM profiles WHERE user_id = auth.uid())
);

-- Policy: Allow agents to create properties for their team
CREATE POLICY "Allow agents to create properties" ON properties
FOR INSERT WITH CHECK (
  team_id = (SELECT team_id FROM profiles WHERE user_id = auth.uid()) AND
  agent_id = auth.uid()
);

-- Policy: Allow agents to update their own properties
CREATE POLICY "Allow agents to update their own properties" ON properties
FOR UPDATE USING (
  agent_id = auth.uid()
);
```

### `chatbot_configs` Table

**Requirement:** Agents can manage their own chatbot configurations. Team admins can view all configurations for their team.

```sql
-- Enable RLS
ALTER TABLE chatbot_configs ENABLE ROW LEVEL SECURITY;

-- Policy: Allow agents to manage their own config
CREATE POLICY "Allow agents to manage their own config" ON chatbot_configs
FOR ALL USING (
  agent_id = auth.uid()
);

-- Policy: Allow team admins to view team configs
CREATE POLICY "Allow team admins to view team configs" ON chatbot_configs
FOR SELECT USING (
  team_id = (SELECT team_id FROM profiles WHERE user_id = auth.uid() AND role = 'team_admin')
);
```

### `chatbot_sessions` & `chatbot_conversations` Tables

**Requirement:** To protect end-customer privacy, agents can only access sessions and conversations associated with their own agent ID.

```sql
-- Enable RLS on sessions
ALTER TABLE chatbot_sessions ENABLE ROW LEVEL SECURITY;

-- Policy: Allow agents to access their own chatbot sessions
CREATE POLICY "Allow agents to access their own sessions" ON chatbot_sessions
FOR ALL USING (
  agent_id = auth.uid()
);

-- Enable RLS on conversations
ALTER TABLE chatbot_conversations ENABLE ROW LEVEL SECURITY;

-- Policy: Allow access to conversations linked to accessible sessions
CREATE POLICY "Allow access to conversations via session" ON chatbot_conversations
FOR ALL USING (
  EXISTS (SELECT 1 FROM chatbot_sessions WHERE id = session_id)
);
```

### `regulations` Table

**Requirement:** All authenticated users can read regulations, but only system administrators can write to the table.

```sql
-- Enable RLS
ALTER TABLE regulations ENABLE ROW LEVEL SECURITY;

-- Policy: Allow all authenticated users to read regulations
CREATE POLICY "Allow read access to all users" ON regulations
FOR SELECT USING (auth.role() = 'authenticated');

-- Policy: Restrict write access to system admins
-- Note: Write operations should be handled via a trusted service role or specific admin functions
-- to prevent direct modification by users.
CREATE POLICY "Restrict writes to admins" ON regulations
FOR ALL USING (false); -- Deny by default
```
