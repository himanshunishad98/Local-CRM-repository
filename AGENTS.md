# Smart Web-Based CRM — Development Instructions

## Working rules
- Treat `docs/PROJECT_SPEC.md` as the product source of truth.
- Treat `docs/BUILD_PLAN.md` as the progress source of truth and `docs/NEXT_STEP.md` as the immediate task.
- Work on one stage at a time. Do not start a later stage before the current stage is accepted.
- Keep the application runnable after every implementation stage.
- Inspect before editing; preserve existing working functionality and avoid unrelated rewrites.
- Make focused changes only. Reuse existing components and dependencies; do not add packages without a demonstrated need.
- Do not generate or paste whole source files when a targeted edit is sufficient.
- Test the changed behavior, fix regressions, and record exact results before marking a stage complete.
- Stop at each checkpoint and wait for the explicit instruction `CONTINUE TO NEXT STAGE`.
- Do not claim that an external service, deployment, call, message, or test succeeded without evidence.
- Never commit credentials or secrets. Use environment variables and `.env.example` only.
- Keep project docs concise and update them at every completed stage.

## Product constraints
- This is a responsive, cloud-hosted web CRM with PWA support; no Windows desktop application is required.
- Use normal device calling handoff (`tel:` where supported); never promise silent SIM control or universal call-state detection.
- Call recording is permanently out of scope. Do not build recording, upload, storage, playback, synchronization, or audio processing.
- Log call metadata, outcomes, and user-entered notes only.
- Opening WhatsApp, email, or SMS handoff does not prove sending or delivery.
- Enforce authorization in the database with Supabase RLS, not only in the frontend.
- Use Asia/Kolkata as the default timezone.

## Stage protocol
1. Inspect repository, existing stack, dependencies, Supabase configuration, and reusable code.
2. Record the plan and decisions before implementation.
3. Implement only the current stage.
4. Run relevant checks and verify acceptance criteria.
5. Update `docs/BUILD_PLAN.md`, `docs/DEV_LOG.md`, and `docs/NEXT_STEP.md`.
6. Stop and report the checkpoint.
