# Cascade - Migration-Focused Autonomous Coding Boilerplate

## Overview

**Cascade** is a **silent scaffolding system** for migrating and developing applications. It provides the intelligence to migrate apps from Google AI Studio and continue their development, but it is designed to disappear from the final product. It serves as a **standardized scaffolding system** for migrating and developing complex software applications using autonomous AI agents.

Instead of starting from zero, Cascade provides the essential "instructional architecture" required to migrate an existing Google AI Studio app and turn it into a production-ready application. It implements a strictly defined **Migration-Focused Workflow** that separates concerns between app migration, architectural planning, database migration (when needed), project initialization, iterative development, and release management.

## Core Philosophy

As a boilerplate, this project aims to:

1. **Migrate Existing Apps:** Transform Google AI Studio exports into production-ready local projects.
2. **Enforce Standards:** Ensure every migrated project has a robust specification (`app_spec.txt`) and a rigorous testing plan (`feature_list.json`).
3. **Ensure Quality:** Mandate a "Test-First" development approach using real browser automation (Playwright) rather than fragile DOM emulation.

## The Migration-Focused Workflow

Cascade defines a sequence of agents for migrating and developing applications. You will use these agents sequentially, with the Database Migration agent being optional (only when the app has a database to migrate). The agents cascade from one to the next, each building upon the previous agent's output.

### Workflow Sequence

```
1. @ai-studio-migration → migration_report.txt
2. @architect (first call) → app_spec.txt (from migrated app)
3. @db-migration (if needed) → db_migration_report.txt + db_schema.txt
4. @architect (second call) → app_spec.txt (updated with DB schema)
5. @project-initializer → feature_list.json (for migrated features)
6. @coder → implements/verifies features
7. @release-engineer → versioning (automatic)
```

### 1. The AI Studio Migration Agent

- **Agent File:** `.claude/agents/ai-studio-migration.md`
- **Command:** `@ai-studio-migration`
- **Role:** Migrates a Google AI Studio exported app from buildless CDN-based architecture to production-ready local project with proper build tooling. **Also installs professional design foundation** (CVA, clsx, tailwind-merge, lucide-react) and enhances Tailwind config with CSS variable-based design tokens.
- **Input:** AI Studio export directory (extracted ZIP file)
- **Output:** `migration_report.txt` - Complete documentation of migration process, tech stack, file structure changes, and dependencies
- **Why:** Google AI Studio exports use a buildless architecture with CDN imports. This agent converts them to proper npm-based projects with build tooling (Vite/Next.js) and adds professional design infrastructure to avoid "AI slop" aesthetics.

### 2. The Specification Writer (Architect) - First Call

- **Agent File:** `.claude/agents/architect.md`
- **Command:** `@architect`
- **Role:** Analyzes the migrated app and generates a comprehensive technical specification file. **Acts as both technical architect AND design system analyst**, creating pixel-perfect design specifications to avoid generic "AI slop" aesthetics.
- **Input:** `migration_report.txt` (required), migrated code structure
- **Output:** `app_spec.txt` - Complete technical specification in XML format with detailed design_system section (color palette, typography, component specs, animations)
- **Why:** Creates a single source of truth for all future agents. The architect analyzes the migrated code to extract features, components, and tech stack, then generates the specification with professional design standards. Also interacts with user to determine database AND design aesthetic preferences (Distinctive Creative, Professional Dashboard, Minimal Refined, or Custom Brand).

### 3. The Database Migration Agent (Optional)

- **Agent File:** `.claude/agents/db-migration.md`
- **Command:** `@db-migration`
- **Role:** Migrates an existing application's database to a new database system (Grist, SQLite, PostgreSQL, etc.).
- **Input:** `app_spec.txt` (required), existing database config/schema files, application code using database
- **Output:** 
  - `db_migration_report.txt` - Complete documentation of database migration
  - `db_schema.txt` - Complete database schema definition for target database
- **When to use:** Only if the migrated app has a database that needs to be migrated to a new system.
- **Why:** Handles schema design, data migration, ID mapping, and code updates for database changes.

### 4. The Specification Writer (Architect) - Second Call

- **Agent File:** `.claude/agents/architect.md`
- **Command:** `@architect`
- **Role:** Updates the existing `app_spec.txt` with database schema information from the database migration.
- **Input:** `app_spec.txt` (required), `db_migration_report.txt` (required), `db_schema.txt` (required)
- **Output:** Updated `app_spec.txt` with complete database schema section
- **Why:** Ensures the specification includes complete database information after migration.

