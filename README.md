# Cascade - Migration-Focused Autonomous Coding Boilerplate

## Overview

**Cascade** is a **silent scaffolding system** for migrating and developing applications. It provides the intelligence to migrate apps from Google AI Studio and continue their development, but it is designed to disappear from the final product. It serves as a **standardized scaffolding system** for migrating and developing complex software applications using autonomous AI agents.

Instead of starting from zero, Cascade provides the essential "instructional architecture" required to migrate an existing Google AI Studio app and turn it into a production-ready application. It implements a strictly defined **Migration-Focused Workflow** that separates concerns between app migration, architectural planning, database migration (when needed), project initialization, iterative development, and release management.

## Core Philosophy

As a boilerplate, this project aims to:

1. **Migrate Existing Apps:** Transform Google AI Studio exports into production-ready local projects.
2. **Enforce Standards:** Ensure every migrated project has a robust specification (`app_spec.txt`) and a rigorous testing plan (`feature_list.json`).
3. **Ensure Quality:** Mandate a "Test-First" development approach using real browser automation rather than fragile DOM emulation.

## Prerequisites

To use Cascade effectively, you need:

1. **An LLM Interface:** Claude Code CLI, Google Antigravity, Cursor, or similar AI-powered development environment.

2. **Chrome DevTools MCP Server:** The Coding Agent uses the Model Context Protocol (MCP) to control Chrome DevTools for browser automation and visual verification.

   **Installation:**
   ```bash
   # The chrome-devtools MCP server will be automatically available if you're using Claude Code
   # For manual installation, add to your MCP client config:
   npx chrome-devtools-mcp@latest
   ```

   **Alternative - Playwright MCP Server:** If you prefer Playwright over Chrome DevTools, you can use the Playwright MCP server instead. Note that you'll need to modify the browser tool references in the `@coder` agent file (`.claude/agents/coder.md`) to match Playwright's tool names.

   **Required Tools (chrome-devtools):** `navigate_page`, `click`, `fill`, `take_screenshot`, `take_snapshot`, `list_console_messages`, `get_network_request`, etc.

3. **Chrome Browser:** Chrome DevTools MCP requires Google Chrome to be installed on your system.

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

### The Agents

#### 1. The AI Studio Migration Agent
- **Command:** `@ai-studio-migration`
- **Role:** Migrates a Google AI Studio exported app from buildless CDN-based architecture to production-ready local project with proper build tooling.
- **Input:** AI Studio export directory (extracted ZIP file)
- **Output:** `migration_report.txt`

#### 2. The Specification Writer (Architect)
- **Command:** `@architect`
- **Role:** Generates comprehensive technical specifications with pixel-perfect design system details. Operates in three modes: (1) Migration spec generation, (2) Database update, (3) Improvement specification.
- **Output:** `app_spec.txt` or `improvement_spec.txt`

#### 3. The Database Migration Agent (Optional)
- **Command:** `@db-migration`
- **Role:** Migrates existing databases to new database systems (Grist, SQLite, PostgreSQL, etc.).
- **When to use:** Only if the migrated app has a database to migrate.
- **Output:** `db_migration_report.txt`, `db_schema.txt`

#### 4. The Project Initializer
- **Command:** `@project-initializer`
- **Role:** Sets up testing foundation with comprehensive test cases (50-75 tests including visual regression tests).
- **Output:** `feature_list.json`, `improvement_list.json`, `init.sh`

#### 5. The Coding Agent
- **Command:** `@coder`
- **Role:** Iteratively implements and verifies features using browser automation. Enforces Visual Quality Mandate to prevent generic "AI slop" aesthetics. Automatically calls release-engineer after each feature completion.
- **Output:** Application code files, updates to test lists, `claude-progress.txt`

#### 6. The Release Engineer (Automatic)
- **Command:** `@release-engineer`
- **Role:** Performs SemVer versioning, changelog updates, and git tagging. Called automatically by coder agent after each feature.
- **Output:** Version manifests, `CHANGELOG.md`, annotated git tags

#### 7. The QA Engineer (On-Demand)
- **Command:** `@qa-engineer`
- **Role:** Performs black-box testing (Smoke/Monkey/Scenario) using browser automation and maintains documentation. **Does not modify application code.**
- **When to use:** Anytime you want to verify the app or update documentation.
- **Output:** `qa_report.md` (for Architect), updated `README.md`/`docs/`

