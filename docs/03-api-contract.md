# API Contract

Use server actions where possible. Route handlers are fine for uploads, AI calls, webhooks, and public APIs.

## Auth

### `POST /api/auth/profile/init`
Creates profile after first login if missing.

Response:
```json
{ "profile": { "id": "uuid", "role": "citizen" } }
```

## Issues

### `POST /api/issues`
Create draft issue.

Body:
```json
{
  "raw_description": "text",
  "category": "road_damage",
  "location_label": "string",
  "city": "string",
  "state": "string",
  "latitude": 17.0,
  "longitude": 78.0,
  "location_precision": "approximate"
}
```

Response:
```json
{ "issue_id": "uuid", "status": "draft" }
```

### `PATCH /api/issues/:id`
Update owner draft issue only.

### `POST /api/issues/:id/submit`
Move issue from `draft` to `pending_review`.

### `GET /api/issues/:id`
Returns issue detail. Public users only see public-approved fields.

### `GET /api/issues/nearby`
Query params:
- `city`
- `category`
- `status`
- `severity`
- `page`

Returns public approved issues.

## Evidence

### `POST /api/evidence/upload-url`
Create signed upload path for issue evidence.

Body:
```json
{ "issue_id": "uuid", "file_type": "image", "mime_type": "image/jpeg", "file_size_bytes": 12345 }
```

### `POST /api/evidence`
Save uploaded evidence metadata.

## AI

### `POST /api/ai/structure-issue`
Runs Intake Structuring Agent for owner draft issue.

Body:
```json
{ "issue_id": "uuid" }
```

Response:
```json
{
  "title": "string",
  "summary": "string",
  "category": "road_damage",
  "severity": "medium",
  "missing_information": [],
  "risk_flags": []
}
```

### `POST /api/ai/generate-complaint-draft`
Runs Complaint Draft Agent for approved issue.

Body:
```json
{ "issue_id": "uuid", "draft_types": ["formal", "email", "social", "whatsapp"] }
```

## Support and verification

### `POST /api/issues/:id/support`
Adds “this affects me too”. One per user.

### `POST /api/issues/:id/verify`
Adds confirmation. One per user.

Body:
```json
{ "verification_type": "seen_personally", "note": "optional" }
```

## Admin moderation

### `GET /api/admin/issues/pending`
Admin/moderator only.

### `POST /api/admin/issues/:id/approve`
Approves issue and creates public case page.

### `POST /api/admin/issues/:id/reject`
Rejects issue with reason.

### `POST /api/admin/issues/:id/request-more-evidence`
Moves to `needs_more_evidence`.

### `POST /api/admin/issues/:id/mark-duplicate`
Marks duplicate.

## Error shape

All APIs should return consistent errors:

```json
{
  "error": {
    "code": "UNAUTHORIZED | VALIDATION_ERROR | NOT_FOUND | FORBIDDEN | AI_FAILED | INTERNAL",
    "message": "safe user-facing message",
    "details": {}
  }
}
```

Never leak stack traces, prompts, API keys, service-role keys, or private evidence paths.