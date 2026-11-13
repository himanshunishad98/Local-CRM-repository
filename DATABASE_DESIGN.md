# Initial Database Design Draft

This is a logical draft only. No SQL migration has been applied. Finalize after inspecting the target Supabase project and deciding single- vs multi-organization scope.

## Core entities

| Table | Purpose / key relationships |
|---|---|
| `profiles` | `id` references `auth.users`; profile details, active flag, role reference/enum |
| `leads` | Lead identity and business/contact fields; `owner_id`, `created_by`, `updated_by` reference profiles; source/status/stage references |
| `lead_sources` | Configurable source lookup |
| `lead_statuses` | Configurable operational status lookup |
| `pipeline_stages` | Configurable ordered stages, probability, color, terminal/outcome flags |
| `lead_stage_history` | Append-only stage transition history: lead, from/to stage, actor, timestamp |
| `lead_custom_fields` | Configurable field definitions and type/options |
| `lead_custom_field_values` | Typed/validated or JSON values linked to lead and field definition |
| `lead_tags` | Tag definitions |
| `lead_tag_relations` | Many-to-many lead/tag relation with unique pair constraint |
| `lead_activities` | Chronological communication, note, meeting and other activity events linked to lead/user |
| `calls` | Call metadata linked 1:1 to an activity: direction, outcome, entered/available duration, call timestamp; **no audio fields or storage** |
| `followups` | Scheduled action, due time, type, assigned user, status, notes, completion metadata; linked lead |
| `automation_rules` | Trigger, conditions, actions, enabled state, schedule/configuration |
| `automation_executions` | Rule run history, idempotency key, result/error, timestamps |
| `notifications` | Recipient, type, payload/reference, read/delivery state where applicable |
| `audit_logs` | Security-sensitive changes with actor, entity, operation, timestamp, metadata |
| `settings` | Company/application settings, timezone, preferences and non-secret configuration |

## Relationships (simplified)

```text
auth.users 1──1 profiles
profiles 1──* leads (owner / creator / updater)
lead_sources 1──* leads
lead_statuses 1──* leads
pipeline_stages 1──* leads
leads 1──* lead_activities 1──0..1 calls
leads 1──* lead_stage_history
leads *──* lead_tags (through lead_tag_relations)
leads 1──* lead_custom_field_values *──1 lead_custom_fields
leads 1──* followups
profiles 1──* followups (assignee)
automation_rules 1──* automation_executions
profiles 1──* notifications
```

## Important constraints and indexes
- UUID primary keys for internal records; unique human-facing lead number generated transactionally in PostgreSQL (sequence/counter strategy to be selected during migration design).
- Normalize phone values for duplicate detection; index normalized primary/alternate/WhatsApp phone values as supported by the chosen model.
- Index common list filters: lead owner, status, pipeline stage, source, priority, created timestamp; follow-up assignee/status/due timestamp; activity lead/timestamp; automation execution idempotency key.
- Foreign keys and explicit delete policies. Prefer archive/soft delete for leads where history must remain. Avoid cascading deletion of activities and audit records.
- Constrain allowed roles and activity/call/follow-up result values; validate all user-supplied values server-side.
- Use RLS for every user-accessible table. Design policies for Admin and permitted Sales users; test cross-user access denial.
- Keep secrets out of `settings` if they can be held in provider secrets/environment variables.
- Use UTC timestamps in storage and Asia/Kolkata for default presentation.

## Deferred until relevant stages
Import job/row staging tables, email-provider delivery events, external messaging webhook events, and multi-tenant organization tables should be added only when requirements and architecture justify them.
