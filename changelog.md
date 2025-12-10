# FITS Changelog

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
