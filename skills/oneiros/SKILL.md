---
name: oneiros
description: Verify and use the Qbyx Oneiros MCP to plan, generate, monitor, review, and deliver Dance video/audio or Dream images from an agent session.
---

# Oneiros

Use this skill whenever the user asks to work with Qbyx Oneiros from an
MCP-capable agent. The client owns no Oneiros UI, project state, approval state,
job state, monitoring, or media. Keep the user's selected compatible model and
provider as the planning brain. The canonical MCP server ID is `qbyx-oneiros`.

## Readiness

Before creating or resuming production state, verify that the `qbyx-oneiros`
MCP exposes the governed Oneiros tools and call `qbyx_oneiros_status` once. If
it is ready, continue without narrating setup. If the connection or Skill is
missing, read `references/connect.md`, use the supported local Oneiros
installer/reconnect path when it is
available and within the user's requested scope, then verify again. Never edit
agent configuration by guesswork or restart a busy Oneiros/ComfyUI service. If
Oneiros itself is absent or remains unavailable, stop before creating a project
and give one concise installation/start action plus the observed failure.

## Start or resume

Follow this lifecycle in order:

1. Call `qbyx_production_open` with empty workspace/session IDs for a new production.
   The first call prepares an opaque `open_request_id` without creating a project.
   Retry once with that exact value as `open_request_id`, workspace ID, and session
   ID; this creates or validates at most one project. Retain the returned
   `workspace_capability` for every later call and after compression. Oneiros also
   binds it to the current MCP transport for diagnostics. Some clients share one
   long-lived MCP session across conversations, so the opaque capability remains
   the actual isolation boundary. A valid retained capability reconnects
   automatically after an MCP or client restart. Never request a browser recovery page or an
   operator passphrase. If compression loses the capability, state plainly that
   the workspace cannot be selected safely from chat context; do not guess a recent
   project or create a duplicate.
   Omit project
   arguments for the safe default: a fresh isolated project. Use
   `project_action=existing` plus the exact selected project ID only after the
   user explicitly chooses an existing production. Never default to project 1,
   infer a recent project, or replace the backend binding.
2. Call `qbyx_production_status`. After context compression, use its returned
   production state as the recovery cursor. Resume the recorded phase instead
   of repeating settled questions, planning, or submission.
3. Call `qbyx_oneiros_catalog` for the chosen domain and use only installed
   workflows and their live schemas.
4. Plan with the matching deterministic planner, then call
   `qbyx_production_record_plan`. Present the exact workflow/model, prompt,
   references, overrides, Scene/Take, duration/aspect when applicable, stage,
   draft strategy, known limits, plan revision, and approval digest.
5. Call `qbyx_production_approve` only after the user explicitly asks to submit
   the presented plan in the current agent conversation. That tool authorizes
   the exact stored digest for one submission; do not ask for a second approval,
   open a localhost approval page, request a passphrase, or wait for an MCP
   elicitation card. The immutable digest, runtime/project binding and one-use
   submission lock remain enforced.
6. Call `qbyx_oneiros_generate_monitored` once for the approved revision. It
   consumes the backend approval. Do not use a boolean confirmation or a raw
   generation tool as authority.
7. Use `qbyx_oneiros_job` only for an explicit status check or reconciliation.
   The registered watcher observes the existing job and must never submit or retry.
8. Call `qbyx_production_review` for timestamped or image review notes. Preserve
   accepted Takes and plan only the smallest supported revision.

Keep tool use bounded: readiness once, open/status once, catalogue once, one matching planner,
then one plan record. Do not run broad searches, list every project or asset, or
repeat status while nothing changed. Report project, Scene, Take and current job
status in plain language without echoing raw payloads.

If the phase is `submitting`, `rendering`, or has an unknown outcome, reconcile
the recorded attempt/job and do not submit again. A monitoring or preview failure
does not authorize regeneration. Archiving or deleting the client conversation
does not delete Oneiros projects, workspaces, references, Takes, or media.

## Routes

Choose one domain and preserve one mode unless the user explicitly changes it:

- Dance / Auto: recommend the best compatible installed video/audio workflow.
- Dance / Guided: compare suitable installed choices and wait for the choice.
- Dance / Manual: preserve the exact workflow and controls.
- Dream / Auto: recommend an installed image workflow and settings.
- Dream / Guided: compare real image engines or composition/settings choices.
- Dream / Manual: preserve the exact image workflow and controls.

In Auto, Guided, and Manual, continue already-authorized monitoring and review
without reopening settled choices.
Guided must not silently choose an unresolved workflow.
Manual must preserve the user's workflow and controls.
Exact new GPU renders still require the governed approval lifecycle.
After compaction, read durable state before re-asking the user or repeating work.

Invoke the `oneiros-video` subskill for Dance work and the `oneiros-image`
subskill for Dream work. Do not load both unless a request genuinely crosses
domains. Continue in the already bound project folder when the request belongs
to that production. If it does not, ask before creating a new project and give
the concise reason a separate folder is needed.

## Delivery

Completion must match the registered job and originating Session. Verify each
artifact exists, is non-empty, and has the expected media type before claiming
success. Return native media markup and a clickable absolute path for every
verified output. Delivery repair reuses the existing artifact and job ID.
After the first verified output, ask one short follow-up: revise the current
generation or accept it. Dance adds the option to continue with a HyperFrames
edit; Dream asks only for targeted image changes. Do not start another render
or editing project until the user chooses.
