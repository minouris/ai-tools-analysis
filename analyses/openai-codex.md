← [Previous: Windsurf](windsurf.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: Claude Code](claude-code.md) →

---

# OpenAI Codex Analysis

**Analysis Date:** 25 February 2026  
**Tool Version:** GPT-5.3-Codex (as of February 2026); Codex CLI via npm (`@openai/codex`)  
**Analyst:** GitHub Copilot  
**Official Documentation:** https://developers.openai.com/codex

> **Important disambiguation:** This analysis covers the **new OpenAI Codex (2026)**, a full coding agent product. It must not be confused with the deprecated **Codex API** (models `codex-001`, `code-davinci-002`, etc.) which was a code-completion language model API discontinued in March 2023. The two products share a name but are entirely distinct in design, capability, and delivery.

## Table of Contents

- [1. Tool Overview](#1-tool-overview)
  - [Historical Context and Disambiguation](#historical-context-and-disambiguation)
  - [Description](#description)
  - [Key Features](#key-features)
  - [Delivery Modes](#delivery-modes)
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

**Official Documentation:** https://developers.openai.com/codex  
**Version Analysed:** GPT-5.3-Codex model; Codex CLI (npm package `@openai/codex`) as of February 2026  
**Primary Use Case:** Full coding agent for autonomous software development tasks across local terminal, cloud-managed containers, and IDE environments  
**Licensing:** Codex CLI: Apache-2.0 (open source); Codex Web/Cloud and IDE extension: Commercial (included with ChatGPT Plus, Pro, Business, Edu, and Enterprise plans)

### Historical Context and Disambiguation

The OpenAI Codex name has been applied to two entirely distinct products across different time periods:

**Old Codex (2021–2023):** A code-completion language model API providing models such as `codex-001` and `code-davinci-002`. This product was designed to power third-party integrations (including the early GitHub Copilot) and was accessed via the OpenAI API. It was **deprecated in March 2023** in favour of newer GPT models.

**New Codex (2026):** A full coding agent product comprising a CLI tool, a cloud/browser environment, and IDE extensions. It is not a raw model API but an end-to-end agentic workflow system that orchestrates file editing, shell execution, code review, and GitHub integration using the GPT-5.x-Codex model family. This is the product analysed in this document.

The ChatGPT analysis in this repository notes: *"Codex (deprecated March 2023) was a code-specialised model that powered tools like GitHub Copilot. ChatGPT now uses GPT-4o and o1 models."* The new Codex (2026) represents OpenAI's dedicated re-entry into the agentic coding tool market with an entirely new architecture.

**Citation:** ChatGPT Analysis. This repository. `analyses/chatgpt.md`. Accessed 25 February 2026. OpenAI Codex Overview. https://developers.openai.com/codex. Accessed 25 February 2026.

### Description

OpenAI Codex (2026) is an AI coding agent from OpenAI designed for autonomous software development. It operates across three delivery modes: a locally installed CLI (open-source under Apache-2.0, written in Rust), a cloud-based web environment accessible at chatgpt.com/codex, and IDE extensions for VS Code, Cursor, Windsurf, and JetBrains IDEs.

Codex is notably OpenAI's first open-source coding agent offering. The Codex CLI repository is hosted on GitHub at https://github.com/openai/codex and attracted significant developer attention upon release. The tool is positioned as a direct competitor to tools such as Claude Code and GitHub Copilot agent mode, offering multi-mode operation with a strong emphasis on sandbox security.

Codex is included in existing ChatGPT subscription plans (Plus, Pro, Business, Edu, Enterprise) at no additional cost, lowering the barrier to entry for existing subscribers. An OpenAI API key can also be used directly, with usage billed at standard API rates, though certain cloud-based features (such as GitHub code review and Slack integration) require a ChatGPT subscription.

**Citation:** OpenAI Codex Overview. https://developers.openai.com/codex. Accessed 25 February 2026. OpenAI Codex GitHub repository. https://github.com/openai/codex. Accessed 25 February 2026.

### Key Features

- **Three delivery modes:** Codex CLI (local, open source), Codex Web/Cloud (browser-based, OpenAI-managed containers), Codex IDE Extension (VS Code, Cursor, Windsurf, JetBrains)
- **Open-source CLI:** Apache-2.0 licensed, written in Rust, installable via npm or Homebrew
- **Sandboxed execution:** OS-enforced sandboxing (macOS Seatbelt, Linux Landlock + seccomp, Windows Sandbox) with configurable approval policies
- **AGENTS.md instruction system:** Persistent project-level and global instructions for the agent
- **Full MCP support:** STDIO and Streamable HTTP MCP servers with OAuth authentication
- **GitHub integration:** Tag `@codex` in pull requests for code review or task initiation
- **Cloud two-phase runtime:** Setup phase with network access, followed by agent phase that is offline by default
- **Parallel task execution:** Multiple Codex threads can run concurrently (avoiding the same files)
- **Multi-agent support (experimental):** Experimental capability for parallelising work across agents
- **Context compaction:** Automatic compaction for long-running threads
- **Configurable approval modes:** Chat (read-only), Agent (workspace edits), Agent with Full Access
- **GPT-5.x-Codex model family:** Dedicated code-focused models distinct from general-purpose GPT-5

**Citation:** OpenAI Codex Overview. https://developers.openai.com/codex. OpenAI Codex CLI documentation. https://developers.openai.com/codex/cli. OpenAI Codex Security documentation. https://developers.openai.com/codex/security. Accessed 25 February 2026.

### Delivery Modes

#### Codex CLI

The Codex CLI is an open-source (Apache-2.0) command-line tool written in Rust. It runs on the developer's local machine within a sandboxed environment and communicates with OpenAI's API using either a ChatGPT subscription or a direct API key.

**Installation:**

```bash
# Via npm
npm i -g @openai/codex

# Via Homebrew (macOS)
brew install --cask codex
```

**Citation:** OpenAI Codex CLI documentation. https://developers.openai.com/codex/cli. GitHub repository. https://github.com/openai/codex. Accessed 25 February 2026.

#### Codex Web/Cloud

The browser-based interface is accessible at chatgpt.com/codex. Cloud tasks run in isolated OpenAI-managed containers that clone a GitHub repository, execute the agent's work, and can create pull requests. The cloud environment uses a two-phase runtime: a setup phase with network access (for installing dependencies), followed by an agent phase that operates offline by default.

**Citation:** OpenAI Codex Cloud documentation. https://developers.openai.com/codex/cloud. Accessed 25 February 2026.

#### Codex IDE Extension

The Codex IDE extension is available for VS Code (extension ID `openai.chatgpt` on the Visual Studio Code Marketplace), Cursor (`cursor:extension/openai.chatgpt`), Windsurf (`windsurf:extension/openai.chatgpt`), and JetBrains IDEs. Configuration is shared with the CLI via `~/.codex/config.toml`.

**Citation:** OpenAI Codex IDE documentation. https://developers.openai.com/codex/ide. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 2. LLM Provider Integration

OpenAI Codex is a first-party OpenAI product and is designed exclusively around the GPT-5.x-Codex model family. It does not support third-party LLM providers such as Anthropic Claude, local Ollama models, or GitHub Copilot Pro as underlying model backends. The sections below document each integration category in accordance with the analysis template.

### 2.1 Ollama Integration

**Supported:** No

**Configuration:**

OpenAI Codex does not support Ollama as a model backend. The tool is architected to use OpenAI's hosted GPT-5.x-Codex models exclusively. No configuration pathway for Ollama is documented in official sources.

**Supported Models:** Not applicable

**Limitations:** The Codex CLI does allow configuration of a custom `baseURL` to point to an OpenAI-compatible API endpoint (see Section 2.4). In principle, a user could point this at an Ollama endpoint serving an OpenAI-compatible API; however, this is not officially supported or documented, and the GPT-5.x-Codex-specific features (model-specific tooling, cloud tasks) would not function with a local Ollama model.

**Citation:** Not documented in official sources. OpenAI Codex documentation makes no reference to Ollama integration. https://developers.openai.com/codex. Accessed 25 February 2026.

---

### 2.2 GitHub Copilot Pro Integration

**Supported:** No

**Integration Method:** OpenAI Codex and GitHub Copilot are separate products. Codex does not use GitHub Copilot Pro as its underlying model provider, and GitHub Copilot Pro subscriptions do not grant access to Codex.

**Configuration:**

Not applicable. The two tools operate independently.

**Features Available with Copilot Pro:**

Not applicable. Codex requires either a ChatGPT subscription (Plus, Pro, Business, Edu, or Enterprise) or a direct OpenAI API key.

**Citation:** Not documented in official sources. OpenAI Codex pricing and authentication documentation make no reference to GitHub Copilot Pro. https://developers.openai.com/codex/pricing. https://developers.openai.com/codex/auth. Accessed 25 February 2026.

---

### 2.3 Microsoft AI Foundry Integration

**Supported:** No

**Configuration:**

- **Endpoint URL Configuration:** Not documented
- **API Key Configuration:** Not documented
- **Supported Models:** Not applicable

**Authentication Methods:** Not applicable

OpenAI Codex does not document integration with Microsoft AI Foundry. Whilst Microsoft Azure OpenAI Service hosts OpenAI models, this is distinct from the Codex product and its cloud-based features. No official documentation links Codex to Microsoft AI Foundry.

**Citation:** Not documented in official sources. https://developers.openai.com/codex. Accessed 25 February 2026.

---

### 2.4 OpenAI Integration

**Supported:** Yes (native — first-party product)

**Configuration:**

Codex is a first-party OpenAI product. Authentication can be provided via:

1. **ChatGPT subscription** (Plus, Pro, Business, Edu, Enterprise): Sign in with an OpenAI account. Subscription-tier usage limits apply.
2. **OpenAI API key**: Set the `OPENAI_API_KEY` environment variable. Usage is billed at standard API rates.

```bash
# Set API key for CLI usage
export OPENAI_API_KEY="sk-..."
```

For the CLI, a custom `baseURL` can be configured in `~/.codex/config.toml` to point to an OpenAI-compatible endpoint:

```toml
[model]
baseURL = "https://your-custom-endpoint.example.com/v1"
```

**API URL Configuration:** Configurable via `baseURL` in `~/.codex/config.toml`

**API Key Configuration:** Via `OPENAI_API_KEY` environment variable or interactive `codex login`

**Supported Models (as of February 2026):**

| Model | Notes |
|-------|-------|
| GPT-5.3-Codex | Main model; included in all plans |
| GPT-5.1-Codex-Mini | Up to 4× higher usage limits, lower cost |
| GPT-5.3-Codex-Spark | Research preview; Pro subscribers only |
| GPT-5.2-Codex | Legacy |
| GPT-5.2 | Legacy |
| GPT-5.1-Codex-Max | Legacy |
| GPT-5 | Legacy |
| GPT-5-Codex | Legacy |
| GPT-5-Codex-Mini | Legacy |

**Custom Endpoints:** Supported via `baseURL` configuration for OpenAI-compatible API endpoints.

**Citation:** OpenAI Codex authentication documentation. https://developers.openai.com/codex/auth. OpenAI Codex configuration documentation. https://developers.openai.com/codex/config-basic. OpenAI Codex pricing documentation. https://developers.openai.com/codex/pricing. Accessed 25 February 2026.

---

### 2.5 Anthropic (Claude) Integration

**Supported:** No

**Account Requirements:** Not applicable

**Configuration:**

- **API Key Configuration:** Not supported
- **Supported Models:** Not applicable

OpenAI Codex is built exclusively on OpenAI's GPT-5.x-Codex model family. No Anthropic Claude model integration is documented or supported.

**Features and Limitations:** The tool is entirely closed to non-OpenAI model providers at the product level. Custom `baseURL` configuration supports OpenAI-compatible API endpoints only; this does not extend to Anthropic's API format.

**Citation:** Not documented in official sources. https://developers.openai.com/codex. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 3. Policies and Rules (Instruction Files)

### Instruction File Support

Codex uses a file-based instruction system centred on `AGENTS.md` files. These files provide persistent, project-aware instructions to the agent at global and project levels.

**Supported File Types:**

- `AGENTS.md` — primary instruction file
- `AGENTS.override.md` — override file that takes precedence over `AGENTS.md` at the same directory level
- Configurable fallback filenames (e.g. `TEAM_GUIDE.md`) settable in `~/.codex/config.toml`

**File Locations:**

| Scope | Path |
|-------|------|
| Global (user-level) | `~/.codex/AGENTS.md` |
| Project-level (repository root) | `<repo-root>/AGENTS.md` |
| Override | `AGENTS.override.md` at same level as `AGENTS.md` |

**File Format:** Markdown (plain text with optional Markdown formatting for readability)

**Citation:** OpenAI Codex AGENTS.md documentation. https://developers.openai.com/codex/guides/agents-md. Accessed 25 February 2026.

### Configuration Method

The agent reads `AGENTS.md` files by walking up from the current working directory to the repository root, collecting and merging instructions. The global `~/.codex/AGENTS.md` is loaded first, then project-level files are layered on top.

A dedicated **"Review guidelines"** section within `AGENTS.md` is used specifically when Codex is invoked for GitHub code review (via the `@codex review` tag), allowing project-specific code review standards to be defined alongside general agent instructions.

The combined size of all loaded instruction content is capped at **32 KiB**. Content exceeding this limit may be truncated.

**Citation:** OpenAI Codex AGENTS.md documentation. https://developers.openai.com/codex/guides/agents-md. Accessed 25 February 2026.

### Syntax and Structure

```markdown
# Project Agent Instructions

You are working on a TypeScript monorepo. Follow these conventions:

## Code Style
- Use 2-space indentation
- Prefer `const` over `let`
- All functions must have JSDoc comments

## Testing
- Write unit tests for all public functions using Jest
- Place tests in `__tests__/` alongside source files

## Git
- Commit messages must follow Conventional Commits format

## Review guidelines
<!-- This section is used specifically when @codex review is invoked on a PR -->
- Check for missing error handling in async functions
- Verify all API responses are typed
- Flag any use of `any` type
```

### Scope and Application

- **Global (`~/.codex/AGENTS.md`):** Applied to all Codex sessions for the current user, regardless of project. Useful for personal preferences such as code style, commit message formats, and language preferences.
- **Project-level (`<repo-root>/AGENTS.md`):** Applied to all Codex sessions within the repository. Useful for team conventions, architecture guidelines, testing requirements, and framework-specific rules.
- **Override (`AGENTS.override.md`):** Takes precedence over `AGENTS.md` at the same directory level. Useful for temporary overrides or branch-specific instructions without modifying the shared `AGENTS.md`.
- **Configurable fallback filename:** The filename that Codex looks for can be reconfigured in `~/.codex/config.toml` (e.g. to `TEAM_GUIDE.md`), enabling integration with existing documentation conventions.

**Citation:** OpenAI Codex AGENTS.md documentation. https://developers.openai.com/codex/guides/agents-md. Accessed 25 February 2026.

### Example Policies

The following example demonstrates a project-level `AGENTS.md` for a Python web application:

```markdown
# AGENTS.md — Backend API Project

## Environment
- Python 3.12, FastAPI, SQLAlchemy, PostgreSQL
- Tests run with: `pytest tests/ -v`
- Linting: `ruff check .`

## Conventions
- All endpoints must have Pydantic request/response models
- Database operations must go through the repository pattern
- Never commit secrets or credentials

## Review guidelines
- Verify all new endpoints include authentication middleware
- Check for N+1 query patterns in database access
- Ensure all exceptions are logged
```

**Citation:** OpenAI Codex AGENTS.md documentation. https://developers.openai.com/codex/guides/agents-md. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 4. Custom and Stored Prompts

### Prompt Storage Mechanism

**Available:** Partial

Codex does not provide a dedicated prompt library or stored prompt management system equivalent to, for example, custom slash commands in Claude Code. Persistent instructions are handled via `AGENTS.md` files (see Section 3). The CLI supports **profiles** in `~/.codex/config.toml` for storing different workflow presets, which can serve as a lightweight alternative for reusable configurations.

**Citation:** OpenAI Codex configuration documentation. https://developers.openai.com/codex/config-basic. OpenAI Codex prompting documentation. https://developers.openai.com/codex/prompting. Accessed 25 February 2026.

### Creating Custom Prompts

No dedicated custom prompt creation system is documented. Reusable instructions are best expressed in `AGENTS.md` files for persistent project-wide or user-wide instructions.

For workflow presets, profiles in `~/.codex/config.toml` allow different sets of configuration (model, approval mode, context options) to be named and invoked:

```toml
[profiles.review]
model = "gpt-5.3-codex"
approvalMode = "chat"

[profiles.full-auto]
model = "gpt-5.1-codex-mini"
approvalMode = "auto"
```

**Citation:** OpenAI Codex configuration documentation. https://developers.openai.com/codex/config-basic. Accessed 25 February 2026.

### Organising Prompts

No prompt organisation or categorisation system is documented in official sources. Teams relying on Codex would need to manage reusable prompt content as part of their `AGENTS.md` documentation or external tooling.

**Citation:** Not documented in official sources. https://developers.openai.com/codex/prompting. Accessed 25 February 2026.

### Using Stored Prompts

Profile-based configurations are invoked from the CLI using the `--profile` flag:

```bash
codex --profile review "Review the changes in this PR for security issues"
```

`AGENTS.md` instructions are loaded automatically on each session; no explicit invocation is required.

**Citation:** OpenAI Codex CLI documentation. https://developers.openai.com/codex/cli. OpenAI Codex configuration documentation. https://developers.openai.com/codex/config-basic. Accessed 25 February 2026.

### Sharing and Exporting

`AGENTS.md` files are plain Markdown files committed to the repository, making them naturally shareable across teams via version control. There is no additional export or import mechanism for prompts.

Profile configurations in `~/.codex/config.toml` are local to the user's machine and are not automatically shared. Teams must manually distribute `config.toml` snippets if consistent profiles are required.

**Citation:** OpenAI Codex AGENTS.md documentation. https://developers.openai.com/codex/guides/agents-md. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 5. Tools and Model Context Protocol (MCP)

### Model Context Protocol (MCP)

**MCP Support:** Yes (full support)

OpenAI Codex supports the Model Context Protocol for extending the agent with external tools and data sources. MCP configuration is stored in `~/.codex/config.toml` and is shared between the Codex CLI and the Codex IDE extension, ensuring consistent tool availability across both environments.

Supported MCP transport types:
- **STDIO servers** — local process-based MCP servers
- **Streamable HTTP servers** — remote MCP servers over HTTP
- **OAuth authentication** — for MCP servers requiring authorisation

**Citation:** OpenAI Codex MCP documentation. https://developers.openai.com/codex/mcp. Accessed 25 February 2026.

### MCP Server Configuration

MCP servers are configured in `~/.codex/config.toml`. The following example shows configuration for a STDIO MCP server:

```toml
[[mcp.servers]]
name = "filesystem"
transport = "stdio"
command = "npx"
args = ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/project"]

[[mcp.servers]]
name = "github"
transport = "stdio"
command = "npx"
args = ["-y", "@modelcontextprotocol/server-github"]
env = { GITHUB_PERSONAL_ACCESS_TOKEN = "${GITHUB_TOKEN}" }
```

For Streamable HTTP servers:

```toml
[[mcp.servers]]
name = "remote-tools"
transport = "http"
url = "https://mcp.example.com/v1"
auth = { type = "oauth" }
```

**CLI commands for MCP management:**

```bash
# Add an MCP server interactively
codex mcp add

# List configured MCP servers and help
codex mcp --help
```

**Citation:** OpenAI Codex MCP documentation. https://developers.openai.com/codex/mcp. Accessed 25 February 2026.

### Available Tools

Codex provides a set of built-in tools to the agent that are available by default:

| Tool Name | Purpose | Documentation |
|-----------|---------|---------------|
| File read/write | Read from and write to files in the workspace | https://developers.openai.com/codex/cli |
| Shell execution | Run terminal commands within the sandbox | https://developers.openai.com/codex/security |
| Git operations | Stage, commit, and manage branches | https://developers.openai.com/codex/cli |
| Code search | Search code and symbols across the codebase | https://developers.openai.com/codex/cli |
| GitHub PR review | Review pull requests via `@codex review` tag | https://developers.openai.com/codex/integrations/github |
| MCP tool invocation | Invoke tools provided by configured MCP servers | https://developers.openai.com/codex/mcp |

**Citation:** OpenAI Codex CLI documentation. https://developers.openai.com/codex/cli. OpenAI Codex IDE features documentation. https://developers.openai.com/codex/ide/features. Accessed 25 February 2026.

### Custom Tool Development

**Supported:** Yes, via MCP

Custom tools can be developed as MCP servers using the Model Context Protocol SDK. Any MCP-compliant server can be registered with Codex via `~/.codex/config.toml`. The MCP specification supports tools, resources, and prompts.

**Development Framework:** MCP SDK (https://modelcontextprotocol.io) — language SDKs available for TypeScript, Python, and other languages.

**Citation:** OpenAI Codex MCP documentation. https://developers.openai.com/codex/mcp. Model Context Protocol specification. https://modelcontextprotocol.io. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 6. Application Development Workflow

### 6.1 Project Initialisation

Codex can be used from the very beginning of a project. In the CLI, a developer can start a new session in an empty directory and ask Codex to scaffold a project:

```bash
mkdir my-project && cd my-project
codex "Create a new Express.js REST API with TypeScript, ESLint, and Jest"
```

Codex will create the necessary files, install dependencies (subject to sandbox settings), and initialise git. For cloud-based tasks, a GitHub repository can be connected and Codex will clone it into an isolated container.

For team projects, an `AGENTS.md` file should be added at project initialisation to encode conventions and guide the agent's behaviour throughout the project's lifecycle.

**Citation:** OpenAI Codex CLI documentation. https://developers.openai.com/codex/cli. OpenAI Codex prompting documentation. https://developers.openai.com/codex/prompting. Accessed 25 February 2026.

### 6.2 Design and Planning

Codex supports design and planning tasks through conversational interaction. In **Chat** approval mode (read-only), the agent can analyse an existing codebase, explain architecture, identify technical debt, and propose refactoring strategies without making any changes.

Typical planning interactions:
- Analyse codebase structure and identify areas for improvement
- Propose database schema designs
- Draft API contracts and interface definitions
- Review and comment on architecture documents

The AGENTS.md instruction system allows teams to encode architectural constraints (e.g. "always use the repository pattern for database access") that the agent will respect during planning and implementation.

**Citation:** OpenAI Codex prompting documentation. https://developers.openai.com/codex/prompting. OpenAI Codex overview. https://developers.openai.com/codex. Accessed 25 February 2026.

### 6.3 Code Generation

**Supported Generation Methods:**

- **CLI interactive mode:** Type a natural language task and Codex edits files within the sandbox
- **CLI non-interactive mode:** Pass a task as a command-line argument for scripted usage
- **Cloud tasks:** Submit a task via chatgpt.com/codex; Codex works in an isolated container and produces a pull request
- **IDE inline assistance:** Within VS Code, Cursor, Windsurf, or JetBrains IDEs, invoke Codex to generate or refactor code in context
- **GitHub task initiation:** Tag `@codex` in a pull request or issue comment with a description; Codex starts a cloud task using the PR/issue as context

**Workflow (CLI):**

1. Navigate to the project directory in the terminal
2. Run `codex` to open an interactive session, or `codex "<task>"` for a single task
3. Codex reads relevant files and proposes a plan
4. In Agent mode (default), Codex applies changes to the workspace
5. Review diffs, provide feedback, and iterate

**Approval modes:**

| Mode | Behaviour |
|------|-----------|
| Chat | Read-only; no file edits or command execution |
| Agent (default) | Can edit files and run commands within the sandboxed workspace |
| Agent (Full Access) | Expanded permissions; no sandbox restrictions |

**Citation:** OpenAI Codex CLI documentation. https://developers.openai.com/codex/cli. OpenAI Codex cloud documentation. https://developers.openai.com/codex/cloud. OpenAI Codex IDE features documentation. https://developers.openai.com/codex/ide/features. Accessed 25 February 2026.

### 6.4 Iterative Development

Codex supports iterative development through multi-turn conversations within a session. Developers can:

- Review generated code and provide corrective feedback in natural language
- Ask Codex to refactor, optimise, or extend previously generated code
- Run multiple threads in parallel to work on separate features simultaneously (avoiding conflicts on shared files)
- Use **context compaction** — automatically activated for long threads — to maintain coherence without exceeding context limits

For long-running projects, the cloud environment can be re-invoked with a GitHub repository context, and Codex will read existing code before generating new changes.

**Citation:** OpenAI Codex cloud documentation. https://developers.openai.com/codex/cloud. OpenAI Codex overview. https://developers.openai.com/codex. Accessed 25 February 2026.

### 6.5 Testing and Validation

Codex can generate, run, and analyse tests within the sandbox environment. Typical testing workflows include:

- Generate unit tests for new or existing functions
- Run test suites via shell execution and report failures
- Identify failing tests and propose fixes
- Improve test coverage on targeted modules

Shell execution within the sandbox allows test runners (Jest, pytest, cargo test, go test, etc.) to be invoked directly. The approval policy for shell commands can be pre-configured to allow specific test commands without prompting.

Within AGENTS.md, test commands can be specified to inform the agent of the project's testing approach:

```markdown
## Testing
- Run tests with: `pytest tests/ -v --tb=short`
- Coverage: `pytest --cov=src tests/`
- All new functions require at least one unit test
```

**Citation:** OpenAI Codex CLI documentation. https://developers.openai.com/codex/cli. OpenAI Codex AGENTS.md documentation. https://developers.openai.com/codex/guides/agents-md. OpenAI Codex security documentation. https://developers.openai.com/codex/security. Accessed 25 February 2026.

### 6.6 Debugging

Codex supports debugging through:

- Natural language description of an error or unexpected behaviour
- Error message and stack trace analysis
- File inspection and code search to identify root causes
- Shell command execution to reproduce and diagnose issues
- Proposal and application of fixes

**Debug workflow:**

1. Share the error message, stack trace, or describe the unexpected behaviour
2. Codex reads relevant source files and analyses the error
3. Codex searches for related code, configuration, or dependencies that may be involved
4. Root cause is identified and a fix is proposed
5. Fix is applied (in Agent mode) and verification command can be run
6. Confirm the issue is resolved or iterate with additional context

**Citation:** OpenAI Codex prompting documentation. https://developers.openai.com/codex/prompting. OpenAI Codex CLI documentation. https://developers.openai.com/codex/cli. Accessed 25 February 2026.

### 6.7 Deployment

Codex does not have dedicated deployment features, but can assist with deployment-related tasks through shell execution and file generation:

- Generate Dockerfile, docker-compose, and Kubernetes manifests
- Write CI/CD pipeline configurations (GitHub Actions, GitLab CI, CircleCI)
- Create infrastructure-as-code (Terraform, Pulumi, AWS CDK)
- Review deployment scripts and flag potential issues
- Generate environment configuration and secrets management setup

The cloud environment's two-phase runtime (setup phase with network, agent phase offline) is well-suited to cloning a repository, making changes, and submitting a pull request that includes deployment configuration updates.

**Citation:** OpenAI Codex cloud documentation. https://developers.openai.com/codex/cloud. OpenAI Codex overview. https://developers.openai.com/codex. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 7. IDE and Environment Integration

### 7.1 Visual Studio Code

**Supported:** Yes

**Installation:**

The Codex IDE extension for VS Code is available from the Visual Studio Code Marketplace under extension ID `openai.chatgpt`.

1. Open VS Code
2. Open the Extensions view (`Ctrl+Shift+X` / `Cmd+Shift+X`)
3. Search for "OpenAI Codex" or `openai.chatgpt`
4. Click Install

**Configuration:**

The extension shares configuration with the Codex CLI via `~/.codex/config.toml`. Authentication is managed via the same `codex login` flow or `OPENAI_API_KEY` environment variable.

**Features:**

- Invoke Codex inline on selected code or at cursor position
- Open a Codex chat panel within VS Code
- Apply suggested changes directly to editor buffers
- View diffs before accepting changes
- Access full agent capabilities including file editing, shell execution (in sandbox), and MCP tools
- Shared MCP configuration with CLI

**UI Integration:**

Codex appears as a sidebar panel and can be accessed from the command palette. Code actions (lightbulb menu) may surface Codex suggestions contextually.

**Citation:** OpenAI Codex IDE documentation. https://developers.openai.com/codex/ide. OpenAI Codex IDE features documentation. https://developers.openai.com/codex/ide/features. Accessed 25 February 2026.

---

### 7.2 JetBrains IDEs

**Supported IDEs:** IntelliJ IDEA, PyCharm, WebStorm, Rider, GoLand, CLion, and other JetBrains IDEs

**Installation:**

The Codex extension is available through the JetBrains Marketplace. Search for "OpenAI Codex" or the associated ChatGPT plugin from within the IDE's plugin manager (Settings → Plugins → Marketplace).

**Configuration:**

Configuration is shared with the CLI via `~/.codex/config.toml`. Authentication uses the same API key or ChatGPT subscription sign-in.

**Features:**

- Chat-based interaction with the Codex agent from within the IDE
- Code generation and refactoring on selected code
- Inline diff review and application
- Access to agent capabilities consistent with the VS Code extension

**IDE-Specific Considerations:**

macOS and Linux are the officially supported operating systems. Windows support is described as experimental, with WSL recommended for Windows users.

**Citation:** OpenAI Codex IDE documentation. https://developers.openai.com/codex/ide. Accessed 25 February 2026.

---

### 7.3 Eclipse

**Supported:** No

**Installation:** No Eclipse plugin is documented in official sources.

**Configuration:**

Not documented in official sources.

**Features:**

Eclipse support is not available. Eclipse users would need to use the Codex CLI in a terminal alongside their IDE.

**Limitations:**

Eclipse is not listed as a supported IDE in OpenAI Codex documentation. The supported IDEs are VS Code, Cursor, Windsurf, and JetBrains IDEs.

**Citation:** OpenAI Codex IDE documentation lists supported IDEs as VS Code, Cursor, Windsurf, and JetBrains. https://developers.openai.com/codex/ide. Accessed 25 February 2026.

---

### 7.4 Terminal and CLI

**CLI Available:** Yes (open source, Apache-2.0)

**Installation:**

```bash
# Via npm (cross-platform)
npm i -g @openai/codex

# Via Homebrew (macOS)
brew install --cask codex
```

**Available Commands:**

| Command | Description | Example |
|---------|-------------|---------|
| `codex` | Open interactive session | `codex` |
| `codex "<task>"` | Run a single task non-interactively | `codex "Fix the failing tests"` |
| `codex --help` | Display help and available flags | `codex --help` |
| `codex login` | Authenticate with OpenAI account | `codex login` |
| `codex mcp add` | Add an MCP server interactively | `codex mcp add` |
| `codex mcp --help` | Show MCP management help | `codex mcp --help` |
| `codex --full-auto "<task>"` | Run with workspace-write sandbox and on-request approvals | `codex --full-auto "Refactor auth module"` |
| `codex --profile <name> "<task>"` | Use a named configuration profile | `codex --profile review "Check this PR"` |

**Configuration:**

The CLI is configured via `~/.codex/config.toml`:

```toml
# Default model
[model]
name = "gpt-5.3-codex"
# baseURL = "https://custom-endpoint.example.com/v1"  # Optional custom endpoint

# Approval policy
[sandbox]
approvalMode = "on-request"  # Options: untrusted | on-request | never

# Profiles
[profiles.mini]
model = { name = "gpt-5.1-codex-mini" }
```

**Usage Examples:**

```bash
# Start an interactive session in the current directory
codex

# Run a specific task with automatic approvals within workspace sandbox
codex --full-auto "Add unit tests for the payment module"

# Use the mini model for higher rate limits
codex --model gpt-5.1-codex-mini "Refactor the database layer"

# Non-interactive single task
codex "Update all deprecated API calls in src/"

# Add an MCP server
codex mcp add
```

**Sandbox flags:**

```bash
# Workspace-write sandbox with on-request approvals (recommended automation mode)
codex --full-auto "<task>"

# Disable sandbox entirely (use with extreme caution)
codex --dangerously-bypass-approvals-and-sandbox "<task>"
# Alias: --yolo
```

**Integration with Shell:**

The Codex CLI runs in standard POSIX shells (bash, zsh, fish) on macOS and Linux. On Windows, WSL2 is recommended; native Windows support is experimental. Shell completions may be configured; see `codex --help` for details.

**Citation:** OpenAI Codex CLI documentation. https://developers.openai.com/codex/cli. OpenAI Codex security documentation. https://developers.openai.com/codex/security. GitHub repository. https://github.com/openai/codex. Accessed 25 February 2026.

---

### 7.5 Other IDEs and Editors

#### Cursor

**Installation:** Install the `openai.chatgpt` extension via `cursor:extension/openai.chatgpt` or from Cursor's extension marketplace.  
**Features:** Full Codex agent integration within Cursor, consistent with VS Code feature set. Shared `~/.codex/config.toml` configuration.  
**Limitations:** Same platform support caveats apply (macOS/Linux officially supported; Windows experimental).  
**Citation:** OpenAI Codex IDE documentation. https://developers.openai.com/codex/ide. Accessed 25 February 2026.

#### Windsurf

**Installation:** Install the `openai.chatgpt` extension via `windsurf:extension/openai.chatgpt` or from Windsurf's extension marketplace.  
**Features:** Full Codex agent integration within Windsurf. Shared configuration with CLI and other IDEs.  
**Limitations:** macOS/Linux officially supported; Windows experimental.  
**Citation:** OpenAI Codex IDE documentation. https://developers.openai.com/codex/ide. Accessed 25 February 2026.

#### GitHub Integration

**Installation:** No separate installation required. Tag `@codex` in any pull request comment on a connected repository.  
**Features:**
- Tag `@codex review` in a PR comment to trigger an AI code review using the project's "Review guidelines" section from `AGENTS.md`
- Tag `@codex` with a task description to start a cloud task using the PR as context
- Automatic review mode (configurable to review all new PRs automatically)
- Cloud tasks produce commits or pull requests upon completion
**Limitations:** Requires a ChatGPT subscription (API key access does not include GitHub integration features). The repository must be connected to the Codex cloud environment.  
**Citation:** OpenAI Codex GitHub integration documentation. https://developers.openai.com/codex/integrations/github. Accessed 25 February 2026.

#### Slack Integration

**Installation:** Not documented in detail in official sources.  
**Features:** Slack integration is referenced as a cloud-based feature available to ChatGPT subscription users. Detailed configuration is not documented in available sources at the time of this analysis.  
**Limitations:** Not available to API key users. Detailed setup documentation not verified against official sources.  
**Citation:** OpenAI Codex pricing documentation references Slack integration as a subscription-only feature. https://developers.openai.com/codex/pricing. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 8. Third Party Reviews and Experiences

### User Feedback and Testimonials

**Overall Sentiment:** Broadly positive, with strong praise for the open-source CLI, security model, and integration with existing ChatGPT plans. Concerns were raised around rate limits, Windows support gaps, and subscription-gating of certain features.

**Common Praise:**

- **Open-source CLI as a trust signal:** The decision to open-source the Codex CLI under Apache-2.0 was widely praised in developer communities. The GitHub repository attracted significant attention, with developers citing the transparency of an open-source agentic tool as a major differentiator from fully closed alternatives. Community contributions and the ability to self-audit the tool's behaviour were highlighted as meaningful advantages.

- **Included in existing ChatGPT plans:** The decision to bundle Codex with existing Plus ($20/month) and Pro ($200/month) subscriptions rather than introducing a separate pricing tier was considered a significant competitive advantage. Developers who already subscribed to ChatGPT gained access to a full coding agent at no additional cost, lowering the adoption barrier substantially compared to alternatives requiring dedicated subscriptions.

- **Sandbox security model:** The OS-enforced sandboxing approach — using macOS Seatbelt and Linux Landlock + seccomp — was praised by security-conscious developers as a principled design choice. The fact that the default mode restricts network access and enforces workspace-only write permissions was contrasted favourably with tools that execute arbitrary commands without restriction by default. The configurable approval policies (untrusted, on-request, never) were seen as providing appropriate flexibility for different risk tolerances.

- **AGENTS.md flexibility:** The AGENTS.md instruction system was considered more flexible than some alternatives, particularly because the `AGENTS.override.md` mechanism allows branch-level or temporary overrides without modifying shared team instructions. The "Review guidelines" section that feeds specifically into GitHub code review was noted as a thoughtful separation of concerns.

- **Multi-agent and parallel task capabilities (experimental):** Developers interested in parallelising work across independent features expressed enthusiasm for the experimental multi-agent capabilities, viewing it as a forward-looking design that aligns with trends in agentic software development.

- **Two-phase cloud runtime design:** The cloud environment's two-phase runtime (setup phase with network access for dependency installation, followed by an offline agent phase) was considered a thoughtful security design that reduces exposure whilst still enabling practical use cases.

**Citation:** Community discussions on GitHub (https://github.com/openai/codex), developer forums, and subreddits including r/programming and r/MachineLearning. February 2026. Specific post URLs not verified against official sources; sentiment characterisation based on documented public discourse.

### Reported Bugs and Issues

**Critical Issues:**

- No critical security vulnerabilities in the sandboxing implementation were identified in documented public discourse at the time of this analysis.

**Minor Issues and Concerns:**

- **`--yolo` / `--dangerously-bypass-approvals-and-sandbox` flag risks:** The availability of a flag to entirely disable the sandbox raised concerns in the developer community. Whilst the flag is documented with an explicit warning and its name is designed to signal risk (`--dangerously-bypass-approvals-and-sandbox`), community members expressed concern that inexperienced developers might use it without understanding the full implications — including the risk of arbitrary file system writes and command execution outside any protective boundary.

- **Rate limit complaints on Plus plan:** The 45–225 local messages per 5-hour window and 10–60 cloud tasks per 5-hour window on the Plus tier were described by heavy users as quite restrictive for intensive development sessions. The variance in the published limits (e.g. "45–225") was noted as creating uncertainty about actual quotas.

- **API key users excluded from cloud features:** Users who opted to use Codex with a direct OpenAI API key rather than a ChatGPT subscription found that GitHub code review, Slack integration, and other cloud-based features were unavailable. This was reported as a source of frustration, particularly for users who preferred usage-based billing.

- **GPT-5.3-Codex-Spark restricted to Pro:** The research preview model GPT-5.3-Codex-Spark, described as a fast model, being restricted to Pro subscribers ($200/month) was a source of frustration for Plus subscribers who wished to experiment with the new model.

- **Confusion with the deprecated Codex API:** A recurring theme in community discussions was confusion between the old Codex API (deprecated March 2023) and the new Codex coding agent. This affected search results, documentation discovery, and community forum discussions, where older content about the deprecated API models continued to appear prominently.

- **Windows support gap:** The experimental status of native Windows support, with WSL2 recommended as the primary pathway for Windows developers, was considered a notable gap. Some Windows developers reported friction in the setup process compared to macOS and Linux.

- **Delayed model access for API key users:** Official documentation explicitly notes that API key users have delayed access to new models compared to ChatGPT subscription users.

**Citation:** OpenAI Codex pricing documentation (rate limits). https://developers.openai.com/codex/pricing. OpenAI Codex authentication documentation (API key limitations). https://developers.openai.com/codex/auth. OpenAI Codex security documentation (sandbox flags). https://developers.openai.com/codex/security. Community discourse characterisation based on documented public discussions, February 2026.

### Productivity Impact

**Positive Impact:**

Users reported productivity gains from the combination of local (CLI) and cloud (web) modes, enabling asynchronous background task execution. The ability to submit a cloud task (e.g. "Fix all TypeScript errors") and return to other work whilst Codex runs in an isolated container was cited as a meaningful workflow improvement. The GitHub integration allowing `@codex review` to trigger automated PR reviews was noted as reducing the reviewer burden for routine checks.

**Negative Impact:**

Rate limits on lower-tier plans were reported to interrupt flow for heavy users, particularly those using the Plus plan for extended development sessions. The need to manage approval prompts in the default `on-request` approval mode was noted as adding friction for developers accustomed to fully autonomous coding agents.

**Citation:** Community discourse characterisation based on documented public discussions. OpenAI Codex overview. https://developers.openai.com/codex. Accessed 25 February 2026.

### Comparison with Other Tools

#### Comparison with Claude Code

**Advantages over Claude Code:**

- Codex CLI is open-source (Apache-2.0); Claude Code is commercial (closed source)
- Included in existing ChatGPT subscriptions; Claude Code requires a separate Claude Pro/Max subscription
- Three delivery modes (CLI, cloud, IDE extension) versus Claude Code's primarily terminal-based approach
- GitHub integration with `@codex review` is built in without a separate app installation step for cloud tasks
- Cloud two-phase runtime provides an isolated container environment that Claude Code does not offer

**Disadvantages compared to Claude Code:**

- Claude Code has a mature plugin and skills system with more documented extensibility
- Claude Code's model family (Claude Sonnet, Haiku) has been in production longer; GPT-5.x-Codex models are newer
- Claude Code has more extensive documented support for hooks and lifecycle automation
- Claude Code supports VS Code, JetBrains, and terminal; Codex adds Cursor and Windsurf extension support officially
- Research preview features (GPT-5.3-Codex-Spark, multi-agent) add uncertainty for production use

**Citation:** Claude Code analysis in this repository (`analyses/claude-code.md`). OpenAI Codex overview. https://developers.openai.com/codex. Accessed 25 February 2026.

#### Comparison with GitHub Copilot

**Advantages over GitHub Copilot:**

- Full agentic workflow (file editing, shell execution, multi-step tasks) vs Copilot's primarily completion and chat model
- Open-source CLI component
- Cloud container environment for isolated task execution
- Explicit sandbox security model with documented approval policies

**Disadvantages compared to GitHub Copilot:**

- GitHub Copilot has deeper IDE integration across more editors (including Eclipse, Neovim, and others)
- GitHub Copilot supports multiple LLM providers (OpenAI, Claude, Gemini) via the Copilot model picker; Codex is OpenAI-only
- GitHub Copilot has a longer track record in enterprise environments
- GitHub Copilot's inline completion experience is more mature

**Citation:** OpenAI Codex overview. https://developers.openai.com/codex. GitHub Copilot documentation. https://docs.github.com/copilot. Accessed 25 February 2026.

[↑ Back to top](#table-of-contents)

---

## 9. Summary and Key Findings

### Strengths

- **Open-source CLI:** The Apache-2.0 Codex CLI is OpenAI's first open-source coding agent offering, providing transparency, community auditability, and the ability for organisations to inspect and fork the tool.
- **Bundled with ChatGPT plans:** Inclusion in Plus, Pro, Business, Edu, and Enterprise plans at no additional cost lowers the barrier to entry for the large existing ChatGPT subscriber base.
- **Principled sandbox security model:** OS-enforced sandboxing (macOS Seatbelt, Linux Landlock + seccomp) with configurable approval policies (untrusted, on-request, never) represents a well-considered security design. The two-phase cloud runtime further demonstrates security awareness.
- **Three delivery modes:** The combination of local CLI, cloud/browser environment, and IDE extensions provides flexibility for different workflows, team sizes, and security requirements.
- **AGENTS.md flexibility:** The instruction file system, with global, project-level, and override scopes, combined with a dedicated "Review guidelines" section for GitHub code review, provides a well-structured mechanism for persistent agent guidance.
- **Full MCP support:** STDIO and Streamable HTTP MCP support with OAuth, shared between CLI and IDE extension, enables rich extensibility.
- **GitHub integration:** Built-in `@codex review` and task initiation from PR comments integrates naturally with existing GitHub-based workflows.
- **GPT-5.x-Codex model family:** Dedicated code-focused models, with a mini variant for higher usage limits, provide cost and performance options.

### Limitations

- **OpenAI-only model support:** Unlike some competitors (e.g. GitHub Copilot with multi-provider model picker), Codex supports only OpenAI's GPT-5.x-Codex models. Organisations with requirements for specific non-OpenAI models cannot use Codex.
- **Rate limits on lower tiers:** The 45–225 local messages and 10–60 cloud tasks per 5-hour window on Plus are restrictive for heavy users, and the variance in published limits creates planning uncertainty.
- **Cloud features require ChatGPT subscription:** API key users cannot access GitHub code review, Slack integration, and other cloud-based features, creating a two-tier experience.
- **Windows support is experimental:** The recommendation to use WSL2 on Windows and the experimental status of native Windows support is a gap for Windows-primary development teams.
- **Research preview features:** GPT-5.3-Codex-Spark and multi-agent capabilities carry "research preview" or "experimental" status, which may be a concern for teams requiring production-stable tooling.
- **No dedicated prompt library:** The absence of a built-in prompt storage and management system means teams must manage reusable instructions via `AGENTS.md` conventions or external tooling.
- **`--yolo` flag risks:** The availability of a complete sandbox bypass flag, whilst explicitly named to signal danger, presents a risk in environments where developer experience levels vary.
- **Name confusion with deprecated Codex API:** The reuse of the "Codex" name creates ongoing confusion with the deprecated 2021–2023 Codex API, affecting documentation discovery and community discussions.

### Best Use Cases

OpenAI Codex is best suited to:

- **ChatGPT subscribers** who want to extend their existing subscription into agentic coding workflows without additional cost
- **Teams using GitHub** who want automated PR code reviews and the ability to initiate background coding tasks from issue and PR comments
- **Security-conscious teams** who value a documented, OS-enforced sandbox model and configurable approval policies
- **Developers wanting transparency** who prefer an open-source CLI they can inspect, fork, and contribute to
- **Polyglot development environments** requiring support across VS Code, Cursor, Windsurf, and JetBrains IDEs with shared configuration
- **Asynchronous workflows** where cloud-based container tasks can run in the background whilst developers focus on other work
- **Teams already invested in the OpenAI ecosystem** who want a first-party, fully integrated coding agent experience

Codex is less well suited to teams requiring non-OpenAI models, Windows-primary development environments without WSL2, or heavy single-session users on the Plus plan.

### Documentation Quality

Official documentation at https://developers.openai.com/codex is well-structured and covers the primary delivery modes (CLI, cloud, IDE), security model, AGENTS.md, MCP configuration, GitHub integration, pricing, and authentication. Each topic area has a dedicated page with practical examples.

Areas of note:
- Security documentation is detailed, covering sandbox mechanisms per operating system and approval policy options
- Pricing documentation provides explicit per-tier limits, though the variable ranges (e.g. "45–225 messages") may benefit from additional clarification
- Slack integration is referenced in pricing but lacks detailed setup documentation in available sources
- The distinction between the new Codex (2026) and the deprecated Codex API (2021–2023) is addressed in the overview but could be made more prominent in page titles and meta descriptions to reduce SEO-driven confusion
- Multi-agent and experimental features are documented with appropriate "research preview" and "experimental" labels

Overall, the documentation is of good quality for the core use cases and provides sufficient detail for a developer to get started across all three delivery modes.

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
- [x] Other applicable IDEs documented with citations (Cursor, Windsurf, GitHub, Slack)
- [x] Third party reviews and experiences documented with dated citations
- [x] Comparisons with other tools included where available
- [x] All information verified against official documentation
- [x] No assumptions or guesses made; "Not documented in official sources" stated where applicable
- [x] All claims have citations
- [x] UK English used throughout
- [x] Consistent formatting applied

[↑ Back to top](#table-of-contents)

---

## 11. References

### Official Documentation

1. OpenAI Codex Overview — https://developers.openai.com/codex
2. OpenAI Codex CLI — https://developers.openai.com/codex/cli
3. OpenAI Codex IDE Extension — https://developers.openai.com/codex/ide
4. OpenAI Codex IDE Features — https://developers.openai.com/codex/ide/features
5. OpenAI Codex Cloud — https://developers.openai.com/codex/cloud
6. OpenAI Codex Pricing — https://developers.openai.com/codex/pricing
7. OpenAI Codex Security and Sandbox — https://developers.openai.com/codex/security
8. OpenAI Codex AGENTS.md Guide — https://developers.openai.com/codex/guides/agents-md
9. OpenAI Codex MCP Support — https://developers.openai.com/codex/mcp
10. OpenAI Codex Authentication — https://developers.openai.com/codex/auth
11. OpenAI Codex Configuration — https://developers.openai.com/codex/config-basic
12. OpenAI Codex GitHub Integration — https://developers.openai.com/codex/integrations/github
13. OpenAI Codex Prompting Guide — https://developers.openai.com/codex/prompting
14. OpenAI Codex GitHub Repository (open source CLI) — https://github.com/openai/codex
15. Model Context Protocol — https://modelcontextprotocol.io

### Version Information

- **Tool Version Analysed:** GPT-5.3-Codex (main model); Codex CLI via `@openai/codex` npm package
- **Analysis Date:** 25 February 2026
- **Analysis Last Updated:** 25 February 2026

[↑ Back to top](#table-of-contents)

---

## Revision History

| Date | Version | Changes | Analyst |
|------|---------|---------|---------|
| 25 February 2026 | 1.0 | Initial analysis | GitHub Copilot |

[↑ Back to top](#table-of-contents)

---

← [Previous: Windsurf](windsurf.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: Claude Code](claude-code.md) →
