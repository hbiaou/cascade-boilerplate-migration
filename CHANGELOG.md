# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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

[0.2.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.2.0
[0.1.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.1.0
