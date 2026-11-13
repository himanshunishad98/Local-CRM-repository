# Architecture Decisions

Decision status: **proposed until verified against the target repository**.

1. **Application type:** responsive web app with PWA capability; no desktop executable.
2. **Frontend proposal:** React + TypeScript + Vite; Tailwind CSS if not already superseded by a working UI system.
3. **Backend proposal:** Supabase PostgreSQL, Auth, RLS, and Edge Functions where needed. No separate Node backend unless a concrete requirement warrants it.
4. **Hosting proposal:** select Vercel, Cloudflare, or Render based on the existing deployment and project configuration; not yet selected.
5. **Authorization:** enforce Admin/Sales access in database policies and server-side operations; frontend controls are supplementary.
6. **Lead identity:** UUID primary key plus human-facing sequential `LEAD-000001` identifier allocated safely in the database.
7. **Activity history:** append-only lead activity timeline; stage changes do not erase communication records.
8. **Calls:** device handoff (`tel:` where supported) plus manual post-call logging. No guaranteed browser call-state detection.
9. **Call recording:** explicitly and permanently excluded.
10. **External messaging:** handoff links do not prove sending/delivery. Direct messaging requires authorized provider APIs.
11. **Automation:** server-side scheduled execution with idempotency; no browser-only timers.
12. **Timezone:** store timestamps consistently (UTC in the database) and present using organization/user setting; default `Asia/Kolkata`.
13. **Multi-tenancy:** not assumed. Confirm whether one CRM deployment serves one organization or multiple organizations before introducing `organization_id` boundaries.
14. **Offline behavior:** cache only the application shell/static assets; do not cache sensitive lead records in an unsecured service-worker cache.

## Open questions to resolve during repository confirmation
- Which repository is the intended CRM project, or is a new repository explicitly desired?
- Does the existing project already use React/Vite/Tailwind or another stack?
- Is Supabase already provisioned, and which project/environment is intended? Never request or record secret keys in chat.
- Is this a single-company CRM or a multi-organization SaaS?
- Is email sending only a `mailto:` handoff initially, or is a provider already selected?


## Repository inspection — 2026-11-13
- Target repository is confirmed as `himanshunishad98/Local-CRM-repository`, public, default branch `main`, empty (no root files, branches or commits).
- No existing framework, dependency set, Supabase project configuration, migration or tests are present.
- Stage 1 therefore starts from a clean repository after the Stage 0 documentation checkpoint is persisted. The proposed stack above is not yet installed or runtime-verified.
- Hosting provider and exact dependency versions remain intentionally undecided.
- GitHub Contents API write attempt was denied with HTTP 403 by the connected integration; no remote changes were made.