### 5. The Project Initializer (Project Lead)

- **Agent File:** `.claude/agents/project-initializer.md`
- **Command:** `@project-initializer`
- **Role:** Sets up the foundation for testing and development of the migrated app. Works with existing migrated project structure.
- **Input:** `app_spec.txt` (required), `migration_report.txt` (required), `db_schema.txt` (optional, if database migration occurred)
- **Output:** `feature_list.json` (50-75 test cases: 30-45 functional + 20-30 visual design), `init.sh` (environment setup), `.gitignore`, git repository initialization
- **Key Task:** Generates `feature_list.json` containing **50-75** strictly defined test cases to verify both functionality AND design quality. Includes pixel-perfect visual tests to enforce design_system specifications.
- **Why:** Creates the testing foundation with emphasis on visual regression prevention. Test count increased from 25-50 to 50-75 to include comprehensive visual design validation (typography, colors, components, spacing, animations).

### 6. The Coding Agent (Developer)

- **Agent File:** `.claude/agents/coder.md`
- **Command:** `@coder`
- **Role:** An iterative worker that picks **one** failing test, implements fixes or new features with pixel-perfect design quality, and verifies it using browser automation. **Enforces Visual Quality Mandate** to prevent generic "AI slop" aesthetics.
- **Input:** `app_spec.txt`, `feature_list.json`, `init.sh` (required), `migration_report.txt`, `db_schema.txt`, `claude-progress.txt` (optional)
- **Output:** Application code files (unpredictable, depends on tech stack), updates to `feature_list.json` (pass/fail status only), updates to `claude-progress.txt`
- **Tooling:** Configured to use **Playwright MCP** for visual regression testing and end-to-end verification. Uses DevTools inspection to verify pixel-perfect implementation.
- **Design Enforcement:** Before implementing ANY UI component, reads design_system section from app_spec.txt and uses EXACT Tailwind classes, CSS variables, and specifications. Verifies with DevTools that computed styles match spec.
- **Constraint:** Cannot move to feature B until feature A passes (both functional AND visual tests).

### 7. The Release Engineer (Finalization)

- **Agent File:** `.claude/agents/release-engineer.md`
- **Command:** `@release-engineer`
- **Role:** Performs SemVer versioning, changelog updates, annotated tags, and pre-flight checks. Does not deploy.
- **Input:** Version manifest files (package.json, pyproject.toml, Cargo.toml, etc.), git repository, `CHANGELOG.md` (optional, creates if missing)
- **Output:** Updated version manifests, `CHANGELOG.md` (created or updated), annotated git tags (`v{version}`), release commit
- **When to use:** Called AUTOMATICALLY by the coder agent after each feature completion. Can also be called manually for milestone releases.
- **Why:** Ensures professional, error-free releases following semantic versioning best practices.

## Repository Structure

```text
cascade/
├── .claude/
│   └── agents/
│       ├── ai-studio-migration.md      # Agent 1: Migrates AI Studio export
│       ├── architect.md                # Agent 2 & 4: Generates/updates app_spec.txt
│       ├── db-migration.md             # Agent 3 (Optional): Database migration
│       ├── project-initializer.md      # Agent 5: Sets up testing foundation
│       ├── coder.md                    # Agent 6: Implements/verifies features
│       └── release-engineer.md         # Agent 7: Versioning & releases
├── templates/
│   └── app_spec_example.txt            # Reference implementation of a spec file
└── AI_WORKFLOW.md
```

## Directory Info

- **`.claude/`**: Contains the agent definitions. Ignored by git.

- **`templates/`**: Reference files. Ignored by git.

- **`AI_WORKFLOW.md`**: This guide. Ignored by git.

- **`Root`**: The actual application code lives here (after migration).

To use Cascade effectively, you need:

1. **An LLM Interface:** (e.g., Claude Code, Google Antigravity, Cursor, or a CLI).
2. **Playwright MCP Server:** The Coding Agent is configured to use the Model Context Protocol (MCP) to control a headless browser.
   - *Required Tools:* `browser_navigate`, `browser_click`, `browser_take_screenshot`, etc.

## When to Use Which Agent

Each agent has specific trigger conditions:

### Migration Workflow Agents

