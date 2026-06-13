# Architecture

## MVP architecture

```txt
Next.js App Router
  -> Server Actions / Route Handlers
  -> Supabase Auth
  -> Supabase Postgres
  -> Supabase Storage
  -> AI Provider Adapter
  -> Admin Moderation Dashboard
```

Use a monolith first. Do not split into microservices before product-market proof.

## Frontend

- Next.js App Router
- TypeScript
- Tailwind CSS
- shadcn/ui-compatible components
- Server components by default
- Client components only for interactive forms, upload UI, maps, and local state

## Backend

For MVP, use Next.js route handlers and server actions.

Core modules:

```txt
lib/domain      constants, types, schemas
lib/supabase    browser/server clients
lib/auth        role checks and session helpers
lib/agents      prompts, schemas, AI workflows
lib/moderation  risk checks and visibility rules
lib/maps        maps/geocoding provider wrapper
server/actions  issue/evidence/support/admin mutations
```

## Database

Supabase Postgres with RLS from day one.

Important design choices:

- Public users can read only approved public-safe issue fields.
- Authenticated users can create issues.
- Only owners can edit draft issues.
- Admins/moderators can review issues.
- Evidence is private until approved.
- All status changes create audit events.

## AI integration

Never call the LLM directly from UI components.

Use this pattern:

```txt
UI -> server action -> agent function -> provider adapter -> schema validation -> ai_runs log -> result returned
```

Every AI output must be schema-validated. Failed or invalid AI output should not break the user flow.

## Storage

Use private Supabase buckets first:

- `issue-evidence-private`
- later optional `issue-evidence-public`

Prefer signed URLs over public file paths.

## Moderation architecture

All submitted issues go through moderation before public visibility.

Automatic checks can suggest risk level, but human admin decides for high-risk categories.

## Later architecture

Only after MVP traction:

```txt
Web app
  -> API service
  -> Issue service
  -> Evidence service
  -> Agent service
  -> Notification service
  -> Queue/jobs
  -> Postgres + storage + vector search
```

## Non-goals in MVP

- Auto-posting to X
- Real-time chat
- Full social graph
- Payment system
- Mobile app
- Authority login
- Complex AI agent orchestration
- Vector duplicate search

Keep the first version focused and shippable.