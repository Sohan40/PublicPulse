# START HERE — Codex Prompt

Paste this into Codex after opening the `Sohan40/PublicPulse` repo.

```md
You are working on PublicPulse, an agentic civic-action SaaS.

First read these files fully:
- AGENTS.md
- PLAN.md
- docs/00-product-brief.md
- docs/01-architecture.md
- docs/02-data-model.md
- docs/06-security-moderation.md

Then implement Phase 1 only:

Create a Next.js App Router + TypeScript project shell with Tailwind and shadcn-compatible structure.

Routes required:
- /
- /login
- /signup
- /app
- /app/issues/new
- /app/issues/[id]
- /app/nearby
- /app/admin

Create components:
- AppShell
- MarketingHeader
- IssueStatusBadge
- EmptyState
- PrimaryCTA

Create files:
- .env.example
- lib/domain/constants.ts
- lib/domain/types.ts
- lib/domain/schemas.ts

Do not implement Supabase yet, except placeholders in .env.example.
Do not implement AI yet.
Do not build a feed-first social app.
Keep the UI serious, clean, and outcome-focused.

When done, provide:
1. What changed
2. Files touched
3. How to run
4. Manual test checklist
5. Next recommended prompt
```