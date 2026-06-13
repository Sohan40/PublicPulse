# GitHub Issues Backlog

Create these issues manually or with GitHub CLI after the repo is ready.

## Epic 1 — Foundation

### Issue 1: Initialize Next.js project shell
Labels: `phase-1`, `frontend`, `foundation`

Acceptance:
- App runs locally.
- Placeholder routes render.
- App shell and marketing shell exist.

### Issue 2: Add domain constants and schemas
Labels: `phase-0`, `types`, `validation`

Acceptance:
- Categories, statuses, severities, roles, identity modes, and risk flags are defined.
- Zod schemas exist.

## Epic 2 — Database/Auth

### Issue 3: Add Supabase migrations and RLS
Labels: `phase-2`, `database`, `security`

Acceptance:
- Tables created.
- RLS enabled.
- Seed file added.
- Policies documented.

### Issue 4: Implement auth and onboarding
Labels: `phase-3`, `auth`

Acceptance:
- Signup/login/logout work.
- Profile row created.
- Admin route protected.

## Epic 3 — Issue Reporting

### Issue 5: Build issue creation wizard
Labels: `phase-4`, `frontend`, `issues`

Acceptance:
- Multi-step wizard works.
- Draft issue created.
- Submit for review works.

### Issue 6: Add evidence upload
Labels: `phase-5`, `storage`, `security`

Acceptance:
- Upload works.
- Metadata saved.
- Signed/private access used.

## Epic 4 — AI Agents

### Issue 7: Add AI provider abstraction
Labels: `phase-6`, `ai`, `architecture`

Acceptance:
- Provider interface exists.
- No client-side AI calls.
- Failures handled.

### Issue 8: Implement Intake Structuring Agent
Labels: `phase-6`, `ai`, `agents`

Acceptance:
- Strict JSON output.
- Zod validation.
- ai_runs logging.

### Issue 9: Implement Complaint Draft Agent
Labels: `phase-9`, `ai`, `agents`

Acceptance:
- Formal/email/social/WhatsApp drafts generated.
- Disclaimer shown.
- No auto-send.

## Epic 5 — Trust and moderation

### Issue 10: Admin moderation dashboard
Labels: `phase-7`, `admin`, `moderation`

Acceptance:
- Pending queue.
- Approve/reject/request evidence/duplicate actions.
- Status events created.

### Issue 11: Public issue page
Labels: `phase-7`, `frontend`, `public`

Acceptance:
- Approved issue visible.
- Private fields hidden.
- Timeline shown.

### Issue 12: Support and verification
Labels: `phase-8`, `community`, `trust`

Acceptance:
- One support per user.
- One verification per user.
- Counts shown.

## Epic 6 — Resolution workflow

### Issue 13: Status timeline
Labels: `phase-10`, `workflow`

Acceptance:
- Status events visible.
- Admin/system updates create events.

### Issue 14: Escalation recommendations
Labels: `phase-12`, `workflow`

Acceptance:
- Rule-based recommendations.
- No auto-posting.

## Epic 7 — Launch

### Issue 15: Beta analytics and safety audit
Labels: `phase-14`, `launch`, `security`

Acceptance:
- Basic metrics tracked.
- Security notes updated.
- MVP test checklist complete.