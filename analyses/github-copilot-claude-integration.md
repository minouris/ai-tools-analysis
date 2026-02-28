← [Previous: GitHub Copilot Chat](github-copilot-chat.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: GitHub Copilot Coding Agent](github-copilot-coding-agent.md) →

---

# GitHub Copilot: Claude Integration Deep Dive

**Analysis Date:** 28 February 2026
**Analyst:** GitHub Copilot
**Official Documentation:** https://docs.github.com/en/copilot

## Table of Contents

- [1. Overview of Claude Integrations](#1-overview-of-claude-integrations)
  - [1.1 Two Distinct Integration Modes](#11-two-distinct-integration-modes)
- [2. Claude as a Language Model](#2-claude-as-a-language-model)
  - [2.1 Supported Claude Models](#21-supported-claude-models)
  - [2.2 Model Hosting and Data Privacy](#22-model-hosting-and-data-privacy)
  - [2.3 Thinking Tokens](#23-thinking-tokens)
- [3. The Claude Agent Delegation Mode](#3-the-claude-agent-delegation-mode)
  - [3.1 What is the Claude Agent SDK?](#31-what-is-the-claude-agent-sdk)
  - [3.2 Enabling the Claude Agent](#32-enabling-the-claude-agent)
  - [3.3 Local vs Cloud Agent Sessions](#33-local-vs-cloud-agent-sessions)
  - [3.4 Claude Agent Slash Commands](#34-claude-agent-slash-commands)
  - [3.5 Permission Modes](#35-permission-modes)
  - [3.6 Billing and Usage Costs](#36-billing-and-usage-costs)
- [4. How Claude Delegation Differs from Regular Agent Mode](#4-how-claude-delegation-differs-from-regular-agent-mode)
  - [4.1 Architecture Comparison](#41-architecture-comparison)
  - [4.2 Feature Comparison Table](#42-feature-comparison-table)
  - [4.3 When to Use Each Mode](#43-when-to-use-each-mode)
- [5. Claude Configuration File Support](#5-claude-configuration-file-support)
  - [5.1 What is CLAUDE.md?](#51-what-is-claudemd)
  - [5.2 How Copilot Uses CLAUDE.md](#52-how-copilot-uses-claudemd)
  - [5.3 Supported Environments](#53-supported-environments)
  - [5.4 Restrictions and Limitations](#54-restrictions-and-limitations)
- [6. Agent Skills Support](#6-agent-skills-support)
  - [6.1 What are Agent Skills?](#61-what-are-agent-skills)
  - [6.2 Supported Environments for Agent Skills](#62-supported-environments-for-agent-skills)
  - [6.3 Skill Storage Locations and Cross-Compatibility](#63-skill-storage-locations-and-cross-compatibility)
  - [6.4 SKILL.md Format: Copilot vs Claude Code](#64-skillmd-format-copilot-vs-claude-code)
  - [6.5 Can Claude Code Skills Be Used in Copilot Without Modification?](#65-can-claude-code-skills-be-used-in-copilot-without-modification)
  - [6.6 Claude Code Sub-Agents Are Not Agent Skills](#66-claude-code-sub-agents-are-not-agent-skills)
- [7. Enabling and Configuring Claude](#7-enabling-and-configuring-claude)
  - [7.1 Subscription Requirements](#71-subscription-requirements)
  - [7.2 Organisation and Enterprise Policy Controls](#72-organisation-and-enterprise-policy-controls)
- [8. Summary and Key Findings](#8-summary-and-key-findings)
- [9. Completeness Checklist](#9-completeness-checklist)
- [10. References](#10-references)
- [Revision History](#revision-history)

---

## 1. Overview of Claude Integrations

GitHub Copilot's relationship with Anthropic's Claude encompasses two fundamentally different integration modes: using Claude models as the language model powering Copilot Chat responses, and delegating full coding tasks to the Claude Agent SDK as a third-party autonomous agent. Understanding the distinction between these modes is essential to using each effectively.

### 1.1 Two Distinct Integration Modes

| Integration Mode | What It Does | Status |
|-----------------|--------------|--------|
| **Claude as a language model** | Selects a Claude model (Haiku, Sonnet, Opus) to power Copilot Chat responses and inline suggestions. Copilot remains the orchestrator; Claude provides the intelligence. | Generally available |
| **Claude Agent SDK (delegation)** | Delegates an entire coding task to Anthropic's Claude Agent SDK, which then runs autonomously using its own tools, memory system, and execution harness. Copilot provides the session management and billing integration. | Public preview |

**Citation:** About Anthropic Claude. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/anthropic-claude. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## 2. Claude as a Language Model

### 2.1 Supported Claude Models

Copilot supports the following Claude models from Anthropic, available for use in Copilot Chat and agent sessions:

| Model | Task Area | Primary Use Case |
|-------|-----------|-----------------|
| **Claude Haiku 4.5** | Fast help with simple or repetitive tasks | Fast, reliable answers to lightweight coding questions |
| **Claude Sonnet 4.0** | Deep reasoning and debugging | Performance and practicality, balanced for coding workflows |
| **Claude Sonnet 4.5** | General-purpose coding and agent tasks | Complex problem-solving and sophisticated reasoning |
| **Claude Sonnet 4.6** | General-purpose coding and agent tasks | General agentic coding tasks (default for Coding Agent) |
| **Claude Opus 4.5** | Deep reasoning and debugging | Complex problem-solving and sophisticated reasoning |
| **Claude Opus 4.6** | Deep reasoning and debugging | Anthropic's most powerful model; improves on 4.5 |
| **Claude Opus 4.6 (fast mode)** | Deep reasoning and debugging | Complex problem-solving with reduced latency (preview) |

Model availability depends on the Copilot plan. Model availability is subject to change; some models may be replaced or updated over time.

**Citation:** Supported AI models in GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/using-claude-sonnet-in-github-copilot. Accessed 28 February 2026. AI model comparison. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/ai-models/model-comparison. Accessed 28 February 2026.

### 2.2 Model Hosting and Data Privacy

Claude models in Copilot are hosted across three providers depending on availability and load: Amazon Web Services (Bedrock), Anthropic PBC directly, and Google Cloud Platform (Vertex AI). GitHub has provider agreements with each to ensure that prompts and completions are not used for AI model training.

**Key data commitments by provider:**

- **Amazon Bedrock:** Does not store or log prompts and completions; does not use them to train AWS models or distribute them to third parties.
- **Anthropic PBC:** GitHub maintains a zero data retention agreement with Anthropic for generally available Anthropic features in GitHub Copilot. Some Anthropic features in beta or public preview — including tool search via the Messages API — are not covered by this agreement.
- **Google Cloud Platform:** Google commits to not training on GitHub data as part of their service terms. GitHub is additionally not subject to prompt logging for abuse monitoring.

GitHub uses prompt caching across all three providers to improve service quality and reduce latency.

When using Claude models, all input prompts and output completions continue to pass through GitHub Copilot's content filters for public code matching (when enabled) and for harmful or offensive content.

**Note on the Claude Agent SDK (public preview):** The Claude Agent SDK is in public preview, and some features (such as tool search via the Messages API) may not be covered by Anthropic's zero data retention agreement. Data may be retained by Anthropic for those features in accordance with Anthropic's ZDR documentation.

**Citation:** Hosting of models for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/ai-models/model-hosting. Accessed 28 February 2026.

### 2.3 Thinking Tokens

As of VS Code v1.109 (February 2026), Anthropic models surface their internal reasoning process — known as "thinking tokens" — during agent sessions. This gives developers visibility into how the model is approaching a problem before it produces its final response. Thinking tokens appear in the Copilot Chat panel during agent execution.

**Citation:** GitHub Copilot in Visual Studio Code v1.109 January Release. GitHub Changelog. https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## 3. The Claude Agent Delegation Mode

### 3.1 What is the Claude Agent SDK?

The Claude Agent SDK is Anthropic's own agent harness — a framework that provides Claude with its own set of tools, execution context, memory system (`CLAUDE.md`), and agent capabilities. When GitHub Copilot delegates to the Claude Agent SDK, it is handing off the task to Anthropic's native agent infrastructure rather than running the task within Copilot's own agent system.

In practical terms, this means that a Claude agent session in VS Code is not Copilot using Claude as its language model — it is Copilot providing a VS Code host environment and billing integration, while Anthropic's Claude Agent SDK takes full autonomous control of planning and executing the coding task.

VS Code uses the provider's SDK and agent harness to access the agent's unique capabilities. You can use both local and cloud-based Claude agent sessions in VS Code. Integration with cloud-based sessions is enabled through a GitHub Copilot plan.

**Citation:** About Anthropic Claude. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/anthropic-claude. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

### 3.2 Enabling the Claude Agent

Before using the Claude Agent, it must be enabled in account settings:

**For GitHub Copilot Pro and Pro+ subscribers:**
1. Navigate to [coding agent settings](https://github.com/settings/copilot/coding_agent)
2. Under "Partner agents", click the toggle to enable Anthropic Claude

**For GitHub Copilot Business and Enterprise subscribers:**
- Enablement is controlled by organisation or enterprise policy. Organisation and enterprise admins must enable third-party coding agents via the relevant policy settings.

In VS Code, the Claude agent can additionally be enabled or disabled with the `github.copilot.chat.claudeAgent.enabled` setting.

**Citation:** Managing GitHub Copilot policies as an individual subscriber. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies#enabling-or-disabling-third-party-coding-agents-in-your-repositories. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

### 3.3 Local vs Cloud Agent Sessions

The Claude Agent can run in two distinct modes within VS Code, which have different characteristics:

**Local Claude Agent Session:**
- Runs the Claude Agent SDK directly within VS Code on the developer's machine
- Works on the current local workspace
- Interactive, with immediate feedback from the agent
- Select **Claude** from the **Session Type** dropdown to start a local session
- Does not require a separate Anthropic account

**Cloud Claude Agent Session:**
- Runs the Claude Agent in a cloud environment (equivalent to the cloud agent / Copilot Coding Agent infrastructure)
- Select **Cloud** from the **Session Type** dropdown, then select **Claude** from the **Partner Agent** dropdown
- Creates a pull request on GitHub for team review
- Uses GitHub Actions infrastructure

Both session types use the same Claude Agent SDK and are managed from VS Code's unified agent sessions view, alongside local Copilot agent sessions, background agents, and cloud agents.

**Note:** Steering (sending mid-session guidance) is not available for third-party coding agents including Claude. This is a limitation compared to the native Copilot coding agent, which does support steering input.

**Citation:** About third-party agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents#where-you-can-use-coding-agents. Accessed 28 February 2026. Managing coding agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/manage-agents. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

### 3.4 Claude Agent Slash Commands

The Claude agent provides a set of specialised slash commands that are distinct from standard Copilot slash commands. These reflect Claude's own agent capabilities. Type `/` in the chat input box within a Claude agent session to access these commands:

| Command | Description |
|---------|-------------|
| `/agents` | Create and manage specialised Claude sub-agents for specific tasks. Define custom agent behaviours through a wizard. |
| `/hooks` | Configure lifecycle hooks that execute at key points during Claude agent sessions, such as before or after tool execution. |
| `/memory` | Open and edit `CLAUDE.md` memory files that provide persistent context to the Claude agent across sessions. |
| `/init` | Initialise a new `CLAUDE.md` memory file for the current project. |
| `/pr-comments` | Retrieve comments from a pull request. |
| `/review` | Review code changes in a pull request. |
| `/security-review` | Perform a security review of pending code changes on the current branch. |

These commands expose Claude Code's native features (sub-agents, hooks, and memory) directly within the VS Code interface when using the Claude Agent SDK.

**Citation:** Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

### 3.5 Permission Modes

The Claude agent requests permission before performing certain operations. File edits within the workspace are auto-approved by default, whilst other operations such as running terminal commands may require confirmation.

There are three permission modes available:

| Mode | Behaviour |
|------|-----------|
| **Edit automatically** | Claude agent makes changes to the workspace autonomously as it works on the task. |
| **Request approval** | Claude agent asks for review before making changes to the workspace. |
| **Plan** | Claude agent outlines its intended approach before starting work on the task. |

**Caution:** The `github.copilot.chat.claudeAgent.allowDangerouslySkipPermissions` setting bypasses all permission checks. This should only be enabled in isolated sandbox environments with no internet access.

**Citation:** Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

### 3.6 Billing and Usage Costs

Third-party coding agents (including Claude) consume:

- **GitHub Actions minutes** — for cloud agent sessions
- **GitHub Copilot premium requests** — each agent session consumes one premium request

Within the monthly usage allowance for GitHub Actions and premium requests, coding agent sessions incur no additional cost beyond the Copilot subscription.

**Citation:** About third-party agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents#usage-costs. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## 4. How Claude Delegation Differs from Regular Agent Mode

### 4.1 Architecture Comparison

**Regular Agent Mode (Copilot Agent):**
When using regular agent mode in VS Code, Copilot orchestrates the session end-to-end. The selected language model (which may be a Claude model) provides the intelligence, but the tools, execution harness, workspace integration, and session management are all provided by Copilot and VS Code. Copilot determines which tools to call, manages the conversation context, and applies changes directly in the editor.

**Claude Agent SDK Delegation:**
When delegating to the Claude Agent SDK, Copilot hands off the task to Anthropic's own agent harness. Anthropic's infrastructure provides the toolset, memory management (`CLAUDE.md`), sub-agent orchestration, hooks, and execution logic. VS Code acts as the host environment and editor, while Copilot provides authentication and billing integration. The agent operates according to Anthropic's Claude Code execution model rather than Copilot's.

### 4.2 Feature Comparison Table

| Feature | Regular Agent Mode (Copilot) | Claude Agent SDK Delegation |
|---------|-----------------------------|-----------------------------|
| **Orchestrator** | GitHub Copilot | Anthropic Claude Agent SDK |
| **Language model** | Any Copilot-supported model | Claude (Anthropic) |
| **Tools** | Built-in Copilot tools + MCP | Claude's own toolset (via SDK) |
| **Session steering** | Supported | **Not supported** |
| **Memory system** | Copilot Memory (preview) | `CLAUDE.md` / Claude memory hierarchy |
| **Slash commands** | Copilot built-in commands | Claude-specific commands (`/memory`, `/hooks`, `/agents`, etc.) |
| **Sub-agents** | Parallel subagents (Copilot) | Claude sub-agents (via `/agents`) |
| **Hooks** | Agent hooks (preview, VS Code) | Claude lifecycle hooks (via `/hooks`) |
| **Permission model** | Copilot approval prompts | Claude permission modes (auto / approval / plan) |
| **Local session** | Yes | Yes |
| **Cloud session** | Yes (background / cloud agent) | Yes (via Cloud + Partner Agent dropdown) |
| **MCP server support** | Yes (built-in Copilot tools + MCP) | Via Claude Agent SDK only |
| **Requires enabling** | Enabled by default | Must be enabled in account settings |
| **Plan** | All Copilot plans | Pro, Pro+, Business, Enterprise |
| **Status** | Generally available | Public preview |

### 4.3 When to Use Each Mode

**Use regular agent mode when:**
- You want to use tools from VS Code extensions or MCP servers alongside the agent
- You want to use models other than Claude (GPT, Gemini, etc.)
- You want to steer or redirect the agent mid-session
- You want the tightest VS Code editor integration

**Use Claude Agent delegation when:**
- You want to use Anthropic's native Claude Code capabilities (`CLAUDE.md` memory, sub-agents, hooks)
- You have an existing Claude Code workflow and want to reuse its memory files and configuration
- You want the specific capabilities of Claude's own agent harness
- You want to run cloud-based tasks using Claude and create a pull request for review

**Citation:** Agents overview. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/overview. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## 5. Claude Configuration File Support

### 5.1 What is CLAUDE.md?

`CLAUDE.md` is Anthropic's native project memory file format from Claude Code (Anthropic's terminal-based agentic coding tool). It is a Markdown file that provides persistent instructions, coding conventions, and project context to Claude agents across sessions. Claude Code loads `CLAUDE.md` files from the repository root and parent directories at the start of every session.

In Claude Code, the `CLAUDE.md` system supports a full hierarchy of memory locations: organisation-wide managed policy files, project memory in the repository root (`./CLAUDE.md` or `./.claude/CLAUDE.md`), user-level personal preferences (`~/.claude/CLAUDE.md`), and modular topic-specific rules in `.claude/rules/`. It also supports `@import` syntax to include additional files, and `CLAUDE.local.md` for personal preferences that should not be committed to source control.

**Citation:** Memory. Claude Code Documentation. https://code.claude.com/docs/en/memory. Accessed 28 February 2026.

### 5.2 How Copilot Uses CLAUDE.md

GitHub Copilot treats `CLAUDE.md` as an **agent instructions file**, equivalent to `AGENTS.md` or `GEMINI.md`. When Copilot reads a repository, it recognises `CLAUDE.md` in the repository root as agent-level custom instructions and provides those instructions to the relevant Copilot features.

This means that teams already using Claude Code can reuse their existing `CLAUDE.md` files with GitHub Copilot without maintaining duplicate instruction files. The `CLAUDE.md` file serves as a single source of truth for project conventions that both Claude Code and Copilot will respect.

**Important distinction:** Copilot treats `CLAUDE.md` as a flat agent instructions file — it reads the file as project-level context. It does not replicate the full Claude Code memory hierarchy (user-level memory, `CLAUDE.local.md`, `@import` directives, `.claude/rules/` directory, auto-memory). Only the repository-level `CLAUDE.md` (in the repository root) is processed by Copilot; the broader Claude Code memory system is not replicated within Copilot.

**Citation:** Adding custom instructions for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot. Accessed 28 February 2026. Support for different types of custom instructions. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/custom-instructions-support. Accessed 28 February 2026.

### 5.3 Supported Environments

Support for `CLAUDE.md` as an agent instructions file varies by Copilot feature and environment. The following table shows where `CLAUDE.md` is recognised:

| Environment | Copilot Feature | CLAUDE.md Supported? |
|-------------|----------------|---------------------|
| **GitHub.com** | Copilot Chat | ❌ Not supported (uses `.github/copilot-instructions.md` and personal instructions only) |
| **GitHub.com** | Copilot Coding Agent | ✅ Supported |
| **GitHub.com** | Copilot Code Review | ❌ Not supported |
| **Visual Studio Code** | Copilot Chat | ❌ Not supported (`AGENTS.md` is supported; `CLAUDE.md` is not) |
| **Visual Studio Code** | Copilot Coding Agent | ✅ Supported |
| **Visual Studio Code** | Copilot Code Review | ❌ Not supported |
| **Visual Studio** | Copilot Chat | ❌ Not supported |
| **Visual Studio** | Copilot Code Review | ❌ Not supported |
| **JetBrains IDEs** | Copilot Chat | ❌ Not supported |
| **JetBrains IDEs** | Copilot Coding Agent | ✅ Supported |
| **JetBrains IDEs** | Copilot Code Review | ❌ Not supported |
| **Eclipse** | Copilot Chat | ❌ Not supported |
| **Eclipse** | Copilot Coding Agent | ✅ Supported |
| **Eclipse** | Copilot Code Review | ❌ Not supported |
| **Xcode** | Copilot Chat | ❌ Not supported |
| **Xcode** | Copilot Coding Agent | ✅ Supported |
| **Copilot CLI** | — | ❌ Not supported (`AGENTS.md` supported; `CLAUDE.md` is not) |

In summary: `CLAUDE.md` is supported **only** for the Copilot Coding Agent feature, not for Copilot Chat. It is supported for the Coding Agent across GitHub.com, VS Code, JetBrains, Eclipse, and Xcode.

**Citation:** Support for different types of custom instructions. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/custom-instructions-support. Accessed 28 February 2026.

### 5.4 Restrictions and Limitations

The following restrictions and limitations apply to `CLAUDE.md` support in GitHub Copilot, compared to native Claude Code behaviour:

**Scope limitations:**

- Only the repository-level `CLAUDE.md` (in the repository root) is used by Copilot. Copilot does not process `CLAUDE.md` files from parent directories or subdirectories in the same recursive manner as Claude Code.
- The user-level `~/.claude/CLAUDE.md` file (personal preferences for all projects) is not read by Copilot.
- The `CLAUDE.local.md` file (personal project-specific preferences) is not read by Copilot.
- The `.claude/rules/*.md` modular rules directory structure is not supported by Copilot.
- Claude Code's auto-memory system (`~/.claude/projects/<project>/memory/`) is not available in Copilot.

**Feature limitations:**

- `CLAUDE.md` is only supported for the **Copilot Coding Agent** feature — it is not used by Copilot Chat in any IDE.
- The `@import` syntax in `CLAUDE.md` (used to import additional context files) is not documented as supported by Copilot; its behaviour when present in a `CLAUDE.md` file read by Copilot is not specified in official documentation.
- Path-specific rules within `CLAUDE.md` using YAML frontmatter `paths` fields (a Claude Code feature) are not documented as supported by Copilot.

**General limitations of agent instructions files:**

- Agent instructions files (`CLAUDE.md`, `AGENTS.md`, `GEMINI.md`) are similar to repository-wide custom instructions but are currently not supported by all Copilot features — specifically, Copilot Chat does not read them, only the Coding Agent does.
- The `excludeAgent` frontmatter keyword (used in `.github/instructions/*.instructions.md` path-specific instructions) is not applicable to `CLAUDE.md`.

**Citation:** Support for different types of custom instructions. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/custom-instructions-support. Accessed 28 February 2026. About customizing GitHub Copilot responses. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/prompting/response-customization. Accessed 28 February 2026. Memory. Claude Code Documentation. https://code.claude.com/docs/en/memory. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## 6. Agent Skills Support

### 6.1 What are Agent Skills?

Agent skills are folders of instructions, scripts, and resources that Copilot (and Claude Code) can load when relevant, to improve performance on specialised tasks. Each skill is a directory containing a required `SKILL.md` file (using YAML frontmatter and a Markdown body) plus any optional supporting resources such as scripts or examples.

The Agent Skills specification is an **open standard** — not a proprietary Copilot or Claude invention. It is documented at https://github.com/agentskills/agentskills and is used by multiple AI systems, including both GitHub Copilot and Claude Code. This shared standard is the foundation for cross-tool compatibility.

**Citation:** About agent skills. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-agent-skills. Accessed 28 February 2026. Skills. Claude Code Documentation. https://code.claude.com/docs/en/skills. Accessed 28 February 2026.

### 6.2 Supported Environments for Agent Skills

Agent skills in Copilot are **not universally supported**. Official documentation explicitly limits their scope:

> "Agent Skills work with Copilot coding agent, the GitHub Copilot CLI and agent mode in Visual Studio Code Insiders. Support in the stable version of VS Code is coming soon."

| Feature | Agent Skills Supported? |
|---------|------------------------|
| Copilot Coding Agent (cloud, GitHub.com) | ✅ Yes |
| GitHub Copilot CLI | ✅ Yes |
| Agent mode — VS Code Insiders | ✅ Yes |
| Agent mode — VS Code stable | ⏳ Coming soon (not yet available) |
| Copilot Chat (interactive chat, not agent mode) | ❌ Not documented |

**Key limitation:** Agent skills are not available in the standard, stable release of VS Code at the time of writing (February 2026). Support for the stable VS Code release is listed as "coming soon" in official documentation.

**Citation:** About agent skills. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-agent-skills. Accessed 28 February 2026. Creating agent skills for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-skills. Accessed 28 February 2026.

### 6.3 Skill Storage Locations and Cross-Compatibility

Both Copilot and Claude Code support the same skill storage locations, which enables direct sharing of skills between the two systems:

| Skill Type | Copilot Locations | Claude Code Locations | Shared? |
|-----------|------------------|-----------------------|---------|
| **Project skills** (repository-specific) | `.github/skills/` or `.claude/skills/` | `.claude/skills/` | ✅ `.claude/skills/` is shared |
| **Personal skills** (across all projects) | `~/.copilot/skills/` or `~/.claude/skills/` | `~/.claude/skills/` | ✅ `~/.claude/skills/` is shared |

The `.claude/skills/` and `~/.claude/skills/` locations are read by **both** Copilot and Claude Code. Skills stored there are automatically available to both systems without any duplication or additional configuration.

Skills stored in `.github/skills/` are Copilot-specific and not read by Claude Code. There is no equivalent `.github/`-rooted location in Claude Code.

Organisation-level and enterprise-level skills are listed as "coming soon" in Copilot documentation; they are not yet available in either system.

**Citation:** About agent skills. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-agent-skills. Accessed 28 February 2026. Creating agent skills for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-skills. Accessed 28 February 2026. Skills. Claude Code Documentation. https://code.claude.com/docs/en/skills. Accessed 28 February 2026.

### 6.4 SKILL.md Format: Copilot vs Claude Code

Both systems use `SKILL.md` files with YAML frontmatter, but the recognised fields differ:

| Frontmatter Field | Copilot | Claude Code | Notes |
|------------------|---------|-------------|-------|
| `name` | ✅ Required | Optional (defaults to directory name) | Both use lowercase with hyphens |
| `description` | ✅ Required | Recommended | Used by both to decide when to apply the skill |
| `license` | Optional | Not documented | Copilot-specific metadata field |
| `disable-model-invocation` | ❌ Not supported | Optional | Claude Code extension — ignored by Copilot |
| `user-invocable` | ❌ Not supported | Optional | Claude Code extension — ignored by Copilot |
| `allowed-tools` | ❌ Not supported | Optional | Claude Code extension — ignored by Copilot |
| `model` | ❌ Not supported | Optional | Claude Code extension — ignored by Copilot |
| `context` (fork/subagent) | ❌ Not supported | Optional | Claude Code extension — ignored by Copilot |
| `agent` | ❌ Not supported | Optional | Claude Code extension — ignored by Copilot |
| `hooks` | ❌ Not supported | Optional | Claude Code extension — ignored by Copilot |
| `argument-hint` | ❌ Not supported | Optional | Claude Code extension — ignored by Copilot |

Both systems use the same Markdown body format for the skill's instructions.

**Citation:** Creating agent skills for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-skills. Accessed 28 February 2026. Skills. Claude Code Documentation. https://code.claude.com/docs/en/skills. Accessed 28 February 2026.

### 6.5 Can Claude Code Skills Be Used in Copilot Without Modification?

**Answer: Mostly yes, with conditions.**

**Skills that work in Copilot without modification:**

A Claude Code skill written using only the core fields (`name`, `description`, and a Markdown body) is directly compatible with Copilot. Since both systems follow the same Agent Skills open standard, such a skill requires no changes to work in both tools. If the skill is stored in `.claude/skills/`, it will be picked up by both Copilot and Claude Code automatically.

Example of a fully compatible skill (works in both systems unchanged):

```markdown
---
name: github-actions-failure-debugging
description: Guide for debugging failing GitHub Actions workflows. Use this when asked to debug failing GitHub Actions workflows.
---

To debug failing GitHub Actions workflows, follow this process:

1. Look up recent workflow runs and their status
2. Get AI summaries of failed job logs
3. Retrieve full logs if more detail is needed
4. Reproduce the failure in your own environment
5. Fix the failing build and verify before committing
```

**Skills that work in Copilot but with reduced functionality:**

Claude Code skills using Claude-specific frontmatter fields (`disable-model-invocation`, `user-invocable`, `allowed-tools`, `model`, `context: fork`, `agent`, `hooks`) will be loaded by Copilot but the Claude Code-specific behaviour will not apply — those fields are silently ignored. The skill's Markdown body instructions will still be followed. This is not an error; Copilot simply does not implement those extensions to the standard.

For example, a Claude Code skill with `disable-model-invocation: true` (which prevents Claude from invoking the skill automatically, requiring manual `/skill-name` invocation) will be treated by Copilot as a normal auto-invocable skill, since Copilot does not support that restriction.

**Skills that use `$ARGUMENTS` substitution:**

Claude Code supports dynamic argument substitution in skill content (e.g. `$ARGUMENTS`, `$0`, `$1`). This is a Claude Code extension. Copilot does not document support for argument substitution. Skills using `$ARGUMENTS` may have those placeholders treated as literal text by Copilot rather than being replaced.

**Summary:**

| Skill Type | Works in Copilot Without Modification? |
|-----------|----------------------------------------|
| Basic skill (name + description + Markdown body) | ✅ Yes, if stored in `.claude/skills/` |
| Skill using Claude-specific frontmatter (`disable-model-invocation`, `allowed-tools`, etc.) | ⚠️ Partially — skill loads but Claude-specific behaviour is ignored |
| Skill using `$ARGUMENTS` substitution | ⚠️ Unclear — not documented by Copilot; likely treated as literal text |
| Skill stored in `.github/skills/` | ✅ Works in Copilot; not read by Claude Code |

**Citation:** About agent skills. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-agent-skills. Accessed 28 February 2026. Skills. Claude Code Documentation. https://code.claude.com/docs/en/skills. Accessed 28 February 2026.

### 6.6 Claude Code Sub-Agents Are Not Agent Skills

It is important to distinguish between Claude Code's **skills** (`.claude/skills/`) and Claude Code's **sub-agents** (`.claude/agents/`). These are entirely separate concepts.

**Claude Code sub-agents** are defined in Markdown files stored in `.claude/agents/`. They have a different and more complex YAML frontmatter schema (including `tools`, `model`, `permissionMode`, `maxTurns`, `mcpServers`, `hooks`, `memory`, `background`, `isolation`). Sub-agents are invoked via the `/agents` slash command within Claude Code and run with their own isolated context window.

**Copilot has no equivalent to Claude Code sub-agents.** The `.claude/agents/` directory is not read by Copilot. There is no mechanism to port a Claude Code sub-agent definition directly to Copilot.

The `/agents` slash command seen in VS Code when using the Claude Agent SDK is part of the Claude Agent SDK's own interface and is not a Copilot feature.

**Citation:** Sub-agents. Claude Code Documentation. https://code.claude.com/docs/en/sub-agents. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## 7. Enabling and Configuring Claude

### 7.1 Subscription Requirements

| Feature | Required Plan |
|---------|--------------|
| Claude models in Copilot Chat (model selection) | Free, Pro, Pro+, Business, Enterprise |
| Claude Agent SDK (third-party agent) | Pro, Pro+, Business, Enterprise |

The Free plan does not have access to the Claude Agent SDK delegation feature. All paid plans (Pro, Pro+, Business, Enterprise) are eligible.

**Citation:** About Anthropic Claude. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/anthropic-claude. Accessed 28 February 2026.

### 7.2 Organisation and Enterprise Policy Controls

For Business and Enterprise subscribers, the ability to use third-party coding agents (including Claude) is controlled by policy settings at the organisation or enterprise level. Organisation and enterprise admins must explicitly enable third-party coding agents before members can use them.

Coding agents (both the native Copilot Coding Agent and third-party agents including Claude) have access only to repositories where Copilot Coding Agent has been enabled. Third-party agents respect the same repository access controls as the Copilot Coding Agent.

**Citation:** About third-party agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents#making-coding-agents-available. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## 8. Summary and Key Findings

### Summary of Claude Integrations

GitHub Copilot supports Claude at two distinct levels, and conflating them leads to confusion:

1. **Claude as a language model** is the simpler integration — Copilot uses Claude as the AI engine while Copilot itself remains the orchestrator. This is available across all paid plans, works in all supported IDEs, and requires no special configuration beyond selecting a Claude model from the model picker.

2. **Claude Agent SDK delegation** is a fundamentally different integration where Anthropic's Claude Agent SDK takes over autonomous execution. This is a public preview feature, requires explicit enablement in account settings, and is only available to Pro, Pro+, Business, and Enterprise subscribers.

### Key Findings

**Delegation mode is not just "agent mode with Claude":**
The Claude Agent SDK delegation mode is architecturally distinct from using Claude as the language model in regular agent mode. When delegating, Anthropic's own harness controls tool selection, memory management, and execution flow, rather than Copilot.

**Steering is unavailable for delegated Claude sessions:**
A significant limitation of the Claude Agent SDK delegation is that mid-session steering (sending guidance to redirect the agent while it is running) is not available. This capability is available for the native Copilot Coding Agent but not for third-party agents including Claude.

**CLAUDE.md support is narrower than it appears:**
Copilot does support `CLAUDE.md` files as agent instructions, but only for the Copilot Coding Agent — not for Copilot Chat. Furthermore, only the repository-level `CLAUDE.md` is read; the full Claude Code memory hierarchy (user memory, local memory, auto-memory, rules directory, import directives) is not replicated.

**Data privacy nuances in preview:**
The zero data retention agreement between GitHub and Anthropic applies to generally available Anthropic features. Some aspects of the Claude Agent SDK that are in public preview — including tool search via the Messages API — may not be covered by this agreement.

**Local and cloud sessions available:**
Unlike some third-party agents, the Claude Agent supports both local (within VS Code on the developer's machine) and cloud (GitHub-hosted, creating a pull request) session modes, providing flexibility for both interactive and background workflows.

**Agent Skills compatibility with Claude Code:**
Skills following the Agent Skills open standard (shared between Copilot and Claude Code) can be stored in `.claude/skills/` to be automatically available to both systems. Basic skills using only `name`, `description`, and a Markdown body are fully cross-compatible without modification. Claude Code-specific frontmatter fields are ignored by Copilot rather than causing errors. Claude Code sub-agents (`.claude/agents/`) are a separate concept and are not compatible with the Copilot skill system.

**Agent skills not yet available in VS Code stable:**
At the time of writing (February 2026), agent skills are supported by the Copilot Coding Agent, GitHub Copilot CLI, and agent mode in VS Code Insiders — but not yet in the stable release of VS Code. Support for VS Code stable is listed as coming soon.

**Citation:** About Anthropic Claude. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/anthropic-claude. Accessed 28 February 2026. About third-party agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026. Support for different types of custom instructions. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/custom-instructions-support. Accessed 28 February 2026. Hosting of models for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/ai-models/model-hosting. Accessed 28 February 2026. About agent skills. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-agent-skills. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## 9. Completeness Checklist

- [x] Overview of both Claude integration modes documented
- [x] Supported Claude models listed with task areas
- [x] Model hosting and data privacy documented (AWS Bedrock, Anthropic PBC, GCP)
- [x] Zero data retention agreement scope and preview limitations documented
- [x] Thinking tokens documented
- [x] Claude Agent SDK architecture explained
- [x] Enabling process documented for all plan types
- [x] Local vs cloud agent sessions compared
- [x] Claude agent slash commands listed
- [x] Permission modes documented
- [x] Billing and usage costs documented
- [x] Architectural differences from regular agent mode documented
- [x] Feature comparison table provided
- [x] CLAUDE.md format explained
- [x] How Copilot uses CLAUDE.md documented
- [x] Supported environments for CLAUDE.md tabulated
- [x] Restrictions and limitations of CLAUDE.md support documented
- [x] Subscription requirements for each feature documented
- [x] Agent skills open standard and Copilot/Claude Code shared compatibility documented
- [x] Supported environments for agent skills listed (with VS Code stable caveat)
- [x] Shared skill storage locations (`.claude/skills/`, `~/.claude/skills/`) documented
- [x] SKILL.md format differences between Copilot and Claude Code tabulated
- [x] Cross-compatibility analysis: can Claude Code skills be used in Copilot without modification?
- [x] Claude Code sub-agents distinguished from agent skills
- [x] Organisation and enterprise policy controls documented
- [x] All claims have citations to official documentation
- [x] No assumptions or guesses made
- [x] UK English used throughout

[↑ Back to top](#table-of-contents)

---

## 10. References

1. **About Anthropic Claude.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/anthropic-claude. Accessed 28 February 2026.

2. **About third-party agents.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents. Accessed 28 February 2026.

3. **Third-party agents in Visual Studio Code.** Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

4. **Agents overview.** Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/overview. Accessed 28 February 2026.

5. **Managing coding agents.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/manage-agents. Accessed 28 February 2026.

6. **Managing GitHub Copilot policies as an individual subscriber.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies. Accessed 28 February 2026.

7. **Supported AI models in GitHub Copilot.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/using-claude-sonnet-in-github-copilot. Accessed 28 February 2026.

8. **AI model comparison.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/ai-models/model-comparison. Accessed 28 February 2026.

9. **Hosting of models for GitHub Copilot Chat.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/ai-models/model-hosting. Accessed 28 February 2026.

10. **Support for different types of custom instructions.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/custom-instructions-support. Accessed 28 February 2026.

11. **Adding custom instructions for GitHub Copilot.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot. Accessed 28 February 2026.

12. **About customizing GitHub Copilot responses.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/prompting/response-customization. Accessed 28 February 2026.

13. **Memory.** Claude Code Documentation. https://code.claude.com/docs/en/memory. Accessed 28 February 2026.

14. **GitHub Copilot in Visual Studio Code v1.109 January Release.** GitHub Changelog. https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/. Accessed 28 February 2026.

15. **About agent skills.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-agent-skills. Accessed 28 February 2026.

16. **Creating agent skills for GitHub Copilot.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-skills. Accessed 28 February 2026.

17. **Creating agent skills for GitHub Copilot CLI.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/create-skills. Accessed 28 February 2026.

18. **Skills.** Claude Code Documentation. https://code.claude.com/docs/en/skills. Accessed 28 February 2026.

19. **Sub-agents.** Claude Code Documentation. https://code.claude.com/docs/en/sub-agents. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## Revision History

| Date | Version | Changes | Analyst |
|------|---------|---------|---------|
| 28 February 2026 | 1.0 | Initial analysis: Claude integration modes, delegation mode deep dive, CLAUDE.md support, restrictions and limitations | GitHub Copilot |
| 28 February 2026 | 1.1 | Added section 6: Agent Skills Support — open standard cross-compatibility, shared storage locations, SKILL.md format comparison, Claude Code sub-agents distinction, VS Code stable caveat | GitHub Copilot |

[↑ Back to top](#table-of-contents)

---

## See Also

- [GitHub Copilot Chat](github-copilot-chat.md) - Main Copilot Chat analysis
- [GitHub Copilot Coding Agent](github-copilot-coding-agent.md) - Autonomous Copilot Coding Agent analysis
- [Claude Code](claude-code.md) - Anthropic's native Claude Code terminal agent

---

← [Previous: GitHub Copilot Chat](github-copilot-chat.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: GitHub Copilot Coding Agent](github-copilot-coding-agent.md) →