- **`@ai-studio-migration`**: Use first when you have an exported Google AI Studio app to migrate. This creates `migration_report.txt`.
- **`@architect`** (Mode 1): Use after migration to generate `app_spec.txt` from the migrated app.
- **`@architect`** (Mode 2): Use after database migration to update `app_spec.txt` with database schema.
- **`@db-migration`**: Use only if the migrated app has a database that needs to be migrated to a new system. This creates `db_migration_report.txt` and `db_schema.txt`.
- **`@project-initializer`** (Mode 1): Use after `app_spec.txt` exists (and optionally after database migration). This creates `feature_list.json` and `init.sh` for the migrated app.
- **`@coder`** (Standard mode): Use repeatedly during development. Run this agent to verify and fix features one at a time from `feature_list.json`.
- **`@release-engineer`**: Called AUTOMATICALLY by the coder agent after each feature completion. Can also be called manually for milestone releases.

### Improvement Workflow Agents

- **`@architect`** (Mode 3): Use when you want to add new features/improvements to an existing app. This creates `improvement_spec.txt`.
- **`@project-initializer`** (Mode 2): Use after `improvement_spec.txt` exists. This creates `improvement_list.json` with tests for improvements.
- **`@coder`** (Improvement mode): Automatically detects and prioritizes `improvement_list.json`. Implements improvements and merges them into `feature_list.json` when complete.
- **`@release-engineer`**: Still called AUTOMATICALLY after each improvement completion.

---

## Iterative Improvement Workflow (Post-Migration)

After your initial migration is complete and you have a working app with `feature_list.json`, you may want to add new features or make improvements. Use this workflow:

### Workflow Sequence for Improvements

```
1. @architect (improvement mode) → improvement_spec.txt
2. @project-initializer (improvement mode) → improvement_list.json
3. @coder (improvement mode) → implements/verifies improvements
4. @release-engineer → versioning (automatic)
```

### When to Use Improvement Workflow

- App already migrated and `feature_list.json` exists
- User wants to add NEW features not in original migration
- User wants to make improvements/enhancements to existing features
- User wants to refactor or optimize existing functionality

### Improvement Workflow Steps

#### Step 1: Define Improvements

```bash
@architect I want to add [describe new features/improvements]
```

Example: `@architect I want to add a dark mode toggle and user preferences page`

The architect will:
- Analyze your request and ask clarifying questions
- Review existing `app_spec.txt` for context
- Analyze current codebase to identify integration points
- Create `improvement_spec.txt` with detailed improvement requirements

#### Step 2: Create Improvement Tests

```bash
@project-initializer Set up tests for the improvements
```

The project-initializer will:
- Read `improvement_spec.txt` and `app_spec.txt`
- Generate `improvement_list.json` with 5-25 test cases
- Include integration tests to verify compatibility with existing features
- Tests focus only on new/changed functionality

#### Step 3: Implement Improvements

```bash
@coder Work on the improvements
```

The coder will:
- **Automatically detect `improvement_list.json` and prioritize it**
- Implement and verify improvements one by one
- Test integration with existing features
- Automatically call release-engineer after each improvement completion
- When all improvements pass, merge `improvement_list.json` into `feature_list.json`

#### Step 4: Releases (Automatic)

The release-engineer is called automatically after each improvement completion, just like with features.

### Key Differences from Migration Workflow

1. **Smaller Scope:** Improvements typically have 5-25 tests vs. 25-50 for migration
2. **Integration Focus:** Improvement tests emphasize compatibility with existing features
3. **Separate Tracking:** `improvement_list.json` exists separately until all improvements complete
4. **Automatic Merge:** When all improvements pass, they're merged into `feature_list.json`
5. **Iterative:** You can run this workflow multiple times to continuously add features

---

## Usage Guide

### Step 1: Export from Google AI Studio

Export your app from Google AI Studio's Build mode as a ZIP file. Extract it to a directory.

### Step 2: Migrate the App

Run the AI Studio Migration agent:

```bash
@ai-studio-migration. Migrate my AI Studio export
```

The agent will:
- Analyze the export structure
- Convert CDN imports to npm packages
- Set up proper build tooling (Vite/Next.js)
- Migrate environment variables
- Create `migration_report.txt`

### Step 3: Generate Specification with Design System

Run the Architect agent (first call):

```bash
@architect. Generate app specification from migrated app
```

The agent will:
- Analyze the migrated app structure
- Extract features and components
- **Ask you about design aesthetic preference:**
  - Option 1: Distinctive Creative Theme (recommended - unique, memorable)
  - Option 2: Professional Dashboard (clean, data-focused)
  - Option 3: Minimal Refined (understated elegance)
  - Option 4: Custom Brand (provide your brand colors/fonts)
