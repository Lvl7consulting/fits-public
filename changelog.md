# FITS Changelog

## [v8.9.0] - 2026-03-12

### Fixed
- **Employee CRUD**: Form validation fixes, security scoping for organization-bound queries, orphaned actor cleanup with per-actor delete action
- **Employee/Server hardening**: Deduplication in `get_applications_and_environments` using `(app, actor)` pairs; null-role guards in `get_projects`/`get_scopes`; sort by `(role, name)`; accessor migrations from `.
- **Server detail**: Lazy-resolved caching (`_ensure_resolved`) to avoid repeated DB hits; null-safe breadcrumbs and back-URL when environment/application missing
- **View improvements**: Standardized `json_error` signatures, proper exception imports, `get_object_or_404` usage, caching guards across employee/server views
- **Server list**: Guard against missing IPv4 in list metadata

## [v8.8.9] - 2026-03-12

### Changed
- **New Features**
- Added user notifications to confirm successful questionnaire saves and alert users to save failures
- **Bug Fixes**
- Improved error handling with more informative messages when save operations encounter issues
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Navigate to a questionnaire detail page with generated answers
- [ ] Edit an answer field and click Save — verify success toast appears and changes persist after reload
- [ ] Verify the Save button works for answers whose UIDs start with letters (a-f)
- [ ] Verify error toast appears when save fails (e.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Added missing `X-CSRFToken` header to `AnswerSaver.
- Fixed answer URL lookup in `CardHandler.
- Added user-facing success/error toast notifications via `NotificationSystem` so save results are visible

## [v8.8.8] - 2026-03-12

### Changed
- **Chores**
- Improved asset caching behavior to ensure users receive the latest version of resources when updates are deployed, reducing unnecessary downloads.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Verify Vite build produces hashed chunk filenames
- [ ] Verify entry files keep stable names (e.
- [ ] Confirm pages load correctly after deploy (no 404s on chunks)
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Adds `[hash]` to `chunkFileNames` in `vite.
- Entry files keep stable names since templates already cache-bust with `?v=` timestamps
- Fixes stale browser cache when shared chunk content changes but filename stays the same

## [v8.8.7] - 2026-03-12

### Changed
- **New Features**
- Added a "Delete Question" action in the answer editor with confirmation, safe question preview, CSRF-protected deletion, and user notifications.
- **Bug Fixes**
- Ensured questionnaire status updates reload the latest model state before marking processing/ready/failed to reduce consistency issues.
- **Refactor**
- Centralized CSRF token retrieval across the frontend to a single utility, replacing many in-file implementations.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Upload a questionnaire document
- [ ] While it's processing, select a policy from the dropdown
- [ ] Verify the policy selection persists after the page reloads upon processing completion
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Adds `self.
- Fixes race condition where the Celery parsing task's stale in-memory copy of the questionnaire node overwrites a concurrently saved `selected_policy_uid` on `save()`

## [v8.8.6] - 2026-03-12

### Changed
- **Style**
- Improved layout and positioning of questionnaire display in review and editor modes to better preserve surrounding layout structure.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Open a questionnaire that has no generated answers (review mode) — verify "Generate All Answers" button now works
- [ ] Open a questionnaire that already has answers (editor mode) — verify everything still works as before
- [ ] Verify review mode UI (question list, section toggles) still renders correctly inside the editor container
- <!-- This is an auto-generated comment: release notes by coderabbit.
- The `#questionnaire-editor` div was inside the `{% else %}` branch of the `review_mode` conditional in `detail.
- Without it, the JS entry point found no container, never instantiated `QuestionnaireEditor`, and the "Generate All Answers" button had no click handler — this is the root cause of the button doing nothing on production.
- Move the div outside the conditional so it always renders with the required data attributes.

## [v8.8.53] - 2026-05-10

