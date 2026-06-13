# Security and Moderation

PublicPulse can become dangerous if it allows false accusations, doxxing, harassment, or political manipulation. Build safety into the MVP.

## Main risks

1. False allegations against individuals.
2. Doxxing through phone numbers, addresses, IDs, or vehicle numbers.
3. Political brigading.
4. Fake evidence.
5. Harassment against officials or citizens.
6. Sensitive reports involving minors, medical claims, legal claims, or identity groups.
7. AI hallucinating facts or authority contacts.
8. Publicly exposing exact location when it could harm someone.

## Moderation defaults

- New issues enter `pending_review` before public visibility.
- High-risk issues are hidden until admin approval.
- Evidence is private until approved.
- Complaint drafts are not auto-sent.
- Public pages use public-safe summaries.

## Risk flags

Use these risk flags:

- personal_data
- named_individual
- defamation_risk
- harassment
- hate_or_abuse
- political
- medical
- legal
- minor_safety
- violence
- self_harm
- emergency
- weak_evidence

## Admin review actions

Admins/moderators can:

- approve
- reject
- request more evidence
- mark duplicate
- hide
- block
- redact personal data

Every action must create a moderation event and admin audit log.

## AI safety rules

AI must not:

- invent facts
- invent laws
- invent authority contacts
- declare someone guilty
- claim evidence is authentic
- write defamatory language
- auto-submit complaints
- auto-post to social platforms

AI may:

- structure user claims neutrally
- ask for missing information
- draft factual complaint language
- suggest safer wording
- flag risk

## Privacy rules

Public pages should hide:

- exact user identity if anonymous mode is selected
- phone numbers
- email addresses
- personal IDs
- house/flat numbers
- exact location for sensitive reports
- private evidence files

## Evidence rules

Evidence should have states:

- private
- public_approved
- rejected

Do not expose raw storage paths.
Use signed URLs where needed.

## Emergency disclaimer

For urgent public safety issues, show:

> PublicPulse is not an emergency service. If there is immediate danger, contact local emergency services or the relevant authority directly.

## Legal disclaimer

For complaint drafts, show:

> This is an AI-generated draft based on information provided by users. Verify all facts before sending. This is not legal advice.

## Rate limiting

Add rate limits before public beta:

- issue creation per user/day
- evidence uploads per user/day
- AI runs per user/day
- support/verification mutations
- admin actions logging

## Abuse reporting

Public issue page should have a report button:

- false information
- personal data exposed
- harassment
- duplicate
- spam
- other

## Brutal rule

If moderation is weak, this product becomes a liability. Do not launch publicly without admin review, private evidence handling, and basic abuse reporting.