## Quick Start

### Step 1: Export from Google AI Studio
Export your app from Google AI Studio's Build mode as a ZIP file. Extract it to a directory.

### Step 2: Migrate
```bash
@ai-studio-migration. Migrate my AI Studio export
```

### Step 3: Generate Specification
```bash
@architect. Generate app specification from migrated app
```

### Step 4: (Optional) Migrate Database
```bash
@db-migration. Migrate my database to [target system]
```

### Step 5: Initialize Testing
```bash
@project-initializer. Set up feature tracking for migrated app
```

### Step 6: Develop (The Loop)
```bash
@coder. Verify and fix the next failing test
```
Repeat until all tests pass. The release-engineer is called automatically after each feature.

## Iterative Improvement Workflow

After migration is complete, you can add new features using the improvement workflow:

```
1. @architect (improvement mode) → improvement_spec.txt
2. @project-initializer (improvement mode) → improvement_list.json
3. @coder (improvement mode) → implements/verifies improvements
4. @release-engineer → versioning (automatic)
```

Example:
```bash
@architect I want to add dark mode toggle and user preferences
@project-initializer Set up tests for the improvements
@coder Work on the improvements
```

## Repository Structure

```text
cascade/
├── .claude/
│   └── agents/
│       ├── ai-studio-migration.md      # Agent 1: Migrates AI Studio export
│       ├── architect.md                # Agent 2, 4, & Improvement: Generates/updates specs
│       ├── db-migration.md             # Agent 3 (Optional): Database migration
│       ├── project-initializer.md      # Agent 5 & Improvement: Sets up testing foundation
│       ├── coder.md                    # Agent 6: Implements/verifies features
│       ├── release-engineer.md         # Agent 7: Versioning & releases (automatic)
│       └── qa-engineer.md              # Agent 8 (On-Demand): QA & Documentation
├── templates/
│   ├── app_spec_example.txt            # Reference implementation
│   └── improvement_spec_example.txt    # Reference for improvements
└── AI_WORKFLOW.md                      # Detailed workflow guide
```

## Known Issues & Troubleshooting

### Browser Automation with Docker (If Using Playwright MCP)

If you choose to use Playwright MCP instead of Chrome DevTools MCP, note that Playwright runs in a Docker container and requires special configuration:

**Problem:** Browser cannot access `localhost` directly because it resolves to the container, not your host machine.

**Solution:** Use `host.docker.internal` hostname and configure your dev server:

**Required Vite Configuration:**
```typescript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    host: '0.0.0.0', // Listen on all interfaces
    port: 3000,      // Or your project's port
    strictPort: true,
    allowedHosts: [
      'host.docker.internal', // REQUIRED for Docker browser access
      'localhost',
      '127.0.0.1'
    ]
  }
})
```

**Browser Navigation (Playwright only):**
```typescript
// Navigate using host.docker.internal
browser_navigate("http://host.docker.internal:3000")
```

**Note:** Chrome DevTools MCP does NOT have this issue as it accesses localhost directly without Docker.

## Key Differences from New App Creation

This workflow is specifically designed for **migrating existing apps**, not creating new ones:

1. **Migration First:** Starts with migrating an existing AI Studio app, not creating from scratch.
2. **Analysis-Based Specs:** The architect analyzes migrated code to generate specs.
3. **Feature Verification:** Tests focus on verifying migrated features work correctly.
4. **Database Migration:** Optional step to migrate existing databases to new systems.

## Contributing

Cascade is a living boilerplate. If you find that the agents consistently fail at a specific task, update the relevant agent file in `.claude/agents/` to provide better logic.

## Acknowledgments

Cascade was inspired by research and best practices from the AI agent development community:

- **"AI Agents That Actually Work"** by Nate B Jones
  [YouTube Video](https://www.youtube.com/watch?v=xNcEgqzlPqs)

- **"Effective harnesses for long-running agents"** by Anthropic
  [Blog Post](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)

- **Anthropic Autonomous Coding Quickstart**
  [GitHub Repository](https://github.com/anthropics/claude-quickstarts/tree/main/autonomous-coding)
