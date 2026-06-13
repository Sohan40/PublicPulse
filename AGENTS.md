# AGENTS.md — Codex Instructions for PublicPulse

## Mission

Build **PublicPulse**, an agentic civic-action SaaS. The product converts citizen frustration into structured, evidence-backed public cases that can be verified, supported, escalated, and tracked until resolution.

Core transformation:

```txt
Rant -> structured issue -> evidence -> verification -> complaint draft -> escalation -> resolution tracking
```

This must not become another X, Reddit, or anonymous rant feed. Build a case-management system for public problems.

## Product constraints

1. Proof-first design: every issue should support evidence such as image, video, screenshot, document, or clear written context.
2. No generic outrage feed: rank by locality, severity, verification, status, and resolution progress.
3. No fake official status: never imply government acknowledgement unless recorded.
4. No doxxing: hide phone numbers, home addresses, IDs, vehicle numbers, minors, and private personal details by default.
5. Anonymous public, verified private: users may appear anonymous publicly while verification metadata remains private.
6. Human review for high-risk cases: corruption accusations, named individuals, medical claims, legal claims, identity-related content, or political manipulation require moderation.
7. No auto-posting or auto-sending in MVP: AI may draft, but users/admins approve before anything is sent externally.
8. Audit trail: every status change must create a status event.
9. AI must not invent facts, authorities, emails, phone numbers, or legal claims.
10. Civic issues first. Scam alerts, hospital complaints, workplace reports, and corruption workflows are later phases.

## MVP stack

Use this unless there is a strong reason not to:

- Next.js App Router
- TypeScript
- Tailwind CSS
- shadcn/ui-compatible components
- Supabase Auth
- Supabase Postgres
- Supabase Storage
- Vercel deployment
- OpenAI-compatible LLM provider adapter
- Later: Trigger.dev/Inngest for scheduled escalation jobs

## Required app routes

```txt
/
/login
/signup
/app
/app/issues/new
/app/issues/[id]
/app/nearby
/app/admin
```

## Suggested directories

```txt
app/
  (marketing)/
  (app)/
  api/
components/
  ui/
  issue/
  evidence/
  map/
  admin/
lib/
  ai/
  agents/
  auth/
  db/
  domain/
  maps/
  moderation/
  supabase/
  validations/
server/
  actions/
  jobs/
supabase/
  migrations/
  seed.sql
docs/
tests/
```

## Domain constants

Start with these categories:

- road_damage
- drainage
- garbage
- streetlight
- water_supply
- public_safety
- other

Start with these statuses:

- draft
- pending_review
- public
- needs_more_evidence
- complaint_drafted
- sent_to_authority
- authority_acknowledged
- in_progress
- resolved
- rejected
- closed_duplicate

Start with these severities:

- low
- medium
- high
- urgent

Urgent issue pages must show: **PublicPulse is not an emergency service. Contact local emergency services for immediate danger.**

## AI workflows

Do not build infinite multi-agent conversations in the MVP. Build deterministic LLM calls with strict schemas.

### Intake Structuring Agent

Input: raw issue text, location, category if selected, evidence metadata.

Output JSON:

```json
{
  "title": "short neutral title",
  "summary": "neutral issue summary",
  "category": "road_damage | drainage | garbage | streetlight | water_supply | public_safety | other",
  "severity": "low | medium | high | urgent",
  "missing_information": [],
  "suggested_questions": [],
  "public_safe_summary": "summary safe for public display",
  "risk_flags": []
}
```

Rules: neutralize abusive language, do not invent facts, flag personal accusations, flag weak evidence.

### Evidence Quality Agent

Output should score usefulness of evidence, not truth. Never claim forensic verification.

### Authority Routing Agent

Use only authority records stored in the database. If no record exists, return unknown. Do not hallucinate government contact details.

### Complaint Draft Agent

Generate formal complaint, email subject/body, short social post draft, and WhatsApp/community message. Add disclaimer: AI-generated draft, verify facts before sending, not legal advice.

### Moderation/Risk Agent

Flag personal data, harassment, hate, defamation risk, medical/legal claims, political manipulation, violence, and self-harm. High-risk content must be hidden until admin review.

## Security rules

- Use strict TypeScript.
- Use Zod for server validation.
- Never call AI from client components.
- Never trust client-supplied user IDs.
- Enable Supabase RLS from the beginning.
- Store evidence in private buckets first.
- Use signed URLs for private evidence access.
- Check ownership on every mutation.
- Admin-only routes must check server-side role.
- Log AI runs with prompt version, model, schema, status, and error metadata.

## UX principles

The UI should feel calm, serious, local, trustworthy, and outcome-driven.

Primary CTA: **Raise an issue**
Secondary CTA: **Support nearby issue**

Avoid vanity follower counts, rage ranking, political shouting, and infinite feeds.

## MVP issue flow

```txt
1. User describes issue
2. User selects/sets location
3. User uploads evidence
4. AI structures the issue
5. User reviews/edit AI summary
6. Issue enters pending_review
7. Admin approves/rejects/requests more evidence
8. Public case page is created
9. Nearby users support/verify
10. Complaint draft is generated
11. Status timeline tracks progress
```

## Codex execution rules

- Implement one phase at a time from PLAN.md.
- After every phase, run typecheck/lint/build where available.
- Never skip security notes.
- Prefer simple shippable code over over-engineered agent frameworks.
- Keep AI prompts centralized.
- Every PR/commit summary should include changed files, test status, and next step.
