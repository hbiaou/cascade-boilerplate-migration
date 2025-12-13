# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.3.1] - 2025-12-13

### Fixed

- **Critical Bug Fix:** Mode-aware prerequisite check in `project-initializer` agent
  - Prerequisite check now detects mode before validating required files
  - Mode 1 (Migration) requires: `app_spec.txt`, `migration_report.txt`
  - Mode 2 (Improvement) requires: `improvement_spec.txt`, `app_spec.txt`
  - Previously blocked improvement workflow by requiring `migration_report.txt` unconditionally
  - Mode 2 now explicitly validates `improvement_spec.txt` presence (was missing)
  - Removed redundant file existence check from Mode 2 block
  - Users can now successfully run improvement initialization without migration files

## [0.3.0] - 2025-12-13

### Added

- **Iterative Improvement Workflow** - Complete workflow for adding new features to migrated apps
  - `architect` agent Mode 3: Generates `improvement_spec.txt` for new features/improvements
  - `project-initializer` agent Mode 2: Creates `improvement_list.json` with 5-25 improvement tests
  - `coder` agent improvement mode: Automatically detects and prioritizes `improvement_list.json`
  - Automatic merge of completed improvements into `feature_list.json`
  - Integration testing requirements for backward compatibility
- `templates/improvement_spec_example.txt` - Reference implementation for improvement specifications
- Comprehensive documentation in `AI_WORKFLOW.md` for improvement workflow
- Mode detection and workflow guidance in all affected agents

### Changed

- `architect` agent now operates in three modes: Migration (Mode 1), Database Update (Mode 2), and Improvement (Mode 3)
- `project-initializer` agent now supports both migration initialization and improvement tracking
- `coder` agent automatically prioritizes improvements when `improvement_list.json` exists
- Enhanced "When to Use Which Agent" section with separate Migration and Improvement workflow guidance

### Technical Details

- Total additions: ~710 lines across 4 agent files
- New template file: `improvement_spec_example.txt` (12KB)
- Backward compatible: Existing migration workflow unchanged
- Improvement workflow is completely optional and iterative

## [0.2.0] - 2025-12-13

### Added

- Visual verification workflow in `ai-studio-migration` agent with mockup comparison capabilities
  - Automated visual comparison using browser tools with Docker environment support
  - Manual visual verification steps and checklist
  - Common styling issues troubleshooting guide
  - Migration report integration for visual regression tracking
- Docker environment support for browser testing in `coder` agent
  - Vite configuration for Docker container browser access using `host.docker.internal`
  - Browser navigation examples and setup verification steps
  - Documentation for resolving localhost resolution issues in containerized environments

### Changed

- Enhanced `ai-studio-migration` agent documentation with detailed visual verification phase
- Updated agent tool declarations for improved clarity
- Improved `architect` agent documentation with optional user-provided document references

### Fixed

- Docker browser testing configuration to resolve `localhost` connection failures in containerized environments

## [0.1.0] - 2025-12-12

### Added
- Initial repository structure for Cascade AI Studio migration framework
- Custom Claude agents for automated migration workflow:
  - `ai-studio-migration` - Migrates Google AI Studio exports to production-ready projects
  - `architect` - Generates and updates app specifications
  - `coder` - Autonomous development with feature tracking
  - `db-migration` - Database migration support (Grist, SQLite, PostgreSQL)
  - `project-initializer` - Project initialization from specifications
  - `release-engineer` - Semantic versioning and release management
- AI_WORKFLOW.md documentation outlining the complete migration process
- Git configuration with appropriate ignore rules

[0.3.1]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.3.1
[0.3.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.3.0
[0.2.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.2.0
[0.1.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.1.0
