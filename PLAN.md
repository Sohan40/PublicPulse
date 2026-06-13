# PublicPulse Phase-wise Implementation Plan

## Product north star

Build the smallest serious civic-action platform that proves this workflow:

```txt
Raise issue in 60 seconds -> attach evidence -> AI structures it -> admin approves -> public case page -> people verify/support -> AI drafts complaint -> status gets tracked
```

Do not build a generic social network.

---

## Phase 0 — Product boundary and domain model

### Goal
Define the product vocabulary before writing feature code.

### Tasks
- Define categories, statuses, severities, roles, identity modes, and risk flags.
- Create TypeScript domain types.
- Create Zod schemas for issue creation, evidence metadata, status events, complaint drafts, support, and verification.
- Document what is explicitly out of scope.

### Acceptance criteria
- Domain constants exist in `lib/domain/constants.ts`.
- Types exist in `lib/domain/types.ts`.
- Zod schemas exist in `lib/domain/schemas.ts`.
- No UI/backend feature invents its own category/status strings.

---

## Phase 1 — Next.js project shell

### Goal
Create a clean app skeleton that Codex can extend safely.

### Tasks
- Initialize Next.js App Router with TypeScript.
- Add Tailwind and shadcn-compatible structure.
- Create marketing shell and app shell.
- Create placeholder routes: `/`, `/login`, `/signup`, `/app`, `/app/issues/new`, `/app/issues/[id]`, `/app/nearby`, `/app/admin`.
- Add reusable components: `AppShell`, `MarketingHeader`, `IssueStatusBadge`, `EmptyState`, `PrimaryCTA`.

### Acceptance criteria
- App runs locally.
- Placeholder pages render.
- UI is serious and outcome-focused.
- No database/AI integration yet.

---

## Phase 2 — Supabase database and RLS

### Goal
Create the secure data foundation.

### Core tables
- `profiles`
- `issues`
- `evidence`
- `issue_status_events`
- `issue_supports`
- `issue_verifications`
- `authorities`
- `complaint_drafts`
- `ai_runs`
- `moderation_events`
- `admin_audit_logs`

### Tasks
- Add Supabase migration files.
- Add seed file with sample authorities and sample public issues.
- Enable RLS on all tables.
- Add policies for public approved issue reads, owner access, and admin moderation.

### Acceptance criteria
- RLS enabled.
- Private evidence cannot be publicly listed.
- Only owner/admin can edit draft issue.
- Admin actions are logged.

---

## Phase 3 — Auth and onboarding

### Goal
Allow real users to create and manage issues.

### Tasks
- Add Supabase Auth.
- Implement signup/login/logout.
- Create profile on first login.
- Add user role: `citizen`, `moderator`, `admin`, `authority`.
- Add public identity mode: `real_name`, `display_name`, `anonymous_public`.

### Acceptance criteria
- Protected app routes require login.
- Admin page requires admin role.
- User can choose public identity mode.

---

## Phase 4 — Issue creation wizard

### Goal
Let a citizen create a structured draft issue.

### Steps
1. Describe issue.
2. Select category.
3. Set location.
4. Upload evidence.
5. Review AI-structured summary later.
6. Submit for moderation.

### Tasks
- Build multi-step wizard.
- Persist draft issue.
- Add validation and save/resume.
- Add `pending_review` submission state.

### Acceptance criteria
- User can create draft issue.
- User can submit issue for review.
- Empty/abusive/invalid data is blocked or flagged.

---

## Phase 5 — Evidence upload

### Goal
Make proof central to the product.

### Tasks
- Configure Supabase Storage private bucket.
- Upload images/videos/documents.
- Save evidence metadata: type, file path, caption, location metadata if available, uploader, visibility.
- Add signed URL access.
- Add file size/type limits.

### Acceptance criteria
- Evidence upload works.
- Evidence is private by default before moderation.
- Public page only shows approved public-safe evidence.

---

## Phase 6 — AI provider and Intake Structuring Agent

### Goal
Convert raw user text into structured issue data.

