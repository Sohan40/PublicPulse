# Security Notes

This repo is currently a planning/starter repo. When implementation begins, keep this file updated after every security-relevant phase.

## Non-negotiable rules

- Enable Supabase RLS before storing real user data.
- Never expose service role keys to the browser.
- Store evidence privately by default.
- Use signed URLs for private evidence.
- Do not make unreviewed issues public.
- Do not auto-send complaints or auto-post to X/social platforms in MVP.
- Do not hallucinate authority contact details.
- Do not expose exact location for sensitive reports.
- Do not expose user identity when anonymous public mode is selected.

## MVP risks to handle before beta

- False allegations.
- Doxxing through uploaded images or text.
- Spam issue creation.
- AI generating defamatory wording.
- Weak moderation queue.
- Exact location leakage.
- Private evidence URL leakage.
- Admin role misconfiguration.
- No rate limits on AI calls.

## Required before public launch

- RLS audit.
- Admin moderation flow.
- Abuse report flow.
- Privacy policy.
- Terms/disclaimer.
- Emergency disclaimer.
- Complaint draft disclaimer.
- Manual test checklist for issue creation, evidence, moderation, and public page visibility.