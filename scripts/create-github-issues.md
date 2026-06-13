# Optional: Create GitHub Issues Manually

The ChatGPT GitHub connector can write files, but creating a full issue backlog is better done deliberately after you review the plan.

Use `docs/08-github-issues.md` as the source.

Example with GitHub CLI:

```bash
gh issue create \
  --title "Initialize Next.js project shell" \
  --body "Create the Phase 1 Next.js app shell from PLAN.md." \
  --label phase-1,frontend,foundation
```

Better: create one issue at a time from `docs/08-github-issues.md`, not one giant issue.