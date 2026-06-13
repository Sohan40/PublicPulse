# Agent Workflows

PublicPulse should use small, reliable AI workflows, not chaotic autonomous agents.

## Principles

- AI suggests; user/admin approves.
- Strict JSON for structured tasks.
- Zod validates every AI output.
- Log every run in `ai_runs`.
- Prompts must be versioned.
- Do not invent facts, contacts, authorities, laws, or official responses.

## Workflow 1 — Issue intake

```txt
Raw user issue
+ location
+ category hint
+ evidence metadata
-> Intake Structuring Agent
-> schema validation
-> user review/edit
-> save structured issue fields
```

Output:
- title
- summary
- public-safe summary
- category
- severity
- missing information
- suggested questions
- risk flags

## Workflow 2 — Evidence quality

```txt
Issue description
+ evidence metadata
+ optional captions later
-> Evidence Quality Agent
-> evidence usefulness score
-> suggested missing proof
```

The agent scores usefulness only. It must not claim that evidence is authentic.

## Workflow 3 — Moderation risk

```txt
Raw issue
+ structured summary
+ evidence captions
-> Moderation/Risk Agent
-> low/medium/high/block
-> flags
-> recommended visibility
```

High-risk cases stay hidden until admin review.

## Workflow 4 — Authority routing

```txt
Issue category
+ city/state
+ authority DB rows
-> rule-based mapper first
-> optional AI explanation later
```

Do not hallucinate authority contacts. Unknown is valid.

## Workflow 5 — Complaint draft generation

```txt
Approved issue
+ approved evidence list
+ optional authority
-> Complaint Draft Agent
-> formal complaint
-> email draft
-> X/social draft
-> WhatsApp/community draft
```

Drafts must include disclaimer: AI-generated, verify facts before use, not legal advice.

## Workflow 6 — Escalation recommendation

MVP should start rule-based:

- Public for 3 days + 5 supporters -> suggest complaint draft.
- Complaint drafted but not sent -> suggest manual sending.
- Sent to authority for 7 days without response -> suggest public update draft.
- Urgent issue -> show emergency disclaimer.

Later AI can explain recommendations, but it should not directly escalate.

## Prompt storage

Store prompts in:

```txt
lib/agents/prompts/
```

Each prompt should have:

- name
- version
- input schema
- output schema
- safety notes

## Failure handling

If AI fails:

- Save failed run.
- Show safe fallback.
- Let user manually continue.
- Never block issue creation entirely because AI failed.
