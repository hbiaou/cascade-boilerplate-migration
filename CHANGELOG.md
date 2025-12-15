# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.6.1] - 2025-12-15

### Changed

- **Documentation:** Updated `README.md` to include:
  - QA Engineer agent in the Agent list.
  - QA Engineer agent in the Repository Structure.

## [0.6.0] - 2025-12-15

### Added

- **QA Engineer Agent:** Added `qa-engineer.md`, a new on-demand agent for Black-Box testing (browser automation) and documentation maintenance.
  - Supports Smoke Tests, Targeted Scenarios, and Exploratory/Monkey Testing using `chrome-devtools` MCP.
  - Generates structured `qa_report.md` for the Architect agent.
  - Enforces strict no-code-modification rule (docs only).

### Changed

- **Workflow Update:** Updated `AI_WORKFLOW.md` to include coverage of the new QA Engineer agent.
  - Defined explicit "On-Demand" role for QA.
  - Added repository structure reference.

## [0.5.0] - 2025-12-15

### Changed

- **Browser Automation Migration:** Migrated from Playwright MCP to chrome-devtools MCP as the primary browser automation tool
  - Updated `coder` agent with comprehensive chrome-devtools MCP tool reference (26 tools across 6 categories):
    - Input Automation: click, drag, fill, fill_form, handle_dialog, hover, press_key, upload_file
    - Navigation Automation: close_page, list_pages, navigate_page, new_page, select_page, wait_for
    - Emulation: emulate, resize_page
    - Performance: performance_analyze_insight, performance_start_trace, performance_stop_trace
    - Network: get_network_request, list_network_requests
    - Debugging: evaluate_script, get_console_message, list_console_messages, take_screenshot, take_snapshot
  - Simplified Browser Testing Setup: Removed Docker configuration requirements
    - chrome-devtools MCP accesses localhost directly (no Docker container)
    - Navigation now uses standard localhost URLs (no host.docker.internal needed)
  - Fixed default port references: Changed from localhost:5173 to localhost:3000
  - Playwright MCP documented as alternative option with Docker configuration guidance
  - Updated tool references across all agent documentation (AI_WORKFLOW.md, ai-studio-migration.md)

### Added

- **README.md** - Comprehensive project documentation
  - Project overview and core philosophy
  - Prerequisites section with chrome-devtools MCP as primary tool
  - Complete workflow sequence and agent descriptions
  - Quick start guide
  - Iterative improvement workflow documentation
  - Known Issues & Troubleshooting section for Playwright Docker setup
  - Repository structure reference
  - Acknowledgments and inspiration sources

### Removed

- Docker browser configuration from standard workflow (moved to Known Issues for Playwright users)
- `IMPLEMENTATION_STATUS.md` file (no longer needed)

### Fixed

- Browser testing setup now correctly references localhost:3000 as default port
- Visual verification in ai-studio-migration agent updated to use chrome-devtools MCP tools

### Technical Details

- Total changes: 75 additions, 214 deletions across 4 files
- New file: README.md (comprehensive project documentation)
- Simplified browser automation workflow eliminates Docker complexity
- Maintains backward compatibility with Playwright option for users who prefer it

## [0.4.1] - 2025-12-14

### Changed

- **Documentation Enhancement:** Updated `AI_WORKFLOW.md` to comprehensively document Improvement Mode workflow
  - Added mode labels to all agent descriptions (Mode 1, Mode 2, Mode 3)
  - Created new "Agent Modes Summary" section with detailed breakdowns:
    - Architect agent's three modes (Migration Specification, Database Update, Improvement Specification)
    - Project Initializer agent's two modes with mode-aware prerequisite checks
    - Coder agent's automatic mode detection and prioritization logic
  - Documented mode-aware prerequisites from v0.3.1 bug fix:
    - Mode 1 (Migration): Requires `app_spec.txt` + `migration_report.txt`
    - Mode 2 (Improvement): Requires `improvement_spec.txt` + `app_spec.txt` (no migration_report.txt)
  - Updated repository structure to include `improvement_spec_example.txt` template
  - Enhanced improvement workflow steps with automatic mode detection details
  - Corrected test count references (5-25 for improvements, 50-75 for migration)
  - Improved "When to Use Which Agent" section with detailed prerequisite specifications

### Technical Details

- Documentation updates: 72 additions, 13 deletions to AI_WORKFLOW.md
- Ensures users understand the complete improvement workflow introduced in v0.3.0
- Clarifies the critical mode-aware prerequisite checking from v0.3.1

## [0.4.0] - 2025-12-14

