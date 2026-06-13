# Data Model

This is the first-pass Supabase/Postgres model for PublicPulse.

## profiles

Stores user metadata separate from auth provider.

Fields:
- `id uuid primary key references auth.users(id)`
- `display_name text`
- `role text` — citizen, moderator, admin, authority
- `public_identity_mode text` — real_name, display_name, anonymous_public
- `city text`
- `state text`
- `created_at timestamptz`
- `updated_at timestamptz`

## issues

Main case record.

Fields:
- `id uuid primary key`
- `created_by uuid references profiles(id)`
- `title text`
- `raw_description text`
- `summary text`
- `public_safe_summary text`
- `category text`
- `severity text`
- `status text`
- `location_label text`
- `city text`
- `state text`
- `latitude numeric`
- `longitude numeric`
- `location_precision text` — exact, approximate, locality_only
- `is_public boolean`
- `risk_level text`
- `risk_flags text[]`
- `duplicate_of uuid references issues(id)`
- `created_at timestamptz`
- `updated_at timestamptz`

Public pages should not expose exact coordinates by default. Use approximate display where needed.

## evidence

Uploaded proof for issues.

Fields:
- `id uuid primary key`
- `issue_id uuid references issues(id)`
- `uploaded_by uuid references profiles(id)`
- `storage_path text`
- `file_type text` — image, video, document, screenshot
- `mime_type text`
- `file_size_bytes bigint`
- `caption text`
- `visibility text` — private, public_approved, rejected
- `metadata jsonb`
- `created_at timestamptz`

## issue_status_events

Audit timeline.

Fields:
- `id uuid primary key`
- `issue_id uuid references issues(id)`
- `actor_id uuid references profiles(id)`
- `actor_type text` — user, admin, system, authority
- `from_status text`
- `to_status text`
- `note text`
- `metadata jsonb`
- `created_at timestamptz`

## issue_supports

Affected-user support.

Fields:
- `id uuid primary key`
- `issue_id uuid references issues(id)`
- `user_id uuid references profiles(id)`
- `note text`
- `created_at timestamptz`

Constraint: unique `(issue_id, user_id)`.

## issue_verifications

Confirmation that issue exists.

Fields:
- `id uuid primary key`
- `issue_id uuid references issues(id)`
- `user_id uuid references profiles(id)`
- `verification_type text` — seen_personally, affected, evidence_added, local_knowledge
- `note text`
- `created_at timestamptz`

Constraint: unique `(issue_id, user_id)`.

## authorities

Verified or manually maintained authority directory.

Fields:
- `id uuid primary key`
- `name text`
- `authority_type text` — municipality, water_board, electricity, police, panchayat, campus, apartment, unknown
- `city text`
- `state text`
- `jurisdiction_label text`
- `contact_email text`
- `contact_phone text`
- `website_url text`
- `is_verified boolean`
- `source_url text`
- `created_at timestamptz`

Do not display or use authority contacts unless verified or manually approved.

## complaint_drafts

AI-generated complaint text.

Fields:
- `id uuid primary key`
- `issue_id uuid references issues(id)`
- `created_by uuid references profiles(id)`
- `draft_type text` — formal, email, social, whatsapp
- `subject text`
- `body text`
- `disclaimer text`
- `ai_run_id uuid references ai_runs(id)`
- `created_at timestamptz`

## ai_runs

AI call audit log.

Fields:
- `id uuid primary key`
- `user_id uuid references profiles(id)`
- `issue_id uuid references issues(id)`
- `agent_name text`
- `prompt_version text`
- `model text`
- `input_hash text`
- `output_json jsonb`
- `status text` — success, failed, invalid_schema
- `error_message text`
- `created_at timestamptz`

Do not store unnecessary private raw content if avoidable. Keep logs useful but privacy-aware.

## moderation_events

Review history.

Fields:
- `id uuid primary key`
- `issue_id uuid references issues(id)`
- `moderator_id uuid references profiles(id)`
- `action text` — approve, reject, request_more_evidence, mark_duplicate, hide, block
- `reason text`
- `metadata jsonb`
- `created_at timestamptz`

## admin_audit_logs

Sensitive admin action trail.

Fields:
- `id uuid primary key`
- `actor_id uuid references profiles(id)`
- `action text`
- `entity_type text`
- `entity_id uuid`
- `metadata jsonb`
- `created_at timestamptz`

## RLS baseline

- Public can read approved public issues only.
- Authenticated users can create issues.
- Owners can view their private drafts.
- Owners cannot approve their own issue unless admin.
- Admins/moderators can read pending review queue.
- Evidence reads require owner/admin or public_approved.
- AI logs are admin/owner scoped, not globally public.