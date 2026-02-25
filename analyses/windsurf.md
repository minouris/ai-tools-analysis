← [Previous: Tabnine](tabnine.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: OpenAI Codex](openai-codex.md) →

---

# Windsurf Analysis

**Analysis Date:** 25 February 2026  
**Tool Version:** Wave 13 / v1.13.3 (as of February 2026)  
**Analyst:** GitHub Copilot  
**Official Documentation:** https://docs.windsurf.com

---

## Table of Contents

- [1. Tool Overview](#1-tool-overview)
  - [Description](#description)
  - [Key Features](#key-features)
- [2. LLM Provider Integration](#2-llm-provider-integration)
  - [2.1 Ollama Integration](#21-ollama-integration)
  - [2.2 GitHub Copilot Pro Integration](#22-github-copilot-pro-integration)
  - [2.3 Microsoft AI Foundry Integration](#23-microsoft-ai-foundry-integration)
  - [2.4 OpenAI Integration](#24-openai-integration)
  - [2.5 Anthropic (Claude) Integration](#25-anthropic-claude-integration)
- [3. Policies and Rules (Instruction Files)](#3-policies-and-rules-instruction-files)
  - [Instruction File Support](#instruction-file-support)
  - [Configuration Method](#configuration-method)
  - [Syntax and Structure](#syntax-and-structure)
  - [Scope and Application](#scope-and-application)
  - [Example Policies](#example-policies)
- [4. Custom and Stored Prompts](#4-custom-and-stored-prompts)
  - [Prompt Storage Mechanism](#prompt-storage-mechanism)
  - [Creating Custom Prompts](#creating-custom-prompts)
  - [Organising Prompts](#organising-prompts)
  - [Using Stored Prompts](#using-stored-prompts)
  - [Sharing and Exporting](#sharing-and-exporting)
- [5. Tools and Model Context Protocol (MCP)](#5-tools-and-model-context-protocol-mcp)
  - [Model Context Protocol (MCP)](#model-context-protocol-mcp)
  - [MCP Server Configuration](#mcp-server-configuration)
  - [Available Tools](#available-tools)
  - [Custom Tool Development](#custom-tool-development)
- [6. Application Development Workflow](#6-application-development-workflow)
  - [6.1 Project Initialisation](#61-project-initialisation)
  - [6.2 Design and Planning](#62-design-and-planning)
  - [6.3 Code Generation](#63-code-generation)
  - [6.4 Iterative Development](#64-iterative-development)
  - [6.5 Testing and Validation](#65-testing-and-validation)
  - [6.6 Debugging](#66-debugging)
  - [6.7 Deployment](#67-deployment)
- [7. IDE and Environment Integration](#7-ide-and-environment-integration)
  - [7.1 Visual Studio Code](#71-visual-studio-code)
  - [7.2 JetBrains IDEs](#72-jetbrains-ides)
  - [7.3 Eclipse](#73-eclipse)
  - [7.4 Terminal and CLI](#74-terminal-and-cli)
  - [7.5 Other IDEs and Editors](#75-other-ides-and-editors)
- [8. Third Party Reviews and Experiences](#8-third-party-reviews-and-experiences)
  - [User Feedback and Testimonials](#user-feedback-and-testimonials)
  - [Reported Bugs and Issues](#reported-bugs-and-issues)
  - [Productivity Impact](#productivity-impact)
  - [Comparison with Other Tools](#comparison-with-other-tools)
- [9. Summary and Key Findings](#9-summary-and-key-findings)
  - [Strengths](#strengths)
  - [Limitations](#limitations)
  - [Best Use Cases](#best-use-cases)
  - [Documentation Quality](#documentation-quality)
- [10. Completeness Checklist](#10-completeness-checklist)
- [11. References](#11-references)
  - [Official Documentation](#official-documentation)
  - [Version Information](#version-information)
- [Revision History](#revision-history)

---

## 1. Tool Overview

**Official Documentation:** https://docs.windsurf.com  
**Version Analysed:** Wave 13 / v1.13.3 (as of February 2026)  
**Primary Use Case:** AI-first code editor (full IDE) with agentic AI coding via Cascade  
**Licensing:** Free tier; Pro at $15/month; Teams at $30/user/month; Enterprise (custom pricing)

### Description

Windsurf is a standalone AI-first code editor (full IDE) built by Windsurf Inc., the company previously known as Codeium. It was publicly launched in November 2024. Windsurf is a distinct product from the Codeium extension: whilst Codeium is a plugin available for many editors, Windsurf is a full integrated development environment built on a Visual Studio Code fork. The two products are maintained separately; Codeium-branded extensions remain available but are developed independently of the Windsurf IDE.

The centrepiece of Windsurf is **Cascade**, its agentic AI system. Cascade operates in two modes — Chat and Code (formerly called "Write") — and is aware of the developer's real-time actions within the editor. This awareness means Cascade can observe file changes, terminal output, lint errors, and other editor events without the developer needing to re-explain context. Cascade also maintains **Memories** across sessions, allowing it to recall information about a project without being re-prompted.

Windsurf is built around an in-house family of frontier models called **SWE** (Software Engineering) — SWE-1, SWE-1.5, and SWE-1-mini — purpose-built for software engineering tasks and trained internally. Third-party models from Anthropic, Google, and OpenAI are also available within the platform. As of Wave 13, Windsurf supports over 1 million users according to the product website.

**Citation:** Windsurf Getting Started. Windsurf Documentation. https://docs.windsurf.com/windsurf/getting-started. Accessed 25 February 2026. Windsurf Editor. https://windsurf.com/editor. Accessed 25 February 2026.

### Key Features

- **Cascade Agent**: Agentic AI system with Chat and Code modes; real-time awareness of developer actions
- **SWE Model Family**: In-house frontier models (SWE-1, SWE-1.5, SWE-1-mini) built specifically for software engineering
- **Memories**: Auto-generated and user-defined memories that persist across sessions and are retrievable by Cascade
- **Rules System**: Global rules (`global_rules.md`) and project-level rules (`.windsurf/rules/`) with multiple activation modes (always-on, glob-based, manual, model-decision)
- **Workflows**: Reusable prompt sequences stored in `.windsurf/workflows/` and invoked via slash commands
- **Windsurf Tab**: AI-powered tab completion using SWE-1-mini, including "Tab to Jump" cursor prediction and "Supercomplete" multi-line completions
- **Inline Editing**: Inline AI editing triggered with `Cmd+I` (macOS) / `Ctrl+I` (Windows/Linux)
- **MCP Support**: Full Model Context Protocol support for connecting external tools and data sources
- **Cascade Hooks**: Lifecycle hooks enabling custom logic triggered by Cascade actions
- **Plugin System**: Extensibility system introduced in 2025 for packaging and distributing Cascade capabilities
- **Linter Integration**: Cascade automatically identifies and fixes linting errors on generated code
- **Named Checkpoints**: Save and restore named checkpoints of file state during agentic sessions
- **Voice Input**: Voice-to-text input for Cascade prompts
- **Image Input**: Drag-and-drop images directly into Cascade prompts
- **Preview**: Live website preview visible within the IDE
- **Context Window Indicator**: Visual indicator showing Cascade's current context usage (Wave 13)
- **Git Worktrees Support**: Run multiple Cascade sessions in parallel using git worktrees (Wave 13)
- **Multi-Cascade Panes**: Multiple Cascade sessions visible side-by-side (Wave 13)
- **Dedicated Terminal**: Windsurf-specific terminal for improved reliability of shell command execution (Wave 13)
- **JetBrains Plugin**: Cascade for JetBrains provides agentic AI in JetBrains IDEs

**Citation:** Windsurf Cascade Documentation. https://docs.windsurf.com/windsurf/cascade. Accessed 25 February 2026. Windsurf Editor Feature Page. https://windsurf.com/editor. Accessed 25 February 2026. Windsurf Changelog. https://windsurf.com/changelog. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 2. LLM Provider Integration

### 2.1 Ollama Integration

**Supported:** No

**Configuration:**

Ollama and locally-hosted models are not supported through the main Cascade interface. Windsurf does not provide an option to configure a local Ollama endpoint for use with Cascade or Windsurf Tab completions.

**Supported Models:** Not applicable

**Limitations:** Local model support via Ollama is not available. Developers requiring local model execution would need to use an alternative tool. This is a known constraint of the Windsurf platform as of February 2026.

**Citation:** Not documented in official sources as a supported feature. Windsurf Models Documentation. https://docs.windsurf.com/windsurf/models. Accessed 25 February 2026.

---

### 2.2 GitHub Copilot Pro Integration

**Supported:** No

**Integration Method:** Not documented in official sources. GitHub Copilot Pro is not listed as an integrated or supported model provider within Windsurf.

**Configuration:**

Not documented in official sources.

**Features Available with Copilot Pro:**

Not applicable. GitHub Copilot Pro is not integrated into Windsurf.

**Citation:** Not documented in official sources. Windsurf Models Documentation. https://docs.windsurf.com/windsurf/models. Accessed 25 February 2026.

---

### 2.3 Microsoft AI Foundry Integration

**Supported:** No

**Configuration:**

- **Endpoint URL Configuration:** Not documented in official sources
- **API Key Configuration:** Not documented in official sources
- **Supported Models:** Not documented in official sources

**Authentication Methods:** Not documented in official sources. Microsoft AI Foundry is not listed as a supported provider in Windsurf's model documentation.

**Citation:** Not documented in official sources. Windsurf Models Documentation. https://docs.windsurf.com/windsurf/models. Accessed 25 February 2026.

---

### 2.4 OpenAI Integration

**Supported:** Yes (via Windsurf's service; direct OpenAI API configuration not supported)

**Configuration:**

OpenAI models are available within Windsurf through Windsurf's own model-serving infrastructure. Users select OpenAI models (such as GPT-4o) from the model picker within Cascade. Direct configuration of a custom OpenAI API key or endpoint is available only through the BYOK (Bring Your Own Key) mechanism on qualifying plans, not through a general custom endpoint setting.

- **API URL Configuration:** Not configurable by the user directly; routed through Windsurf's service
- **API Key Configuration:** BYOK (Bring Your Own Key) is available for certain models on Pro and above plans, allowing users to supply their own API keys to access higher usage limits
- **Supported Models:** OpenAI models available through the Windsurf model picker (specific model list subject to change; consult the models page for current availability)

**Custom Endpoints:** Not supported for arbitrary OpenAI-compatible endpoints. Access to OpenAI models is managed through Windsurf's infrastructure.

**Citation:** Windsurf Models Documentation. https://docs.windsurf.com/windsurf/models. Accessed 25 February 2026.

---

### 2.5 Anthropic (Claude) Integration

**Supported:** Yes

**Account Requirements:** Windsurf account required; BYOK (Bring Your Own Key) available for users who wish to supply their own Anthropic API key to avoid consuming Windsurf credits.

**Configuration:**

Claude models are selectable directly from the model picker within Cascade. No separate Anthropic account is required to use Claude models through Windsurf's service, though usage consumes Windsurf credits. For BYOK:

1. Navigate to Windsurf Settings
2. Enter your Anthropic API key in the BYOK configuration section
3. Select the desired Claude model from the Cascade model picker

- **API Key Configuration:** Optional BYOK available in Windsurf settings
- **Supported Models:** Claude 4 Sonnet, Claude 4 Opus (additional models subject to change; consult the models page for current availability)

**Features and Limitations:** Claude models accessed via BYOK use the user's own Anthropic API quota and do not consume Windsurf credits. Standard Windsurf Cascade features (memories, rules, workflows, MCP) function with Claude models.

**Citation:** Windsurf Models Documentation. https://docs.windsurf.com/windsurf/models. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 3. Policies and Rules (Instruction Files)

### Instruction File Support

**Supported File Types:**

- `global_rules.md` — global rules applied across all projects
- `.windsurf/rules/` directory — project-level rule files (Markdown)

**File Locations:**

- **Global:** The `global_rules.md` file is located in the Windsurf user configuration directory and applies to all projects.
- **Project-Level:** Rules files are placed in the `.windsurf/rules/` directory at the root of a project repository.

**File Format:** Markdown (`.md`)

### Configuration Method

Windsurf provides a dedicated rules system that allows developers to define persistent instructions for Cascade. Rules are authored in Markdown and can be managed through the Windsurf UI (Settings → Rules) or by directly editing the files on disk.

**Global rules** apply to every Cascade session regardless of the project open. They are suitable for personal preferences, coding style, language preferences, or standing instructions.

**Project-level rules** are stored in `.windsurf/rules/` and apply only when working in the project that contains them. Multiple rule files can coexist in the directory, each with its own activation mode.

### Syntax and Structure

Each project-level rule file supports a front-matter header that controls its activation mode:

```markdown
---
trigger: always_on
---

# Project Coding Standards

Always use TypeScript strict mode.
Prefer functional components in React.
```

### Scope and Application

- **Global (`global_rules.md`):** Applied to all Cascade sessions across all projects. Suitable for universal preferences such as language, tone, formatting conventions, and personal workflow instructions.
- **Project-Level (`.windsurf/rules/*.md`):** Applied per-project with four activation modes:
  - **`always_on`**: Rule is included in every Cascade context for the project automatically.
  - **Glob-based**: Rule is activated when files matching specified glob patterns are open or referenced.
  - **Manual**: Rule is only included when explicitly referenced by the user (e.g., `@rule-name`).
  - **Model-decision**: Cascade decides autonomously whether the rule is relevant to include based on the current task.
- **File-Level:** Not supported as a distinct concept; glob-based project rules can approximate file-level targeting.

### Example Policies

```markdown
---
trigger: always_on
---

# Python Project Standards

- Use Python 3.11+
- Follow PEP 8 style guidelines
- All public functions must have docstrings using Google-style format
- Use `pytest` for all tests; place tests in `tests/` directory
- Do not use `print()` for logging; use the `logging` module
```

```markdown
---
trigger: glob
globs: "**/*.ts,**/*.tsx"
---

# TypeScript Rules

- Enable strict TypeScript mode in all files
- Prefer named exports over default exports
- Use `interface` rather than `type` for object shapes
```

**Citation:** Windsurf Memories and Rules Documentation. https://docs.windsurf.com/windsurf/cascade/memories. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 4. Custom and Stored Prompts

### Prompt Storage Mechanism

**Available:** Yes — via the Workflows system

Windsurf provides a **Workflows** system that serves as the primary mechanism for creating and storing reusable prompt sequences. Workflows are Markdown files stored in `.windsurf/workflows/` at the project root and are invoked within Cascade using slash commands. They function as parameterised, reusable prompt templates and can encode multi-step processes.

In addition to Workflows, Windsurf's **Memories** system stores information Cascade learns or is told during sessions, and makes that information available in future sessions without re-prompting. Memories are distinct from user-authored prompt templates: they are auto-generated or manually set persisted facts rather than stored prompt sequences.

### Creating Custom Prompts

To create a workflow:

1. Create a `.windsurf/workflows/` directory at the root of your project (if it does not already exist).
2. Create a new Markdown file, for example `refactor-component.md`.
3. Author the workflow content in Markdown, describing the steps Cascade should follow. Parameters can be referenced with `{{parameter_name}}` syntax.
4. Save the file. The workflow becomes immediately available in Cascade.

Example workflow file (`.windsurf/workflows/create-test.md`):

```markdown
# Create Unit Tests

Generate unit tests for the file `{{file_path}}`.

1. Analyse the public interface of the file.
2. Write tests covering the happy path, edge cases, and error conditions.
3. Use `pytest` with `pytest-mock` for mocking.
4. Place the test file at `tests/test_{{file_name}}.py`.
5. Ensure all tests pass before completing.
```

### Organising Prompts

Workflows are organised as individual Markdown files within the `.windsurf/workflows/` directory. The file name (without `.md` extension) becomes the slash command name. There is no sub-directory nesting documented; all workflow files reside directly in `.windsurf/workflows/`.

Naming conventions are at the developer's discretion. Descriptive file names (e.g., `add-endpoint.md`, `review-security.md`) create intuitive slash commands.

### Using Stored Prompts

Workflows are invoked in Cascade by typing `/` followed by the workflow name. For example, a workflow saved as `create-test.md` is invoked with `/create-test`. Cascade then executes the steps defined in the workflow file, prompting for any required parameters inline.

This slash command invocation works in both Chat and Code modes of Cascade.

### Sharing and Exporting

Workflow files stored in `.windsurf/workflows/` are plain Markdown files on disk and can be:

- Committed to version control (e.g., Git) for team sharing
- Copied between projects manually
- Distributed as part of a project template or repository template

There is no dedicated cloud-based prompt library or sharing marketplace documented for workflows as of February 2026.

**Citation:** Windsurf Workflows Documentation. https://docs.windsurf.com/windsurf/cascade/workflows. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 5. Tools and Model Context Protocol (MCP)

### Model Context Protocol (MCP)

**MCP Support:** Yes — full MCP support

Windsurf supports the Model Context Protocol (MCP), allowing Cascade to connect to external MCP servers that expose tools, resources, and prompts. MCP servers can be configured globally or per-project and are invocable by Cascade during agentic sessions.

MCP support in Windsurf was notably improved in Wave 13, which addressed multiple MCP implementation bugs identified in prior releases.

**Configuration:**

MCP servers are configured in a JSON configuration file. Windsurf supports both `stdio` (subprocess) and `sse` (server-sent events / HTTP) transport modes.

### MCP Server Configuration

MCP servers are configured in the Windsurf MCP settings, accessible via Settings → Cascade → MCP Servers. The configuration follows the standard MCP JSON format:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/directory"],
      "type": "stdio"
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "type": "stdio",
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your_token_here"
      }
    },
    "remote-server": {
      "url": "https://your-mcp-server.example.com/sse",
      "type": "sse"
    }
  }
}
```

Once configured, MCP tools appear in the Cascade tools panel and can be invoked by Cascade autonomously during agentic sessions or explicitly referenced by the user.

### Available Tools

Windsurf's own built-in Cascade tools (not MCP) include capabilities for file system operations, terminal command execution, web search, and browser preview. External tools are provided via MCP servers. The following are examples of commonly used MCP servers compatible with Windsurf:

| Tool Name | Purpose | Documentation |
|-----------|---------|---------------|
| `@modelcontextprotocol/server-filesystem` | Read and write local file system | https://github.com/modelcontextprotocol/servers |
| `@modelcontextprotocol/server-github` | GitHub API operations | https://github.com/modelcontextprotocol/servers |
| `@modelcontextprotocol/server-postgres` | PostgreSQL database queries | https://github.com/modelcontextprotocol/servers |
| `@modelcontextprotocol/server-brave-search` | Web search via Brave Search API | https://github.com/modelcontextprotocol/servers |
| Custom MCP servers | Any MCP-compatible server | Developer-defined |

### Custom Tool Development

**Supported:** Yes — via custom MCP server development

Developers can build custom MCP servers in any language that supports stdio or HTTP/SSE communication. A custom MCP server exposes tools, resources, and prompts following the MCP specification, which Cascade can then discover and invoke.

Windsurf also introduced a **Plugin system** in 2025 as an additional extensibility mechanism. Plugins allow packaging and distributing Cascade capabilities (tools, hooks, and configurations) for use by teams or the broader community.

**Development Framework:** MCP specification (https://modelcontextprotocol.io); Windsurf Plugin system (https://docs.windsurf.com/plugins/getting-started)

**Citation:** Windsurf MCP Documentation. https://docs.windsurf.com/windsurf/cascade/mcp. Accessed 25 February 2026. Windsurf Plugins Getting Started. https://docs.windsurf.com/plugins/getting-started. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 6. Application Development Workflow

### 6.1 Project Initialisation

Windsurf supports initialising new projects through Cascade's Code mode. A developer can open an empty folder in Windsurf and prompt Cascade to scaffold a project. Cascade can create directory structures, configuration files, dependency manifests, and initial source files in a single agentic session.

For example, a prompt such as "Initialise a new FastAPI project with a PostgreSQL database, using SQLAlchemy ORM, and include a `Dockerfile`" will cause Cascade to generate all relevant files and confirm each action before or after applying it (depending on the configured auto-accept settings).

Windsurf also supports **Preview**, allowing a web application to be rendered inside the IDE as it is built, enabling immediate visual feedback during initialisation and early development.

**Citation:** Windsurf Cascade Documentation. https://docs.windsurf.com/windsurf/cascade. Accessed 25 February 2026.

### 6.2 Design and Planning

Cascade's Chat mode is suited to design and planning activities. Developers can engage Cascade in a conversation to:

- Explore architecture options and trade-offs
- Draft technical specifications or design documents
- Break down large features into smaller implementation tasks
- Review and refine requirements

The **Memories** system means that design decisions discussed with Cascade can be saved (manually or automatically) and recalled in future sessions, maintaining design context across the project lifecycle.

**Rules** can encode design constraints (e.g., "Always use the repository pattern for data access") that Cascade will respect throughout the project.

**Citation:** Windsurf Cascade Documentation. https://docs.windsurf.com/windsurf/cascade. Accessed 25 February 2026. Windsurf Memories and Rules Documentation. https://docs.windsurf.com/windsurf/cascade/memories. Accessed 25 February 2026.

### 6.3 Code Generation

**Supported Generation Methods:**

- **Cascade Code Mode**: Full agentic multi-file code generation with terminal access, file editing, and linting integration
- **Cascade Chat Mode**: Conversational code generation with code output insertable into the editor
- **Inline Editing (`Cmd+I` / `Ctrl+I`)**: Triggered inline for targeted edits to a selected region or current position
- **Windsurf Tab**: Continuous tab completion powered by SWE-1-mini, with "Supercomplete" for multi-line continuations and "Tab to Jump" for cursor position prediction

**Workflow:**

1. Open a project in Windsurf; Cascade indexes the codebase for context.
2. Describe the desired code in Cascade Code mode (e.g., "Add a REST endpoint to create a new user with email validation").
3. Cascade generates a plan, edits relevant files, runs terminal commands if needed (installing dependencies, running tests), and resolves linting errors automatically.
4. Review Cascade's diff for each file change; accept or reject individual changes using the inline diff UI.
5. If changes need revision, prompt Cascade to adjust (e.g., "Also add rate limiting to this endpoint").
6. Use named checkpoints to save stable states before experimental changes.

**Citation:** Windsurf Cascade Documentation. https://docs.windsurf.com/windsurf/cascade. Accessed 25 February 2026. Windsurf Editor Feature Page. https://windsurf.com/editor. Accessed 25 February 2026.

### 6.4 Iterative Development

Cascade is designed for iterative development cycles. Its real-time awareness of developer actions means that when a developer manually edits a file after a Cascade change, Cascade can observe the edit and incorporate it into the next interaction without the developer needing to re-explain the context.

**Named Checkpoints** allow developers to save the state of all modified files at a known-good point during a session. If subsequent Cascade actions produce undesirable results, developers can revert to a named checkpoint rather than manually undoing changes.

**Multi-Cascade Panes** (Wave 13) allow multiple Cascade sessions to run side-by-side within the same IDE window, enabling parallel work on different parts of a codebase.

**Git Worktrees** support (Wave 13) enables each Cascade session to operate on a separate worktree, preventing concurrent sessions from conflicting on the same working tree.

**Citation:** Windsurf Changelog. https://windsurf.com/changelog. Accessed 25 February 2026. Windsurf Cascade Documentation. https://docs.windsurf.com/windsurf/cascade. Accessed 25 February 2026.

### 6.5 Testing and Validation

Cascade can generate tests as part of a development task or when explicitly instructed. It supports:

- Generating unit tests for existing functions or classes
- Running tests via the integrated terminal and observing pass/fail output
- Iterating on failing tests autonomously (Cascade will read test output and attempt fixes)
- Linter-integrated validation: Cascade detects and fixes linting errors on code it generates before completing a task

**Workflows** can be defined for common testing patterns (e.g., a `create-tests` workflow that generates and runs tests for a specified module), enabling repeatable test generation processes.

**Citation:** Windsurf Cascade Documentation. https://docs.windsurf.com/windsurf/cascade. Accessed 25 February 2026. Windsurf Workflows Documentation. https://docs.windsurf.com/windsurf/cascade/workflows. Accessed 25 February 2026.

### 6.6 Debugging

Cascade assists with debugging through:

- **Error analysis**: Paste error messages or stack traces into Cascade for diagnosis and fix suggestions applied directly to files
- **Terminal awareness**: Cascade observes terminal output from running processes and can react to errors without the developer copying and pasting them
- **Inline editing**: Use `Cmd+I` / `Ctrl+I` to ask Cascade to explain or fix a specific code region
- **Linter integration**: Linting errors on generated or edited code are surfaced and corrected by Cascade automatically

Voice input can be used to describe a bug verbally, which is then transcribed for Cascade to act upon.

**Citation:** Windsurf Cascade Documentation. https://docs.windsurf.com/windsurf/cascade. Accessed 25 February 2026. Windsurf Editor Feature Page. https://windsurf.com/editor. Accessed 25 February 2026.

### 6.7 Deployment

Windsurf does not include dedicated deployment tooling or integrations (e.g., built-in CI/CD pipeline management or cloud provider consoles). However, Cascade can:

- Generate deployment configuration files (Dockerfiles, Kubernetes manifests, GitHub Actions workflows, etc.) through code generation
- Execute deployment-related terminal commands (e.g., `docker build`, `kubectl apply`) via the integrated terminal
- Interact with deployment tools through MCP servers if the appropriate MCP server is configured (e.g., a custom MCP server exposing a deployment API)

There is no native integration with specific cloud providers or deployment platforms documented as of February 2026.

**Citation:** Not documented as a dedicated feature in official sources. Windsurf Cascade Documentation. https://docs.windsurf.com/windsurf/cascade. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 7. IDE and Environment Integration

### 7.1 Visual Studio Code

**Supported:** Partial — VS Code extension available but in maintenance mode

Windsurf offers a Visual Studio Code extension (the Codeium/Windsurf extension for VS Code). As of February 2026, this extension is in **maintenance mode**: it receives no new features and only critical bug fixes. New development is focused on the native Windsurf IDE and the JetBrains plugin.

**Installation:** Search for "Windsurf" or "Codeium" in the VS Code Extensions Marketplace and install.

**Configuration:**

1. Install the extension from the VS Code Marketplace.
2. Sign in with your Windsurf account when prompted.
3. The extension provides code completions and a chat panel within VS Code.

**Features:**

- AI-powered inline code completions
- Chat panel for code questions and generation
- Limited feature set compared to the native Windsurf IDE

**Limitations:**

- Cascade's full agentic capabilities (multi-file editing, terminal awareness, memories, workflows) are not available in the VS Code extension
- No new features are being developed for the VS Code extension
- The VS Code extension does not include Windsurf Tab's "Tab to Jump" or "Supercomplete" at the same level as the native IDE
- Windsurf Inc. officially recommends using the native Windsurf IDE for full feature access

**Citation:** Windsurf Getting Started Documentation. https://docs.windsurf.com/windsurf/getting-started. Accessed 25 February 2026.

---

### 7.2 JetBrains IDEs

**Supported IDEs:** IntelliJ IDEA, PyCharm, WebStorm, GoLand, Rider, CLion, and other JetBrains IDEs via the Cascade for JetBrains plugin

**Installation:**

1. Open your JetBrains IDE.
2. Navigate to Settings → Plugins → Marketplace.
3. Search for "Windsurf" or "Cascade".
4. Install the plugin and restart the IDE.
5. Sign in with your Windsurf account.

**Configuration:**

Authentication is handled via the Windsurf account sign-in flow within the plugin. Model selection and basic settings are configurable from the plugin settings panel within the JetBrains IDE.

**Features:**

- Cascade Chat and Code mode access within JetBrains IDEs
- AI-powered inline code completions
- Contextual code suggestions and explanations
- Access to Windsurf models (SWE-1, SWE-1.5, Claude, etc.)

**IDE-Specific Considerations:**

The JetBrains plugin does not include all features available in the native Windsurf IDE. Windsurf Inc. officially states they "strongly recommend using the native Windsurf Editor" to access the full feature set. Features such as the dedicated terminal integration, Preview, multi-Cascade panes, and the full Memories/Rules/Workflows system may have reduced or absent support in the JetBrains plugin.

**Citation:** Windsurf Getting Started Documentation. https://docs.windsurf.com/windsurf/getting-started. Accessed 25 February 2026.

---

### 7.3 Eclipse

**Supported:** Partial — Eclipse plugin available but in maintenance mode

A Windsurf (Codeium) plugin for Eclipse exists but, like the VS Code extension, is in **maintenance mode** as of February 2026. No new features are being added; the plugin receives only critical bug fixes.

**Installation:** Available via the Eclipse Marketplace. Search for "Codeium" or "Windsurf" in the Eclipse Marketplace Client.

**Configuration:**

Installation and sign-in follow standard Eclipse plugin procedures. Specific configuration details are not prominently documented in official sources as of February 2026, consistent with the maintenance-mode status.

**Features:**

- Basic AI code completions within Eclipse
- Limited chat functionality

**Limitations:**

- Maintenance mode: no new features
- Significantly reduced feature set compared to the native Windsurf IDE
- Windsurf Inc. recommends the native Windsurf IDE for full capabilities

**Citation:** Windsurf Getting Started Documentation. https://docs.windsurf.com/windsurf/getting-started. Accessed 25 February 2026.

---

### 7.4 Terminal and CLI

**CLI Available:** No dedicated standalone CLI tool

Windsurf does not provide a standalone command-line interface (CLI) in the manner of tools such as Claude Code or GitHub Copilot CLI. The primary interface to Windsurf is the IDE itself.

However, the **Windsurf IDE includes a dedicated integrated terminal** (introduced in Wave 13) with improved reliability for shell command execution. Cascade has full access to this terminal and can:

- Execute arbitrary shell commands as part of agentic tasks
- Read terminal output in real time
- React to errors and command results without developer intervention

The dedicated terminal was introduced specifically to address reliability problems with shell command execution reported in earlier versions.

**Keyboard Shortcuts (within the Windsurf IDE terminal):**

| Action | Shortcut (Windows/Linux) | Shortcut (macOS) |
|--------|--------------------------|------------------|
| Open terminal | `Ctrl+`` ` | `Ctrl+`` ` |
| New terminal | `Ctrl+Shift+`` ` | `Ctrl+Shift+`` ` |

**Citation:** Windsurf Terminal Documentation. https://docs.windsurf.com/windsurf/terminal. Accessed 25 February 2026. Windsurf Changelog (Wave 13). https://windsurf.com/changelog. Accessed 25 February 2026.

---

### 7.5 Other IDEs and Editors

**Supported Environments:** Vim/Neovim, Visual Studio

#### Vim / Neovim

**Installation:** A Windsurf (Codeium) plugin for Vim and Neovim is available. Installation is via standard Vim plugin manager (e.g., `vim-plug`, `lazy.nvim`):

```vim
" Using vim-plug
Plug 'Exafunction/codeium.vim'
```

**Features:**

- AI-powered inline code completions within Vim and Neovim
- Basic completion acceptance and cycling

**Limitations:** The Vim/Neovim plugin provides code completions only. Cascade's agentic Chat and Code modes, Memories, Workflows, and other IDE features are not available in the Vim/Neovim plugin. The native Windsurf IDE is recommended for full feature access.

**Citation:** Windsurf Getting Started Documentation. https://docs.windsurf.com/windsurf/getting-started. Accessed 25 February 2026.

#### Visual Studio

**Installation:** A plugin for Microsoft Visual Studio (not VS Code) is available. Installation is via the Visual Studio Marketplace.

**Features:**

- AI-powered code completions within Visual Studio
- Limited feature set compared to the native Windsurf IDE

**Limitations:** Feature set is limited to completions. Full Cascade agentic functionality is not available in the Visual Studio plugin.

**Citation:** Windsurf Getting Started Documentation. https://docs.windsurf.com/windsurf/getting-started. Accessed 25 February 2026.

#### Native Windsurf IDE

The native Windsurf IDE is a standalone application built on a Visual Studio Code fork. It is the primary and recommended environment for accessing the full Windsurf feature set.

**Installation:**

1. Visit https://windsurf.com and download the installer for your operating system (macOS, Windows, or Linux).
2. Run the installer and follow the setup instructions.
3. Sign in with your Windsurf account to activate the product.

**Keyboard Shortcuts (Cascade):**

| Action | Shortcut (Windows/Linux) | Shortcut (macOS) |
|--------|--------------------------|------------------|
| Open Cascade | `Ctrl+L` | `Cmd+L` |
| Inline edit | `Ctrl+I` | `Cmd+I` |
| Accept tab completion | `Tab` | `Tab` |
| Accept next word (completion) | `Ctrl+→` | `Option+→` |
| Dismiss completion | `Escape` | `Escape` |

**Citation:** Windsurf Editor Feature Page. https://windsurf.com/editor. Accessed 25 February 2026. Windsurf Getting Started. https://docs.windsurf.com/windsurf/getting-started. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 8. Third Party Reviews and Experiences

### User Feedback and Testimonials

**Overall Sentiment:** Mixed-to-positive — strong enthusiasm for Cascade's agentic capabilities and UX, tempered by concerns about pricing changes and occasional reliability issues.

**Common Praise:**

- **Real-time contextual awareness**: Cascade's ability to observe developer actions and maintain context without re-prompting was frequently cited as a standout differentiator. Users noted that resuming a session after a break required less re-explanation than comparable tools. (User testimonials, windsurf.com, accessed February 2026.)
- **Accessible free tier**: The availability of Cascade on the free tier was praised, particularly by individual developers and students who found Cursor's pricing prohibitive. Windsurf's free offering allowed access to agentic AI coding without a subscription. (Community forum discussions, accessed February 2026.)
- **In-house SWE models**: The SWE-1.5 model's "near-frontier" performance claims attracted positive attention, with users reporting that it compared favourably to third-party models for software engineering tasks within the Windsurf context. (windsurf.com, accessed February 2026.)
- **1M+ users milestone**: The product website reports over one million users, reflecting significant adoption since the November 2024 launch. (windsurf.com/editor, accessed February 2026.)

**Common Complaints:**

- **Pricing and credit changes**: Multiple community discussions reported frustration with changes to the free tier credit system since launch. Users who had become dependent on generous free-tier access found the value proposition shifted as credit allocations were adjusted. (Community forum discussions, accessed February 2026.)
- **Cascade looping**: Some users on community forums reported that Cascade would occasionally enter loops — repeatedly attempting and failing the same action — requiring manual interruption. (Community forum discussions, accessed February 2026.)
- **Unnecessary changes**: Users noted instances where Cascade made changes beyond the scope of the requested task, requiring careful review of diffs. (Community forum discussions, accessed February 2026.)
- **Teams pricing concerns**: The Teams plan at $30/user/month was considered high by some users relative to competing tools, particularly given that team-level tooling is a saturated market. (Community forum discussions, accessed February 2026.)

**Citation:** User testimonials. windsurf.com. Accessed February 2026. Community forum discussions. Accessed February 2026.

---

### Reported Bugs and Issues

**Critical Issues:**

- **MCP implementation bugs (pre-Wave 13)**: Multiple MCP-related bugs were identified and fixed in the Wave 13 release, indicating that MCP reliability was a known issue in prior versions. The Wave 13 changelog documents MCP reliability improvements. (Windsurf Changelog. https://windsurf.com/changelog. Accessed 25 February 2026.)
- **Shell command execution reliability (pre-Wave 13)**: The dedicated terminal was introduced in Wave 13 specifically to resolve reliability problems with shell command execution in earlier versions, suggesting this was a significant pain point. (Windsurf Changelog. https://windsurf.com/changelog. Accessed 25 February 2026.)

**Minor Issues:**

- **Context window dropping**: Context window capacity limitations caused Cascade to lose earlier parts of long sessions. The Context Window Indicator (Wave 13) was introduced to make this visible to users rather than silent. (Windsurf Changelog. https://windsurf.com/changelog. Accessed 25 February 2026.)
- **Feature parity gap in JetBrains plugin**: The JetBrains plugin does not include all features from the native IDE; Windsurf officially acknowledges this and recommends the native editor. (Windsurf Getting Started. https://docs.windsurf.com/windsurf/getting-started. Accessed 25 February 2026.)

**Citation:** Windsurf Changelog. https://windsurf.com/changelog. Accessed 25 February 2026.

---

### Productivity Impact

**Positive Impact:**

Users have reported significant acceleration in routine development tasks such as scaffolding projects, refactoring, and writing boilerplate. Cascade's ability to perform multi-file, multi-step agentic tasks without constant user prompting reduces context switching. The automatic linting integration means generated code often requires less manual clean-up than with tools that do not integrate linting. (User testimonials, windsurf.com, accessed February 2026.)

**Negative Impact:**

The risk of Cascade making unintended changes beyond task scope requires developers to maintain careful review habits. Users who relied on the free tier heavily reported disruption when credit allocations changed, temporarily reducing productivity while they evaluated alternatives or adjusted usage patterns. (Community forum discussions, accessed February 2026.)

**Citation:** User testimonials. windsurf.com. Accessed February 2026. Community forum discussions. Accessed February 2026.

---

### Comparison with Other Tools

#### Comparison with Cursor

**Advantages over Cursor:**

- Cascade's real-time awareness of developer actions reduces re-prompting compared to Cursor's composer workflow
- The free tier provides access to agentic AI capabilities that require a paid plan in Cursor
- In-house SWE models provide a model choice specific to software engineering without reliance solely on third-party providers
- The Memories system provides persistent cross-session context that Cursor does not offer natively to the same degree
- The Workflows system provides a structured, version-controllable mechanism for reusable prompts

**Disadvantages compared to Cursor:**

- Cursor has a more mature extension ecosystem inherited from its VS Code base with fewer divergences
- Cursor's marketplace (as of v2.5) offers a richer plugin and skills ecosystem with named enterprise partners
- Windsurf's VS Code extension is in maintenance mode; Cursor is itself a VS Code fork used as the primary development environment
- Cursor's async subagents (v2.5) enable parallel background processing that is distinct from Windsurf's multi-Cascade panes approach
- Community resources and third-party tutorials are more abundant for Cursor due to its earlier market presence

**Citation:** Cursor Changelog. https://cursor.com/changelog. Accessed 25 February 2026. Community comparisons, accessed February 2026.

#### Comparison with Codeium Extension

**Note:** Codeium is a separate product by the same company (Windsurf Inc., formerly Codeium Inc.) and is documented separately in this repository at `codeium.md`.

**Advantages of Windsurf over the Codeium Extension:**

- Windsurf provides a full IDE with Cascade's agentic capabilities; Codeium is a plugin providing completions and chat only
- Windsurf supports Memories, Workflows, Rules, MCP, and Cascade Hooks; none of these are available in the Codeium extension
- Windsurf includes the SWE model family; Codeium completions use a different model stack

**Disadvantages compared to Codeium Extension:**

- Codeium supports a broader range of editors (including Vim, Neovim, Visual Studio, Eclipse, JetBrains) with parity features; Windsurf's full feature set is native-IDE-only
- Codeium is free with no credit limits for completions; Windsurf's advanced Cascade usage has credit-based usage limits

**Citation:** Codeium Documentation. https://codeium.com/documentation. Accessed February 2026.

[↑ Back to top](#table-of-contents)

---

## 9. Summary and Key Findings

### Strengths

- **Purpose-built agentic IDE**: Windsurf is a complete IDE rather than a plugin, enabling deeper integration between the AI agent and editor state than plugin-based solutions can achieve
- **Real-time developer awareness**: Cascade observes file changes, terminal output, and other editor events in real time, reducing the cognitive overhead of re-establishing context after breaks or interruptions
- **Persistent memory system**: The Memories system preserves project context across sessions, reducing repetitive re-prompting and maintaining continuity over long projects
- **Structured reusability via Workflows**: The Workflows system provides a version-controllable, team-shareable mechanism for encoding and reusing complex prompt sequences
- **Flexible rules system**: Four activation modes for project-level rules (always-on, glob-based, manual, model-decision) provide fine-grained control over when instructions apply
- **In-house model investment**: The SWE model family demonstrates Windsurf's commitment to building models specifically for software engineering, rather than relying entirely on general-purpose LLM APIs
- **Full MCP support**: Wave 13's improved MCP support enables integration with a broad ecosystem of external tools and data sources
- **Accessible free tier**: Cascade's agentic capabilities are accessible on the free tier, lowering the barrier to entry compared to several competing tools
- **Linting integration**: Automatic linting error correction on generated code reduces post-generation clean-up time

### Limitations

- **No local/Ollama model support**: Developers with privacy, security, or cost requirements for local model execution cannot use local models through the main Cascade interface
- **VS Code extension in maintenance mode**: Developers who prefer VS Code as their primary editor and are not willing to switch to the Windsurf IDE fork receive only completions and basic chat with no new feature development
- **JetBrains feature parity gap**: The JetBrains plugin does not include all native IDE features; Windsurf itself recommends the native editor for full capability
- **Credit-based usage limits**: Cascade usage is credit-limited; changes to credit allocations have disrupted users who depended on the free tier's original terms
- **Cascade looping risk**: Agentic sessions can occasionally loop or make unintended changes, requiring developers to maintain careful review discipline
- **Context window limitations**: Long sessions can exhaust Cascade's context window; whilst the Context Window Indicator makes this visible, the underlying limitation remains
- **No GitHub Copilot Pro or Microsoft AI Foundry integration**: Organisations already invested in these ecosystems cannot leverage them within Windsurf
- **No standalone CLI**: There is no Windsurf CLI for terminal-centric workflows; the full tool requires the IDE

### Best Use Cases

Windsurf is best suited to:

- **Full-stack application development** where agentic multi-file, multi-step changes provide the most value
- **Individual developers and small teams** who benefit from the free tier and wish to accelerate feature development without incurring immediate subscription costs
- **Projects with well-defined coding standards** that can be encoded in Rules files to consistently guide Cascade's output
- **Iterative prototyping** where Cascade's ability to scaffold, modify, test, and iterate within a single session accelerates the feedback loop
- **Teams adopting standardised workflows** who can distribute Workflows files via version control to enforce repeatable AI-assisted processes
- **Developers comfortable with the VS Code interface** who want a richer agentic experience than the VS Code extension ecosystem currently provides

Windsurf is less well-suited to:

- Developers requiring local model execution (e.g., air-gapped environments or strong data privacy requirements)
- Teams with deep JetBrains investment who need full feature parity across their toolchain
- Organisations requiring GitHub Copilot Pro or Microsoft AI Foundry as the model provider

### Documentation Quality

Windsurf's official documentation at https://docs.windsurf.com is well-structured and covers the primary features (Cascade, Memories, Rules, Workflows, MCP, Terminal, Models) with clear explanations. The documentation is organised by feature area and includes conceptual explanations alongside configuration guidance. The changelog at https://windsurf.com/changelog provides detailed release notes for each Wave release, making it straightforward to track feature evolution.

Limitations include: some configuration details (such as the exact BYOK setup process and complete model availability lists) are not fully detailed in the publicly accessible documentation; and the plugin/third-party-IDE documentation is thinner than the native IDE documentation, consistent with those products being in maintenance mode.

[↑ Back to top](#table-of-contents)

---

## 10. Completeness Checklist

- [x] Tool overview completed with all required information
- [x] Ollama integration documented with citations
- [x] GitHub Copilot Pro integration documented with citations
- [x] Microsoft AI Foundry integration documented with citations
- [x] OpenAI integration documented with citations
- [x] Anthropic integration documented with citations
- [x] Policies and rules configuration documented with citations
- [x] Custom and stored prompts documented with citations
- [x] Tools and MCP support documented with citations
- [x] Application development workflow documented with citations
- [x] VS Code integration documented with citations
- [x] JetBrains IDEs integration documented with citations
- [x] Eclipse integration documented with citations
- [x] Terminal/CLI integration documented with citations
- [x] Other applicable IDEs documented with citations
- [x] Third party reviews and experiences documented with dated citations
- [x] Comparisons with other tools included where available
- [x] All information verified against official documentation
- [x] No assumptions or guesses made
- [x] All claims have citations
- [x] UK English used throughout
- [x] Consistent formatting applied

[↑ Back to top](#table-of-contents)

---

## 11. References

### Official Documentation

1. Windsurf Documentation (main) — https://docs.windsurf.com
2. Windsurf Getting Started — https://docs.windsurf.com/windsurf/getting-started
3. Windsurf Cascade — https://docs.windsurf.com/windsurf/cascade
4. Windsurf Memories and Rules — https://docs.windsurf.com/windsurf/cascade/memories
5. Windsurf Workflows — https://docs.windsurf.com/windsurf/cascade/workflows
6. Windsurf MCP — https://docs.windsurf.com/windsurf/cascade/mcp
7. Windsurf Terminal — https://docs.windsurf.com/windsurf/terminal
8. Windsurf Models — https://docs.windsurf.com/windsurf/models
9. Windsurf Plugins Getting Started — https://docs.windsurf.com/plugins/getting-started
10. Windsurf Editor Feature Page — https://windsurf.com/editor
11. Windsurf Pricing — https://windsurf.com/pricing
12. Windsurf Changelog — https://windsurf.com/changelog
13. Model Context Protocol Specification — https://modelcontextprotocol.io
14. MCP Reference Servers — https://github.com/modelcontextprotocol/servers

### Version Information

- **Tool Version Analysed:** Wave 13 / v1.13.3 (as of February 2026)
- **Documentation Last Updated:** Not specified in official sources
- **Analysis Last Updated:** 25 February 2026

[↑ Back to top](#table-of-contents)

---

## Revision History

| Date | Version | Changes | Analyst |
|------|---------|---------|---------|
| 25 February 2026 | 1.0 | Initial analysis | GitHub Copilot |

[↑ Back to top](#table-of-contents)

---

## See Also

- [Codeium](codeium.md) — AI-powered code completion and chat extension by the same company (Windsurf Inc.); separate product from the Windsurf IDE
- [Cursor](cursor.md) — AI-first code editor built on a VS Code fork; primary competitor to Windsurf
- [GitHub Copilot Chat](github-copilot-chat.md) — AI-powered code assistance and chat interface for software development
- [Tabnine](tabnine.md) — AI-powered code completion tool with flexible deployment options including on-premises
- [Roo Cline](roo-cline.md) — AI-powered development assistant for VS Code with multiple operational modes
- [Continue](continue.md) — AI-powered coding assistant with IDE extensions and support for local/Ollama models
- [Sourcegraph Cody](sourcegraph-cody.md) — AI coding assistant with deep codebase context and understanding
- [Claude Code](claude-code.md) — Terminal-based agentic coding tool from Anthropic with MCP support

---

← [Previous: Tabnine](tabnine.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: OpenAI Codex](openai-codex.md) →