### Changed
- **New Features**
- Activate/Deactivate toggle for individual email providers with immediate UI feedback and page reload.
- Inactive providers display a warning banner and disable the “Send Test Email” action.
- Dev/test safety flag to force-null email routing (prevents real sends for safe runs).
- **Bug Fixes**
- Email routing enforces provider active state per priority level — no silent fallthrough.
- <!-- end of auto-generated comment: release notes by coderabbit.
- `.
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- [x] Unit: ~3,770 tests pass via `.
- [ ] Manually flip Activate/Deactivate on a tenant email provider detail page and confirm the banner and greyed-out test button update without a server restart
- [ ] Manually click Send Test Email with the provider active (and `EMAIL_FORCE_NULL_PROVIDER=false`) — verify a real test mail arrives at the operator's address
- [ ] Manually click Send Test Email with the provider inactive — verify the 400 "Activate this provider" message
- [ ] Run \`npm run test:e2e -- email-providers/email-provider-activation.
- The branch went through a long planning loop before any code:
- Spec at `docs/superpowers/specs/2026-05-10-email-provider-toggle-design.
- 10 split implementation plans at `docs/superpowers/plans/2026-05-10-email-provider-toggle/` — cursor-agent (gpt-5.
- 10 implementation commits, then a `/simplify` cleanup pass, a final cursor-agent correctness review, and three follow-up commits to land the remaining review findings on this branch (no separate PRs).
- **Routing fix:** `UnifiedEmailService` no longer falls through to the system provider when a tenant has any configured provider but none active.
- **Single-active invariant:** activating a tenant provider deactivates any sibling active providers, making routing deterministic.
- **Cross-tenant ownership:** new `ProviderOwnershipMixin` enforces the owner check on detail / update / delete / test / activate / deactivate / assign / unassign — closing a pre-existing leak path.
- **UI:** new primary header button with the toggle, yellow inactive banner (reusing `alert_banner.
- **Template fix:** detail templates used `{% if provider.
- Replaces the global `EMAIL_PROVIDER_ENABLED` env var with a per-provider `is_active` toggle exposed via Activate/Deactivate buttons on tenant-admin and super-admin email-provider detail pages — no more container restart to pause mail.
- Closes the long-standing bypass where the **Send Test Email** button hit real providers even when global mail was disabled.
- Adds a separate dev/CI safeguard `EMAIL_FORCE_NULL_PROVIDER` plus a server-side `/__test__/email-safety/` probe so Playwright runs cannot leak real mail under any model state.

## [v8.8.52] - 2026-05-09

### Changed
- **Chores**
- Updated minimum langchain-core version requirement to >= 1.
- [![Review Change Stack](https://storage.
- <!-- end of auto-generated comment: release notes by coderabbit.
- Adds CVE-2026-44843 to the pip-audit ignore list.
- Cherry-picked from greenfield commit \`0aa5d5cbd\` so main's pip-audit goes green again.
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.

## [v8.8.51] - 2026-05-09

### Changed
- [x] `.
- [ ] Manual smoke: scope + project detail pages render correct gate state in browser.
- [ ] Verify Publish-locally + Confluence-publish disabled tooltip surfaces per-scope reasons.
- 🤖 Generated with [Claude Code](https://claude.
- Bundle of greenfield work since the last main merge:
- Local AI provider work (PR #422) follow-up: codex P2 fixes (URL `/v1` normalization, local chat-completions probe, keyless-local edit-page placeholder).
- "Publish locally" button on scope + project detail pages with eligibility gates (≥1 scope, ≥1 application, ≥1 audit template, ≥1 SME).
- Confluence "Publish Scope" + "Publish Project" buttons gated on per-scope content prerequisites with diagnostic tooltips.
- UI controller respects server-rendered `disabled` state.
- Employee-search performance: fulltext index, single-roundtrip count+page, multi-word matching across name/email.
- Two simplify passes: shared `scope_content_reasons` helper, `cached_property` migration, frozen-tuple eligibility, unified `publish_disabled` / `publish_reasons` template context.
- Various test/coverage adds and fixes (template comment leak, autouse stub-flag fixture, multi-policy-chat stale STATUS_UPDATE refs).

## [v8.8.50] - 2026-05-09

### Changed
- **New Features**
- Redesigned SME dashboard with co‑branding, per‑tenant briefing, and three buckets
- Persistent Submit with preview, background evaluation progress, and SOC “Evaluate now” via WebSocket
- **Improvements**
- Two‑column assessment UI, grouped sidebar, All‑done states and reusable Submit CTA
- Safer uploads: size/type checks, XLSX→CSV conversion; sign‑out flush ensures saves complete
- New evaluation KPIs surfaced in dashboard
- **Tests / Docs**
- Expanded unit, integration, Playwright coverage and rollout guidance
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] `.
- [ ] `.
- [ ] `.
- [ ] Resize viewport to 600px — sidebar stacks above panel, headers go static (per existing media query), questions still render under their control.
- [ ] After Playwright snapshot regen, spot-check diff to confirm intentional change.
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- **Playwright snapshot regen** — the new sidebar DOM (h3 headers + nested `<ul>`) will trip the existing 2% visual-diff threshold on `assessment.
- **Lands after #420a** (currently open as #420).
- **`de38bbb52`** `[rbac] feat(assessment-view): expose control_uid/title/number for SME sidebar grouping` — extends `_ASSESSMENT_CONTEXT_QUERY` RETURN with three control columns + ORDER BY `tc.
- **`e571c81fd`** `[frontend] feat(sidebar): group questions under their TemplateControl` — extends `Question` interface with optional `controlUid`/`controlTitle`/`controlNumber`; rewrites `renderQuestionList` to bucket by control via insertion-ordered `Map` and emit `<section data-testid="control-group-{uid}"><h3 class="sidebar-control-heading">{number} {title}</h3><ul class="sidebar-control-list">…</ul></section>`.
- **`9ff70ec11`** `[tests] test(question-list): control-group assertions for sidebar grouping` — adds Jest assertions covering group count, header content, and per-group question membership.
- **`240b15a99`** `[tests] test(assessment-view): real-Neo4j integration for control-field surfacing` — un-mocked Cypher round-trip confirming the new payload shape.
- **`1e3da4abd`** `[tests] test(model-inflate): DateTimeProperty round-trip lock-down` — carry-over from #420a smoke fixes; tightens the regression net for the neomodel datetime issue caught during smoke verification.
- Group the SME assessment-page sidebar's flat 20-question list under its parent **TemplateControl** as sticky `<h3>` headers, so SMEs answering a multi-control audit retain the section context they'd see on any printed compliance questionnaire.
- Plan: [`~/.

## [v8.8.5] - 2026-03-12

### Changed
- **Bug Fixes**
- Automatically reloads the questionnaire editor after background tasks complete, ensuring users see up-to-date content without manual refresh.
- Refined progress indicator behavior so it appears only while processing, reducing spurious or misleading progress displays.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Upload a questionnaire file, navigate to its detail page while still processing
- [ ] Verify the progress bar shows "Processing questionnaire.
- [ ] Wait for parsing to complete -- verify the page reloads automatically after ~1.
- [ ] Verify "Generate All Answers" bulk generation still reloads correctly after completion
- <!-- This is an auto-generated comment: release notes by coderabbit.
- When a questionnaire is in "processing" state, the editor now subscribes to `TASK_COMPLETED` events and triggers a page reload when parsing finishes.
- Previously only `STATUS_UPDATE` with `final_completion` (the bulk-generate pattern) triggered reloads.

## [v8.8.49] - 2026-04-30

### Changed
- **New Features**
- Local publication target with one-way migrate-to-local action and magic-link SME access flows
- Background local document evaluation, post-eval summary updates, and magic-link emit task
- **Backend**
- New local-publication endpoints, session/middleware, audit events, document storage, and dedicated Celery queue/worker
- **Frontend**
- New publication UI islands: dashboard, project, assessment, yes/no input, description, upload, document list, progress, and target/migrate controls
- **Tests**
- Extensive unit, integration, and Playwright E2E specs added
- **Documentation**
- Comprehensive planning, design, and runbooks for local publication and RAG optimization
- <!-- end of auto-generated comment: release notes by coderabbit.
- `0-docs/local-publication-workflow/12-decisions-log.
- `0-docs/local-publication-workflow/13-sme-access-flow.
- `0-docs/local-publication-workflow/plan/` — the 54-segment TDD plan this branch implements.
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Commit history is muddled in places.
- B-21's local document-evaluation Celery task wires the framework but returns a `NEEDS_CONTEXT` sentinel because the existing RAG core requires a `Policy` + `AIProvider` not present in the local SME flow.
- 7 of 8 Playwright e2e specs are `test.
- Out-of-scope side-threads tracked separately: project-wide delete-flow redesign (don't-delete-client-data rule), FITS-user access control for local SME pages.
- [ ] `.
- [ ] `.
- [ ] `npm test --prefix e2e-playwright -- tests/local-publication/` — 1 spec runs, 7 skipped pending Neo4j seed + Daphne + Vite-built bundles.
- [ ] Anonymous SME flow: GET `/publication/access-request/` → POST email → neutral confirmation regardless of match.
- [ ] Magic-link round-trip: email link click → 302 to `/publication/dashboard/` → cookie set → second click rejected.
- [ ] Re-issue invalidation: SME session 1 stays alive; re-request link; session 1's next protected request flushes (via `EmployeeSessionGen`).
- [ ] FITS-side: only users in the project's organization with `projects` RBAC module can flip `publication_target` or trigger `migrate-to-local`.
- [ ] Regression: confluence-only project's existing publish flow runs identically; no `local_publication` task enqueued.
- [ ] CSRF: authenticated POST/DELETE to `/publication/.
- [ ] Don't-delete-client-data rule: project-scope deletion design surface flagged for follow-up (out of plan scope).
- New `local_publication` Django app **parallel** to `confluence/` — per-project `publication_target` enum gates routing.
- **Magic-link SME access**: one-time tokens (sha256, `select_for_update` race-safe), long-lived signed-cookie sessions, audit log, 5/hr/IP rate limiting, per-employee `EmployeeSessionGen` counter so re-issue invalidates prior sessions across any session backend.
- **Live evaluation pipeline**: SME doc upload → Celery RAG → DocumentEvaluation update → post-eval status recompute → WebSocket push to live SME UI.
- **TS islands** per page (dashboard, project, assessment, Yes/No, description, upload, doc list, eval indicator, WS client, progress bar, hash-based nav) with their own calm design system.
- **30 backend + 19 frontend + 5 integration** TDD segments + 7 review-driven blocker fixes (post-eval dispatch, session-gen invalidation, MEDIA_ROOT, download endpoint, CSRF re-enable, RBAC + tenant scope on FITS endpoints).

## [v8.8.48] - 2026-04-18

### Changed
- [ ] Resolve the remaining 3 codex blockers above.
- [ ] `.
- [ ] Manual: log in as tenant admin, create a group, assign modules, add/remove members, and confirm user create/edit flow shows and submits `groups`.
- 🤖 Generated with [Claude Code](https://claude.
- `app/views/tenant_admin/groups/` — list / create / update / delete / members views + templates.
- `app/services/rbac/user_groups.
- `app/templates/v2/components/forms/group_assignment.
- Tests for list/create/update/delete/members flows.
- **[P1 — FIXED in this PR via 749ba645]** `form.
- **[P1]** Default-group conflict is detected too late — `app/services/rbac/user_groups.
- **[P2]** Admin accounts leak into the group-member picker — `app/views/tenant_admin/groups/members.
- **[P2]** Empty-modules selection silently reverts on edit retries — `app/views/tenant_admin/groups/update.
- **Status: draft** — needs PR-1.
- RBAC PR-5: tenant-admin UI.
- Stack: PR-0 → PR-1 → PR-2 → PR-3 → PR-4 → **PR-5** (tip).

## [v8.8.47] - 2026-04-18

### Changed
- [ ] Resolve kill-switch + org-switcher regressions.
- [ ] `.
- [ ] Manual: log in as a user missing `dashboard` and verify the landing cascade + 403 page work; flip `RBAC_ENFORCEMENT_ENABLED=false` and verify legacy routing.
- 🤖 Generated with [Claude Code](https://claude.
- `app/rbac/middleware.
- `app/utils/navigation_*` — post-login landing cascade by `landing_priority`.
- `app/rbac/sidebar.
- `app/views/auth/no_module_access.
- **[P1]** `RBAC_ENFORCEMENT_ENABLED` kill-switch is not honored in post-login routing — `app/utils/navigation_context.
- **[P2]** Org-switcher controls still hard-target `organizations:dashboard` — `app/templates/v2/pages/base.
- **[P3]** Sidebar recomputes `effective_modules()` from Neo4j on every render — `app/rbac/sidebar.
- **Status: draft** — needs PR-1.
- RBAC PR-4: middleware + post-login landing + dynamic sidebar.
- One deviation from the design doc: template restrictions forced `request.
- Stack: PR-0 → PR-1 → PR-2 → PR-3 → **PR-4** → PR-5.

## [v8.8.46] - 2026-04-18

### Changed
- [ ] Audit the allowlist entries flagged above.
- [ ] `.
- 🤖 Generated with [Claude Code](https://claude.
- 42 urlconf files tagged via `module_urls(<code>, urlpatterns)`.
- `app/rbac/constants.
- `app/rbac/tests/test_url_coverage.
- Two allowlist buckets in `app/rbac/constants.
- **[P2 / security]** Import APIs allowlisted without tenant/org checks — `app/rbac/constants.
- **[P2 / security]** Recovery endpoints allowlisted without ownership checks — `app/rbac/constants.
- **Fix direction:** either add ownership checks to the views (preferred — the allowlist comment already claims they exist) or drop the entries and tag the URLs with their real module.
- **Status: draft** — needs PR-1, PR-2 merged first, and the two P2 bypasses resolved.
- RBAC PR-3: enforcement wiring.
- Stack: PR-0 → PR-1 → PR-2 → **PR-3** → PR-4 → PR-5.

## [v8.8.45] - 2026-04-18

### Changed
- [ ] Resolve the P1 idempotency issue.
- [ ] `.
- [ ] Dry-run `rbac_seed_default_groups` in staging and verify rerunning is a no-op.
- 🤖 Generated with [Claude Code](https://claude.
- `app/models/tenant/user_group.
- `app/models/auth/user*.
- `app/management/commands/rbac_seed_default_groups.
- Tests for model invariants and `effective_modules()`.
- **[P1]** `rbac_seed_default_groups` loses idempotency on partial runs — `app/management/commands/rbac_seed_default_groups.
- **[P2]** Single-default invariant can be bypassed on create — `app/models/tenant/user_group.
- **[P3]** Seed enrolls tenant admins into `MEMBER_OF` — `app/management/commands/rbac_seed_default_groups.
- **Status: draft** — PR-1 must merge first, and the P1 above should be resolved before landing PR-2.

### Security
- RBAC PR-2: data model.
- Stack: PR-0 → PR-1 → **PR-2** → PR-3 → PR-4 → PR-5.

## [v8.8.44] - 2026-04-18

### Changed
- **New Features**
- Introduced a module registry system containing 13 modules with metadata (display names, descriptions, icon paths).
- Added URL pattern tagging functionality to organize routing.
- **Tests**
- Added comprehensive test suites validating module registry integrity and URL tagging behavior.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] `.
- [ ] Review for clarity / naming / docstrings.
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- **[P2]** `Module` currently exposes `display_name`/`icon_svg_path`/`landing_priority` but no `link_target` or `active_path_prefix`.
- **[P3]** `module_urls()` validates the module code with `assert module_code in MODULES`.
- `app/rbac/modules.
- `app/rbac/url_helpers.
- `app/rbac/constants.
- 13 unit tests for registry integrity and helper behavior.
- RBAC PR-1: foundation layer.
- Stack: PR-0 (design) → **PR-1** → PR-2 → PR-3 → PR-4 → PR-5.

## [v8.8.43] - 2026-04-18

### Changed
- **Documentation**
- Added a design spec for tenant-scoped, group-based RBAC: group assignment of module access, a tenant “Default” group for new users, admin bypass, dynamic sidebar gating based on effective group access, post-login landing selection by module priority, customizable access-denied page content, enforcement toggle (kill‑switch), URL coverage assurance, and an ordered rollout/rollback strategy with a comprehensive testing matrix.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Reviewers read the design doc end to end and leave comments where the spec is ambiguous or disagrees with stated constraints.
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- `0-docs/rbac-user-groups-modules/design.
- Design document for the RBAC user-groups + modules feature (see `0-docs/rbac-user-groups-modules/design.
- Landing order:
- 1.
- 2.
- 3.
- 4.
- 5.
- 6.

## [v8.8.42] - 2026-04-17

### Changed
- [x] Full unit suite (2545 tests) passes in pre-commit hook
- [x] Rendered all four templates via \`render_to_string\` and verified in Chrome at 1440x900 (light + dark)
- [ ] Manual smoke on staging: trigger a 404 (nonexistent URL), a 403 (cross-org link), a 500 (with DEBUG=False) and confirm each matches the design
- 🤖 Generated with [Claude Code](https://claude.
- Added: \`app/static/css/errors.
- Updated: \`app/templates/403.
- Replaces the bare unstyled 400/403/404/500 templates with a shared shell and four thin extensions.
- Shell renders a large gradient numeral, blueprint-grid backdrop, contextual icon, recovery CTAs (return home + go back), and a monospace detail strip.
- Per-status accent: 404 indigo, 403 amber, 500 rose, 400 sky.
- Self-contained \`app/static/css/errors.
- Dark-mode aware via the existing \`color-theme\` localStorage convention (preload script mirrors \`darkmode.

## [v8.8.41] - 2026-04-17

### Changed
- **New Features**
- Assessment templates now use organization-scoped URLs and navigation throughout the UI.
- Search and counts support organization+framework-scoped queries.
- **Bug Fixes**
- Removed legacy non-organization template route to prevent cross-organization URL leakage.
- Enforced organization/policy consistency during template create/update and tightened scoped access.
- **Tests**
- Added broad unit/integration tests covering org scoping, URL generation, queries, and regression checks.
- **Documentation**
- Added rollout plan and verification checklist for the migration.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] Full unit suite green (`.
- [x] New tests: org+framework query, mixin, list/detail/update/delete/questions/create scoping, header actions, framework row onclick, scope context, legacy URL resolver, TS endpoint (mock + integration marker)
- [x] Codex review × 3, all findings addressed
- [ ] **Manual smoke (before merge):**
- Log in as two users in different orgs; each visits `/organizations/<oid>/frameworks/<fw>/assessment-templates/` and sees only their own templates.
- Each manipulates the URL to another org's template uid → expect 404.
- Legacy `/frameworks/<fw>/templates/` → expect 404.
- Super-admin and tenant-admin: navigate frameworks → framework detail → audit templates without errors.
- [ ] **Data audit (before merge):** on demo DB, run:
- ```cypher
- MATCH (t:AssessmentTemplate)
- OPTIONAL MATCH (o:Organization)-[:OWNS]->(t)
- RETURN t.
- ORDER BY 3
- ```
- Attribute or delete any `<no-owner>` rows.
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- New `AssessmentTemplateQueries.
- New `TemplateOrgOwnershipMixin` wired into detail / update / delete / questions views.
- `AssessmentTemplateUrlService`: six non-org helpers deleted; all callers migrated to `get_org_*`.
- `AssessmentTemplate.
- `AssessmentTemplateCreateView` / `UpdateView` read org from URL `oid` (super-admin safe) and reject foreign policies with 403.
- `TemplateQuestionsManageView` verifies `templateRequirement_uid` belongs to the scoped template.
- Frontend: HTML `{% url %}` tags and `helpers.
- `frameworks/detail.
- Plan: `.

### Security
- **Security fix**: users could see every organization's AssessmentTemplates on `/frameworks/<fw>/templates/`.
- Removes the non-org URL mount; every template URL now requires `oid`.
- Fails closed: orphan templates (no org edge) cannot be created; foreign policy_uid on create/update returns 403.
- Codex CLI reviewed the diff in three rounds; all 8 findings fixed (P1 detail/questions header crash, TS endpoint drift, foreign-requirement leak, foreign-policy-on-update, orphan templates, etc.

## [v8.8.40] - 2026-04-17

### Changed
- **Chores**
- Updated dependency versions for enhanced stability and security, including core libraries, text processing tools, image handling, testing frameworks, and supporting packages.
- Updated security audit configuration to address known vulnerability advisories in dependencies.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] Local `pip-audit -r requirements.
- [x] Pre-commit hook ran full CI suite: 2491 passed, 75 deselected
- [ ] CI pip-audit workflow passes on this branch
- <!-- This is an auto-generated comment: release notes by coderabbit.
- **`GHSA-r7w7-9xr2-qq2r`** — langchain-openai image-token-counting SSRF.
- Fix is in `langchain-openai` 1.
- Repo currently pins `openai==1.
- Per the advisory itself, impact is limited to blind probing — the response body is consumed by `Image.
- | Package | From | To | Advisory |
- |---|---|---|---|
- | langchain-core | 1.
- | langchain-text-splitters | 1.
- | langsmith | 0.
- | pillow | 12.
- | pytest | 9.
- | python-multipart | 0.
- Nightly pip-audit run [#236](https://github.
- Adds `GHSA-r7w7-9xr2-qq2r` to the ignore list pending a separate `openai` 1.
- Local `pip-audit` with CI's ignore list now reports **"No known vulnerabilities found, 7 ignored"**

## [v8.8.4] - 2026-03-12

### Changed
- **New Features**
- Added progress indicator that displays when processing questionnaires.
- **Bug Fixes**
- Added user notifications for WebSocket connection errors to keep users informed of connectivity issues.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Upload a questionnaire file, then immediately navigate to its detail page -- verify the progress bar appears with "Processing questionnaire.
- [ ] On the detail page, verify that when the WebSocket connection is active, "Generate All Answers" works normally
- [ ] Simulate a WebSocket disconnect (e.
- [ ] Verify the same error toast appears when clicking individual "Regenerate Answer" buttons while disconnected
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Show the progress bar immediately when navigating to a questionnaire that is still being parsed after upload, by reading `data-questionnaire-status` from the template on page load.
- Surface a user-visible error notification when "Generate All Answers" or single answer generation is attempted while the WebSocket is disconnected, instead of silently failing.

## [v8.8.39] - 2026-04-17

### Changed
- **New Features**
- EU AI Act framework import/export and CSV generation
- New operational and scope reports with Excel export and charts
- Improved reliable policy chat with session persistence and robust UI components
- **Improvements**
- Modular, unified chart system for consistent visuals
- Refactored assessment and background task handling for more reliable progress updates
- Enhanced super-admin metrics dashboard with clearer sections and error states
- **Tests**
- Expanded unit tests for AI response manager and response streaming
- **Documentation**
- Added progress and guidance doc for refactor efforts
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Reviewer: spot-check a mixin split (e.
- [ ] Reviewer: spot-check a management command (e.
- [ ] CI runs green
- [ ] `pre-commit run check-file-length --all-files` passes
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- `.
- `.
- `.
- Test counts preserved exactly across every split (45→45, 65→65, suite-wide 2491→2491).
- Vite build verified for both TS refactors.
- | File type | Pattern | Example |
- |---|---|---|
- | Neo4j models | Mixin decomposition → `foo/__init__.
- | Non-command helpers | Package split → `foo/__init__.
- | Real mgmt commands | Thin `.
- | TS entry pages | Entry file kept + sibling directory with focused modules | `reliable-policy-chat/`, `super-admin-dashboard-metrics/` |
- | Pytest test files | Split by feature area + shared fixtures in `conftest.
- | Monitoring CLI scripts | Same as real commands (thin entry + underscore package) | `scripts/monitoring/test_confluence_credentials.
- **In:** Files >700 lines in `app/`, `confluence/`, `scripts/`, `e2e-playwright/`, `FITS/`.
- **Out:** Files 200–700 lines (deferred to round 2, ~270 files); `admin/` and `auth/` (Django vendored).
- **Refactored 12 files** >700 lines into ≤200-line focused modules (models, management commands, TS pages, components, test suites).
- **Deleted 3 verified-unused files** (~2,687 lines: `matrix_original_backup.
- **Added pre-commit enforcement** via `.
- **Excluded Django-vendored `admin/` and `auth/`** from the file-length checker.
- **Fixed one bug found during refactor:** restored `logger.
- Spec: `docs/superpowers/specs/2026-04-17-200-line-limit-round-1-design.

## [v8.8.38] - 2026-04-16

### Changed
- **New Features**
- New user-facing task exception for "vector store not ready" and centralized error handlers for task flows.
- Host-side file-length check added to lint/test workflow.
- **Bug Fixes**
- More consistent task-failure reporting, safer error-reporting when notification/event bus calls fail.
- Stable re-exports preserving public APIs after internal reorganizations.
- **Tests**
- Expanded/reorganized test helpers and suites for vector-store errors, task decorators, progress events, and RAG workflows.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] `.
- [x] `.
- [x] Pre-commit full CI suite (lint + unit) ran green on commit
- [ ] Manual: trigger a policy chat with no processed vector store → expect the friendly "No processed vector store available…" toast via WebSocket, no backend-exception email
- [ ] Manual: delete a VS on OpenAI while it is still `processed` in DB → expect the "re-upload the policy documents" message and the VS node flipped to `failed`
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- `get_validated_remote_vector_store_id` raises `VectorStoreNotReadyError` (UserFacingTaskError subclass) instead of `RuntimeError`.
- No other runtime logic changed — the refactor is a pure move of code into smaller modules with matching imports.
- Surface vector-store-not-ready to the user via WebSocket with a specific `VECTOR_STORE_NOT_READY` error_code (was a generic backend exception + failure email).
- Split `app/tasks/base.
- Split the corresponding test modules along the same boundaries; each test file now stays ≤200 lines.
- Add `scripts/check_file_length.

## [v8.8.37] - 2026-04-15

### Changed
- **Bug Fixes**
- Enhanced detection and handling of vector stores that have expired or been deleted on the provider side, with improved error messaging for better troubleshooting.
- **Documentation**
- Added validation guidelines for vector store readiness and documented guard mechanisms to prevent usage of stale or failed stores.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] Docs-only change — CI passes (no app code changed)
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Updates three architecture docs to match the `get_validated_remote_vector_store_id()` helper shipped in #405.
- **`05-policy-chat-flow.
- **`03-vector-stores-and-files.
- **`03-single-policy-task.

## [v8.8.36] - 2026-04-15

### Changed
- **New Features**
- Added support for independent Questionnaire and Documentation publication types in Confluence publishing workflow.
- Enabled separate folder structures and page organization per publication type.
- Added publication tracking with status monitoring and error recording.
- **Documentation**
- Comprehensive design documentation for publication-type feature architecture, page hierarchy, model changes, trigger architecture, folder lifecycle, unpublish behavior, and testing strategy.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] 9-cell pytest matrix: `{questionnaire, documentation, all} × {first-publish, republish, unpublish}`
- [ ] Partial failure under `all` — questionnaire committed, documentation `last_error` set
- [ ] Dedup collision — second button press during in-flight task correctly blocked
- [ ] Folder creation race — advisory lock prevents duplicate folders
- [ ] Version CAS — concurrent republish handled correctly
- [ ] Cross-domain auth denial
- [ ] Jest: two-button UI (disabled state, progress label, error banner)
- [ ] Run via `.
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Full spec and implementation plan in `0-docs/confluence-publication-type/`:
- `README.
- `00-problem.
- `implementation-plan.
- `progress.
- Adds two independent publish buttons per AssessmentTemplate: **Publish Questionnaire** and **Publish Documentation**
- Introduces `PublicationType` enum (`questionnaire` / `documentation` / `all`) threaded through the existing Celery publish pipeline
- Two thin folder pages under `EnvironmentPage` isolate the page hierarchies — all existing page titles unchanged (parser contract preserved)
- New `TemplatePublication` node tracks per-`(scope, env, template, type)` Confluence page IDs with optimistic version locking
- Typed `confluence_page_id_questionnaire` / `confluence_page_id_documentation` fields added to structural models; legacy `confluence_page_id` backfilled then retired
- Advisory lock per `(env_uid, publication_type)` prevents folder creation races
- `find_active_task` dedup extended with `publication_type` key

## [v8.8.35] - 2026-04-15

### Changed
- **Bug Fixes**
- Remote-assistant flows now require a processed vector store ID and perform preflight checks with the AI service; clear RuntimeErrors are raised if a store is missing or deleted.
- Stale or deleted vector stores are proactively marked as failed to avoid repeated attempts.
- **New Features**
- Added remote vector-store validation and a utility to verify existence with the AI service before use.
- **Tests**
- Expanded coverage for status guarding, preflight validation, error propagation, and end-to-end remote vector store selection.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] All 2459 unit tests pass (CI green)
- [ ] `TestGetPolicyVectorStoreIdStatusGuard` — status guard for all non-processed statuses
- [ ] `TestValidateVectorStoreExists` — returns bool, re-raises non-404 errors
- [ ] `TestMarkVectorStoreFailed` — sets status, swallows only DoesNotExist, re-raises infra errors
- [ ] `TestGetValidatedRemoteVectorStoreId` — happy path, missing VS, deleted-on-OpenAI
- [ ] Each task file: resolves VS for remote_assistant, skips for local_rag, raises when VS missing, raises when VS deleted on OpenAI
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- | File | Before | After |
- |------|--------|-------|
- | `policy_chat_rag_v2/task.
- | `multi_policy_query_single_v2/task.
- | `questionnaire_answer_rag_v2/task.
- | `policy_requirement_processing_rag_v2/task.
- | `template_question_generator_rag_v2/task.
- | `questionnaire_adapter.
- **Root cause**: OpenAI vector store IDs stored as `status=processed` in Neo4j could be deleted/expired on OpenAI's side, causing `Vector store with id [.
- **Fix — Scenario A (race condition)**: Status guard added to all three VS-ID lookup paths — only returns an ID when `status == 'processed'`; pending/uploaded/failed stores are skipped.
- **Fix — Scenario B (stale-processed)**: New `validate_vector_store_exists()` makes a cheap `retrieve()` call to OpenAI before any AI query; `mark_vector_store_failed()` self-heals the DB node on 404.
- **Centralized helper**: `get_validated_remote_vector_store_id(policy, ai_provider)` combines status guard + raise-on-missing + proactive OpenAI existence check + self-heal into a single call, applied uniformly across all entry points.
- **Silent fallback eliminated**: Four task files (`questionnaire_answer_rag_v2`, `policy_requirement_processing_rag_v2`, `template_question_generator_rag_v2`, `questionnaire_adapter`) were either silently falling back to `local_rag` or passing `[]` to file_search when no VS was available — all now raise `RuntimeError` with a clear message.

## [v8.8.34] - 2026-04-14

### Changed
- # Release Notes
- **New Features**
- Multi-policy chat for simultaneously querying multiple policies
- Intelligent policy routing to direct questions to relevant policies
- Answer synthesis combining responses into a single summary
- Conversation history with ability to resume previous chats
- Optional policy pre-selection for targeted queries
- Multi-policy questionnaire answering
- **Improvements**
- Enhanced knowledge profile generation for improved routing accuracy
- Refined access control for policy management
- Extended WebSocket heartbeat timeout for better connection stability
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] TDD — tests written before each implementation chunk
- [ ] `.
- [ ] Playwright E2E: Strong Tiger org, 3 seed policies with RAG stores
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- | # | Chunk | Status |
- |---|-------|--------|
- | 01 | Branch + Constants | ⬜ |
- | 02 | Data Models | ⬜ |
- | 03 | Single-Policy Task (scatter) | ⬜ |
- | 03b | Synthesis Task (gather+cleanup) | ⬜ |
- | 03c | Knowledge Profile Task | ⬜ |
- | 04 | Router LLM + Consumer | ⬜ |
- | 05 | Policy Chat UI | ⬜ |
- | 09 | Chat List + Resume | ⬜ |
- | 10 | Policy Pre-selection | ⬜ |
- | 06 | Questionnaire Integration | ⬜ |
- | 07 | Unit Tests | ⬜ |
- | 08 | E2E Tests (Playwright) | ⬜ |
- A reusable engine that intelligently routes a user query to relevant policies, collects RAG-grounded answers, and synthesizes them into one concise response.
- **Architecture**: Router LLM → Selective Scatter → Gather → Synthesize
- Router reads Knowledge Registry (per-policy profiles) + conversation history → selects relevant policies only
- One Celery task per selected policy (parallel) → each queries its own RAG store
- Synthesis task merges N raw answers into one response via single LLM call
- Sub-chat results are ephemeral — deleted after synthesis
- Master chat conversation persists with full history
- **Zero touch to existing features** — all new files.

## [v8.8.33] - 2026-04-14

### Changed
- **New Features**
- Role-based gating applied broadly to policy and chat pages: super-admins and tenant-admins are redirected to their dashboards; regular users keep access.
- **Tests**
- Added comprehensive tests covering redirect and non-redirect behavior for SUPER_ADMIN, TENANT_ADMIN, and USER across policy, chat, super-admin, and tenant-admin flows.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] 45 policy access tests — all green
- [x] 10 domain segregation tests — all green
- [x] Full unit suite — 2287 passed, 0 failures
- [x] Lint clean
- [ ] Manual: log in as super-admin, confirm redirect to `/super-admin/` on any `/organizations/{id}/policies/*` URL
- [ ] Manual: log in as tenant-admin, confirm redirect to `/tenant-admin/` on any `/organizations/{id}/policies/*` URL
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Super-admins and tenant-admins were able to navigate directly to regular-user domain URLs such as `/organizations/{id}/policies/create/`
- Added new `RegularUserOnlyMixin` — only `USER` role passes through; `SUPER_ADMIN` → `/super-admin/`, `TENANT_ADMIN` → `/tenant-admin/`
- Applied to all 15 policy views (create, list, detail, update, delete, chat, chat_list, chat_detail, chat_delete, chat_rename, download×2, sync_knowledge_base, sections, assistant_model)
- 45 new TDD tests for policy views (3 per view: super-admin blocked, tenant-admin blocked, user allowed through)
- 10 new domain segregation tests for super-admin and tenant-admin domains

## [v8.8.32] - 2026-04-13

### Changed
- **New Features**
- Remote-assistant question generation using vector-store IDs; progress events and automatic parsing/saving of generated questions.
- **Improvements**
- Mode-aware session initialization and validation; session metadata records the active store ID.
- Frontend: form actions use template-rendered create/update URLs; form button overlay retrieved lazily; more robust template rendering context for question lists.
- **Bug Fixes**
- Update handler now returns a controlled error response on failure.
- **Tests**
- Extensive unit, integration and E2E coverage for generation paths, routing, helpers, persistence, and UI.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] `test_remote_assistant_with_vector_store_id_succeeds` — Chat.
- [x] `test_remote_assistant_without_vector_store_id_reports_error` — CONFIGURATION_ERROR reported
- [x] `test_local_rag_with_rag_store_id_succeeds` — Chat.
- [x] `test_local_rag_without_rag_store_id_reports_error` — CONFIGURATION_ERROR reported (regression)
- [x] Full unit suite: 2096 passed
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- `get_assistant_info` now returns `(rag_store_id, vector_store_id, integration_mode)` matching the `PolicyChatUtils` pattern
- `_handle_initiate_session` is now mode-aware: checks the right ID per mode and passes the correct kwarg to `Chat.
- Updated `test_vector_store_id_responses.
- Added 4 new TDD tests covering both modes (success + missing ID paths)
- `get_assistant_info` only returned `(rag_store_id, integration_mode)` — it never fetched `vector_store_id` from `policy.
- `_handle_initiate_session` checked `if not rag_store_id:` unconditionally — always `None` in `remote_assistant` mode, so the error always fired regardless of configuration
- `Chat.

## [v8.8.31] - 2026-04-13

### Changed
- **New Features**
- Added Google Generative AI integration.
- **Refactor**
- Modernized RAG pipeline for improved retrieval, parsing, and consolidated answer+source responses.
- **Bug Fixes**
- More consistent conversation history routing and effective window sizing for session-based chats.
- **Chores**
- Upgraded core dependencies and LangChain ecosystem; added npm package resolution override.
- **Documentation**
- Added a security vulnerability remediation plan.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] 2091 unit tests passing on branch
- [x] Docker build resolves all dependencies cleanly (`requirements-audit.
- [x] Pre-push dependency resolution check passed
- [ ] Verify RAG v2 chain behaviour in staging (LangChain LCEL migration)
- [ ] Confirm Celery workers restarted after deploy
- 🤖 Generated with [Claude Code](https://claude.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- **ujson 5.
- **PyMuPDF 1.
- **Django ≥5.
- **npm flatted 3.
- **LangChain ecosystem v0.
- **Pygments CVE-2026-4539**: No fix available upstream — alert dismissed with `tolerable_risk` reason

## [v8.8.30] - 2026-03-25

### Changed
- [ ] Open `0-docs/presentations/fits-coherence-deck.
- [ ] Review data-flow docs in `0-docs/data-flow/` for accuracy
- 🤖 Generated with [Claude Code](https://claude.
- | # | Slide |
- |---|-------|
- | 01 | The Compliance Chaos Problem (dark hook) |
- | 02 | The Fragmented Tool Landscape |
- | 03 | Meet Sarah — A Day Without FITS |
- | 04 | The Hidden Cost (stat callouts) |
- | 05 | Introducing FITS (hero slide) |
- | 06 | Feed It Your World (inputs) |
- | 07 | AI Does the Heavy Lifting |
- | 08 | One Action.
- | 09 | Sarah's Day — With FITS |
- | 10 | Not Another AI Chat.
- | 11 | From Chaos to Coherence (CTA) |
- **`0-docs/data-flow/`** — Mermaid data-flow diagram (md/svg/png/hires), abstract marketing diagram, and 10 detailed findings docs covering: file upload pipeline, AI providers, Confluence/Jira, email providers, report generation, core data models, Celery tasks, RAG/vector store, API endpoints, and policy workflow
- **`0-docs/presentations/`** — "From Chaos to Coherence" 11-slide marketing pitch deck (`.
- **`docs/superpowers/specs/`** — Presentation design spec
- **`.

## [v8.8.3] - 2026-03-12

### Changed
- [x] `migrate_data --list` shows `migrate_system_frameworks` at order 100
- [x] `migrate_system_frameworks --dry-run` completes 6/6
- [x] `migrate_system_frameworks` (live) refreshes all 6 existing frameworks without errors
- [x] Docker production build succeeds
- **New file**: `app/management/commands/migrate_system_frameworks.
- **Modified**: All 6 `generate_*_framework.
- New `migrate_system_frameworks` data migration that orchestrates all 6 `generate_*_framework` commands, auto-discovered by `migrate_data` on every deploy
- Existing frameworks get metadata refreshed (description, is_system) via direct Cypher; controls and requirements are never overwritten
- Fixes BCDR framework missing `is_system=True` on initial creation

## [v8.8.29] - 2026-03-18

### Changed
- [ ] Verify README renders correctly on GitHub repo page
- [ ] Confirm all sections are accurate and complete
- 🤖 Generated with [Claude Code](https://claude.

### Security
- Complete rewrite of README.
- Covers all 4 user roles: super admin, tenant admin, organization user, client
- Documents every feature: policies, policy factory (7-step AI workflow), AI chat, frameworks, assessments, document evaluation, questionnaires, employees, spaces/Confluence, self-service import, dashboard/reporting
- Full AI & RAG architecture documentation (local RAG vs remote assistant, 4 LLM providers)
- Real-time WebSocket communication system with 12 consumer types
- Complete technology stack, deployment architecture, security model
- CI/CD pipeline and testing documentation
- ~800 lines of comprehensive documentation

## [v8.8.28] - 2026-03-18

### Changed
- [ ] Check GitHub repo page shows the root README after merge
- 🤖 Generated with [Claude Code](https://claude.
- Remove `.
- The repo was showing "GitHub Configuration" instead of the actual project README

## [v8.8.27] - 2026-03-18

### Changed
- [ ] pip-audit GitHub Action passes on this branch
- [ ] Docker container builds successfully with updated packages
- 🤖 Generated with [Claude Code](https://claude.
- **pyasn1** 0.
- **PyJWT** 2.
- **pyOpenSSL** 25.

## [v8.8.26] - 2026-03-18

### Changed
- **New Features**
- Executive Brief mode (policy statements) and deep-linking to individual processes.
- Hierarchical Process → Procedure model with per-process editing and nested steps.
- **Improvements**
- Redesigned policy UI with legend-driven cards, clearer process/procedure display, generated-policy pages, DOCX export improvements, and KB sync/status indicators.
- Questionnaire AI suggests titles; answers now record model confidence.
- **Bug Fixes**
- Safer temporary file handling and improved extraction fallback for uploaded documents.
- <!-- end of auto-generated comment: release notes by coderabbit.
- **docs: separating process and procedures from policies and safeguards (requirements, analysis)**
- **feat: process/procedures separation – docs, models, services, tasks, views**
- **Policy template, process/procedures separation, sections and related updates**
- **feat: executive brief skips procedures, shows "Policy Statements"**
- **Policy template: schemas, prompts, AI generation and tests**
- **Add icon-document-check and icon-document-text header icons**
- **Policy template review list and section UI/view updates**
- **Process/procedures separation: questionnaire parser, detail view, and task updates**
- <!-- This is an auto-generated comment: release notes by coderabbit.

## [v8.8.25] - 2026-03-16

### Changed
- [ ] `.
- 🤖 Generated with [Claude Code](https://claude.
- Add `task.
- Previously task status stayed IN_PROGRESS in the database on exception — now explicitly marked FAILED
- Addresses PR #387 review: Space.

## [v8.8.24] - 2026-03-16

### Changed
- [ ] `.
- [ ] Open manage-content in two tabs: Tab 2 sees active task status on connect
- [ ] Duplicate INITIATE_TASK returns validation error
- 🤖 Generated with [Claude Code](https://claude.
- Add `ActiveTaskChecker` helper for concurrent task prevention
- Update `ConnectionHelper` to check active tasks on WebSocket connect
- Update `DeletionHandler` to guard against duplicate INITIATE_TASK
- Fix `CompletionHandler` to report errors to client on failure
- Fix mutable default argument in `AssessmentTemplate.
- Mask `NEO4J_PASSWORD` in `restart_celery.
- Add 12 new tests, update docs and background-task-setup skill

## [v8.8.23] - 2026-03-16

### Changed
- [ ] Space page deletion flow works end-to-end
- [ ] Spinner renders correctly in buttons
- [ ] Policy and login pages render correctly
- 🤖 Generated with [Claude Code](https://claude.
- Space page deletion UI improvements
- Spinner component updates
- Policy and login template fixes

## [v8.8.22] - 2026-03-16

### Changed
- [ ] Verify README renders correctly
- [ ] Existing tests pass
- 🤖 Generated with [Claude Code](https://claude.
- Update README documentation
- Space page deletion consumer, task, and related docs

## [v8.8.21] - 2026-03-16

### Changed
- **New Features**
- Real-time progress tracking for Confluence page deletion with live WebSocket updates showing deletion progress as it happens
- Persistent task tracking that survives reconnections and resumes from where it left off
- **Improvements**
- Replaced form submission with WebSocket-driven deletion for faster, more responsive operations
- Enhanced error handling and recovery for page deletion tasks
- <!-- end of auto-generated comment: release notes by coderabbit.
- **fix: reliable-scope-ai-assessment class updates**
- **chore: v2 consumers, progress-bar utils, restart scripts and tests**
- **feat: space page deletion consumer v2, confluence page delete task, assessment template and manage content updates**
- <!-- This is an auto-generated comment: release notes by coderabbit.

## [v8.8.20] - 2026-03-16

### Added
- feat: left menu icons and related template/component updates

## [v8.8.2] - 2026-03-12

### Deferred (2 alerts — require separate LCEL migration)
- [x] All 1430 unit tests pass
- [x] `npm audit` reports 0 vulnerabilities
- [x] `pip install -r requirements.

## [v8.8.19] - 2026-03-15

### Changed
- **New Features**
- Comprehensive v1 to v2 migration framework with 44-step implementation plan and detailed coordination protocols.
- Added v2 WebSocket consumer infrastructure with updated coordination patterns.
- New policy processing completion coordination documentation.
- New scope assessment questions retrieval consumer with full task orchestration.
- **Breaking Changes**
- WebSocket endpoints migrated from `/ws/v1/` to `/ws/v2/`.
- API endpoints migrated from `/api/v1/` to `/api/v2/`.
- Integration mode simplified: remote_assistant mode removed; all providers now use local_rag exclusively.
- All consumer classes renamed to V2; V1 versions no longer available.
- **Improvements**
- Unified local RAG implementation across all AI providers.
- Updated chat initialization to use rag_store_id instead of vector_store references.
- Streamlined task and message handling with v2 async patterns.
- Enhanced completion coordination and task tracking for WebSocket consumers.
- <!-- end of auto-generated comment: release notes by coderabbit.
- Frontend/API callers still using `/api/v1/` or `/ws/v1/` may need a coordinated follow-up (see plan review in docs).
- Pre-commit (lint + unit tests) passed on commit.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- **Consumers:** `app/consumers/v1/` → `v2/` (dir + file renames, class renames, all imports)
- **Celery tasks:** All `_celery_v1` → `_celery_v2` (confluence, policy, questionnaire, notifications)
- **Task model:** `send_*_v1_async` → `send_*_v2_async`
- **Routing:** WebSocket route names and `ws/v1/` → `ws/v2/` paths; API remains `/api/v1/` (no `api/v2/` in this PR)
- **Settings:** `CELERY_TASK_ROUTES` and related keys updated to v2 task names
- **Docs:** `0-docs/2026-03-14-v1-to-v2-migration/` — README, AGENT-PROTOCOL, 44 step files
- **Cursor rule:** `websocket-v1-architecture.
- **Cleanup:** Removed stale `app/tasks/0-docs/celery_task_improvements/` docs
- Complete v1→v2 rename across consumers, Celery tasks, Task model, WebSocket/API routing, and settings.

## [v8.8.18] - 2026-03-13

### Changed
- [x] Tested on both dev and demo environments during live policy processing
- Adds `scripts/development/diagnose_channel_layer.
- Works with read-only containers via stdin piping
- Useful for debugging WebSocket consumers (policy processing, document evaluation, publishing, etc.

## [v8.8.17] - 2026-03-13

### Fixed
- Progress bar flicker on demo: alternating per-task (30/100) and aggregate (2/21) progress values caused the bar to disappear and reappear erratically

### Changed
- [x] All 26 existing message forwarder + completion handler tests pass
- [x] Manual verification: dev shows stable "Completed X/Y tasks" without flicker
- Splits `_launch_tasks` into two passes: create+track all Task nodes first, then dispatch `.
- Closes a race window where fast Celery workers send `TASK_PROGRESS` before all UIDs are registered in the tracker, causing those events to bypass `is_tracked()` and leak raw per-task progress (0-100%) to the frontend

## [v8.8.16] - 2026-03-13

### Fixed
- Neo4j `CartesianProduct` INFORMATION notification: `MATCH (them), (us) WHERE elementId(them)=$them and elementId(us)=$self MERGE(us)-[r:\`ADDRESSES\`]->(them)` — now silenced across all call sites

### Changed
- [x] 9 new unit tests in `app/services/queries/tests/test_instruction_connect_relationships.
- [x] Existing connection tests updated to assert delegation to `InstructionQueries.
- [x] All 13 tests pass (`pytest` inside container)
- **`app/services/queries/instruction_queries.
- **`app/tasks/v1/policy_template_generation/ai_generation/content_saver.
- **`app/tasks/v1/policy_processing/instruction_handling.
- Replaces neomodel's `.
- Introduces `InstructionQueries.

## [v8.8.15] - 2026-03-13

### Changed
- The toast suppression was in reliable-policy-chat.

## [v8.8.14] - 2026-03-13

### Fixed
- Stale `chat_manager.
- Neo4j UID passed as vector_store_id instead of OpenAI `vs_*` ID (3 consumers)
- `additionalProperties: false` missing from structured JSON schemas
- Chat completion green toast notification shown unnecessarily
- [x] 1,543+ unit tests pass (pre-commit hook runs full suite)
- [x] All new TDD tests cover Responses API flows: streaming, structured output, file_search, vector store ops
- [x] Vector store ID resolution tests verify OpenAI `vs_*` IDs used (not Neo4j UIDs)
- [x] Sync Knowledge Base view tests: success, non-finalized rejection, service error handling
- [ ] Manual: send chat message, verify streaming response with no green toast
- [ ] Manual: sync knowledge base on finalized policy, verify vector store updated
- [ ] Manual: verify policy analysis/gap closing still works end-to-end

### Removed
- `AIAssistantManager`, `AIChatManager`, `ai_factory`, `ai_assistant_ops`, `ai_chat_ops/`, `ai_thread_ops`, `ai_context_managers`
- `question_generation_models.
- Legacy `vector_store/files.
- All legacy Assistants API test files
- Deprecated model fields and their read sites

### Changed
- All AI consumers/tasks now use `OpenAIResponsesManager` instead of `AIAssistantManager`/`AIChatManager`
- Chat model uses `last_response_id` instead of `thread_id` for conversation continuity
- Policy finalization checks `VectorStore` relationship instead of `openai_assistant_id`
- `cleanup_ai_resources` management command updated for Responses API
- Vector store ID resolution uses `vectorStore.

### Added
- `OpenAIResponsesManager` — thin wrapper around `client.
- `PolicySyncKnowledgeBaseView` + URL route + TypeScript handler with confirmation modal
- ~2,800 lines of new TDD tests across 20+ test files covering all migrated flows
- Stream event type debug logging in `stream_response`

## [v8.8.13] - 2026-03-13

### Changed
- **Bug Fixes**
- Settlement now counts both completed and failed tasks; final completion is sent only after all tasks are settled and failure events are handled.
- **New Features**
- Failure events are intercepted and routed to the settlement handler so failed tasks update progress, counts, and finalization.
- **Documentation**
- Multi-task coordination docs updated to explain settled vs completed and the need to handle both success and failure events.
- **Tests**
- Expanded tests covering completion, failure, mixed settlements, delivery semantics, and final_completion emission.
- **Chores**
- Reduced logging verbosity across several background processing paths.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] 43 tests pass across all 4 test files (tracking, completion, forwarder, orchestrator)
- [x] `test_realistic_59_tasks_with_15_failures` reproduces the exact 44/59 scenario
- [x] Mixed complete/fail, all-fail, partial settlement, edge cases all covered
- [x] New `test_message_forwarder.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- `MessageForwarder` now intercepts `TASK_FAILED` for tracked tasks (same as `TASK_COMPLETED`), routing them to `TaskCompletionHandler.
- `TaskTrackingHelper` tracks `failed_tasks` alongside `completed_tasks`; settlement = completed + failed >= total
- `TaskCompletionHandler.
- Updated `multi-task-coordination/SKILL.
- **Root cause:** When tasks failed, `MessageForwarder` forwarded `TASK_FAILED` to the client unhandled.

## [v8.8.12] - 2026-03-13

### Changed
- Docstrings generation was requested by @bbalvl7.

## [v8.8.11] - 2026-03-13

### Added
- Regression tests for `user.
- Tests for brace-balanced JSON extraction (nested objects, trailing braces)
- Tests exercising `_retry_with_backoff` coroutine with mocked `asyncio.

### Fixed
- **Milestone email crash** — `consumer.
- **Defensive null check** — skip milestone email when `consumer.
- **AI response extraction** — iterate all `TextContentBlock` items in messages, not just `msg.
- **JSON over-capture** — replace greedy `\{.
- **Pydantic v1 deprecation** — replace `schema.
- **Inconsistent string conversion** — normalize `{e}` / `{str(e)}` to `{e!s}` in AI processing error path
- **Dead code** — remove unused variable extractions in `process_completion_data`
- **Test reliability** — convert async retry tests from `unittest.
- **Test strictness** — add `strict=True` to `zip()` calls in test assertions

### Changed
- **New Features**
- Enhanced progress tracking for policy processing workflows.
- **Bug Fixes & Improvements**
- Improved policy processing completion flow to ensure final status is always delivered, even when auxiliary operations fail.
- Better handling of API rate limits—now retried automatically instead of failing immediately.
- Cleaner AI-generated content with citation annotations removed.
- Strengthened JSON parsing and response extraction with fallback mechanisms.
- **Performance**
- Increased concurrent task processing capacity for faster policy handling.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] All new and existing tests pass (`pytest` in Docker container)
- [ ] Verify milestone emails send correctly after policy generation on staging
- [ ] Verify milestone emails send correctly after policy processing on staging
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Fix `AttributeError: 'PolicyTemplateGenerationConsumerV1' object has no attribute 'user_uid'` crash on production when sending milestone emails after policy generation/processing completion
- Harden AI structured output pipeline: fix JSON parsing, response extraction, and retry logic

## [v8.8.10] - 2026-03-13

### Changed
- **New Features**
- Visual "Processing.
- Buttons now show distinct busy (spinning/disabled) and ready states so progress and availability are clearer
- **Bug Fixes / Behavior**
- Stop action now performs a gentler cancellation flow and cleans up the UI on confirmation
- Improved handling of empty or malformed assistant responses with clearer error signaling
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Navigate to a policy detail page and click "Analyze Framework Compliance"
- [ ] Verify the progress bar appears smoothly without a page reload
- [ ] Verify the "Analyze" button switches to "Analyzing.
- [ ] Verify the stop button appears in the status card
- [ ] Verify the page reloads only once when analysis completes (final_completion)
- [ ] Verify clicking "Stop Analysis" still works correctly
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Removed the `schedulePageReload(1500)` that fired when the "Policy processing initiated!" WebSocket message arrived, causing a jarring progress bar flash
- Both button states (active and analyzing/busy) are now pre-rendered in the template with `hidden` class toggling, and a new `switchToAnalyzingUI()` function toggles them dynamically when analysis starts
- The stop button, analyzing badges, and disabled buttons are all shown instantly via JS instead of waiting for a page reload
- The proper `final_completion` reload (when all tasks finish) remains unchanged

## [v8.8.1] - 2026-03-12

### Fixed
- **List page UI gap**: `can_delete` was hardcoded to `True` and `update_url`/`delete_url` were always set, making edit/delete actions appear for system frameworks
- Now consistent with the detail page which already guards with `{% if not framework.

### Changed
- [x] All 19 existing system protection tests pass (model-level + view-level)
- [ ] Verify system frameworks on list page no longer show edit/delete icons
- [ ] Verify user-created frameworks still show edit/delete icons
- Protection was already in place at the view layer (403 responses) and model layer (`ValueError` on save/delete), but the list page UI did not hide the buttons.
- Fix system framework protection gap on the frameworks list page where edit and delete icons were visible and clickable for system frameworks (`is_system=True`)
- Gate `update_url`, `delete_url`, and `can_delete` on `not fw.

## [v8.8.0] - 2026-03-04

### Security
- Bump version to v8.
- Add changelog entries for 4 commits that landed on main without a PR: employee/server security hardening, CRUD form fixes, view improvements, and accessor migrations

### Added
- **Collapsible sidebar**: Toggle button (chevron) at the bottom of the sidebar collapses it to an icon-only strip (`4.
- **Organization selector in navbar**: Multi-organization users now see a compact dropdown in the top navbar (`#navbar-org-selector`) instead of the sidebar.
- **Theme toggle and Version link in sidebar**: The dark/light mode toggle and version info are now integrated as the last items in each role's sidebar card.

### Changed
- [x] No code changes, version bump only
- [x] Changelog renders correctly at `/changelog/`
- `version.
- `package.
- `CHANGELOG.
- `changelogs/v8.
- **Sidebar icons**: Replaced gradient-colored icon containers with flat, monochrome Heroicons outline SVGs (`stroke="currentColor"`, `stroke-width="1.
- **Single sidebar card per role**: Removed separate dark-mode card and version-info card from `base.
- **Tenant admin Quick Actions**: "Create Organization" and "Create User" quick-action links now use the same sidebar item component format (monochrome icon + label) as the rest of the navigation.
- **Super admin sidebar**: Removed colored header/badge; replaced with a plain uppercase section label that hides in collapsed mode.

### Files changed
- `app/templates/v2/components/sidebar_item_component.
- `app/templates/v2/components/sidebar_regular_user.
- `app/templates/v2/components/sidebar_tenant_admin.
- `app/templates/v2/pages/base.
- `app/static/src/styles/navigation.
- `app/static/src/pages/sidebar-collapse.
- `app/static/src/pages/sidebar-entry.
- `e2e-playwright/tests/multi-organization-assignment/multi-org-assignment.

## [v8.7.9] - 2026-02-27

### Fixed
- **CSS missing on deployed server**: Tailwind purged all utility classes (responsive `sm:`, `lg:`, hover `hover:`, dark mode `dark:`, and many base utilities) because templates weren't in the container at build time
- Root cause: Dockerfile ran Vite build before `COPY .

### Changed
- Optimized Tailwind CSS configuration by consolidating content paths and removing redundant references, reducing build complexity
- Enhanced Docker build process to properly include template and template tag directories, ensuring complete asset compilation
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] Verified locally: CSS builds correctly with all Tailwind utilities retained
- [ ] CI build produces image with working CSS (check after merge)
- <!-- This is an auto-generated comment: release notes by coderabbit.
- `production/Dockerfile`: add `COPY app/templates/` and `COPY app/templatetags/` before the Vite build step
- `app/static/tailwind.
- Copy `app/templates/` and `app/templatetags/` into the Docker image **before** `npm run vite:build` so Tailwind can scan HTML templates during CSS purge
- Remove stale `tailwind.

## [v8.7.8] - 2026-02-25

### Changed
- **New Features**
- Added `--list-keys` flag to the deployment script to display available SSH public keys with deterministic indexing, enabling easier key selection for deployments.
- **Chores**
- Fixed file ownership permissions for Vite build output in container images and deployment initialization.
- <!-- end of auto-generated comment: release notes by coderabbit.
- …rors
- Sort SSH keys alphabetically for stable --key-index mapping, add --list-keys flag.
- <!-- This is an auto-generated comment: release notes by coderabbit.

## [v8.7.7] - 2026-02-20

### Changed
- …ixes

## [v8.7.6] - 2026-02-20

### Changed
- **Improvements**
- Enhanced organization context resolution with improved fallback mechanisms for non-organization users
- Strengthened user role detection with additional verification layers
- Improved error handling and logging for more reliable system diagnostics
- **Updates**
- Refined developer tooling rules for better code guidance
- <!-- end of auto-generated comment: release notes by coderabbit.

### Security
- …r mixin rules
- Added descriptions to clarify the purpose of the rules for container security hardening and relationship manager mixin.
- Changed `alwaysApply` to false for both rules to allow for more flexible application.
- Enhanced comments in the OrganizationMiddleware to improve clarity on user roles and organization context handling.
- Introduced a new method `_is_non_org_user` to streamline the identification of users who do not require organization context.
- Updated navigation context retrieval to include a fallback for users not yet enhanced by the auth middleware.
- <!-- This is an auto-generated comment: release notes by coderabbit.

## [v8.7.5] - 2026-02-13

### Changed
- **New Features**
- System frameworks now hide Add, Edit and Delete actions while keeping View available.
- Quick navigation and detail pages omit Add/Edit for system frameworks.
- **Improvements**
- Header action menus no longer show empty primary or secondary entries, reducing unused/disabled controls.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] All 26 existing system framework protection tests pass
- [ ] Navigate to a system framework control detail — no Edit/Delete header actions, no Add/Edit requirement buttons
- [ ] Navigate to a system framework requirement detail — no Edit/Delete header actions, no "Add Another Requirement" link
- [ ] Non-system frameworks still show all actions as before
- Made with [Cursor](https://cursor.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Closes UI gaps left after the system framework protection feature (#351).
- Hide Add/Edit/Delete buttons on control and requirement detail pages for system frameworks
- Make `include_delete_action` a property and `get_primary_action()` return `None` for system frameworks in both `FrameworkControlDetailView` and `FrameworkRequirementDetailView`
- Wrap template action links in `{% if not framework.

## [v8.7.4] - 2026-02-13

### Changed
- Framework import commands (ISO 27001, CIS, NIS2, DORA, EU AI Act) now set `is_system=True`
- Edit/delete buttons hidden in UI for system frameworks
- CRUD operations on system frameworks return 403 Forbidden
- 13 unit tests for model-level protection
- View-level protection tests for frameworks, controls, and requirements

### Added
- System framework protection to prevent modification of imported ISMS frameworks
- `is_system` property on Framework model to mark system frameworks as immutable
- `is_system_framework()` helper method on FrameworkMember base class
- "System Framework" badge displayed on framework detail pages
- Comprehensive unit tests for model and view-level protection

## [v8.7.3] - 2026-02-13

### Added
- **`.
- Determines version bump type from PR labels (`release:patch` / `release:minor` / `release:major`; defaults to patch)
- Calculates next semver from latest git tag
- Updates `version.
- Generates changelog entry from PR description via `changelog_manager.
- Commits version bump, creates git tag, creates GitHub Release
- Builds production Docker image and pushes to GHCR (`ghcr.
- Dispatches `publish-changelog.
- **GitHub labels**: `release:patch`, `release:minor`, `release:major` created on the repo

### Changed
- **New Features**
- Upload questionnaires as plain-text (.
- Automated release & changelog publishing with optional manual trigger.
- Richer dashboard compliance analysis: risk indicators, recommendations, trends.
- **Improvements**
- Drag-and-drop file uploads with improved previews and validation.
- System frameworks are now protected from modification/deletion.
- Numerous UI, navigation and dashboard rendering refinements for robustness and usability.
- <!-- end of auto-generated comment: release notes by coderabbit.
- **`.
- **`scripts/devops/github/release.
- **`.
- Made with [Cursor](https://cursor.
- <!-- This is an auto-generated comment: release notes by coderabbit.
- Automate the entire release process via GitHub Actions when a PR is merged to `main`
- Replace manual `release.
- Build and push Docker images to GHCR as part of the release

## [v8.7.2] - 2026-02-13

### Added
- Added TXT file support for AI questionnaire uploads.

## [v8.7.17] - 2026-03-12

### Changed
- **New Features**
- New publish workflow and reliable publisher UI with recovery/progress controls; policy template detail-level and audit-template options; post-generation consolidation.
- Orphaned access cleanup: per-actor remove action on employee pages.
- **Bug Fixes**
- Stronger WebSocket auth/connection guards, improved error reporting, and de-duplicated ping handling.
- **Improvements**
- Enum-backed task statuses (PROCESSING, WARNING); centralized WebSocket/envelope/session helpers; safer scheduled page reloads; server listings now show domain/IPv4; simplified employee create/update form handling.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] `test_delegates_to_helper` passes with new return-value assertion
- [x] `test_policy_create_rag_fallback_matches_consumer` exercises real consumer import
- [x] All resolve_channel_group tests pass
- [x] No TypeScript lint errors in modified files
- [x] Pre-existing lint failures in unrelated files (settings, celery config) are unchanged
- <!-- This is an auto-generated comment: release notes by coderabbit.
- **WebSocket type safety**: Extended `Meta` interface with `resource_id`/`resource_type`, removed all `as any` casts across 5 files
- **Error handling**: Re-throw in `initializeWebSocketConnection` for proper caller cleanup; surface unhandled errors in template question generator; fix null dereference in `buildCancelEnvelope` via optional chaining
- **Publisher refactor**: Split monolithic `reliable-publisher.
- **Celery/consumer alignment**: Standardize channel group resolution, progress manager signatures, and task event bus usage across v1/v2 tasks
- **Scope publisher fix**: Changed no-environments condition from `task_failed` (which triggers failure UI) to `task_progress` warning (allows continued processing)
- **Test improvements**: Fixed tautology test, added missing return-value assertion, added tests for page counter, scope publisher, progress managers, envelope, ws-helpers, and more
- **Template fix**: Corrected `{% block javascript %}` to `{% block extra_js %}` in employee update template
- Resolve WebSocket consumer/task inconsistencies across publishers, evaluators, and chat handlers
- Refactor ReliablePublisher into modular helper-subfolder pattern (657-line monolith → 7 focused files)
- Add `resource_id`/`resource_type` to TypeScript `Meta` interface, eliminating 7 unsafe `as any` casts
- Fix error propagation in `initializeWebSocketConnection` so callers can execute cleanup
- Add comprehensive test coverage: unit tests for envelope, helpers, publisher config, operation handlers

## [v8.7.16] - 2026-03-11

### Changed
- **New Features**
- Added Submission Analysis page: new interim review stage displaying submitted content, uploaded files, AI findings, compliance gaps, topic plan, and optional deeper evaluation before entering the questionnaire wizard.
- Implemented Deeper Evaluation option providing document quality scores, coverage assessment, and improvement recommendations.
- Added AI assistant model selection and management capability in policy settings.
- Introduced dynamic question limits based on detected topic count for more intelligent question planning.
- Added policy sections accordion view organizing instructions by control and requirement.
- **Improvements**
- Enhanced AI assistant model fallback logic with intelligent version sorting and error recovery.
- Improved wizard navigation supporting question history traversal.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [x] Unit tests for dynamic model sorting and fallback (`test_assistant_ops.
- [x] Unit tests for assistant model view (`test_assistant_model_view.
- [x] Unit tests for policy sections view (`test_sections_view.
- [x] Unit tests for analysis view, deeper evaluation, submission metadata
- [x] Unit tests for wizard navigation, question generation, compute max questions
- [x] Unit tests for instruction grouping accordion
- [x] All 1121 tests passing in CI pre-commit hook
- <!-- This is an auto-generated comment: release notes by coderabbit.
- **Analysis interim stage**: New step between form submission and questionnaire that shows compliance context analysis, gap inventory, document evaluation, and estimated question count before proceeding
- **Dynamic AI model selection**: Assistant creation now discovers all available models from the OpenAI account, sorts by version descending (best-first), and tries each until one is accepted — no more hardcoded fallback lists
- **Post-creation model change**: Users can change the assistant's model after finalization via a dropdown on the policy detail page
- **Policy sections page**: Grouped accordion view of ActionableInstructions available for any policy with instructions (not just template-generated), reusing shared grouping logic with the review page
- **Wizard improvements**: Topic-driven dynamic question limits, option strength indicators, progress bar fixes, navigation/URL tracking fixes
- **Sidebar fix**: Wrapped localStorage in try/catch to prevent CSP/private browsing errors

## [v8.7.15] - 2026-03-06

### Changed
- **New Features**
- Enhanced activity tracking with real-time data sources for unified dashboard.
- Added recent entity queries for improved visibility into system usage.
- **Bug Fixes**
- Fixed race condition in dashboard data loading.
- Prevented duplicate data calculation in unified dashboard metrics.
- Improved system health status reporting accuracy.
- **Security**
- Implemented per-user access control for organization dashboards with 403 error handling.
- Scoped cache keys by user to prevent unauthorized data access.
- **Removals**
- Removed experimental trend data generator (returns empty for now).
- Removed debug logging from production dashboard.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Verify dashboard loads for a normal org user (no 500 errors)
- [ ] Verify accessing another org's dashboard returns 403
- [ ] Verify super admin dashboard health check shows correct status
- [ ] Verify recent activity shows real data (not placeholders)
- [ ] Run unit tests: `pytest app/api/v1/dashboard/tests/ app/services/queries/tests/test_user_queries.
- <!-- This is an auto-generated comment: release notes by coderabbit.

### Removed
- `dashboard-debug.
- Dead webpack `<script>` comment from `dashboard.

### Fixed
- `unified/main.
- `activity_trackers.
- `data_generators.
- `formatters.
- `super_admin/dashboard.
- `super_admin/dashboard.
- `set_main_project.
- `api/v1/dashboard/main.
- `dashboard-data-service.
- `user_queries.

### Security
- `chart_queries.
- `api/v1/dashboard/main.
- `api/v1/dashboard/set_main_project.
- Cache key changed from `hash()` (non-deterministic across Gunicorn workers) to `','.
- **P0 Security**: Fixed cross-tenant data leaks in chart queries and missing org membership checks on dashboard API endpoints
- **P1 Data**: Fixed KPI doubling bug, replaced synthetic/hardcoded data with real Cypher queries
- **P2 Logic**: Fixed missing `User` import (silent NameError on every health check), phantom validator call, health status precedence bug, and template key mismatch
- **P2 Perf**: Replaced unbounded `.
- **P3 Cleanup**: Removed dead debug file, dead webpack comment, fixed frontend memory leak and no-op refresh stub
- **Tests**: Added 100 unit tests (0 pre-existing) covering all fixes

## [v8.7.14] - 2026-03-06

### Security
- **CVE-2026-25528**: Fixed in langsmith >= 0.

### Changed
- Upgrades `langsmith` from `0.

## [v8.7.13] - 2026-03-06

### Changed
- **Audit Template rename**: 8 HTML templates + 13 Python views updated
- **Icons aligned with sidebar**: `icon-questionnaire`, `icon-framework`, `icon-assessment-template`, `icon-project`, `icon-application`, `icon-search`
- **New**: `icon-lightbulb.
- **New**: `icon-clipboard-check.
- **Removed**: `icon-sparkles.
- `chat_search.
- Policy Factory views updated to use `lightbulb` icon matching sidebar
- Rename "Assessment Template" → "Audit Template" across all UI display strings (templates, view titles, breadcrumbs, report headers) — logic/code names unchanged
- Align all page header icons with canonical left sidebar icons
- Fix broken AI Chat Search header (blank gradient circle)
- Fix missing `icon-clipboard-check.

## [v8.7.12] - 2026-03-05

### Changed
- **New Features**
- Policy Factory: upload documents to auto-analyze, generate compliance-aware plans, assemble factory templates, export full policy DOCX, view gap coverage maps, and generate remediation action plans.
- AI-driven TopicPlan & Planner to scope generation and create reusable templates.
- **UI/UX Enhancements**
- Multi-file drag‑and‑drop upload with processing overlay; wizard shows AI-suggested answers with “Use this” action and per-question context; resume-wizard badge.
- **Industry**
- Added Telecommunications (plus Legal, Transportation) and related policy types.
- <!-- end of auto-generated comment: release notes by coderabbit.
- [ ] Upload a document on Policy Factory create page — verify overlay appears with countdown and steps
- [ ] Submit form — verify no double overlay and `beforeunload` fires only during processing
- [ ] Step through wizard — verify structured questions (select/multiselect), pre-selected options, relevant_context card, and suggestion "Use this" button
- [ ] Confirm page — verify human-readable labels (not snake_case) for structured answers
- [ ] Open a review section — verify URL updates to `#review-{uid}`
- [ ] Reload the review page with hash in URL — verify modal auto-opens to correct section
- [ ] Share hash URL with a colleague and confirm it opens the right section
- [ ] Leave a policy wizard unfinished — verify "Incomplete" badge and "Continue Wizard" link in policy list
- <!-- This is an auto-generated comment: release notes by coderabbit.
- **Policy Factory**: Full AI-driven pipeline — document upload, compliance context extraction, topic-based wizard, and policy generation
- **AI Framework Matching**: Semantic matching with deduplication, handles aliases, translations, and abbreviations
- **Topic-Based Wizard**: `TopicPlan` drives question generation, structured question types (boolean/select/multiselect), document-aware pre-selection, dynamic `relevant_context` per question, and answer label resolution
- **UI/UX**: Processing overlay with countdown + `beforeunload` guard, canonical card frame, selected option highlighting, minimalist review modal (ghost buttons, wider/taller), multi-file drag-and-drop
- **Review Deep-Linking**: URL hash (`#review-{uid}`) updated on open/navigate, restored on reload/share — enables sharing exact review section with colleagues
- **Recovery**: Incomplete wizard policies show "Continue Wizard" link in policy list
- **TDD**: 100+ new tests across extractor, wizard, topic plan, question types, coverage map, and action plan

## [v8.7.11] - 2026-02-27

### Fixed
- Stale `DO_API_TOKEN` reference removed from `hz-deploy.
- FQDN resolution discrepancy: `hz-deploy.
- SCP of `/etc/ssl/fits/` certs now stages to `/tmp` first to work with non-root SSH users

### Added
- `hz-migrate-from-do.
- `scripts/devops/lib/hetzner_api_token_loader.

### Changed
- `hz-deploy.
- `hz-logs.
- `hz-manager.
- `do-deploy-core.
- `hz-import.
- `hetzner-api.
- Refactor the Hetzner deployment toolchain to mirror the DigitalOcean pattern: `hz-deploy.

## [v8.7.10] - 2026-02-27

### Changed
- Unit test generation was requested by @bbalvl7.

## [v8.7.1] - 2026-01-28

### Changed
- Framework import commands (ISO 27001, CIS, NIS2, DORA, EU AI Act) now set `is_system=True`
- Edit/delete buttons hidden in UI for system frameworks
- CRUD operations on system frameworks return 403 Forbidden

### Testing
- 13 unit tests for model-level protection
- View-level protection tests for frameworks, controls, and requirements

### Added
- System framework protection to prevent modification of imported ISMS frameworks
- `is_system` property on Framework model to mark system frameworks as immutable
- `is_system_framework()` helper method on FrameworkMember base class
- "System Framework" badge displayed on framework detail pages
- Comprehensive unit tests for model and view-level protection

## [v8.6.5] - 2026-01-23

### Fixed
- Fixed GitHub Actions CI pipeline failing to start FITS service within timeout
- Fixed SQLite dependency issue in health endpoint causing CI failures
- Fixed Docker image not rebuilding from latest code in CI (added --build flag)
- Fixed linting failures when ruff/black not installed in container

### Changed
- Increased service startup timeout from 60s to 180s with detailed progress logging
- Refactored CI workflow to use `scripts/test.
- Switched dev/CI session engine to signed cookies to eliminate SQLite dependency

### Added
- Added Prettier for TypeScript/JavaScript code formatting
- Added security audit command (`.
- Added comprehensive debug logging on CI service startup failures
- Added container status checks during service health polling

## [v8.6.4] - 2026-01-15

### 4. Technical Implementation
- **Skipped rows tracking**: Added to RecursiveDataLoader with detailed logging
- **New API endpoint**: `GET /api/v1/imports/{job_uid}/download-skipped/`
- **Database changes**: Added `skipped_rows_report` and `skipped_rows_count` fields
- **UI updates**: Import status shows completion with skipped row counts
- `app/services/imports/ai_validator.
- `app/tasks/imports/self_service/ai_validation/validation.
- `app/libs/recursive_data_loader_helper/` - Added skip tracking
- `app/models/imports/` - Added skipped rows storage fields
- `app/tasks/imports/self_service/data_processing.
- `app/api/v1/imports/downloads.
- `app/templates/v2/pages/organizations/imports/validation_results.
- `app/views/client/organizations/imports/validation_results.
- Pre-commit checks passed
- All linter errors resolved
- Code compiles successfully

### 3. User Experience Improvements
- **Import always proceeds**: Unless there are critical file-level issues
- **Downloadable skipped rows report**: Excel file showing exactly what was skipped and why
- **Clear status messaging**: Shows import completed with X rows skipped
- **Full auditability**: Users can download reports to see what happened to each row

### 2. Import Processing Enhancements
- **Row skipping logic**: Invalid rows are logged and skipped, processing continues
- **Comprehensive tracking**: Every skipped row is recorded with reason and original data
- **Duplicate handling**: Existing records are updated instead of blocking (merge semantics)

### 1. AI Validation Behavior Changes
- **Duplicates**: Now treated as warnings (update existing records) instead of blocking errors
- **Missing required fields**: Warnings that skip rows instead of blocking import
- **Referential integrity**: Parent not found issues skip rows instead of blocking
- **Only critical file/config errors still block**: Malformed Excel, invalid configs, etc.

## [v8.6.3] - 2026-01-15

### Fixed
- Self-service import annotated Excel files failing in production

## [v8.6.2] - 2026-01-15

### Testing
- All curl commands include proper headers (`Content-Type: application/json`)
- Commands target `/api/v1/milestones/test-complete` endpoint as specified
- Error scenarios include invalid milestone IDs and missing required fields
- Email failure simulation via test headers for controlled testing

### Added
- Direct executable testing commands that reviewers can run immediately
- Comprehensive coverage of success, partial failure, and error scenarios
- Simulation of email service downtime for graceful degradation testing
- Proper HTTP headers and payload formatting for API testing

### Changed
- **Testing Documentation**: Replaced abstract testing scenarios with concrete curl examples in `03-testing.
- **Manual Testing Scenarios**: Added executable commands for all milestone completion outcomes:
- **Documentation Restructuring**: Split investigation docs into focused `01a-investigation-decisions.
- Enhanced milestone email notification testing documentation with concrete, executable curl commands for comprehensive manual testing coverage.

## [v8.6.1] - 2026-01-15

### Testing
- No functional changes to the public API
- Thread-safety improvements ensure consistent behavior in production
- DEBUG mode continues to work as expected for development
- @codex
- <!-- This is an auto-generated comment: release notes by coderabbit.

### Changed
- **Chores**
- Updated build configuration to include content hashes in asset filenames for improved cache management
- Enhanced asset loading mechanism across application templates
- <sub>✏️ Tip: You can customize this high-level summary in your review settings.
- <!-- end of auto-generated comment: release notes by coderabbit.
- Remove global `_vite_manifest` variable
- Add `functools.
- Preserve DEBUG mode behavior of always loading fresh manifests
- Refactor code to eliminate duplication and improve maintainability
- Fixes thread-safety issue in Vite manifest caching by replacing global mutable variable with functools.
- The `_get_vite_manifest` function was using a global mutable `_vite_manifest` variable that could cause race conditions in multi-threaded Django environments.

## [v8.6.0] - 2026-01-13

### Added
- feat: implement super admin email provider management with OAuth support

## [v8.5.2] - 2026-01-12

### Testing
- Added comprehensive tests for task notification helper
- Verified data migration sets integration_mode on legacy nodes
- Confirmed chat tasks are excluded from email notifications
- Fixes: Chat nodes with None integration_mode causing property access errors
- Fixes: Chat tasks sending email notifications for every message
- @codex

### Added
- Configurable task notification exclusions via Django settings
- Data migration ensures backward compatibility for existing Chat nodes

### Changed
- Add data migration to set integration_mode on legacy Chat nodes with None values
- Move SKIP_EMAIL_NOTIFICATION_TASKS configuration from hardcoded list to Django settings for better configurability
- Exclude chat-related tasks from email notifications:
- policy_chat_process_message_celery_v1
- policy_chat_rag_celery_v2
- policy_gemini_chat_celery_v1
- Fix chat integration_mode property access errors and prevent chat tasks from sending email notifications for every message.

## [v8.5.1] - 2025-12-22

### Testing
- Script follows existing DigitalOcean script patterns (`do-status.
- Uses `ssh-common.
- Tested interactive droplet selection
- Tested dry-run mode
- Tested confirmation prompt (moved to local script to fix stdin issue)
- Verified safety checks work correctly

### Added
- **Safety checks**: Waits for unattended-upgrades to complete before proceeding
- **Upgrade preview**: Shows what packages will be upgraded before execution
- **Kernel update warnings**: Alerts user if kernel updates are included (may require reboot)
- **Security-focused**: Only upgrades existing packages, doesn't install new ones
- **Flexible execution**: Supports interactive, non-interactive, and dry-run modes
- **Standard interface**: Follows same argument patterns as other DigitalOcean scripts

### Changed
- The script implements all features specified in the plan:
- 1.
- 2.
- 3.
- 4.
- 5.
- 6.
- 7.
- 8.
- Changes follow canonical patterns as per @codex rules.
- Created `scripts/devops/digitalocean/do-upgrade-system.
- Implements `wait_for_unattended_upgrades()` function for safety (reused from do-remote-deploy.
- Supports interactive droplet selection when `--ip` is not provided
- Includes upgrade preview functionality showing upgradable packages with count and list
- Interactive and non-interactive modes (`--yes` flag to skip confirmation)
- Dry-run mode (`--dry-run` flag) for previewing upgrades without making changes
- Uses `apt-get upgrade --only-upgrade -y` for security-focused upgrades (only upgrades existing packages)
- Warns about kernel updates that may require reboot
- Provides post-upgrade summary showing upgraded packages and kernel update warnings
- Uses placeholder injection pattern (`__DRY_RUN__`, `__AUTO_YES__`) like other deployment scripts
- Confirmation prompt moved to local script for proper stdin handling (fixes interactive prompt issue)

### Security
- Added `do-upgrade-system.

## [v8.5.0] - 2025-12-18

### Changed
- Refactored Policy model structure: split into core subfolder with model.
- Renamed Policy model file from policy.
- Updated all Policy model import paths throughout codebase

### Added
- Implemented intelligent policy template wizard with dynamic question generation
- Added back/forth navigation for policy template wizard
- Added overall progress indicator for policy template generation
- Added BCDR framework generation management command
- Added wizard chat mixin for thread-based assistant management
- Added wizard data mixin for Q&A pair management
- Added dynamic question generator service
- Added thread manager for saving Q&A pairs to assistant threads
- Added tool suggestions service for wizard
- Added framework context service
- Added policy template generator service
- Added comprehensive test coverage for wizard flow and chat functionality
- Added loading overlay with 90-second timeout for policy template creation
- Added Vite entry point for policy-template-create page

### Fixed
- Fixed fail-safe deletion check: can_be_deleted() now returns False on exception with full traceback logging
- Added proper exception logging for vectorStore deletion failures
- Removed incorrect async_to_sync wrapper from _create_wizard_assistant call
- Added COALESCE for pending_generation_count in Cypher query to prevent None returns
- Removed unused requirement parameter from _generate_with_thread function
- Added exception chaining suppression (from None) to ControlMissingError raise
- Removed duplicate Policy import in assessment_template/create.
- Removed unused organization parameter from handle_edit_and_regenerate
- Fixed button alignment on policy template review page
- Converted text inputs to textareas in policy template wizard for better UX

### Removed
- Removed PolicyIntakeAnswer model and related tests
- Removed static intake questions and industry-specific question files
- Removed old intake.
- Removed intake_form.

## [v8.4.6] - 2025-12-18

### Fixed
- Fixed 8 code quality issues: fail-safe deletion check returns False on errors, proper exception logging for vectorStore deletion, removed incorrect async_to_sync wrapper, added COALESCE for null values in queries, removed unused parameters, added exception chaining suppression, removed duplicate imports

## [v8.4.5] - 2025-12-17

### Fixed
- Fixed import_data error where Space model composite_keys incorrectly included 'title' property that doesn't exist on the model

## [v8.4.4] - 2025-12-17

### Fixed
- Fixed SCRIPT_DIR references in shell scripts to handle CRLF-fix temp copy scenario

## [v8.4.3] - 2025-12-17

### Fixed
- Fixed CRLF handling to copy scripts to /tmp instead of modifying mounted volume

## [v8.4.2] - 2025-12-17

### Fixed
- Fixed Docker entrypoint to strip CRLF at runtime for Windows volume mounts

## [v8.4.1] - 2025-12-17

### Fixed
- Fixed Windows CRLF line ending issue in shell scripts by adding .

## [v8.4.0] - 2025-12-17

### Added
- Policy template generation system: Complete workflow from intake questionnaire to final policy export
- AI-powered content generation: Industry-specific policy content generation with user context injection
- Intake questionnaire: User context collection system capturing regulatory requirements, technical environment, and risk tolerance before generation
- Review workflow: Comprehensive review interface with approve, edit, and reject functionality for generated content
- Live client-side search: Real-time search with highlighting in policy review list
- Export functionality: DOCX and PDF export with improved table of contents and domain heading support
- WebSocket integration: Real-time progress updates during policy generation
- Modular architecture: Refactored codebase into focused files under 100 lines for better maintainability

### Changed
- Policy template generation workflow: Improved navigation and status display throughout the generation process
- Form handler integration: Unified form handling across policy template views
- Export service: Enhanced TOC generation and temporary file management utilities

## [v8.3.9] - 2025-12-12

### Changed
- Removed legacy ADMIN role; system now uses only SUPER_ADMIN, TENANT_ADMIN, and USER roles

### Fixed
- Fixed 404 error on Excel template download for tenant admin users
- Removed obsolete `/v2/` URL prefix checks from authentication middleware
- Updated organization URL pattern matching in middleware to match current URL configuration
- Replaced PII email logging with non-PII identifiers (user ID or hashed email) in orphaned session handler
- Removed password change restriction for tenant admins; password changes are now allowed as security best practice
- Replaced naive datetime.
- Fixed user self-edit validation to compare UIDs instead of object references in tenant scoping middleware
- Fixed DigitalOcean deploy scripts token handling + DNS preflight checks to support trusted SSL issuance per droplet subdomain

## [v8.3.8] - 2025-12-12

### Fixed
- Fix generated-tenants directory permissions for Excel generation.

## [v8.3.7] - 2025-12-11

### Changed
- ## Summary

## [v8.3.6] - 2025-12-11

### Changed
- Removed changelog detail header secondary actions so the ellipsis dropdown no longer renders
- Left the existing back navigation and header layout intact

## [v8.3.5] - 2025-12-11

### Added
- Automatic git hooks installation: Git hooks are now automatically installed from scripts/git-hooks/ to .

### Changed
- Enhanced pre-push hook: Added changelog validation to pre-push hook to ensure changelog entries are created when pushing to main branch
- Updated changelog-required.

### Removed
- Settings menu item from super admin user dropdown: Removed redundant settings option from user navigation menu to simplify interface

## [v8.3.4] - 2025-12-09

### Added
- Public changelog RSS feed: Users can subscribe to FITS updates via RSS readers or integrate into websites like Squarespace
- Automated changelog publishing: New releases automatically appear in the public RSS feed without manual steps
- Public landing page: Provides FITS information and easy access to changelog feed for external users

### Changed
- Updated documentation with correct organization repository URLs for better clarity

## [v8.3.3] - 2025-12-09

### Added
- Public changelog RSS feed: Users can subscribe to FITS updates via RSS readers or integrate into websites like Squarespace
- Automated changelog publishing: New releases automatically appear in the public RSS feed without manual steps
- Public landing page: Provides FITS information and easy access to changelog feed for external users

## [v8.3.2] - 2025-12-05

### Added
- Enhanced authentication security testing: Improved reliability of login security features including account locking and suspicious login detection
- Comprehensive test coverage: Login security features now have better test coverage to prevent regressions

## [v8.3.12] - 2025-12-15

### Added
- feat: Add Cursor hooks verification and setup tools

## [v8.3.11] - 2025-12-15

### Fixed
- Fixed tenant text clamping in super admin tenant list: removed redundant max-width Tailwind class and added text-overflow ellipsis for better browser compatibility
- Fixed pre-push hook bug where requirements-audit.

## [v8.3.10] - 2025-12-15

### Added
- feat: Enhanced DigitalOcean deployment with subdomain nginx configuration support and improved SSL certificate management

## [v8.3.1] - 2025-12-05

### Security
- Enhanced authentication security testing: Improved reliability of login security features including account locking and suspicious login detection
- Comprehensive test coverage: Login security features now have better test coverage to prevent regressions

## [v8.3.0] - 2025-12-04

### Fixed
- Azure OAuth redirect URI: Fixed incorrect redirect URI detection that prevented Azure OAuth from working properly - now correctly detects IP or domain
- Azure OAuth refresh tokens: Fixed missing refresh tokens by adding required offline_access scope, allowing long-lived sessions
- Super admin user management: Fixed user edit redirects and user list display so super admins can properly manage users across tenants
- Duplicate email sending: Fixed issue where clicking test email sent two emails instead of one
- Transformers cache warning: Fixed deprecation warning that appeared during startup

### Added
- Test email functionality: Email provider detail pages now have "Send Test Email" button that sends actual test emails to tenant admin for verification
- Gmail email sending: Gmail provider now actually sends emails via Gmail API (previously returned success without sending)
- Exchange email sending: Exchange provider now sends emails via Exchange API (previously returned success without sending)
- Centralized user URLs: User navigation now uses role-based redirect logic for better user experience

### Changed
- Unified OAuth workflow: Removed separate "Connect" buttons - creating a provider now automatically initiates OAuth flow for simpler setup
- Azure setup guide: Now dynamically displays the correct redirect URI based on current host, making setup easier
- Email provider documentation: Updated to reflect the simplified OAuth workflow

## [v8.2.2] - 2025-12-01

### Added
- User-selectable main project: Dashboard users can now choose which project to display as their main project for personalized views
- Improved dashboard performance: Dashboard now loads significantly faster with optimized data retrieval

### Changed
- Dashboard query optimization: Eliminated performance bottlenecks that caused slow dashboard loading times
- Enhanced dashboard caching: Better data organization reduces redundant queries and improves response times

## [v8.2.1] - 2025-12-01

### Fixed
- Scope publishing bug: Fixed critical issue where scopes with the same name in different projects could be published to the wrong project's Confluence space
- Scope page identification: Scope pages now include project name in title to ensure unique identification and prevent cross-project confusion

## [v8.2.0] - 2025-11-30

### Changed
- Project unpublish validation: Unpublish button now properly checks for blocking relationships (assessments, templates) before allowing unpublish
- Project detail view improvements: Better organization of project detail page components for improved usability

### Fixed
- Error logging consistency: Project operations now have consistent error logging for easier troubleshooting
- Project update error handling: Improved error messages and handling when project updates fail

### Added
- Project deletion safety checks: System now prevents deleting projects that have scopes with assessments or assessment templates, preventing data loss
- Enhanced project deletion: Two-step confirmation process for Confluence page deletion to prevent accidental data loss
- Confluence page management: System now checks if Confluence pages exist before deletion and provides better feedback
- Improved delete workflow: Better validation and user feedback throughout the project deletion process

## [v8.1.2] - 2025-11-28

### Fixed
- Scope unpublish button: Fixed button remaining clickable when scope has assessments, which could cause data integrity issues
- Delete button feedback: Fixed delete button not showing why it's disabled, leaving users confused about why they can't delete

### Changed
- Unpublish button messaging: Button now clearly displays "Cannot unpublish (has assessments)" when disabled, explaining why action is unavailable
- Delete button messaging: Button now shows descriptive message like "Cannot delete (has 2 assessments)" when disabled, providing clear feedback to users

## [v8.1.1] - 2025-11-28

### Fixed
- Confluence status badges: Fixed badges showing raw markup text instead of clickable links, making them unusable
- Dark mode readability: Fixed unreadable badge text in Confluence dark mode that made status information invisible
- Table header visibility: Fixed missing text color in dark mode that made table headers invisible

### Changed
- Confluence status display: Replaced Confluence status macros with custom styled badges that work reliably in all themes
- Badge theming: Improved badge styling to automatically adapt to both light and dark Confluence themes for better visibility
- Environment links: Updated to use proper link elements that work correctly in all Confluence themes

## [v8.1.0] - 2025-11-27

### Fixed
- JSON utilities error: Fixed syntax error that could cause application failures when processing JSON data

### Changed
- Docker standardization: Unified Docker base image across development and production environments for consistency and easier maintenance
- Docker build performance: Improved build caching reduces build times and speeds up deployments
- Deployment reliability: Enhanced error handling and improved deployment scripts reduce deployment failures

## [v8.0.1] - 2025-11-26

### Fixed
- Report download fallback: Fixed reports not downloading when API response was missing URLs - system now uses fallback mechanism
- KPI dropdown behavior: Fixed dropdown staying open when clicking outside, which could cause multiple menus to remain visible

### Changed
- Report navigation: Improved handling of report downloads with better fallback support for backward compatibility
- Code organization: Better separation of concerns improves maintainability and reduces bugs

## [v8.0.0] - 2025-11-26

### Fixed
- Documentation accuracy: Fixed documentation inconsistencies that could mislead developers about AI implementation details
- AI provider capabilities: Fixed incorrect capability descriptions in UI that showed wrong information about provider features

### Changed
- AI provider configuration: Enhanced with integration mode support for better flexibility in provider setup
- AI query optimization: Unified prompts and optimized queries across all AI tasks for better performance and consistency

### Added
- Composite AI providers: New pattern allows combining chat and embedding providers for optimal AI functionality
- Automatic embedding fallback: System automatically uses HuggingFace embeddings when providers don't have native embedding support
- HuggingFace integration: Added HuggingFace embedding provider as automatic fallback for providers without native embeddings

## [v7.9.0] - 2025-11-15

### Added
- Changelog system: Implemented per-version changelog files for better organization and easier navigation
- Changelog list view: Users can browse all versions with proper semantic version sorting
- Changelog detail view: Each version has a dedicated page with markdown rendering for easy reading
- Navigation access: Added navbar link for quick access to changelog from anywhere in the application

### Fixed
- Release script security: Fixed shell variable injection vulnerability that could allow code execution
- Version sorting: Fixed incorrect version ordering in changelog list - now uses proper semantic versioning

## [v7.8.5] - 2025-11-15

### Fixed
- Development server performance: Fixed CPU spike reaching 99% usage that made development environment unusable
- Auto-reload optimization: Constrained auto-reload to template directories only, preventing unnecessary restarts
- Uvicorn reload: Disabled uvicorn reload to prevent high CPU usage while maintaining browser auto-reload for HTML changes

## [v7.8.4] - 2025-11-14

### Fixed
- Uvicorn reload error: Fixed NotImplementedError that prevented development server from reloading properly

## [v7.8.3] - 2025-11-14

### Added
- Automated release management: Integrated changelog creation and versioning into release workflow for streamlined releases

## [v7.8.2] - 2025-11-14

### Security
- Non-root container execution: All container services now run as non-root user, significantly reducing security attack surface
- Read-only filesystem: Production containers use read-only root filesystem with explicit writable paths, preventing unauthorized file modifications
- Capability reduction: Dropped unnecessary capabilities and added only required ones (NET_BIND_SERVICE) for minimal privilege principle
- Production hardening: Production containers default to non-root user execution for enhanced security

### Changed
- Service execution: All application services (Celery, Daphne, nginx) now run as non-root user by default
- Container security: Improved security posture through comprehensive container hardening measures

## [v7.11.7] - 2025-11-15

### Fixed
- Production deployment failures: Fixed multiple critical issues causing container crash loops that prevented successful deployments

## [v7.11.4] - 2025-11-15

### Fixed
- Database configuration: Fixed SQLite database path issues for read-only filesystem environments
- Neo4j warnings: Fixed constraint warnings being treated as fatal errors that blocked operations
- Nginx configuration: Fixed inability to edit nginx config on read-only filesystem
- Container permissions: Fixed permission errors when running as appuser that prevented proper operation
- SSL certificates: Fixed certificate permission issues for container user that blocked HTTPS setup
- Certificate fallback: Fixed automated self-signed certificate generation when proper certificates unavailable
- Nginx process management: Fixed PID file permission errors that prevented nginx from starting
- Docker logging: Fixed log rotation configuration that could cause disk space issues

## [v7.11.3] - 2025-11-15

### Added
- Enhanced markdown support: Added code blocks with syntax highlighting, tables, and improved nested list handling for better documentation display
- Automatic markdown styling: Tailwind typography plugin automatically styles all markdown content for consistent, readable presentation
- Security auditing: GitHub Actions workflow automatically audits dependencies for security vulnerabilities

### Changed
- Markdown rendering: Code blocks now display with proper syntax highlighting for better readability
- Table display: Markdown tables now render correctly with proper formatting
- List formatting: Nested lists now display properly with correct indentation

## [v7.11.20] - 2025-11-19

### Added
- Hetzner Cloud deployment: Full support for deploying FITS to Hetzner Cloud infrastructure
- Server management tools: Complete set of tools for managing Hetzner Cloud servers including listing, creation, and deployment workflows
- Deployment documentation: Comprehensive guides for deploying to Hetzner Cloud

### Changed
- Deployment platform support: Extended deployment capabilities from DigitalOcean to Hetzner Cloud for more hosting options
- Server labeling: Enhanced labeling system supports project, environment, and tenant labels for better organization of multi-tenant deployments

### Fixed
- Server selection: Fixed issues with Hetzner Cloud API response handling that prevented proper server selection
- Error handling: Improved error messages for missing API tokens and empty server lists to help diagnose deployment issues

## [v7.11.2] - 2025-11-15

### Fixed
- Changelog version ordering: Fixed incorrect version sorting that showed v7.

### Changed
- Code organization: Better structure improves maintainability and makes code easier to understand
- Complexity reduction: Improved separation of concerns makes the codebase more manageable

## [v7.11.19] - 2025-11-19

### Fixed
- Employee deletion: Fixed delete button on employee detail pages that appeared but didn't work, preventing users from deleting employees
- Application deletion: Fixed delete button on application detail pages that appeared but didn't work, preventing users from deleting applications

## [v7.11.18] - 2025-11-18

### Fixed
- AI provider model selection: Fixed model dropdown being empty when editing existing AI providers, forcing users to re-enter API key just to see available models
- Model visibility: Users can now see and change AI models when editing providers without needing to re-enter credentials

## [v7.11.17] - 2025-11-18

### Fixed
- AI model changes: Fixed issue preventing users from changing AI models for existing providers without re-entering their API key, which was unnecessarily restrictive
- Credential requirement: Users can now change AI models without re-entering API key credentials, making provider management easier

## [v7.11.16] - 2025-11-18

### Fixed
- AI provider model updates: Fixed issue where users couldn't change AI provider models without re-entering API key, which was unnecessarily restrictive
- Model dropdown population: Model dropdown now always shows available models when updating providers, even when connection parameters haven't changed

### Changed
- Model fetching: System now always fetches available models when updating AI providers for better user experience
- Model validation: Improved validation logic - model field is required when connection changes, optional when unchanged

### Added
- Model change flexibility: Users can change AI provider models without re-entering API key, making provider management more convenient
- Emergency model fallback: System gracefully falls back to emergency models if API key is unavailable, ensuring providers remain usable

## [v7.11.15] - 2025-11-18

### Security
- API key exposure prevention: Fixed browser autofill exposing API keys on update pages, which could leak sensitive credentials
- API key protection: Improved handling prevents accidental exposure of API keys through browser autofill

### Changed
- AI provider updates: Users can now update AI providers without providing API key - system preserves existing encrypted key, making updates easier
- Conditional model validation: Model field is now required only when connection parameters change, providing more flexibility
- Code organization: Better structure improves maintainability and reduces bugs

### Added
- Flexible provider updates: Update AI providers without re-entering API key when only changing non-sensitive fields
- Smart validation: Model validation adapts based on whether connection parameters changed, providing appropriate requirements

## [v7.11.14] - 2025-11-17

### Removed
- Redundant Space field: Removed unnecessary title field from Space model that was causing confusion and data duplication

### Added
- Confluence credential validation: Centralized validation system checks Confluence space credentials and provides status indicators
- Validation caching: Daily caching prevents redundant API calls, improving performance and reducing Confluence API usage
- Credential status indicators: Visual indicators across all Space management pages show credential validity at a glance
- Dynamic space loading: Space selection modals now load spaces on-demand, improving page load times

### Changed
- Deferred validation: Space credentials are validated only when modals are opened, not on page load, making pages load faster
- Confluence error handling: Improved error handling for Confluence API responses provides better feedback when credentials fail
- Performance optimization: Project and scope detail pages load faster by deferring space validation until needed

### Performance
- Reduced API calls: Daily validation caching prevents checking the same credentials multiple times per day
- Faster page loads: Invalid credential caching skips unnecessary validation attempts, improving response times

## [v7.11.13] - 2025-11-17

### Security
- Cross-organization template access: Fixed security issue where assessment templates from other organizations appeared in scope template selection, potentially allowing unauthorized access
- Organization isolation: Added validation to prevent users from connecting assessment templates from other organizations to their scopes

### Fixed
- Template selection: Assessment templates from other organizations no longer appear in scope detail page template selection modal

### Changed
- Template filtering: Improved validation now properly filters templates by organization to ensure proper data isolation

## [v7.11.12] - 2025-11-16

### Fixed
- Missing CSS styles: Fixed 404 errors for icons and navbar styles that caused broken UI elements in production
- Self-service import failures: Fixed 500 errors on self-service imports API caused by read-only filesystem preventing file writes
- Production error visibility: Fixed missing error details in production logs that made debugging production issues difficult

### Changed
- CSS bundling: CSS files now bundled through build pipeline for better performance and reliability
- Error logging: Production errors now capture full stack traces for easier debugging and faster issue resolution
- Storage configuration: Updated production configuration to use writable storage paths for file operations

## [v7.11.11] - 2025-11-16

### Fixed
- Application startup failure: Fixed ImportError that prevented Django from starting, causing application crashes
- Development server restarts: Fixed watchdog handler causing false-positive restarts that interrupted development workflow

### Changed
- Watchdog reliability: Improved event filtering prevents unnecessary restarts during normal development activities
- Restart behavior: Increased debounce period and added cooldown after restarts to prevent rapid-fire restart loops

## [v7.11.10] - 2025-11-16

### Fixed
- Multi-tenant deployment failures: Fixed incorrect file paths in deployment scripts that caused import failures and prevented successful deployments

### Changed
- Deployment script paths: Corrected file path references to match actual directory structure
- Error reporting: Improved error messages now include tenant context to help identify which tenant failed during deployment
- Failure tracking: Enhanced tracking provides better visibility into deployment failures

### Added
- Release safety: Duplicate version detection in release script prevents accidentally creating duplicate releases

## [v7.11.1] - 2025-11-15

### Changed
- Docker build performance: Optimized build process by removing redundant operations, reducing build times significantly
- Development autoreload: Re-enabled autoreload with improved watchdog-based system that reduces CPU usage from 99% to normal levels while maintaining auto-reload functionality

## [v7.11.0] - 2025-11-15

### Added
- Changelog system: Implemented per-version changelog files for better organization and easier navigation
- Changelog list view: Users can browse all versions with proper semantic version sorting
- Changelog detail view: Each version has a dedicated page with markdown rendering for easy reading
- Navigation access: Added navbar link for quick access to changelog from anywhere in the application

### Fixed
- Release script security: Fixed shell variable injection vulnerability that could allow code execution
- Version sorting: Fixed incorrect version ordering in changelog list - now uses proper semantic versioning
