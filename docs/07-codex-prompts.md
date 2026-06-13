# Codex Prompts

Use these prompts phase by phase. Do not paste all of them at once.

## Prompt 1 — Read context and implement Phase 1

```md
You are working on PublicPulse, an agentic civic-action SaaS.

Read these files fully first:
- AGENTS.md
- PLAN.md
- docs/00-product-brief.md
- docs/01-architecture.md
- docs/06-security-moderation.md

Implement Phase 1 only.

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

Create reusable components:
- AppShell
- MarketingHeader
- IssueStatusBadge
- EmptyState
- PrimaryCTA

Create domain files:
- lib/domain/constants.ts
- lib/domain/types.ts
- lib/domain/schemas.ts

Do not implement Supabase yet.
Do not implement AI yet.
Do not build a feed-first social app.

When done, provide files touched, how to run, manual test checklist, and next recommended prompt.
```

## Prompt 2 — Domain model and validation

```md
Implement Phase 0 properly.

Create/finish domain constants, TypeScript types, and Zod schemas for issues, evidence, status events, support, verification, moderation, authorities, complaint drafts, and AI run outputs.

All enums must match AGENTS.md and PLAN.md. Replace any hardcoded strings across the app with these constants.
```

## Prompt 3 — Supabase schema

```md
Implement Phase 2.

Create Supabase migration files for the data model in docs/02-data-model.md. Enable RLS and add baseline policies. Add seed.sql with sample categories, authorities, and demo issues.

Do not weaken RLS to make development easier. Document any assumptions.
```

## Prompt 4 — Auth and profiles

```md
Implement Phase 3.

Add Supabase Auth. Create profile initialization after signup/login. Protect /app routes. Protect /app/admin by role. Add public identity mode to profile.

Never trust client-supplied user IDs.
```

## Prompt 5 — Issue creation wizard

```md
Implement Phase 4.

Build the issue creation wizard: description, category, location, evidence placeholder, review, submit. Save draft issue and submit to pending_review.

Use Zod validation and server actions. No AI yet unless Phase 6 is already complete.
```

## Prompt 6 — Evidence upload

```md
Implement Phase 5.

Add private evidence uploads using Supabase Storage. Save evidence metadata. Use signed URLs. Enforce file type and file size limits.

Evidence must not become publicly visible before approval.
```

## Prompt 7 — AI provider and Intake Structuring Agent

```md
Implement Phase 6.

Create AI provider adapter and Intake Structuring Agent. Use strict JSON output validated with Zod. Save ai_runs. Let the user accept/edit AI output before submitting.

No client-side AI calls.
```

## Prompt 8 — Admin moderation

```md
Implement Phase 7 admin moderation.

Build pending review queue. Admin can approve, reject, request more evidence, mark duplicate, and hide. Every action creates moderation_events, status_events, and admin audit logs where appropriate.
```

## Prompt 9 — Public issue page

```md
Implement Phase 7 public issue page.

Approved issues get public case pages. Hide private fields. Show title, summary, category, severity, approximate location, approved evidence, support/verification counts, and timeline.
```

## Prompt 10 — Support and verification

```md
Implement Phase 8.

Add support and verification actions. One support and one verification per user per issue. Verification is not the same as support. Show counts without rage-ranking.
```

## Prompt 11 — Complaint Draft Agent

```md
Implement Phase 9.

Create Complaint Draft Agent using only approved issue data. Generate formal complaint, email draft, social post draft, and WhatsApp/community draft. Save drafts in complaint_drafts.

Add disclaimer. Do not auto-send or auto-post.
```

## Prompt 12 — Timeline and escalation

```md
Implement Phases 10 and 12.

Create status timeline component and rule-based escalation recommendations. Recommendations should be drafts only. High-risk escalation needs admin approval.
```

## Prompt 13 — Hardening audit

```md
Audit the app against AGENTS.md and SECURITY_NOTES.md.

Check auth, RLS, private evidence, AI failures, moderation gates, public privacy, typecheck, lint, and build.

Fix critical issues and document remaining risks.
```