- Ask you about database preferences
- Generate `app_spec.txt` with:
  - Complete technical specification
  - **Detailed design_system section** with:
    - Creative color palette (NOT purple gradients or blue-500 defaults)
    - Distinctive typography (NOT Inter/Roboto/Arial)
    - Pixel-perfect component specifications (exact Tailwind classes)
    - Atmospheric backgrounds (NOT flat white)
    - Animation specifications

### Step 4: (Optional) Migrate Database

**Only if your app has a database to migrate:**

```bash
@db-migration. Migrate my database to [Grist/SQLite/etc.]
```

The agent will:
- Analyze existing database schema
- Design target database schema
- Execute data migration
- Update application code
- Create `db_migration_report.txt` and `db_schema.txt`

### Step 5: Update Specification with Database

**Only if you completed Step 4:**

```bash
@architect. Update app specification with database schema
```

The agent will:
- Read database migration outputs
- Update `app_spec.txt` with complete database schema

### Step 6: Initialize Testing Foundation

```bash
@project-initializer. Set up feature tracking for migrated app
```

The agent will:
- Read `app_spec.txt` and `migration_report.txt`
- Generate `feature_list.json` with **50-75 tests** for migrated features:
  - **30-45 functional tests** (features, API, database)
  - **20-30 visual design tests** (typography, colors, components, spacing, animations)
  - All visual tests are **pixel-perfect** with DevTools verification steps
- Create `init.sh` for development environment
- Initialize git repository (if not already done)

### Step 7: Verify and Develop (The Loop)

Now, iterate with the Coder agent. Run this command repeatedly:

```bash
@coder. Verify and fix the next failing test
```

**Important:** After each feature is completed and verified, the Coder agent will AUTOMATICALLY call the Release Engineer to create an incremental release. This means:

- Each completed feature gets its own version tag (typically PATCH bumps: 1.2.3 → 1.2.4)
- The changelog is updated incrementally with each feature
- Version history is maintained throughout development
- You don't need to manually call the release-engineer during the build loop

*Repeat Step 7 until all tests pass. The release-engineer will be called automatically after each feature completion.*

### Step 8: Final Release (Optional)

If you want to create a milestone release (e.g., moving from 0.x.x to 1.0.0, or creating a beta/rc release), you can manually call:

```bash
@release-engineer. Create a milestone release
```

This is optional - the automatic incremental releases during development are sufficient for most cases.

## Key Differences from New App Creation

This workflow is specifically designed for **migrating existing apps**, not creating new ones:

1. **Migration First:** The workflow starts with migrating an existing AI Studio app, not creating from scratch.
2. **Analysis-Based Specs:** The architect analyzes migrated code to generate specs, rather than creating from user ideas.
3. **Existing Structure:** The project-initializer works with existing migrated structure, not creating new structure.
4. **Feature Verification:** Tests focus on verifying migrated features work correctly, not building new features from scratch.
5. **Database Migration:** Optional step to migrate existing databases to new systems.

## Contributing

Cascade is a living boilerplate. If you find that the agents consistently fail at a specific task (e.g., migration issues), update the relevant agent file in `.claude/agents/` to provide better logic.

## Acknowledgments & Inspiration

Cascade was inspired by research and best practices from the AI agent development community. We gratefully acknowledge the following sources:

### Primary Inspiration

- **"AI Agents That Actually Work"** by Nate B Jones  
  YouTube Video: [https://www.youtube.com/watch?v=xNcEgqzlPqs](https://www.youtube.com/watch?v=xNcEgqzlPqs)  
  YouTube Channel: [AI News & Strategy Daily | Nate B Jones](https://www.youtube.com/@NateBJones)  
  *This video provided the primary inspiration for Cascade's multi-agent workflow architecture.*

### Additional References

- **"Effective harnesses for long-running agents"** by Anthropic  
  Blog Post: [https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)  
  *This research informed our approach to incremental progress tracking, feature lists, and session management across multiple context windows.*

- **Anthropic Autonomous Coding Quickstart**  
  GitHub Repository: [https://github.com/anthropics/claude-quickstarts/tree/main/autonomous-coding](https://github.com/anthropics/claude-quickstarts/tree/main/autonomous-coding)  
  *This quickstart provided valuable insights into initializer and coding agent patterns, testing strategies, and environment management.*

These resources collectively shaped Cascade's design philosophy of using specialized agents, structured feature tracking, and incremental development to enable long-running autonomous coding workflows.
