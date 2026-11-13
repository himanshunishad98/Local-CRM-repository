# Build Plan and Stage Status

Status values: NOT STARTED · IN PROGRESS · BLOCKED · COMPLETED · TEST FAILED

| Stage | Scope | Status | Exit criteria |
|---|---|---|---|
| 0 | Repository inspection, architecture, documentation, database draft | **BLOCKED** | Repository identified and confirmed empty; architecture and project-memory docs drafted; docs committed/read back in target repository |
| 1 | React/TypeScript app shell, routing, responsive layout, design tokens, PWA foundation as appropriate | NOT STARTED | App starts; navigation and responsive layout work; no major console errors; production build passes |
| 2 | Supabase, migrations, profiles, auth, roles, RLS, protected routes | NOT STARTED | Login/logout/reset work; unauthorized data access rejected; migrations and RLS verified |
| 3 | Lead schema, ID generation, manual CRUD, list/profile, search, filters, duplicate detection | NOT STARTED | CRUD persists; search/filter/duplicate rules and permissions pass |
| 4 | XLSX/XLS/CSV import, mapping, preview, validation, batch import, exports | NOT STARTED | Valid/invalid/duplicate rows handled; progress and error report work; UI remains responsive |
| 5 | Configurable pipeline, Kanban, transitions, history, logging | NOT STARTED | Stage changes persist; history retained; unauthorized changes rejected |
| 6 | Calls handoff/logging, WhatsApp/email/SMS handoffs, templates, notes, activity timeline | NOT STARTED | Handoffs work where supported; manual logs attach to correct lead; no recording or false delivery claims |
| 7 | Follow-up CRUD, today/upcoming/overdue/completed lists, calendar, notifications | NOT STARTED | Follow-ups persist, link correctly, and overdue/notification behavior is verified |
| 8 | Automation rules, triggers, conditions, scheduled actions, idempotency, history | NOT STARTED | Correct triggers; no duplicate tasks; failures logged; timezone verified |
| 9 | Dashboard, charts, metrics, reports, filters, exports | NOT STARTED | Metrics reconcile to data; permissions and empty states work |
| 10 | PWA installability, service worker, offline shell, mobile optimization | NOT STARTED | Install works where supported; safe caching; update behavior verified |
| 11 | Full QA, performance/security checks, deployment, documentation | NOT STARTED | Critical workflows and security pass; performance tested at 10k leads/100k activities; deployment guide and QA report delivered |

## Stage 0 sub-checklist
- [x] Inspect mounted local workspace and available files.
- [x] Search connected GitHub repositories for a CRM project.
- [x] Identify and avoid unrelated available repositories.
- [x] Draft product and architectural documentation.
- [x] Draft initial relational database design.
- [x] Inspect the actual CRM repository, branches, commits and root contents.
- [x] Confirm that no source code, dependencies, or Supabase configuration exists.
- [x] Confirm proposed technology choices against the approved brief; exact package versions remain for Stage 1.
- [ ] Commit the project-memory documentation to the target repository and verify it by reading files back.

**Current blocker:** the target repository is now identified and confirmed empty. The GitHub connector returned HTTP 403 (“Resource not accessible by integration”) when attempting to create the initial README, so the documentation could not be committed remotely. No remote files, source code, or migrations were changed. The handoff ZIP contains the complete documentation pack.