### Tasks
- Create AI provider adapter.
- Create prompt/versioning pattern.
- Implement Intake Structuring Agent with strict JSON output.
- Validate output with Zod.
- Save all AI calls in `ai_runs`.
- Let user accept/edit AI output.

### Acceptance criteria
- AI never writes directly to public issue fields without user review.
- Invalid AI JSON is handled gracefully.
- Prompt version and model are logged.

---

## Phase 7 — Admin moderation and public case page

### Goal
Prevent the app from becoming a fake-news or defamation platform.

### Tasks
- Build admin pending review queue.
- Admin can approve, reject, request more evidence, mark duplicate, or flag high-risk.
- Create public issue page for approved cases.
- Public issue page shows status, category, severity, location approximation, evidence, support count, verification count, and timeline.

### Acceptance criteria
- Unapproved issues are not public.
- High-risk issues require review.
- Public page hides private user data.

---

## Phase 8 — Support and verification flow

### Goal
Let nearby/community users validate issues without turning it into shallow upvotes.

### Tasks
- Add support button: “This affects me too.”
- Add verification button: “I can confirm this issue exists.”
- One support and one verification per user per issue.
- Store optional verification note.
- Show counts on issue page.

### Acceptance criteria
- Duplicate support is blocked.
- Verification is separate from support.
- Counts are visible but not rage-ranked.

---

## Phase 9 — Complaint Draft Agent

### Goal
Turn verified issue data into useful complaint drafts.

### Tasks
- Generate formal complaint draft.
- Generate email subject/body.
- Generate short social/X post draft.
- Generate WhatsApp/community message draft.
- Save drafts in `complaint_drafts`.
- Add disclaimer.

### Acceptance criteria
- Drafts use only approved issue facts.
- No auto-send or auto-post.
- User/admin can copy drafts.

---

## Phase 10 — Status timeline

### Goal
Track progress transparently.

### Tasks
- Create timeline component.
- Every status change creates `issue_status_events` row.
- Add notes and actor metadata.
- Show timeline on public and owner views.

### Acceptance criteria
- Status history is visible.
- Admin changes are logged.
- Users can understand what happened and what is pending.

---

## Phase 11 — Authority mapping

### Goal
Suggest the likely responsible authority without hallucinating.

### Tasks
- Add `authorities` table.
- Seed basic authority types: municipality, water board, electricity, police, panchayat, unknown.
- Rule-based mapping by category and location.
- Later: verified authority directory.

### Acceptance criteria
- Unknown is allowed.
- App does not invent contact details.
- Authority confidence is shown.

---

## Phase 12 — Escalation recommendations

### Goal
Recommend next action when issues stagnate.

### Rule examples
- If issue is public for 3 days with 5+ supporters and no complaint draft: suggest complaint draft.
- If complaint drafted and not sent: suggest sending to authority manually.
- If sent_to_authority for 7 days with no response: suggest public update draft.
- If urgent: suggest emergency disclaimer and immediate offline action.

### Acceptance criteria
- Recommendations are drafts only.
- No automatic external posting.
- High-risk escalation requires admin approval.

---

## Phase 13 — Nearby feed and search

### Goal
Make the app locally relevant.

### Tasks
- Nearby issue list by city/locality and approximate radius.
- Filters by category, severity, status, and age.
- Basic search by title/category/location.
- Sort by relevance, not pure virality.

### Acceptance criteria
- Feed is not a random global timeline.
- Default view is locally relevant.

---

## Phase 14 — Beta launch hardening

### Goal
Prepare for real users.

### Tasks
- Add rate limits.
- Add abuse report flow.
- Add basic analytics.
- Add privacy policy and terms placeholders.
- Add security audit checklist.
- Add manual QA script.

### Acceptance criteria
- Build passes.
- Major flows manually tested.
- SECURITY_NOTES.md updated.

---

## Phase 15 — Later expansion

Possible later modules:
- Scam alert vertical.
- Apartment/community private boards.
- Campus issue board.
- Authority dashboard.
- NGO/journalist dashboard.
- Multi-language complaint drafts.
- WhatsApp intake bot.
- X posting integration with approval.
- Evidence vision analysis.
- Semantic duplicate detection.

Do not start these before proving civic issue MVP.
