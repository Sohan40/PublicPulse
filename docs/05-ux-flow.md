# UX Flow

## UX positioning

PublicPulse should feel like a calm, serious civic-action tool.

Avoid the emotional design language of social media feeds. Avoid rage bait, follower vanity, and political shouting.

## Primary user journey

```txt
Open app
-> Raise an issue
-> Describe what happened
-> Add location
-> Add evidence
-> AI structures issue
-> User reviews summary
-> Submit for review
-> Admin approves
-> Public case page goes live
-> Nearby users support/verify
-> Complaint draft generated
-> Timeline tracks status
```

## Marketing homepage

Sections:
1. Hero: “Turn local problems into verified action.”
2. How it works: report, verify, escalate, track.
3. Why not just post on X/Reddit/WhatsApp.
4. Example case cards.
5. CTA: Raise an issue.

## App dashboard

Dashboard should show:
- My issues
- Nearby issues
- Issues needing support
- Drafts needing evidence
- Recently resolved cases

## Issue creation wizard

### Step 1 — What happened?
Fields:
- description
- category optional

### Step 2 — Where is it?
Fields:
- locality/city/state
- optional map pin
- precision mode

### Step 3 — Add evidence
Fields:
- image/video/document upload
- caption

### Step 4 — AI structure
Show:
- generated title
- generated summary
- category
- severity
- missing info
- risk flags if any

User can edit before submit.

### Step 5 — Submit
Show privacy note and moderation note.

## Public case page

Must show:
- title
- category
- severity
- status badge
- public-safe summary
- approximate location
- approved evidence
- support count
- verification count
- complaint draft status
- timeline
- CTA: support / verify / share

Must hide:
- exact user identity if anonymous
- private evidence paths
- exact coordinates if sensitive
- personal phone/address/IDs

## Admin page

Admin queue:
- pending review
- high risk
- needs more evidence
- reported abuse

Actions:
- approve
- reject
- request more evidence
- mark duplicate
- hide
- add moderation note

## Empty states

Examples:
- “No issues near you yet. Raise the first one.”
- “This issue needs better evidence before it can be escalated.”
- “No complaint draft yet. Generate one when the case is ready.”

## Tone

Use firm but neutral civic language.

Good: “This issue needs clearer evidence before public escalation.”
Bad: “Expose them now.”

Good: “5 people say this affects them.”
Bad: “Make this go viral.”