### Added

- **Professional Design Foundation System** - Complete infrastructure to prevent generic "AI slop" aesthetics
  - Design utility installation in `ai-studio-migration` agent:
    - `class-variance-authority` (CVA) for component variant management
    - `clsx` for conditional class name composition
    - `tailwind-merge` for Tailwind class conflict resolution
    - `lucide-react` icon library
  - Enhanced Tailwind configuration with CSS variable-based design tokens
    - Complete color palette (primary, accent, muted, destructive, etc.)
    - Responsive border radius tokens
    - Font family configuration (`font-heading`, `font-body`)
    - shadcn/ui design system compatibility
  - CSS variables for light and dark mode theming
    - Semantic color tokens with HSL format for flexibility
    - Font family CSS variables (`--font-heading`, `--font-body`)

- **Design System Analyst Role in Architect Agent**
  - Step 2.5: Comprehensive design system template with 4 example themes:
    - Warm Terracotta (creative/lifestyle apps)
    - Deep Ocean (productivity/analytics)
    - Forest Sage (wellness/nature apps)
    - Midnight Crimson (bold/editorial)
  - User design preference question with 4 options:
    - Distinctive Creative Theme (unique, memorable)
    - Professional Dashboard (clean, data-focused)
    - Minimal Refined (understated elegance)
    - Custom Brand (user-provided guidelines)
  - Complete design_system section template in app_spec.txt:
    - Color palette specifications (HSL CSS variables)
    - Typography specifications (distinctive fonts with CSS variables)
    - Component specifications (exact Tailwind classes)
    - Background/atmosphere specifications
    - Spacing system (4px grid)
    - Animation specifications
    - Accessibility requirements
  - Anti-slop aesthetics mandate:
    - Forbids generic fonts (Inter, Roboto, Arial, Space Grotesk)
    - Forbids clichéd color schemes (purple gradients, blue-500 defaults)
    - Forbids predictable layouts (flat white backgrounds)

- **Pixel-Perfect Test Requirements in Project Initializer**
  - Enhanced test categories with Visual Design Quality section:
    - Typography tests (5 tests)
    - Color palette tests (5 tests)
    - Component specification tests (5 tests)
    - Responsive design tests (3 tests)
    - Accessibility tests
    - Polish tests
  - 6 pixel-perfect test examples:
    - Card component specifications
    - Typography hierarchy verification
    - Button interactive states
    - Color palette consistency
    - Background atmosphere
    - Spacing/sizing precision
  - Updated test quantity guidelines: 50-75 tests total
    - 30-45 functional tests
    - 20-30 visual design tests

- **Visual Quality Mandate in Coder Agent**
  - Anti-patterns documentation:
    - Generic font usage examples
    - Lazy color implementation patterns
    - Arbitrary spacing violations
  - Design System First approach:
    - 7-step verification checklist
    - Code examples (wrong vs. correct)
    - CSS variable usage patterns
  - Enhanced verification with 8 visual regression check categories:
    - Color & contrast issues
    - Typography problems
    - Layout & spacing issues
    - Component styling issues
    - Interactive states issues
    - Animation issues
    - Background & atmosphere
    - Console & polish
  - Visual Verification Process with example fix workflow
  - DevTools inspection requirements for pixel-perfect implementation

### Changed

- Updated `AI_WORKFLOW.md` to reflect design foundation across all agent descriptions
- Test count increased from 25-50 to 50-75 to include comprehensive visual design validation
- Architect agent now acts as both technical architect AND design system analyst
- Migration verification checklist includes design foundation checks
- All agent workflows updated to emphasize pixel-perfect design quality

### Fixed

- Step numbering in `architect` agent (merged STEP 3 and STEP 3.5 for logical flow)
- Populated empty `design_system` section in app_spec.txt template
- Added font family Tailwind configuration to support `font-heading` and `font-body` classes
- Added `--font-heading` and `--font-body` CSS variables to migration agent output
- Updated typography hierarchy in architect template to use font utility classes

### Technical Details

- Total additions: ~1,411 lines across 6 files
- Design foundation prevents visual regression in migrated apps
- Ensures professional, pixel-perfect design quality from migration through development
- Complete workflow integration from ai-studio-migration → architect → project-initializer → coder

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

[0.5.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.5.0
[0.4.1]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.4.1
[0.4.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.4.0
[0.3.1]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.3.1
[0.3.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.3.0
[0.2.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.2.0
[0.1.0]: https://github.com/hbiaou/cascade-boilerplate-migration/releases/tag/v0.1.0
