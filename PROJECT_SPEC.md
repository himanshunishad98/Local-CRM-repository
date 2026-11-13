# Product Specification — Smart Web-Based CRM

## Objective
A modern, responsive, cloud-hosted CRM for managing the complete enquiry-to-conversion lifecycle. Four pillars: lead management, communication management, sales pipeline, and follow-up automation.

## Users and access
- **Admin:** full CRM access; manage users, leads, pipeline, automation, reports, and settings.
- **Sales user:** access permitted leads; create/update leads; initiate call/WhatsApp/email handoffs; log activity; add notes; schedule follow-ups; update stages.
- Authentication: email/password, password reset, logout, protected routes, secure sessions.
- Database-level role authorization and Supabase Row Level Security are mandatory.

## Lead management
Lead fields include unique Lead ID, name, primary/alternate/WhatsApp phone, email, city/state/address, source, interested product/service, enquiry date, owner, priority, status, pipeline stage, expected value, conversion probability, tags, notes, creator/updater, and timestamps. Custom fields support text, number, dropdown, multi-select, date, checkbox, phone, and email. Required manual-entry fields: name, mobile, source, interest, status, and pipeline stage. IDs use `LEAD-000001` style.

Lead list: server-side search by name/phone/email/ID; filters for source, status, stage, owner, priority, product/service, tags, created date, and follow-up date; sorting, pagination, bulk selection. Lead profile includes contact/business details, owner, next action, notes, chronological activity, and prominent communication/follow-up actions.

## Import and export
Support XLSX, XLS, and CSV with upload, mapping, preview, validation, normalized-phone duplicate detection, policy selection (skip/update/create duplicate), batch processing, progress, summary, and failed-row report. Export to Excel/CSV. Large imports must not freeze the UI.

## Communication
Every activity is linked to a lead and records date/time, type, direction, result, user, and notes. Types include calls, WhatsApp, email, supported SMS/messages, internal notes, meetings, and follow-ups. Preserve history when stages change.

- **Calls:** `tel:`/device dialing handoff where supported. User manually logs result after returning. Outcomes: Connected, Interested, Follow-up, Converted, Not interested, No answer, Busy, Rejected, Failed. Duration is optional/manual or available only where a platform reports it. Clicking Call must not imply completion.
- **No recording:** permanently excluded. Store call metadata and user-entered notes only; no audio capture or processing.
- **WhatsApp:** open conversation through supported links; provide variable-based templates. Do not claim a message was sent/delivered solely because the app opened. Official WhatsApp Business Platform can be a later integration if authorized.
- **Email/SMS:** `mailto:` or supported device handoff for basic use. Direct sending requires a secure provider integration; never expose credentials in the browser. Do not claim sending/delivery without provider confirmation.

## Sales pipeline
Default stages: New, Contacted, Interested, Qualified, Demo/Meeting, Proposal/Offer, Negotiation, Converted. Outcomes: Not Interested, Lost, Invalid. Stages are configuration-driven, with ordering, colors, probability, transitions, drag/drop, and retained stage history.

## Follow-ups and automation
Follow-up fields: date/time, type, notes, assigned user, reminder. Types: Call, WhatsApp, Email, Meeting, Demo, Other. Views: today, upcoming, overdue, completed. Calendar supports day/week/month and opens the linked lead.

Automation examples: create first-call task within an hour of lead creation; schedule a follow-up two days after Interested; create a task after three days without activity. Use server-side scheduling, idempotency, duplicate-task prevention, and execution history. Browser timers are not authoritative.

## Dashboard and reporting
KPIs: total, new, contacted, interested, follow-ups today, overdue, converted, lost. Charts/reports: source, stage, monthly enquiries/conversions, communication, follow-up completion, sales/user performance. Date filters and CSV/Excel exports. Enforce permissions in every metric.

## Settings and notifications
Admin settings: company details/logo, lead sources, statuses, stages, tags, custom fields, user roles, email configuration, WhatsApp templates, automation rules, notification preferences, timezone. Notifications include new lead, approaching/overdue follow-up, inactive lead, upcoming meeting/demo. Default timezone: `Asia/Kolkata`.

## Application and proposed stack
Responsive web application with PWA support for desktop and mobile browsers (Chrome, Edge, Safari; Android and iPhone). No traditional Windows desktop software. Proposed stack from the supplied brief: React + TypeScript + Vite, Tailwind CSS, Supabase PostgreSQL/Auth/Edge Functions, and Vercel/Cloudflare/Render hosting. This is a recommendation, not yet verified against an existing repository.

## Security and reliability
HTTPS; Supabase Auth; RLS and role-based access; server-side validation and authorization; input validation; secure sessions; rate limiting where appropriate; audit logging; indexed/relational data; migrations in version control; backup/export strategy; safe deletion; error logging; duplicate prevention; recovery from interrupted imports. No secrets in frontend or repository.

## Final acceptance workflow
User logs in → uploads spreadsheet → imports leads → opens lead → initiates normal cellular call → logs outcome and notes → schedules follow-up → completes reminder → moves lead through pipeline → marks converted/lost → management reviews reports.

## Out of scope unless explicitly approved
Call recording of any kind; silent SIM control; guaranteed call completion/duration detection on all devices; claiming WhatsApp/email/SMS delivery without a provider; unapproved integrations or product features.
