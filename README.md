# PublicPulse / ResolvePulse — Agentic Civic Action SaaS

A GitHub-ready planning repo for building a platform where citizens convert local problems into verified public cases, AI helps structure the complaint, and the system tracks escalation until resolution.

## Product sentence

**PublicPulse turns citizen anger into structured action: report an issue, verify it with evidence, route it to the right authority, escalate publicly when needed, and track the outcome.**

## What this is not

- Not another X clone.
- Not another Reddit clone.
- Not a political debate app.
- Not an anonymous ranting board.
- Not a legal authority or official government system.

## What this is

A proof-first, location-aware civic issue tracker with agentic workflows:

```txt
User issue → AI intake → evidence check → duplicate detection → jurisdiction mapping
→ verified case page → supporter validation → complaint drafting → escalation → status tracking
```

## Recommended MVP stack

Use this stack unless you have a strong reason not to:

- **Frontend:** Next.js App Router + TypeScript
- **UI:** Tailwind CSS + shadcn/ui
- **Backend:** Next.js API routes/server actions for MVP
- **Database:** Supabase Postgres
- **Auth:** Supabase Auth
- **Storage:** Supabase Storage for images/videos/docs
- **Maps:** Mapbox or Google Maps, abstracted behind a provider interface
- **AI:** LLM provider adapter, initially OpenAI-compatible
- **Background jobs:** Trigger.dev / Inngest / Supabase Edge Functions later
- **Deployment:** Vercel for web app, Supabase for DB/storage/auth

## Repo usage with Codex

1. Create a new GitHub repo manually, for example `publicpulse-civic-agent-saas`.
2. Upload/extract this ZIP into that repo.
3. Open the repo in Codex.
4. Paste the first prompt from `prompts/START_HERE_CODEX.md`.
5. Follow `PLAN.md` phase by phase.
6. Keep `AGENTS.md` at repo root so Codex understands coding rules, product constraints, and safety boundaries.

## Suggested manual repo creation commands

```bash
gh repo create Sohan40/publicpulse-civic-agent-saas --private --description "Agentic civic action SaaS: verified local issues, AI complaints, escalation tracking" --clone
cd publicpulse-civic-agent-saas
# copy the extracted files here
git add .
git commit -m "Add PublicPulse Codex implementation plan"
git push origin main
```

If you do not use GitHub CLI, create the repo from GitHub UI and upload these files.

## Execution philosophy

Build the smallest serious product, not a giant social network.

The MVP should prove one thing:

> Can a user raise a real local issue in 60 seconds and get a clean, shareable, evidence-backed case page with a useful next action?

Everything else is secondary.

## Initial MVP modules

1. Auth and onboarding
2. Location-based issue creation
3. Evidence upload
4. AI issue structuring
5. Public case page
6. Support/verification flow
7. Authority mapping
8. Complaint draft generation
9. Basic status timeline
10. Admin moderation dashboard

## First niche recommendation

Start with **local civic issues** only:

- Road damage
- Drainage overflow
- Garbage collection
- Streetlight failure
- Water supply issue
- Public safety hazard

Do **not** start with all categories. Scam alerts, hospital complaints, workplace issues, and corruption reports can come later after moderation and legal workflows mature.
