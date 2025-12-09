# FITS Changelog

## [v8.3.2] - 2025-12-05

### Added
- Comprehensive unit test suite for email provider utilization branch
- UnlockToken model tests covering token generation, validation, and lifecycle management
- LoginSecurityService handler tests for failed login processing, account locking, and progressive lock duration calculation
- SuspiciousLoginService tests for IP and device detection logic with helper extraction functions
- Email service helper tests for tenant detection and email template rendering

### Changed
- Improved test coverage for authentication and security services
- Standardized test structure across auth service modules with consistent patterns

### Testing
- Created 9 passing unit tests for UnlockToken model (token generation, validation, expiry checks)
- Created unit tests for LoginSecurityService handlers (account lock checking, progressive lock duration, failed attempt processing)
- Created unit tests for SuspiciousLoginService handlers (new IP detection, new device detection, IP/user agent extraction)
- Created unit tests for email service helpers (tenant detection from user, template rendering with fallback)
- All tests follow refactor.
- Tests use pytest with class-based organization matching existing test patterns
- UnlockToken tests verified passing (9/9 tests)
- Note: Some tests blocked by circular import in production code (app.

## [v8.3.1] - 2025-12-05

### Security
- ### Added

## [v8.3.0] - 2025-12-04

### Fixed
- Fixed Azure OAuth redirect URI detection: nginx now forwards correct host (IP or domain) to Django
- Fixed Azure OAuth refresh_token missing error by adding offline_access scope
- Fixed user edit redirect for super admins: now redirects to tenant detail page instead of empty user list
- Fixed user list query for super admins: now correctly displays all users using request.
- Fixed duplicate email sending: removed duplicate test handler causing two emails per click
- Fixed Transformers cache deprecation warning by migrating from TRANSFORMERS_CACHE to HF_HOME

### Added
- Implemented test email functionality: Send Test Email button on email provider detail page sends actual test email to tenant admin
- Implemented Gmail email sending: Gmail provider now actually sends emails via Gmail API (was returning success without sending)
- Implemented Exchange email sending: Exchange provider now sends emails via exchangelib (was returning success without sending)
- Added UserUrlService for centralized user URL generation with role-based redirect logic
- Added exchangelib dependency for Exchange email provider support

### Changed
- Unified OAuth workflow: removed separate Connect buttons, Create Provider now initiates OAuth flow automatically
- Improved Azure setup guide: dynamically displays correct redirect URI based on current host
- Updated email provider documentation to reflect unified OAuth workflow

## [v8.2.2] - 2025-12-01

### Added
- Added batch_fetch_project_scopes_data method to HierarchyQueries for efficient scope data retrieval
- Added URL generation methods to AssessmentUrlService that work with IDs directly (no NeoModel objects required)
- Added main_project_uid support to dashboard API for user-selectable main project feature
- Added data adapter transformation layer for dashboard data format conversion

### Changed
- Refactored dashboard_service.
- Split 434-line file into dashboard_service/ package structure with helpers.
- Extracted helper functions from batch_get_scopes_data to meet 25-line function limit
- Optimized environment_compliance_aggregation to use WHERE IN clause instead of per-environment queries
- Unified dashboard now uses batch queries and caches scope data to eliminate N+1 query problems
- Chart generators now accept cached scope data parameter to avoid duplicate queries
- Dashboard data adapter renamed transformToLegacy to transform for clarity
- Project selector now uses main_project_uid from API response when available
- Unified dashboard eliminates redundant NeoModel lookups by using UID-based URL generation

## [v8.2.1] - 2025-12-01

### Fixed
- Fixed scope publishing to wrong project when multiple projects have scopes with same name
- Updated ScopePage.
- Updated fallback titles in scope unpublish logic to match new title format

## [v8.2.0] - 2025-11-30

### Changed
- Refactored logger configuration from monolithic file to modular directory structure following helper subfolder pattern
- Refactored project views from single-file modules to organized directory structure (create, delete, detail, list, update)
- Improved code organization and maintainability with better separation of concerns
- Updated unpublish button to use blocking relationships check instead of assessment-only check for projects
- Refactored project detail view into modular components (actions, context, helpers, view)

### Fixed
- Fixed exception parameter naming in logger.
- Removed redundant data sanitization in project update error handling by reusing sanitized_data variable
- Improved error logging consistency across project update operations

### Added
- Added Project.
- Enhanced project delete handler with two-step confirmation for Confluence page deletion
- Added Confluence page existence checking and synchronous deletion support for projects
- Added project delete validation module with blocking relationship checks
- Added project detail view context builder with space credential validation
- Added project detail view actions builder with blocking relationship-aware delete action
- Improved project delete TypeScript handler with Confluence page deletion workflow

## [v8.1.2] - 2025-11-28

### Fixed
- Fixed unpublish button remaining active when scope has assessments
- Fixed delete button not showing descriptive text when disabled due to blocking relationships

### Changed
- Refactored scope blocking relationships check into common method `_scope_has_blocking_relationships()` in `ScopeBaseMixin` to eliminate duplication between `ScopeActionsMixin` and `ScopeContextMixin`
- Updated unpublish button to display "Cannot unpublish (has assessments)" when disabled
- Updated delete button to display descriptive message (e.

### Testing
- Verified delete and unpublish buttons are properly disabled when scope has assessments or assessment templates
- Verified button text changes to descriptive message when disabled
- Verified consistent validation logic across all scope action checks

## [v8.1.1] - 2025-11-28

### Fixed
- Fixed Confluence status macros rendering raw DEFAULTLINK markup instead of clickable links
- Fixed unreadable badge text in Confluence dark mode due to hardcoded light colors
- Fixed table headers missing white text color after initial dark mode fixes

### Changed
- Replaced all 29 Confluence status macros with custom span badges across 5 template files
- Migrated from `ac:structured-macro ac:name="status"` to styled `<span>` elements
- Removed explicit `color` property from badges to let Confluence's `legacy-color-text-inverse` handle theming
- Updated environment links in scope.

### Technical Details
- `scope.
- `compliance.
- `control.
- `assessment.
- `compliance_overview.
- Green (#2e7d32): Compliant, Approved states
- Red (#d32f2f): Non-Compliant, Rejected states
- Yellow (#f57c00): Pending, Partially Compliant states
- Grey (#344563): Unknown/Not Evaluated states
- Blue (#205081): Info, Domain, Environments
- Purple (#7b1fa2): Group categorization

### Testing
- Verified all status macros replaced (grep shows 0 remaining)
- No linting errors in modified templates
- Dark backgrounds ensure readability in both light and dark Confluence themes

## [v8.1.0] - 2025-11-27

### Fixed
- Fixed SyntaxError in json_utils.
- Extracted bracket and quote count operations to variables before f-string construction

### Changed
- Updated Dockerfiles: standardized base image to python:3.
- Production Dockerfile: removed --no-cache-dir flag from uv pip install for better caching
- Production docker-compose.
- Production docker-compose.
- Updated runtime paths helper script with improved error handling for directory creation and ownership changes
- Updated DigitalOcean remote deployment script for better reliability
- Removed pipdeptree from requirements.

## [v8.0.1] - 2025-11-26

### Fixed
- Restore fallback mechanism for report downloads when URLs missing from API response
- Add fallback buttons that dispatch project-report-download events for backward compatibility
- Restore event handler in ReportNavigationHandler for fallback path
- Close KPI dropdown on outside click to prevent multiple menus from staying open

### Changed
- Refactor project-kpi.
- Refactor report-navigation-handler.
- Improved code organization with clear single responsibilities

### Testing
- Verify fallback buttons render when report_urls missing
- Confirm events dispatch correctly for fallback path
- Test fallback URL construction
- Ensure analytics tracking works for both direct links and fallback path
- Verify dropdown closes on outside click
- Verify multiple dropdowns don't stay open simultaneously

## [v7.9.0] - 2025-11-15

### Added
- feat: Implement partial changelog system with per-version files and UI access
- Split CHANGELOG.
- Migrated existing changelog entries (v7.
- Updated release script to create per-version files and maintain index
- Added changelog list view at /changelog/ with semantic version sorting
- Added changelog detail view at /changelog/<version>/ with markdown rendering
- Added navbar link to changelog list for easy access
- Fixed shell variable injection vulnerability in release script (use env vars)
- Fixed semantic version sorting in changelog list (parse versions as integer tuples)

## [v7.8.5] - 2025-11-15

### Changed
- test change

### Fixed
- fix: Resolve development server CPU spike by constraining livereload to template directories only.

## [v7.8.4] - 2025-11-14

### Fixed
- fix: Convert absolute paths to relative patterns in uvicorn reload_excludes to resolve NotImplementedError

## [v7.8.3] - 2025-11-14

### Added
- feat: Add automated release management with changelog and versioning integration

## [v7.8.2] - 2025-11-14

### Security
- **Container Security Hardening**: Implemented non-root user execution for all container services

### Changed
- Docker compose files now use `user: "${FITS_UID:-1000}:${FITS_GID:-1000}"` directive
- Production containers use read-only filesystem with explicit volume mounts
- All application services run as non-root user by default

## [v7.11.7] - 2025-11-15

### Changed
- Fixes multiple critical production deployment failures that were causing container crash loops and preventing successful deployments.

## [v7.11.4] - 2025-11-15

### Fixed
- fix: Resolve production deployment issues
- SQLite database path for read-only filesystem
- Neo4j constraint warnings treated as non-fatal
- Nginx config editing on read-only filesystem
- gosu permission errors when already running as appuser
- SSL certificate permissions for container user
- Automated self-signed certificate fallback
- Nginx PID file permission errors
- Docker log rotation configuration

## [v7.11.20] - 2025-11-19

### Added
- Hetzner Cloud API library (`hetzner-api.
- Interactive server selection library (`server-selection.
- Server inventory script (`hz-list-servers.
- Server creation script (`hz-create-server.
- Manager script (`hz-manager.
- Deployment workflow scripts: `hz-deploy.
- SSH common utilities (`ssh-common.
- Comprehensive deployment documentation in `0-docs/hetzner-cloud-deployment/` covering bootstrap, API library, and workflows

### Changed
- Adapted DigitalOcean deployment patterns to Hetzner Cloud API structure
- Replaced DigitalOcean-specific terminology (droplets, DO_API_TOKEN) with Hetzner equivalents (servers, HCLOUD_TOKEN)
- Updated server selection to use Hetzner Cloud API endpoints and response format
- Enhanced labeling system with support for project, environment, and tenant labels

### Fixed
- Server selection now properly handles Hetzner Cloud API JSON response structure
- Auto-detection of `.
- Improved error handling for missing API tokens and empty server lists

## [v7.11.2] - 2025-11-15

### Changes
- Split `app/views/base/changelog.
- All functions <25 lines, all files <100 lines
- **Fixed semantic version sorting**: Changed sort priority to semantic version first, then file timestamp
- Ensures v7.
- Previously, file timestamps within the same second caused incorrect ordering
- Split `scripts/development/run_uvicorn_reloader.
- All functions <25 lines, all files <100 lines
- Maintains backward compatibility via wrapper file

### Features
- ✅ Improved code organization following helper subfolder pattern
- ✅ Fixed changelog version ordering (semantic version priority)
- ✅ Reduced complexity through better separation of concerns
- ✅ All modules maintain backward compatibility

### Testing
- ✅ Syntax validation passed
- ✅ No linter errors
- ✅ Changelog sorting verified (v7.
- ✅ Backward compatibility maintained for existing imports

## [v7.11.19] - 2025-11-19

### Employee Detail Page
- Added missing JavaScript block with \`employee-delete.

### Application Detail Page
- Fixed button class mismatch: changed \`delete-application-btn\` → \`application-delete-btn\` to match the handler expectations
- Added missing JavaScript block with \`application-delete.
- [ ] Verify employee detail page delete button shows confirmation modal
- [ ] Verify employee delete redirects to list page after successful deletion
- [ ] Verify application detail page delete button shows confirmation modal
- [ ] Verify application delete redirects to list page after successful deletion

## [v7.11.17] - 2025-11-18

### Fixed
- **AI Provider Model Changes:** Fixed issue where users could not change the AI model for an existing provider without re-entering their API key credentials.

### Technical Details
- **Root Cause:** Django's ChoiceField validation rejected model names not in the initial choices list.
- **Solution:** When connection_changed is False, the submitted model_name is dynamically added to the form's allowed choices before validation.
- **Impact:** Users can now change the model without re-entering their API key.

### Testing
- **Local Validation:** Ran migrate_validate_ai_provider_models which successfully validated 64 existing AIProvider nodes.
- **No UI Changes:** The select dropdown UI remains unchanged.

## [v7.11.16] - 2025-11-18

### Fixed
- Fixed regression where users cannot change AI provider models without re-entering API key credentials.

### Changed
- Always fetch available models when updating an AI provider, regardless of whether connection parameters changed
- `connection_changed` flag now only controls whether the `model_name` field is required for validation
- Removed conditional branches in `app/views/tenant_admin/ai_providers/update.
- Always call `fetch_models_for_update()` which handles missing API keys gracefully via emergency fallback

### Added
- Users can now change AI provider models without re-entering API key
- Model dropdown always populated with available models from API
- Graceful fallback to emergency models if API key unavailable
- Model field validation: required when connection changes, optional when unchanged

### Testing
- Update AI provider without changing API key → model dropdown populated with all available models
- Update AI provider with new API key → model dropdown populated, model required
- Update AI provider without API key → emergency fallback models shown

## [v7.11.15] - 2025-11-18

### Security
- ## Summary

## [v7.11.14] - 2025-11-17

### Removed
- Removed redundant `title` field from Space model, schema, forms, views, queries, templates, and TypeScript
- Space now uses only `name` and `key` fields (as per Confluence API requirements)

### Added
- **SpaceValidator utility** (`app/utils/space_validator/`) - Centralized credential validation and filtering
- **`credentials_invalid` flag** to Space model for caching invalid credentials
- **`credentials_validated_at` timestamp** to Space model for daily validation caching
- **Daily validation caching**: Spaces validated today skip re-validation on subsequent loads
- **AJAX endpoint** (`AvailableSpacesView`) for dynamic space loading in modals
- **Credential status indicators** across all Space management pages:
- **BaseSpaceOrgFormView** - Shared logic for create/update views

### Changed
- **Deferred validation for modals**: Space selection modals validate credentials only when opened, not on page load
- **Enhanced `AjaxResponseMixin`**: Better error message handling with optional message parameter
- **Improved `ConfluenceManager`**: Robust error handling for non-JSON responses, fallback API calls
- **Refactored space validation logic**: Eliminated duplicated date handling logic

### Performance
- Project/scope detail pages load faster by deferring space validation
- Daily validation caching prevents redundant API calls
- Invalid credential caching (skip if already flagged invalid)

### Files Modified
- **34 files changed**: 1,041 insertions(+), 214 deletions(-)
- Models: `app/models/client/space.
- Utilities: `app/utils/space_validator/` (refactored into helper subfolder)
- Views: `app/views/client/spaces_org/*`, `app/views/client/projects/detail.
- Templates: Space management templates, project/scope detail templates
- Frontend: `app/static/src/pages/space-attachment.
- Services: `confluence/manager.

## [v7.11.13] - 2025-11-17

### Security
- Fix: Filter assessment templates by organization scope

## [v7.11.12] - 2025-11-16

### Added
- ## Summary

## [v7.11.11] - 2025-11-16

### Fixed
- Fixed ImportError in `chat_search.

### Changed
- **Improved watchdog handler reliability**:
- **Template cleanup**: Simplified `chat_search.

### Testing
- Fixed import resolves Django startup error
- Watchdog handler improvements prevent false-positive restarts
- Changes follow canonical patterns as per @codex rules

## [v7.11.10] - 2025-11-16

### Fixed
- Fixed incorrect file paths in multi-tenant deployment scripts that were causing import failures.

### Changes
- **Fixed file paths** in three scripts:
- **Improved error handling**:

### Features
- Multi-tenant deployment scripts now correctly locate generated tenant files
- Better error messages help identify which tenant failed during generation
- Structured output (RESULT_*) properly references correct paths

### Testing
- Verified path corrections match actual file structure
- Error handling improvements tested with invalid inputs
- Changes follow canonical patterns as per @codex rules

### Added
- **Duplicate version detection** in release script to prevent redundant releases:

## [v7.11.1] - 2025-11-15

### Changed
- perf: Optimize Docker build time by using COPY --chown and removing redundant operations
- dev: Re-enabled autoreload using a new watchdog-based uvicorn runner (toggle with `UVICORN_RELOAD=false` or `UVICORN_RELOAD_STRATEGY=off`) so Python/template edits pick up without heavy CPU load

### Changes
- **Dockerfile**: Replaced `COPY .
- **production/Dockerfile**: Applied same optimization for production builds
- **.
- **push_image.

### Features
- Faster Docker builds by eliminating redundant chown operations
- Reduced build layers (one less RUN instruction per Dockerfile)
- Better version management integration in push script
- Smaller build context via improved .

### Testing
- Verified Docker builds complete successfully
- Confirmed file ownership is correct in built images
- Tested push_image.

## [v7.11.0] - 2025-11-15

### Added
- feat: Implement partial changelog system with per-version files and UI access
- Split CHANGELOG.
- Migrated existing changelog entries (v7.
- Updated release script to create per-version files and maintain index
- Added changelog list view at /changelog/ with semantic version sorting
- Added changelog detail view at /changelog/<version>/ with markdown rendering
- Added navbar link to changelog list for easy access
- Fixed shell variable injection vulnerability in release script (use env vars)
- Fixed semantic version sorting in changelog list (parse versions as integer tuples)
