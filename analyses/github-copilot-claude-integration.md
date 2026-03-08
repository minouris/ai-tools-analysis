← [Previous: GitHub Codespaces](github-codespaces.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: GitHub Copilot Coding Agent](github-copilot-coding-agent.md) →

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
  - [3.7 Assigning GitHub Issues to the Claude Coding Agent](#37-assigning-github-issues-to-the-claude-coding-agent)
- [4. How Claude Delegation Differs from Regular Agent Mode](#4-how-claude-delegation-differs-from-regular-agent-mode)
  - [4.1 Architecture Comparison](#41-architecture-comparison)
  - [4.2 Feature Comparison Table](#42-feature-comparison-table)
  - [4.3 When to Use Each Mode](#43-when-to-use-each-mode)
- [5. Claude Configuration File Support](#5-claude-configuration-file-support)
  - [5.1 What is CLAUDE.md?](#51-what-is-claudemd)
  - [5.2 How Copilot Uses CLAUDE.md](#52-how-copilot-uses-claudemd)
  - [5.3 Supported Environments](#53-supported-environments)
  - [5.4 Restrictions and Limitations](#54-restrictions-and-limitations)
  - [5.5 CLAUDE.md Support in Claude Agent SDK Mode vs Default Copilot Agent Mode](#55-claudemd-support-in-claude-agent-sdk-mode-vs-default-copilot-agent-mode)
  - [5.6 Master Comparison: All Claude Configuration File Types](#56-master-comparison-all-claude-configuration-file-types)
  - [5.7 Does the Claude Agent SDK Read Copilot Instruction Files?](#57-does-the-claude-agent-sdk-read-copilot-instruction-files)
- [6. Agent Skills, Commands, Hooks, and Settings Support](#6-agent-skills-commands-hooks-and-settings-support)
  - [6.1 What are Agent Skills?](#61-what-are-agent-skills)
  - [6.2 Supported Environments for Agent Skills](#62-supported-environments-for-agent-skills)
  - [6.3 Skill Storage Locations and Cross-Compatibility](#63-skill-storage-locations-and-cross-compatibility)
  - [6.4 SKILL.md Format: Copilot vs Claude Code](#64-skillmd-format-copilot-vs-claude-code)
  - [6.5 Can Claude Code Skills Be Used in Copilot Without Modification?](#65-can-claude-code-skills-be-used-in-copilot-without-modification)
  - [6.6 Sub-Agents: Copilot Coding Agent vs Claude Agent SDK](#66-sub-agents-copilot-coding-agent-vs-claude-agent-sdk)
  - [6.7 Skills: Claude Agent SDK Mode vs Copilot Coding Agent](#67-skills-claude-agent-sdk-mode-vs-copilot-coding-agent)
  - [6.8 Custom Slash Commands (`.claude/commands/`)](#68-custom-slash-commands-claudecommands)
  - [6.9 Hooks (`.claude/settings.json`)](#69-hooks-claudesettingsjson)
  - [6.10 Settings and Permissions (`.claude/settings.json`)](#610-settings-and-permissions-claudesettingsjson)
  - [6.11 MCP Server Configuration (`.mcp.json`)](#611-mcp-server-configuration-mcpjson)
- [7. Enabling and Configuring Claude](#7-enabling-and-configuring-claude)
  - [7.1 Subscription Requirements](#71-subscription-requirements)
  - [7.2 Organisation and Enterprise Policy Controls](#72-organisation-and-enterprise-policy-controls)
- [8. Cost Comparison: Copilot Claude Mode vs Claude Code Standalone](#8-cost-comparison-copilot-claude-mode-vs-claude-code-standalone)
  - [8.1 GitHub Copilot Plan Allowances and Overage Pricing](#81-github-copilot-plan-allowances-and-overage-pricing)
  - [8.2 Claude Model Multipliers in Copilot](#82-claude-model-multipliers-in-copilot)
  - [8.3 Anthropic API Pricing Reference](#83-anthropic-api-pricing-reference)
  - [8.4 Per-Request Cost: Copilot Chat vs Direct API](#84-per-request-cost-copilot-chat-vs-direct-api)
  - [8.5 Per-Session Cost: Copilot Coding Agent and Claude Agent SDK vs Direct API](#85-per-session-cost-copilot-coding-agent-and-claude-agent-sdk-vs-direct-api)
  - [8.6 Claude Code Standalone Comparison](#86-claude-code-standalone-comparison)
  - [8.7 Model Selection Architecture: Claude Code, Claude Agent SDK, and Copilot Coding Agent](#87-model-selection-architecture-claude-code-claude-agent-sdk-and-copilot-coding-agent)
- [9. Summary and Key Findings](#9-summary-and-key-findings)
- [10. Completeness Checklist](#10-completeness-checklist)
- [11. References](#11-references)
- [Changes in v1.110](#changes-in-v1110)
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

> **Updated in VS Code v1.110 (February 2026):** Steering and queuing, session renaming, context window rendering with compaction, the `getDiagnostics` tool, and significant performance improvements have been added to the Claude agent experience. See [Changes in v1.110](#changes-in-v1110) for full details.

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

**Steering and queuing (added in VS Code v1.110):** You can now send follow-up messages mid-conversation to alter the Claude agent's approach, or to queue up additional requests for after the current response completes. This aligns the Claude agent experience with the steering and queuing capabilities available in regular Copilot agent mode.

**Session renaming (added in VS Code v1.110):** Claude agent sessions can now be renamed to keep track of them more easily.

**Citation:** About third-party agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents#where-you-can-use-coding-agents. Accessed 28 February 2026. Managing coding agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/manage-agents. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

### 3.4 Claude Agent Slash Commands

> **Updated in VS Code v1.110 (February 2026):** The `/compact` slash command has been added for on-demand conversation compaction.

The Claude agent provides a set of specialised slash commands that are distinct from standard Copilot slash commands. These reflect Claude's own agent capabilities. Type `/` in the chat input box within a Claude agent session to access these commands:

| Command | Description |
|---------|-------------|
| `/compact` | Compact the conversation history on demand. Optionally add custom instructions after the command (for example `/compact focus on the database schema decisions`). Added in VS Code v1.110. |
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

### 3.7 Assigning GitHub Issues to the Claude Coding Agent

**Short answer: yes — but only on Pro+ or Enterprise.** The Anthropic Claude coding agent is a full third-party coding agent and supports all the same issue-assignment entry points as the native Copilot Coding Agent. This is the cloud session path: the agent runs on GitHub's infrastructure, implements the issue, and opens a pull request for review — the same end-to-end workflow as Copilot Coding Agent, but powered by Anthropic's Claude Agent SDK.

#### Required plan

The official GitHub documentation for issue assignment is explicit: the agent dropdown that exposes third-party agents including Claude is **only available in GitHub Copilot Pro+ and Copilot Enterprise plans**. This is documented in Step 8 of the "Assigning an issue to Copilot on GitHub.com" workflow:

> "Third-party coding agents are available in the GitHub Copilot **Pro+ and Copilot Enterprise** plans."

Users on the basic **Pro plan** do not have access to the third-party agent dropdown and cannot select Claude from the issue assignment dialog. The top-level `about-third-party-agents` overview page lists Pro, Pro+, Business, and Enterprise in its "Who can use this feature?" header, but this refers to the third-party agents feature broadly. The specific issue-assignment dropdown that exposes Claude requires Pro+ or Enterprise.

**Citation:** Asking GitHub Copilot to create a pull request. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-a-pr#assigning-an-issue-to-copilot-on-githubcom. Accessed 3 March 2026.

#### Prerequisites

Before assigning issues to the Claude coding agent:

1. **Confirm your plan**: You need **GitHub Copilot Pro+ or Enterprise**. The basic Pro plan does not include the third-party agent dropdown.
2. **Enable third-party agents** in your Copilot settings. Navigate to [coding agent settings](https://github.com/settings/copilot/coding_agent) and under "Partner agents", toggle on **Anthropic Claude**.

#### How to assign an issue to Claude (GitHub.com)

1. Open the issue you want to assign in the repository on GitHub.com.
2. In the right sidebar, click **Assignees**.
3. Select **Copilot** from the assignees list. An "Assign to Copilot" dialog appears.
4. In the dialog, click the **agent dropdown** and select **Anthropic Claude** to use the Claude coding agent instead of the default Copilot Coding Agent.
5. Optionally add instructions in the "Optional prompt" field.
6. Click to confirm.

The Claude coding agent will start working on the task, push changes to a new pull request, and request a review from you when it finishes.

#### How to assign a task to Claude (Agents tab)

You can also start Claude agent tasks without an existing issue from the [Agents tab](https://github.com/copilot/agents):

1. Open the [Agents page](https://github.com/copilot/agents) on GitHub.
2. Select the target repository.
3. Click the agent dropdown and select **Anthropic Claude**.
4. Type a prompt describing the task.
5. Submit the task.

#### How to start a cloud Claude session from VS Code

Within VS Code, to start a cloud Claude session that creates a pull request (equivalent to assigning an issue from GitHub.com):

1. Open the Chat view and click **New Chat** (`+`).
2. Select **Cloud** from the **Session Type** dropdown.
3. Select **Claude** from the **Partner Agent** dropdown.
4. Enter your prompt.

#### Differences compared to the Copilot Coding Agent for issue assignment

| Capability | Copilot Coding Agent | Claude Coding Agent (issue assignment) |
|-----------|---------------------|----------------------------------------|
| Assign issue on GitHub.com | ✅ Yes (all plans) | ✅ Yes (Pro+ / Enterprise only) |
| Agents tab on GitHub.com | ✅ Yes | ✅ Yes (via agent dropdown) |
| Mention in PR comments | ✅ Yes (`@copilot`) | ✅ Yes (via third-party agent mention) |
| Cloud session creates PR | ✅ Yes | ✅ Yes |
| Session steering (mid-task redirect) | ✅ Yes | ✅ Yes (added in VS Code v1.110) |
| GitHub Actions minutes consumed | ✅ Yes | ✅ Yes |
| Premium requests consumed | 1 per session (+ model multiplier) | 1 per session (no multiplier in preview) |
| GitHub Mobile | ✅ Yes | ✅ Yes (via Agents tab) |
| Open session in VS Code | ✅ Yes | ✅ Yes |

#### Troubleshooting: "I don't see Claude in the dropdown"

If the issue assignment dialog only shows "Copilot" and "Custom Agent" but not "Anthropic Claude":

**"Custom Agent" is not Claude.** The "Custom Agent" option in the issue assignment dialog creates a custom *Copilot* agent — a `.agent.md` file stored in `.github/agents/` that configures specialised behaviour for the Copilot Coding Agent. This is entirely separate from third-party agents such as Claude. Clicking "Custom Agent" takes you to a text editor for creating a Copilot agent profile, not the Claude Agent SDK.

**Step 1 — Enable the Anthropic Claude partner agent toggle.** This is the most common cause. Claude only appears in the dropdown if you have explicitly enabled it in your account settings, regardless of your plan. The toggle is off by default. To enable it:

1. Navigate to your [Copilot coding agent settings](https://github.com/settings/copilot/coding_agent). Alternatively: click your profile picture in the upper-right corner of any GitHub page → **Copilot settings** → **Coding agent** (in the left sidebar).
2. Scroll to the **Partner agents** section.
3. Click the toggle next to **Anthropic Claude** to turn it on.
4. Return to the issue and try the **Assignees** dropdown again — **Anthropic Claude** should now appear in the agent selection dialog.

**Step 2 — Confirm Copilot coding agent is enabled for the target repository.** Claude uses the same repository access as Copilot coding agent. If Copilot coding agent has been disabled for that repository, Claude cannot work in it either. Check under **Repository access** on the same [coding agent settings page](https://github.com/settings/copilot/coding_agent) and ensure the repository is included.

**Step 3 — Check your plan.** The agent dropdown that surfaces third-party agents is available on Pro+ and Enterprise plans. On the basic Pro plan, the dropdown shows only built-in Copilot and custom Copilot agents. If you are on Pro and see the dropdown but not Claude, upgrading to Pro+ will unlock third-party agents.

**Citation:** About third-party agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents. Accessed 28 February 2026. Anthropic Claude. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/anthropic-claude. Accessed 28 February 2026. Asking GitHub Copilot to create a pull request. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-a-pr. Accessed 3 March 2026. Managing coding agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/manage-agents. Accessed 3 March 2026. Creating custom agents for Copilot coding agent. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-custom-agents. Accessed 3 March 2026.

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
| **Session steering** | Supported | **Supported (added in VS Code v1.110)** |
| **Memory system** | Copilot Memory (preview) | `CLAUDE.md` / Claude memory hierarchy |
| **Slash commands** | Copilot built-in commands | Claude-specific commands (`/memory`, `/hooks`, `/agents`, `/compact`, etc.) |
| **Sub-agents** | Parallel subagents (Copilot) | Claude sub-agents (via `/agents`) |
| **Hooks** | Agent hooks (preview, VS Code) | Claude lifecycle hooks (via `/hooks`) |
| **Permission model** | Copilot approval prompts | Claude permission modes (auto / approval / plan) |
| **Local session** | Yes | Yes |
| **Cloud session** | Yes (background / cloud agent) | Yes (via Cloud + Partner Agent dropdown) |
| **MCP server support** | Yes (built-in Copilot tools + MCP) | Via Claude Agent SDK only |
| **Requires enabling** | Enabled by default | Must be enabled in account settings |
| **Issue assignment on GitHub.com** | Yes (default Copilot agent) | Yes (via agent dropdown, Pro+ / Enterprise) |
| **Plan** | All Copilot plans | Pro, Pro+, Business, Enterprise |
| **Status** | Generally available | Public preview |

### 4.3 When to Use Each Mode

**Use regular agent mode when:**
- You want to use tools from VS Code extensions or MCP servers alongside the agent
- You want to use models other than Claude (GPT, Gemini, etc.)
- You want the tightest VS Code editor integration

**Use Claude Agent delegation when:**
- You want to use Anthropic's native Claude Code capabilities (`CLAUDE.md` memory, sub-agents, hooks)
- You have an existing Claude Code workflow and want to reuse its memory files and configuration
- You want the specific capabilities of Claude's own agent harness
- You want to run cloud-based tasks using Claude and create a pull request for review
- You want to assign GitHub issues directly to Claude for autonomous implementation (cloud session, Pro+ or above)

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
| **Visual Studio Code** | Claude Agent SDK — local session | ✅ Natively supported by Anthropic's agent harness (project-level and user-level) |
| **Visual Studio Code** | Claude Agent SDK — cloud session | ✅ Project-level supported; user-level (`~/.claude/CLAUDE.md`) not applicable in cloud sessions |
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

In summary: `CLAUDE.md` is supported for the Copilot Coding Agent feature (not for Copilot Chat), and also natively by the Claude Agent SDK delegation mode. The Copilot Coding Agent supports `CLAUDE.md` across GitHub.com, VS Code, JetBrains, Eclipse, and Xcode. The Claude Agent SDK is available in VS Code only and is currently in public preview; it supports `CLAUDE.md` through Anthropic's own agent harness. See [Section 5.5](#55-claudemd-support-in-claude-agent-sdk-mode-vs-default-copilot-agent-mode) for a detailed comparison of these two modes.

**Citation:** Support for different types of custom instructions. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/custom-instructions-support. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

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

### 5.5 CLAUDE.md Support in Claude Agent SDK Mode vs Default Copilot Agent Mode

When using the Claude Agent SDK delegation mode in VS Code (the third-party agent accessed via the Session Type dropdown), `CLAUDE.md` support is handled entirely by Anthropic's own agent harness — not by GitHub Copilot's custom instructions system. This produces a materially different level of support compared with what Copilot itself provides.

#### How the Claude Agent SDK handles CLAUDE.md

The Claude Agent SDK natively reads `CLAUDE.md` files as project memory. According to the Anthropic Agent SDK documentation, the SDK supports:

- **Project-level memory:** `CLAUDE.md` or `.claude/CLAUDE.md` in the working directory
- **User-level memory:** `~/.claude/CLAUDE.md` for global instructions applied across all projects

In local sessions (running on the developer's own machine), both project-level and user-level memory are accessible. In cloud sessions (running on GitHub-hosted infrastructure), only the project-level `CLAUDE.md` from the repository is accessible. User-level memory from `~/.claude/CLAUDE.md` is not available in cloud sessions because the file would need to exist on the remote machine, not the developer's local machine.

The VS Code integration confirms this native support via two dedicated slash commands. The `/memory` slash command "Opens and edits `CLAUDE.md` memory files that provide persistent context to Claude agent across sessions". The `/init` slash command initialises a new `CLAUDE.md` for the project.

**Citation:** Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026. Memory and system prompts. Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/modifying-system-prompts. Accessed 3 March 2026.

#### Comparison: Claude Agent SDK mode vs Copilot Coding Agent

The table below compares the degree of `CLAUDE.md` support between the two modes that support the file at all: the Copilot Coding Agent (Copilot's native agent instructions system) and the Claude Agent SDK delegation mode (Anthropic's own agent harness running within VS Code).

| Capability | Copilot Coding Agent | Claude Agent SDK (VS Code local) | Claude Agent SDK (VS Code cloud) |
|-----------|---------------------|-----------------------------------|----------------------------------|
| Project-level `CLAUDE.md` (`./CLAUDE.md` or `./.claude/CLAUDE.md`) | ✅ Supported (repository root only) | ✅ Natively supported | ✅ Natively supported |
| User-level `~/.claude/CLAUDE.md` | ❌ Not supported | ✅ Natively supported | ❌ Not available (cloud machine, not user's local machine) |
| `CLAUDE.local.md` (personal, untracked overrides) | ❌ Not supported | ⚠️ Not documented in Agent SDK documentation | ⚠️ Not applicable (cloud session) |
| `.claude/rules/*.md` (modular rules directory) | ❌ Not supported | ⚠️ Not documented in Agent SDK documentation | ⚠️ Not applicable (cloud session) |
| `@import` directives in `CLAUDE.md` | ❌ Not documented | ⚠️ Not documented in Agent SDK documentation | ⚠️ Not documented |
| Auto-memory (`~/.claude/projects/<project>/memory/`) | ❌ Not supported | ⚠️ Not documented in Agent SDK documentation | ❌ Not available (cloud session) |
| In-session memory management (`/memory` command) | ❌ Not applicable | ✅ Supported via `/memory` slash command | ✅ Supported via `/memory` slash command |
| Memory file initialisation (`/init` command) | ❌ Not applicable | ✅ Supported via `/init` slash command | ✅ Supported via `/init` slash command |
| Treated as flat agent instructions | ✅ Yes — Copilot reads file content as instructions | ❌ No — SDK uses it as a full memory system | ❌ No — SDK uses it as a full memory system |

**Key findings from this comparison:**

1. **Scope of memory loading:** When using the Copilot Coding Agent, Copilot reads the repository-level `CLAUDE.md` as a flat instructions file — equivalent in treatment to `AGENTS.md` or `GEMINI.md`. When using the Claude Agent SDK, Anthropic's harness manages `CLAUDE.md` as a live memory system, including project-level and (in local sessions) user-level files.

2. **User-level memory:** The user-level memory file (`~/.claude/CLAUDE.md`) is supported only in Claude Agent SDK local sessions. Neither the Copilot Coding Agent nor cloud Claude Agent SDK sessions can access the developer's personal machine's home directory.

3. **Claude Code-specific memory features:** The broader Claude Code memory hierarchy — `CLAUDE.local.md`, `.claude/rules/`, `@import` directives, and auto-memory — is not explicitly documented as supported by the Claude Agent SDK. These features are documented for Claude Code (the terminal tool) but are not confirmed for the Agent SDK. Teams relying on these advanced memory features should verify their behaviour in Claude Agent SDK sessions before depending on them.

4. **In-session memory management:** The Claude Agent SDK's `/memory` and `/init` commands allow developers to create and edit `CLAUDE.md` files directly during an agent session, without leaving VS Code. This capability does not exist in the Copilot Coding Agent, where `CLAUDE.md` is read at session start and cannot be modified mid-session via a command.

5. **Default Copilot Chat is unaffected:** Neither the Copilot Coding Agent's CLAUDE.md support nor the Claude Agent SDK's native memory system applies to standard Copilot Chat interactions (the default Copilot Chat mode in VS Code). Those interactions continue to use `AGENTS.md` (not `CLAUDE.md`) for agent-level instructions.

**Citation:** Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026. Memory and system prompts. Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/modifying-system-prompts. Accessed 3 March 2026. Support for different types of custom instructions. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/custom-instructions-support. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

### 5.6 Master Comparison: All Claude Configuration File Types

This section provides a single at-a-glance comparison of every Claude Code configuration file type and the degree of support in each Copilot mode. Detailed treatment of each type follows in subsequent sections: CLAUDE.md in [Section 5.1–5.5](#5-claude-configuration-file-support); and all other config types — skills, sub-agents, commands, hooks, settings, and MCP servers — in [Section 6.1–6.11](#6-agent-skills-commands-hooks-and-settings-support).

**Note on filesystem configuration in the VS Code Claude Agent SDK integration:** When using the Claude Agent SDK via the VS Code third-party agent integration, the SDK loads filesystem settings from the project directory. This is confirmed by the availability of the `/memory`, `/agents`, and `/hooks` slash commands, all of which depend on project-level configuration files being loaded. User-level configuration (`~/.claude/`) is available in local sessions (the developer's own machine) but not in cloud sessions (running on GitHub-hosted infrastructure, which does not have access to the developer's home directory).

| Config File / Directory | Purpose | Copilot Coding Agent | Claude Agent SDK (VS Code local) | Claude Agent SDK (VS Code cloud) |
|------------------------|---------|---------------------|-----------------------------------|----------------------------------|
| `CLAUDE.md` / `.claude/CLAUDE.md` | Project memory and instructions | ✅ Read as flat instructions | ✅ Native memory system | ✅ Native memory system |
| `~/.claude/CLAUDE.md` | User-level personal memory (cross-project) | ❌ Not supported | ✅ Natively supported | ❌ Not available in cloud |
| `CLAUDE.local.md` | Personal untracked memory overrides | ❌ Not supported | ⚠️ Not confirmed in Agent SDK documentation | ❌ Not applicable in cloud |
| `.claude/rules/*.md` | Modular topic-specific rules | ❌ Not supported | ⚠️ Not confirmed in Agent SDK documentation | ⚠️ Not confirmed in Agent SDK documentation |
| `.claude/skills/` | Project skills (auto-invoked specialised tasks) | ✅ Supported | ✅ Supported | ✅ Supported |
| `~/.claude/skills/` | User skills (personal, cross-project) | ✅ Supported (Coding Agent + CLI) | ✅ Supported | ❌ Not available in cloud |
| `.claude/agents/` | Project sub-agents (specialised isolated agents) | ❌ Not supported | ✅ Supported | ✅ Supported |
| `~/.claude/agents/` | User sub-agents (personal, cross-project) | ❌ Not supported | ✅ Supported | ❌ Not available in cloud |
| `.claude/commands/` | Project custom slash commands | ❌ Not supported | ✅ Supported | ✅ Supported |
| `~/.claude/commands/` | User custom slash commands (personal, cross-project) | ❌ Not supported | ✅ Supported | ❌ Not available in cloud |
| `.claude/settings.json` — hooks | Project lifecycle event handlers | ❌ Not supported | ✅ Supported | ✅ Supported |
| `~/.claude/settings.json` — hooks | User-level lifecycle hooks | ❌ Not supported | ✅ Supported | ❌ Not available in cloud |
| `.claude/settings.json` — permissions | Project tool allow/deny rules | ❌ Not supported | ✅ Supported | ✅ Supported |
| `.claude/settings.json` — env vars / model | Project environment variables and model overrides | ❌ Not supported | ✅ Supported | ✅ Supported |
| `.mcp.json` | Project MCP server configuration | ❌ Uses IDE-level MCP config instead | ⚠️ Not confirmed in Agent SDK documentation | ⚠️ Not confirmed in Agent SDK documentation |

**Key patterns:**

1. **Copilot Coding Agent** reads memory/instructions (`CLAUDE.md` as a flat file) and skills only. It does not read any Claude-specific operational configuration — sub-agents, commands, hooks, settings, or the Claude Code MCP file format are all unsupported.

2. **Claude Agent SDK (local)** reads all project-level and user-level configuration files from the Claude Code filesystem layout. This is the most complete implementation of the Claude Code configuration surface available within Copilot.

3. **Claude Agent SDK (cloud)** reads all project-level configuration from the repository (`.claude/` and `CLAUDE.md`), but cannot access user-level configuration since cloud runners do not have access to the developer's `~/.claude/` directory.

4. **Unconfirmed features**: `CLAUDE.local.md`, `.claude/rules/*.md`, and `.mcp.json` are not explicitly confirmed as supported in the Agent SDK documentation for either session type. These features are documented for Claude Code (the terminal tool) but have not been separately verified for the VS Code Agent SDK integration. Teams relying on these should test before depending on them.

**Citation:** See References [3](#11-references), [31–38](#11-references) in the References section.

[↑ Back to top](#table-of-contents)

---

### 5.7 Does the Claude Agent SDK Read Copilot Instruction Files?

The previous sections document how Copilot reads Claude instruction files (`CLAUDE.md`) — but with significant limitations. The reverse question matters equally: **when using the Claude Agent SDK, does it automatically pick up and follow existing Copilot instruction files, or does switching to the Claude Agent SDK mean your project coding standards and conventions are no longer applied?**

**The short answer: No.** The Claude Agent SDK does not read any of Copilot's instruction file formats. If you switch from the Copilot Coding Agent to the Claude Agent SDK without creating Claude-format instruction files, the Claude agent will operate without any of the project context or constraints encoded in your Copilot instructions.

#### Copilot instruction files and whether Claude reads them

Copilot uses three categories of repository instruction file. None are read by the Claude Agent SDK:

| Copilot Instruction File | What It Does | Read by Claude Agent SDK? |
|-------------------------|-------------|--------------------------|
| `.github/copilot-instructions.md` | Repository-wide instructions applied to all Copilot features in the repository | ❌ No |
| `.github/instructions/*.instructions.md` | Path-specific instructions, scoped via `applyTo` glob pattern in YAML frontmatter | ❌ No |
| `AGENTS.md` | Cross-agent instructions readable by multiple agent tools (Copilot Coding Agent, OpenAI Codex, and others) | ⚠️ Not confirmed in official Anthropic documentation |

Anthropic's official Claude Code and Agent SDK documentation exclusively documents `CLAUDE.md` (and the `.claude/` directory hierarchy) as the instruction and memory system. There is no mention of `.github/copilot-instructions.md` or `.github/instructions/*.instructions.md` in Claude Code or Agent SDK documentation. These paths are GitHub Copilot-specific and are loaded only by Copilot features (Chat, Coding Agent, Code Review, and other Copilot tools).

**Citation:** Memory. Claude Code Documentation. https://code.claude.com/docs/en/memory. Accessed 4 March 2026. Memory and system prompts. Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/modifying-system-prompts. Accessed 4 March 2026.

#### `AGENTS.md` is a partial bridge — with caveats

`AGENTS.md` is an open cross-agent standard maintained in the [openai/agents.md](https://github.com/openai/agents.md) repository. The GitHub Copilot Coding Agent reads `AGENTS.md` as an agent instructions file — equivalent in Copilot's hierarchy to `CLAUDE.md` or `GEMINI.md`. However, the official Anthropic and Claude Code documentation does not document reading `AGENTS.md` as part of the Claude Code memory system. Whether Claude Code or the VS Code Claude Agent SDK integration reads `AGENTS.md` is unconfirmed from official sources and should not be relied upon without testing in your specific setup.

Even if Claude were to support `AGENTS.md`, that still does not bridge `.github/copilot-instructions.md` — the most commonly used Copilot instruction file. Teams relying on `.github/copilot-instructions.md` must still take an explicit migration step.

#### Migration strategies

If you have existing Copilot instructions and want the Claude Agent SDK to follow the same project conventions, three approaches are available:

**Option 1 — Duplicate content in `CLAUDE.md` (recommended; unambiguously supported)**

Create a `CLAUDE.md` in the repository root containing the same instructions as your `.github/copilot-instructions.md`. This is the most explicit approach: `CLAUDE.md` is natively supported by both the Copilot Coding Agent (as a flat agent instructions file) and the Claude Agent SDK (as native project memory). Maintaining both files means each tool always reads its natively supported instruction format. Copilot Chat continues to rely on `.github/copilot-instructions.md` and does not read `CLAUDE.md` directly.

**Option 2 — Use `@import` in `CLAUDE.md` to reference the Copilot file**

Claude Code supports `@import` syntax (using `@path/to/file`) to pull in content from other files into the memory context. You can create a minimal `CLAUDE.md` that imports the Copilot instructions file, avoiding duplication:

```markdown
@.github/copilot-instructions.md
```

This approach has two caveats:

- The `@import` directive is documented for Claude Code CLI but is not explicitly confirmed as processed by the VS Code Claude Agent SDK integration. Verify that imports are resolved before relying on this approach in Agent SDK sessions.
- `.github/instructions/*.instructions.md` path-specific instruction files cannot be bridged this way: even if the import works, the `applyTo` YAML frontmatter in those files is Copilot-specific syntax that Claude does not interpret. Path-specific instructions require creating equivalent `.claude/rules/*.md` files (see below).

**Option 3 — Create `AGENTS.md` as a shared instruction source**

If you want a single instruction file readable by multiple AI coding tools, consider placing core project guidelines in an `AGENTS.md` file. Copilot Coding Agent officially reads `AGENTS.md`. You can then have `CLAUDE.md` import it or contain the same content. This approach requires testing to confirm Claude Code and the Agent SDK honour `AGENTS.md` in your environment, as this is not confirmed in official Anthropic documentation.

#### Path-specific instructions: no direct equivalent

Copilot's `.github/instructions/*.instructions.md` files use an `applyTo` YAML frontmatter field to scope instructions to specific file paths. Claude Code uses a different format for the same purpose: `.claude/rules/*.md` files with a `paths` YAML frontmatter field.

| Feature | Copilot path-specific instructions | Claude Code path-specific rules |
|---------|------------------------------------|---------------------------------|
| File location | `.github/instructions/*.instructions.md` | `.claude/rules/*.md` |
| Glob pattern field name | `applyTo` | `paths` |
| Agent exclusion field | `excludeAgent` | Not applicable |
| Read by Copilot Coding Agent | ✅ Yes | ❌ No |
| Read by Claude Agent SDK | ❌ No | ✅ Yes |
| Shared between both systems | ❌ No — incompatible paths and field names | ❌ No — incompatible paths and field names |

These files are not directly portable between systems. If you have path-specific Copilot instructions you want applied to Claude Agent SDK sessions, you need to create equivalent `.claude/rules/*.md` files with the `paths` field substituted for `applyTo`. The instruction content itself can be reused; only the YAML frontmatter key changes.

#### Summary: instruction file asymmetry between Copilot and Claude

The instruction file relationship between Copilot and the Claude Agent SDK is **asymmetric**:

- **Claude → Copilot direction:** Copilot Coding Agent reads `CLAUDE.md` as a flat instructions file (with the limitations documented in Sections 5.3–5.5). This provides some cross-compatibility: teams with an existing `CLAUDE.md` can use the Copilot Coding Agent without additional setup.

- **Copilot → Claude direction:** The Claude Agent SDK does not read any Copilot-specific instruction files (`.github/copilot-instructions.md`, `.github/instructions/*.instructions.md`). There is no automatic path from existing Copilot instructions into the Claude Agent SDK.

This means **teams primarily using Copilot who add the Claude Agent SDK must explicitly create Claude-format instruction files** (`CLAUDE.md`, and optionally `.claude/rules/*.md` for path-specific guidance). Without this step, the Claude Agent SDK has no project-level constraints applied — the concern about "unconstrained AI" is well-founded. The recommended resolution is to create a `CLAUDE.md` in the repository root.

**Citation:** Support for different types of custom instructions. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/custom-instructions-support. Accessed 4 March 2026. Memory. Claude Code Documentation. https://code.claude.com/docs/en/memory. Accessed 4 March 2026. Memory and system prompts. Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/modifying-system-prompts. Accessed 4 March 2026. Adding repository custom instructions for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions. Accessed 4 March 2026.

[↑ Back to top](#table-of-contents)

---

## 6. Agent Skills, Commands, Hooks, and Settings Support

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

### 6.6 Sub-Agents: Copilot Coding Agent vs Claude Agent SDK

It is important to distinguish between Claude Code's **skills** (`.claude/skills/`) and Claude Code's **sub-agents** (`.claude/agents/`). These are entirely separate concepts.

**Claude Code sub-agents** are defined in Markdown files stored in `.claude/agents/`. They have a different and more complex YAML frontmatter schema (including `tools`, `model`, `permissionMode`, `maxTurns`, `mcpServers`, `hooks`, `memory`, `background`, `isolation`). Sub-agents run with their own isolated context window and can be invoked via the `/agents` slash command.

**Copilot Coding Agent has no equivalent to Claude Code sub-agents.** The `.claude/agents/` directory is not read by the Copilot Coding Agent. There is no mechanism to port a Claude Code sub-agent definition directly to Copilot's native coding agent.

**The Claude Agent SDK does support filesystem-based sub-agents.** When using the Claude Agent SDK through the VS Code third-party agent integration, the SDK loads sub-agent definitions from `.claude/agents/` (project-level, shareable via git) and `~/.claude/agents/` (user-level, available in local sessions only). The `/agents` slash command in the VS Code Claude Agent SDK integration provides an interactive interface for creating and managing these sub-agents within the session. Programmatically-defined agents take precedence over filesystem-based agents with the same name.

Sub-agents defined in `.claude/agents/` in the repository are therefore fully supported in Claude Agent SDK sessions but completely ignored by the Copilot Coding Agent — making this a key difference between the two modes for teams that rely on specialised sub-agent workflows.

| Sub-Agent Feature | Copilot Coding Agent | Claude Agent SDK (VS Code local) | Claude Agent SDK (VS Code cloud) |
|------------------|---------------------|-----------------------------------|----------------------------------|
| Project sub-agents (`.claude/agents/`) | ❌ Not read | ✅ Loaded from filesystem | ✅ Loaded from filesystem |
| User sub-agents (`~/.claude/agents/`) | ❌ Not read | ✅ Loaded from filesystem | ❌ Not available in cloud |
| `/agents` slash command | ❌ Not applicable | ✅ Available for managing sub-agents | ✅ Available for managing sub-agents |
| Programmatic sub-agent definition | ❌ Not applicable | ✅ Via SDK `agents` parameter | ✅ Via SDK `agents` parameter |

**Citation:** Sub-agents. Claude Code Documentation. https://code.claude.com/docs/en/sub-agents. Accessed 28 February 2026. Subagents. Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/subagents. Accessed 3 March 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

### 6.7 Skills: Claude Agent SDK Mode vs Copilot Coding Agent

The existing sections 6.1–6.5 compare skills between the Copilot Coding Agent and Claude Code (the terminal tool). This section specifically addresses how skills work in the Claude Agent SDK delegation mode in VS Code, and where it differs from the Copilot Coding Agent.

**Similarities:** Both the Copilot Coding Agent and the Claude Agent SDK load skills from the shared `.claude/skills/` location. Basic skills (using only `name`, `description`, and a Markdown body) work identically in both modes. User skills from `~/.claude/skills/` are available in both the Copilot Coding Agent and in local Claude Agent SDK sessions.

**Key difference — `allowed-tools` SKILL.md field:** The `allowed-tools` frontmatter field in `SKILL.md` is not supported when using skills through the Agent SDK. Per the official Anthropic documentation: "The `allowed-tools` frontmatter field in SKILL.md is only supported when using Claude Code CLI directly. It does not apply when using Skills through the SDK." In Claude Agent SDK sessions, tool access is controlled through the SDK's main `allowedTools` configuration, not through per-skill frontmatter. In the Copilot Coding Agent, `allowed-tools` is also unsupported — it silently ignores the field — but this is because `allowed-tools` is a Claude Code extension to the base Agent Skills open standard, and Copilot only implements the core standard fields (`name`, `description`, and the Markdown body), not Claude Code's extensions.

**Key difference — `$ARGUMENTS` substitution:** Claude Code and the Agent SDK support dynamic argument substitution in skill content (`$ARGUMENTS`, `$ARGUMENTS[N]`, `$N`, `${CLAUDE_SESSION_ID}`). The Copilot Coding Agent does not document support for argument substitution; skills using `$ARGUMENTS` placeholders may have those treated as literal text by Copilot.

| Skill Capability | Copilot Coding Agent | Claude Agent SDK (VS Code local) | Claude Agent SDK (VS Code cloud) |
|-----------------|---------------------|-----------------------------------|----------------------------------|
| Project skills (`.claude/skills/`) | ✅ Supported | ✅ Supported | ✅ Supported |
| User skills (`~/.claude/skills/`) | ✅ Supported (Coding Agent + CLI) | ✅ Supported | ❌ Not available in cloud |
| `.github/skills/` (Copilot-specific) | ✅ Supported | ❌ Not read by Agent SDK | ❌ Not read by Agent SDK |
| `allowed-tools` SKILL.md frontmatter | ❌ Silently ignored | ❌ Not supported in SDK (documented limitation) | ❌ Not supported in SDK |
| Other Claude-specific frontmatter (`disable-model-invocation`, `model`, `context`, `hooks`) | ❌ Silently ignored | ✅ Supported (follows Claude Code behaviour) | ✅ Supported |
| `$ARGUMENTS` substitution | ⚠️ Not documented (likely treated as literal text) | ✅ Supported | ✅ Supported |

**Citation:** Skills. Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/skills. Accessed 3 March 2026. About agent skills. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-agent-skills. Accessed 28 February 2026. Skills. Claude Code Documentation. https://code.claude.com/docs/en/skills. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

### 6.8 Custom Slash Commands (`.claude/commands/`)

**What they are:** Custom slash commands are Markdown files stored in `.claude/commands/<name>.md` (project-level) or `~/.claude/commands/<name>.md` (user-level). The filename (without `.md`) becomes the command name — for example, `.claude/commands/review.md` creates the `/review` command. Commands can include optional YAML frontmatter for configuration, plain Markdown instructions, dynamic `$ARGUMENTS` placeholders, bash command execution markers, and file references. They provide a way to define reusable, named workflows that can be invoked explicitly during a session.

**Copilot Coding Agent:** Custom Claude commands (`.claude/commands/`) are not supported by the Copilot Coding Agent. Copilot has its own reusable prompt mechanism — prompt files (`.github/prompts/*.prompt.md`) in VS Code — but these are a Copilot-specific feature and are not the same as Claude commands.

**Claude Agent SDK (VS Code):** Custom commands are fully supported. When the Claude Agent SDK integration loads project filesystem settings, commands from `.claude/commands/` appear as slash commands available in the VS Code chat input. User-level commands from `~/.claude/commands/` are also available in local sessions. In cloud sessions, only project-level commands from the repository's `.claude/commands/` are accessible.

| Commands Feature | Copilot Coding Agent | Claude Agent SDK (VS Code local) | Claude Agent SDK (VS Code cloud) |
|----------------|---------------------|-----------------------------------|----------------------------------|
| Project commands (`.claude/commands/`) | ❌ Not supported | ✅ Available as slash commands | ✅ Available as slash commands |
| User commands (`~/.claude/commands/`) | ❌ Not supported | ✅ Available | ❌ Not available in cloud |
| `$ARGUMENTS` substitution in commands | ❌ Not supported | ✅ Supported | ✅ Supported |
| Bash command execution in commands | ❌ Not supported | ✅ Supported | ✅ Supported |

**Citation:** Slash Commands. Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/slash-commands. Accessed 3 March 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

### 6.9 Hooks (`.claude/settings.json`)

**What they are:** Hooks are user-defined shell commands, HTTP endpoints, or LLM prompts that execute automatically at specific points in an agent session's lifecycle. They are configured under the `hooks` key in Claude Code settings files (`.claude/settings.json` for project-level hooks shareable via git, `~/.claude/settings.json` for user-level hooks, and `.claude/settings.local.json` for local untracked hooks). Supported hook events include `PreToolUse`, `PostToolUse`, `UserPromptSubmit`, `SessionStart`, `Stop`, and others. Hooks can inspect inputs, block operations, run validators, trigger notifications, and more.

**Copilot Coding Agent:** Claude Code-format hooks (`.claude/settings.json` hooks section) are not supported by the Copilot Coding Agent. Copilot has its own separate "agent hooks" feature (currently in preview in VS Code Insiders for the native Copilot agent), but these are not the same format and are not read from `.claude/settings.json`.

**Claude Agent SDK (VS Code):** Hooks are supported. The VS Code Agent SDK integration exposes a `/hooks` slash command that allows users to "configure lifecycle hooks that execute at key points during Claude agent sessions, such as before or after tool execution." Project-level hooks defined in the repository's `.claude/settings.json` are loaded automatically. User-level hooks from `~/.claude/settings.json` are available in local sessions only. Local overrides in `.claude/settings.local.json` are available in local sessions but are gitignored and therefore not present in cloud sessions.

| Hooks Feature | Copilot Coding Agent | Claude Agent SDK (VS Code local) | Claude Agent SDK (VS Code cloud) |
|--------------|---------------------|-----------------------------------|----------------------------------|
| Project hooks (`.claude/settings.json`) | ❌ Not supported | ✅ Supported | ✅ Supported |
| User hooks (`~/.claude/settings.json`) | ❌ Not supported | ✅ Supported | ❌ Not available in cloud |
| Local hooks (`.claude/settings.local.json`) | ❌ Not supported | ✅ Supported | ❌ Not present (gitignored) |
| `/hooks` command to manage hooks | ❌ Not applicable | ✅ Available | ✅ Available |
| `PreToolUse` / `PostToolUse` hook events | ❌ Not supported | ✅ Supported | ✅ Supported |

**Citation:** Hooks. Claude Code Documentation. https://code.claude.com/docs/en/hooks. Accessed 3 March 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

### 6.10 Settings and Permissions (`.claude/settings.json`)

**What they are:** Claude Code uses `settings.json` files to configure a wide range of operational settings: tool permission rules (`allow`, `deny`), environment variables (`env`), model overrides (`model`), MCP server references, and more. Project settings are stored in `.claude/settings.json` (committed to git, shared with the team). Personal overrides are in `.claude/settings.local.json` (gitignored) or `~/.claude/settings.json` (user-level). Managed organisation-wide settings can also be deployed via policy mechanisms.

**Copilot Coding Agent:** The `.claude/settings.json` file is not read by the Copilot Coding Agent. Copilot manages its own permission model (approval prompts for tool calls, organisation policy controls) independently of Claude Code's settings format. Teams wishing to restrict tool access for Copilot sessions must use Copilot's own policy mechanisms, not Claude Code settings files.

**Claude Agent SDK (VS Code):** Project settings from `.claude/settings.json` are loaded by the Agent SDK integration. This means permissions (`allow`/`deny` tool rules), environment variables, and model overrides defined in the repository's `.claude/settings.json` apply to Claude Agent SDK sessions. User and local settings are available in local sessions only.

| Settings Feature | Copilot Coding Agent | Claude Agent SDK (VS Code local) | Claude Agent SDK (VS Code cloud) |
|----------------|---------------------|-----------------------------------|----------------------------------|
| Project permissions (`.claude/settings.json` `allow`/`deny`) | ❌ Not supported | ✅ Supported | ✅ Supported |
| Project env vars (`.claude/settings.json` `env`) | ❌ Not supported | ✅ Supported | ✅ Supported |
| Project model override (`.claude/settings.json` `model`) | ❌ Not supported | ✅ Supported | ✅ Supported |
| User settings (`~/.claude/settings.json`) | ❌ Not supported | ✅ Supported | ❌ Not available in cloud |
| Local overrides (`.claude/settings.local.json`) | ❌ Not supported | ✅ Supported | ❌ Not present (gitignored) |

**Citation:** Settings. Claude Code Documentation. https://code.claude.com/docs/en/settings. Accessed 3 March 2026.

[↑ Back to top](#table-of-contents)

---

### 6.11 MCP Server Configuration (`.mcp.json`)

**What it is:** Claude Code stores project-level MCP (Model Context Protocol) server configurations in a `.mcp.json` file at the repository root. This file specifies MCP server names, commands, arguments, and environment variables, and is designed to be committed to git so the whole team automatically has the same MCP server integrations when working in the repository. User-level and local MCP configurations are stored in `~/.claude.json`.

**Copilot Coding Agent:** The Copilot Coding Agent does not read `.mcp.json` from Claude Code. Copilot supports MCP, but MCP servers for Copilot are configured through the IDE (VS Code `settings.json`, JetBrains settings, etc.) or through GitHub.com repository settings for the cloud coding agent — not through Claude Code's `.mcp.json` format. These are separate configuration mechanisms that happen to use the same underlying MCP protocol.

**Claude Agent SDK (VS Code):** The Claude Agent SDK uses `.mcp.json` for project MCP server configuration, consistent with Claude Code. The Agent SDK is documented as providing "the same tools, agent loop, and context management that power Claude Code", and the Claude Code settings documentation lists `.mcp.json` as the project MCP configuration file. However, the Agent SDK documentation for VS Code does not explicitly confirm that `.mcp.json` is loaded from the project directory during VS Code sessions. Teams should verify MCP server availability via `.mcp.json` in both local and cloud sessions before relying on it.

| MCP Configuration Feature | Copilot Coding Agent | Claude Agent SDK (VS Code local) | Claude Agent SDK (VS Code cloud) |
|--------------------------|---------------------|-----------------------------------|----------------------------------|
| `.mcp.json` (project MCP config) | ❌ Not read — uses IDE MCP config | ⚠️ Not confirmed in Agent SDK documentation for VS Code | ⚠️ Not confirmed in documentation |
| IDE-level MCP configuration | ✅ Supported (VS Code, JetBrains, etc.) | ✅ VS Code MCP config is separate and also applies | ✅ Supported (cloud coding agent supports MCP via GitHub settings) |

**Note:** Both Copilot and the Claude Agent SDK support MCP as a protocol. The distinction is only in the *configuration file format* — Copilot does not consume `.mcp.json` from Claude Code, while the Claude Agent SDK does. Teams adding MCP servers for both modes need to configure them in both the Claude Code `.mcp.json` and the IDE MCP settings.

**Citation:** MCP. Claude Code Documentation. https://code.claude.com/docs/en/mcp. Accessed 3 March 2026. Model Context Protocol (MCP). GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/context/mcp. Accessed 3 March 2026.

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

## 8. Cost Comparison: Copilot Claude Mode vs Claude Code Standalone

This section compares the cost of using GitHub Copilot with Claude models — both as the language model in Copilot Chat and in the Claude Agent SDK delegation mode — against using Claude Code standalone with an Anthropic subscription. Comparisons are provided per request and per feature ticket, across the Haiku, Sonnet, and Opus model families.

> **Currency note:** All prices in this section are shown in New Zealand dollars (NZD) first, with US dollar (USD) equivalents in brackets. USD is the currency used in all official vendor pricing documentation. NZD equivalents are converted at the mid-market rate of **NZ$1.6974 per USD** (i.e. 1 USD = NZ$1.6974), sourced from XE.com Currency Converter at 22:14 UTC on 3 March 2026. Exchange rates fluctuate; verify the current rate before making purchasing decisions.
>
> **Citation:** XE.com Currency Converter. https://www.xe.com/currencyconverter/convert/?Amount=1&From=USD&To=NZD. Accessed 3 March 2026, 22:14 UTC.

### 8.1 GitHub Copilot Plan Allowances and Overage Pricing

Claude-powered Copilot features consume premium requests from the user's Copilot plan allowance. The following table shows the monthly allowance and overage rate for each plan.

| Plan | Monthly Cost | Premium Requests/Month | Amortised Cost/Request | Overage Rate |
|------|-------------|----------------------|----------------------|--------------|
| Free | NZ$0 (USD $0) | 50 | — | Not available |
| Pro | NZ$16.97/user (USD $10) | 300 | NZ$0.056 (USD $0.033) | NZ$0.068/request (USD $0.04) |
| Pro+ | NZ$66.20/user (USD $39) | 1,500 | NZ$0.044 (USD $0.026) | NZ$0.068/request (USD $0.04) |
| Business | NZ$32.25/user (USD $19) | 300 | NZ$0.107 (USD $0.063) | NZ$0.068/request (USD $0.04) |
| Enterprise | NZ$66.20/user (USD $39) | 1,000 | NZ$0.066 (USD $0.039) | NZ$0.068/request (USD $0.04) |

Unused premium requests expire at the end of each monthly billing period and do not carry over.

*Note: Free, Pro, and Pro+ pricing and premium request allowances are confirmed from the official GitHub plans page and billing documentation. The Business plan price ($19/user/month) is confirmed from the GitHub Copilot billing documentation. Business and Enterprise premium request allowances are listed in the official GitHub Copilot plans comparison table; always verify current values at https://docs.github.com/en/copilot/about-github-copilot/subscription-plans-for-github-copilot. Enterprise plan pricing is listed as "pricing varies" in official billing documentation and should be confirmed with GitHub Sales or on the official plans page.*

**Citation:** Plans for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/about-github-copilot/subscription-plans-for-github-copilot. Accessed 3 March 2026. About billing for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-copilot/about-billing-for-github-copilot. Accessed 3 March 2026. Requests in GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/billing/copilot-requests. Accessed 3 March 2026.

### 8.2 Claude Model Multipliers in Copilot

Each Claude model in Copilot has a premium request multiplier that scales the number of premium requests consumed per interaction. A multiplier of 1× means one user prompt consumes one premium request from the plan allowance.

| Model | Multiplier | Effective Overage Cost per Chat Prompt |
|-------|-----------|---------------------------------------|
| Claude Haiku 4.5 | 0.25× | NZ$0.017 (USD $0.010) |
| Claude Sonnet 4.5 / 4.6 | 1× | NZ$0.068 (USD $0.040) |
| Claude Opus 4.5 | 3× | NZ$0.204 (USD $0.120) |
| Claude Opus 4.6 | ~2× (not confirmed in official documentation) | ~NZ$0.136 (~USD $0.080) |

**Notes:**

- The multiplier values for Claude Haiku 4.5 (0.25×) and Claude Sonnet 4.5/4.6 (1×) are as listed in the official GitHub Copilot model multipliers table; verify current values at https://docs.github.com/en/copilot/concepts/billing/copilot-requests#model-multipliers.
- The Claude Opus 4.5 multiplier (3×) is explicitly confirmed by example in the official documentation: "Using Claude Opus 4.5 in Copilot Chat: With a 3× multiplier, one interaction counts as 3 premium requests."
- The multiplier for Claude Sonnet 4.6 is explicitly noted as "subject to change" in official documentation.
- The multiplier for Claude Opus 4.6 has not been confirmed in official published documentation; the estimate above is based on the pattern established by Opus 4.5. Always verify the current value on the GitHub Copilot model comparison page.
- Using Copilot auto model selection in VS Code provides a 10% discount on multipliers for paid plans (for example, Sonnet 4.6 would be billed at 0.9× rather than 1×).
- The Claude Agent SDK delegation mode (third-party coding agent, currently in public preview) consumes **one premium request per session with no model multiplier**, regardless of which Claude model is used. This pricing may change when the feature reaches general availability.

**Citation:** Requests in GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/billing/copilot-requests#model-multipliers. Accessed 3 March 2026. About third-party agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents. Accessed 3 March 2026. Supported AI models in GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/ai-models/supported-models. Accessed 3 March 2026.

### 8.3 Anthropic API Pricing Reference

The following table shows the Anthropic API direct rates for the equivalent Claude models, as published on the Anthropic developer platform. These rates represent the cost of calling the API directly, without a subscription wrapper.

| Model | Input Tokens | Output Tokens |
|-------|-------------|--------------|
| Claude Haiku 4.5 | NZ$1.70/MTok (USD $1.00) | NZ$8.49/MTok (USD $5.00) |
| Claude Sonnet 4.5 / 4.6 | NZ$5.09/MTok (USD $3.00) | NZ$25.46/MTok (USD $15.00) |
| Claude Opus 4.5 / 4.6 | NZ$8.49/MTok (USD $5.00) | NZ$42.44/MTok (USD $25.00) |

MTok = one million tokens. These are standard (non-cached, non-batch) rates for the Anthropic API. Prompt caching reduces input costs by up to 90% for repeated context; the Batch API offers 50% discounts for asynchronous processing. Neither optimisation is available through the Copilot subscription.

**Citation:** Pricing. Anthropic Documentation. https://docs.anthropic.com/en/about-claude/pricing. Accessed 3 March 2026.

### 8.4 Per-Request Cost: Copilot Chat vs Direct API

Copilot Chat uses one premium request per user prompt, multiplied by the model's rate. The following comparison shows the cost of a single chat interaction at a representative estimated token volume.

**Estimated token volume for a single Copilot Chat coding question:** ~2,000 input tokens + ~600 output tokens.
*This is an estimate for a typical coding Q&A prompt comprising a question, a small code sample, and a detailed response. Actual usage varies with prompt length and response complexity.*

| Model | Premium Requests Consumed | Copilot Overage Cost | Direct API Equivalent Cost | Overage : API Ratio |
|-------|--------------------------|---------------------|---------------------------|---------------------|
| Claude Haiku 4.5 | 0.25 | NZ$0.017 (USD $0.010) | ~NZ$0.008 (~USD $0.005) | ~2.0× |
| Claude Sonnet 4.6 | 1.0 | NZ$0.068 (USD $0.040) | ~NZ$0.025 (~USD $0.015) | ~2.7× |
| Claude Opus 4.5 | 3.0 | NZ$0.204 (USD $0.120) | ~NZ$0.042 (~USD $0.025) | ~4.8× |

*Direct API costs are calculated as (input tokens × input rate) + (output tokens × output rate). For Haiku 4.5: (2,000 × USD $1.00/1,000,000) + (600 × USD $5.00/1,000,000) = USD $0.002 + USD $0.003 = USD $0.005 (NZ$0.008).*

**Finding:** For a single chat interaction, Copilot's marginal (overage) pricing is approximately 2–5× higher than using the Anthropic API directly. Within the plan allowance, the amortised cost per request (NZ$0.044–NZ$0.107, USD $0.026–$0.063, depending on plan, before model multiplier) is comparable to the direct API rate, making the subscription a better overall value for regular use.

### 8.5 Per-Session Cost: Copilot Coding Agent and Claude Agent SDK vs Direct API

The Copilot Coding Agent uses **one base premium request per session**, which is then multiplied by the selected model's premium request multiplier shown above. During preview, Claude Agent SDK delegation instead consumes a flat **one premium request per session** with no multiplier applied. Unlike individual chat turns, an agentic coding session encompasses many internal LLM calls as the agent reads files, writes code, runs tests, and iterates — yet all of this compute is included in the single premium request charge to the user.

**Estimated premium requests consumed per use case:**

| Use Case | Haiku 4.5 | Sonnet 4.6 | Opus 4.5 |
|----------|-----------|-----------|----------|
| Copilot Chat: single question | 0.25 | 1 | 3 |
| Copilot Chat: feature ticket via agent mode (~8 user prompts) | 2 | 8 | 24 |
| Copilot Coding Agent: feature ticket (1 session) | 0.25 | 1 | 3 |
| Copilot Coding Agent: feature ticket + 2 steering messages | 0.75 | 3 | 9 |
| Claude Agent SDK delegation (preview, no multiplier): feature ticket | 1 | 1 | 1 |

*Note: The Claude Agent SDK delegation mode (third-party coding agent, currently in public preview) is documented as consuming one premium request per session with no model multiplier — a flat NZ$0.068 (USD $0.04) at overage rates regardless of the Claude model selected. For the Copilot Coding Agent rows, the multiplier applies to the manually selected model. If using "Auto", which currently resolves to Sonnet 4.5 (1× multiplier), the Sonnet columns are the closest equivalent. See Section 8.7 for a full discussion of model selection and billing interactions across all three products.*

**Estimated token volume for an agentic feature ticket session:** ~150,000 input tokens + ~45,000 output tokens.
*This is a representative estimate for a typical medium-complexity feature implementation. It covers the combined token usage across all internal LLM calls within a single coding agent session: code exploration (~30,000 tokens), code generation and file writes (~50,000 tokens), tool call results and debugging iterations (~50,000 tokens), and validation (~20,000 tokens). A simple bug fix is at the lower end (~30,000–50,000 total tokens); a complex multi-file refactor may exceed 300,000 tokens. The 150,000 token baseline is used throughout this section for consistency; actual costs will scale proportionally.*

| Model | Copilot Coding Agent Overage Cost | Direct API Equivalent Cost | Copilot vs API |
|-------|----------------------------------|---------------------------|----------------|
| Claude Haiku 4.5 | NZ$0.017 (USD $0.010) | ~NZ$0.637 (~USD $0.375) | ~38× cheaper |
| Claude Sonnet 4.6 | NZ$0.068 (USD $0.040) | ~NZ$1.910 (~USD $1.125) | ~28× cheaper |
| Claude Opus 4.5 | NZ$0.204 (USD $0.120) | ~NZ$3.183 (~USD $1.875) | ~16× cheaper |
| Claude Agent SDK delegation (any model, preview) | NZ$0.068 (USD $0.040) | NZ$0.637–NZ$3.183 (USD $0.375–$1.875) | 10–47× cheaper |

*Direct API costs are calculated as (150,000 × input rate) + (45,000 × output rate). For Haiku 4.5: (0.15 × USD $1.00) + (0.045 × USD $5.00) = USD $0.150 + USD $0.225 = USD $0.375 (NZ$0.637). Note: these figures assume the selected main model rate for all tokens; actual Claude Code direct API costs may be lower (Haiku subagent exploration) or higher (Opus as main model, or custom `model: opus` subagents) — see [Section 8.7](#87-model-selection-architecture-claude-code-claude-agent-sdk-and-copilot-coding-agent).*

**Key finding:** The Copilot Coding Agent's session-based pricing is dramatically more cost-effective than direct Anthropic API access for the same agentic compute. At overage rates, a typical feature implementation costs NZ$0.017–NZ$0.204 (USD $0.01–$0.12) through Copilot, compared to NZ$0.637–NZ$3.183 (USD $0.375–$1.875) for equivalent direct API usage — a 16–38× cost advantage for Copilot at overage rates, rising further within the subscription allowance.

### 8.6 Claude Code Standalone Comparison

Claude Code operates under a subscription model that measures usage via rolling 5-hour windows rather than per-request charges. The following table summarises the available Claude Code subscription tiers.

| Plan | Monthly Cost | Approx. Sonnet sessions / 5-hour window | Approx. Opus sessions / 5-hour window |
|------|-------------|----------------------------------------|---------------------------------------|
| Claude Pro | NZ$33.95 (USD $20) | ~100 | ~45 |
| Claude Max 5× | NZ$169.74 (USD $100) | ~500 | ~225 |
| Claude Max 20× | NZ$339.48 (USD $200) (verify at claude.com/pricing) | ~2,000 | ~900 |

*Session counts are approximate rolling-window estimates derived from the plan usage multipliers (5× and 20× more usage than Pro). Actual capacity depends on request complexity and context length. The Max 20× price should be verified at https://claude.com/pricing as it is not explicitly stated in official text documentation reviewed for this analysis.*

**Citation:** Pricing. Claude. https://claude.com/pricing. Accessed 3 March 2026. What is the Max plan? Anthropic Support. https://support.anthropic.com/en/articles/11049741-what-is-the-max-plan. Accessed 3 March 2026.

**Cost comparison for a typical developer workload (20 feature tickets + 100 chat questions per month, Sonnet 4.6):**

| Approach | Plan Pricing (Fixed / Variable) | Cost per Feature Ticket | Cost per Chat Question |
|----------|---------------------------------|------------------------|------------------------|
| Copilot Pro (within 300-request allowance) | NZ$16.97/month (USD $10) subscription | NZ$0.056 (USD $0.033) amortised | NZ$0.056 (USD $0.033) amortised |
| Copilot Pro (at overage) | NZ$0.068/request (USD $0.04) overage | NZ$0.068 (USD $0.040) | NZ$0.068 (USD $0.040) |
| Claude Agent SDK delegation via Copilot (preview) | NZ$0.068/session (USD $0.04) | NZ$0.068 (USD $0.040) | N/A |
| Claude Code Pro | NZ$33.95/month (USD $20) subscription | ~NZ$1.70 (~USD $1.00) amortised, 20 tickets | ~NZ$0.34 (~USD $0.20) amortised, 100 questions |
| Direct Anthropic API (Sonnet 4.6) | Usage-based (see per-ticket/per-question) | ~NZ$1.910 (~USD $1.125) | ~NZ$0.025 (~USD $0.015) |

*Copilot Pro allowance at Sonnet 4.6 (1× multiplier): 20 feature tickets using Copilot Coding Agent (20 requests — one request per session) + 100 chat questions (100 requests) = 120 premium requests, well within the 300-request monthly allowance. Note: if feature tickets are implemented via iterative Copilot Chat agent mode (~8 prompts each) rather than the Coding Agent, the count increases to 160 + 100 = 260 requests — still within allowance.*

**Key observations:**

1. **Copilot Pro offers the lowest effective cost per feature ticket and chat question** for light-to-moderate use (up to 300 premium requests per month at Sonnet 4.6). At NZ$16.97/month (USD $10/month), the typical 20-ticket + 100-question workload fits comfortably within the included allowance at an amortised NZ$0.056 (USD $0.033) per request.

2. **Claude Code Pro (NZ$33.95/month, USD $20/month) is cost-effective for intensive daily agentic use**, as the subscription covers all token consumption without per-session charges. A developer using Claude Code for several hours daily will encounter rate limits under the Pro tier, making Max tiers appropriate for sustained heavy use.

3. **Direct Anthropic API** is the most expensive approach for agentic feature work (NZ$0.637–NZ$3.183, USD $0.375–$1.875, per session at standard rates) but offers maximum flexibility: no subscription, no session limits, and access to prompt caching and Batch API discounts that are unavailable through the Copilot or Claude Code subscription wrappers.

4. **The Claude Agent SDK delegation mode (preview) benefits from a favourable flat rate** of one premium request per session with no model multiplier, making it the cheapest Copilot option per feature ticket (NZ$0.068, USD $0.040, at overage). This pricing may change at general availability.

5. **For heavy Opus usage**, costs escalate quickly through Copilot. Five hundred agentic sessions per month at Opus 4.5 (3× multiplier) consumes the full Pro+ monthly allowance of 1,500 premium requests; 600 sessions would require 1,800 premium requests — exceeding the Pro+ allowance by 300 and incurring approximately NZ$20.37 (USD $12) in overage charges. Claude Code Max may be more predictable for power users who primarily use Opus.

### 8.7 Model Selection Architecture: Claude Code, Claude Agent SDK, and Copilot Coding Agent

Claude Code, the Claude Agent SDK, and the Copilot Coding Agent each approach model selection differently. Understanding these differences matters for billing: the mechanism that determines which model runs directly affects the multiplier charged per session.

#### Claude Code's built-in subagents

Claude Code routes different types of work to specialised subagents, each potentially using a different model. The following built-in subagents are documented officially:

| Subagent | Model | Purpose |
|----------|-------|---------|
| Explore | Haiku (fast, low-latency) | Codebase search and exploration — file discovery, grep, pattern matching |
| Plan | Inherits main session model | Research during plan mode — gathers context before presenting a plan |
| General-purpose | Inherits main session model | Complex multi-step tasks requiring both exploration and code modification |
| Bash | Inherits main session model | Running terminal commands in a separate context |
| statusline-setup | Sonnet | Runs when `/statusline` is invoked to configure the status line |
| Claude Code Guide | Haiku | Answering questions about Claude Code features |

Claude Code's automatic per-operation model selection is confirmed by the documented built-in subagent assignments: the agent autonomously delegates subtasks to built-in subagents running the most appropriate model, with the model decided dynamically during execution rather than set before the session starts. Lightweight models (Haiku) are used where speed matters more than reasoning depth; the main session model handles complex multi-step work. These assignments apply to any matching operation — file exploration, bash execution, plan mode research, and so on. This is a runtime, per-operation dispatch, not a pre-session choice.

Importantly, **no built-in subagent is hardcoded to Opus**. The three "inherit" subagents (Plan, General-purpose, Bash) use the same model as the user's main session. If the user selected Sonnet, those subagents run at Sonnet rates. If the user selected Opus, all three inherit-subagents run at Opus rates — but this is a direct consequence of the user's own model choice, not an autonomous upward escalation by Claude Code. The only built-in path to Opus appearing in a direct API session is when the user explicitly chose Opus as their main model.

**Citation:** Sub-agents. Claude Code Documentation. https://docs.anthropic.com/en/docs/claude-code/sub-agents. Accessed 3 March 2026.

#### Claude Agent SDK subagent support

The Claude Agent SDK exposes the same subagent infrastructure that powers Claude Code, including support for model overrides. Custom subagents can specify `model: haiku`, `sonnet`, `opus`, or `inherit`. The built-in `general-purpose` subagent is available by default when the `Task` tool is included in `allowedTools`. Filesystem-based subagent definitions from `.claude/agents/` directories are also supported when `settingSources` includes `project`. As with Claude Code, a Claude Agent SDK session may internally dispatch Haiku for exploration subtasks and the main session model for complex reasoning — all within a single Copilot billing session.

The `model: opus` option is available for custom subagents defined by developers. When a custom subagent specifies `model: opus`, Claude will automatically trigger it whenever the task matches the subagent's description — even if the user's main session model is Sonnet. For direct API usage, this is the scenario in which Opus tokens can appear unexpectedly in a session that started on Sonnet: not from built-in dispatch, but from a project-level custom subagent with a hardcoded Opus model.

**Citation:** Subagents. Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/subagents. Accessed 3 March 2026.

#### Copilot Coding Agent: session-level auto model selection

The Copilot Coding Agent uses a fundamentally different approach. Rather than per-operation model dispatch, it resolves to **one model for the entire session** before work begins. Users can manually select a model (Claude Sonnet 4.5, Opus 4.5, Opus 4.6, or Codex variants), or choose **Auto**. Official documentation states that "Auto" is currently optimised for model availability and reduces the chance of rate limiting; as of 3 March 2026 it selects Claude Sonnet 4.5 for the Coding Agent. The selected model runs all operations for that session.

Unlike Claude Code's runtime subagent dispatch, this is a pre-session choice: Copilot resolves to a single model before the session starts, and that model's multiplier applies for the entire session.

Key constraints on "Auto" selection for the Copilot Coding Agent:

- Models with a premium request multiplier greater than 1× are **excluded** from "Auto" selection under the current availability-only model — so Opus (3×) will not be auto-selected. Whether this exclusion persists when the planned task-based selection is introduced is not yet documented.
- Auto model selection for the Coding Agent is currently **only available on Pro and Pro+ plans**
- The **10% multiplier discount** that applies to "Auto" selection in Copilot Chat does **not** apply to the Copilot Coding Agent
- Official documentation notes that auto selection will in future also take task type into account when choosing a model — currently it is availability-only

**Citation:** About Copilot auto model selection. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/auto-model-selection. Accessed 3 March 2026. Changing the AI model for GitHub Copilot coding agent. GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/changing-the-ai-model. Accessed 3 March 2026.

#### Effect on Copilot premium request billing

**Copilot Coding Agent:** billing is per-session at the multiplier of the model resolved at session start. If the user selects or Auto-selects Sonnet 4.5 (1×), the session costs one premium request. If the user manually selects Opus 4.5 (3×), it costs three premium requests. Internal operations during the session all run on that same model — there is no per-operation model switching and therefore no change to the multiplier mid-session.

**Claude Agent SDK (third-party coding agent):** GitHub's billing documentation for third-party coding agents states each session consumes one premium request. Unlike the entries for Copilot Chat and the native Copilot Coding Agent, the third-party agents entry does not include a "multiplied by the model's rate" clause, which indicates a flat rate of one premium request per session during preview — NZ$0.068 / USD $0.04 at overage — regardless of the model selected.

The Copilot Chat window does present a model selector with multipliers when using Claude models; this reflects how model-multiplied features are presented across Copilot generally, and does not by itself confirm that the multiplier applies to third-party agent sessions. The absence of the multiplier clause in the official third-party agent billing documentation is the stronger signal during preview. Billing behaviour may change at general availability.

**Internal subagent model switching (Claude Code and Claude Agent SDK):** subagent dispatching — including Haiku subagents invoked for exploration subtasks — does **not** generate additional Copilot premium requests in either product. Copilot bills the session as a single unit. The multiplier (or flat rate) is determined once per session, not once per subagent call.

*Note on direct API cost estimates: the figures in [Section 8.5](#85-per-session-cost-copilot-coding-agent-and-claude-agent-sdk-vs-direct-api) assume the user's selected main model rate for all tokens. Actual costs may be lower or higher than that baseline:*

- ***Lower** (exploration-heavy workflows on Sonnet): Explore-subagent tokens run at Haiku rates rather than Sonnet rates, reducing costs below the Sonnet row in the Section 8.5 table.*
- ***Higher** (main model is Opus): all three "inherit" subagents — Plan, General-purpose, and Bash — run at Opus rates. With the same 150,000 input + 45,000 output token volume, that yields approximately NZ$3.183 (USD $1.875) — about 1.7× more than the Sonnet baseline of NZ$1.910 (USD $1.125), as shown in the Opus row of the Section 8.5 table.*
- ***Higher** (custom `model: opus` subagents): if a project defines custom subagents with `model: opus`, those can be auto-triggered even when the main session model is Sonnet, raising costs above the Sonnet baseline in proportion to how many tokens they consume.*

*For standard usage with no custom Opus subagents, choosing Sonnet as the main model means the Sonnet row in the Section 8.5 table is the reliable ceiling for direct API costs per session.*

**Citation:** About third-party agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents. Accessed 3 March 2026. Requests in GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/billing/copilot-requests. Accessed 3 March 2026.

[↑ Back to top](#table-of-contents)

---

## 9. Summary and Key Findings

### Summary of Claude Integrations

GitHub Copilot supports Claude at two distinct levels, and conflating them leads to confusion:

1. **Claude as a language model** is the simpler integration — Copilot uses Claude as the AI engine while Copilot itself remains the orchestrator. This is available across all paid plans, works in all supported IDEs, and requires no special configuration beyond selecting a Claude model from the model picker.

2. **Claude Agent SDK delegation** is a fundamentally different integration where Anthropic's Claude Agent SDK takes over autonomous execution. This is a public preview feature, requires explicit enablement in account settings, and is only available to Pro, Pro+, Business, and Enterprise subscribers.

### Key Findings

**Delegation mode is not just "agent mode with Claude":**
The Claude Agent SDK delegation mode is architecturally distinct from using Claude as the language model in regular agent mode. When delegating, Anthropic's own harness controls tool selection, memory management, and execution flow, rather than Copilot.

**Steering is now available for delegated Claude sessions (added in VS Code v1.110):**
As of VS Code v1.110 (February 2026), mid-session steering and queuing have been added for Claude agent sessions. You can now send follow-up messages mid-conversation to alter the agent's approach, or queue up additional requests for after the current response completes. Prior to v1.110, steering was only available for the native Copilot Coding Agent.

**CLAUDE.md support differs significantly between Copilot Coding Agent and Claude Agent SDK modes:**
When using the Copilot Coding Agent, `CLAUDE.md` is treated as a flat agent instructions file — equivalent to `AGENTS.md`. When using the Claude Agent SDK delegation mode in VS Code, `CLAUDE.md` is handled natively by Anthropic's own agent harness, which supports both project-level and (in local sessions) user-level memory files, along with in-session memory management via the `/memory` and `/init` slash commands. The broader Claude Code memory hierarchy (`CLAUDE.local.md`, `.claude/rules/`, `@import` directives, auto-memory) is not explicitly documented as supported by the Agent SDK and should be verified before relying on it. Standard Copilot Chat (not delegation mode) does not support `CLAUDE.md` at all.

**Instruction file compatibility between Copilot and the Claude Agent SDK is asymmetric:**
Copilot Coding Agent reads `CLAUDE.md` (with limitations). The Claude Agent SDK does not read any Copilot-specific instruction files: `.github/copilot-instructions.md` and `.github/instructions/*.instructions.md` are Copilot-only and are ignored by the Claude Agent SDK. Teams switching from Copilot to the Claude Agent SDK must explicitly create a `CLAUDE.md` to apply project-level instructions to Claude sessions; without it, the agent operates without project-specific constraints. Teams already using Claude Code can reuse their `CLAUDE.md` in Copilot sessions without changes.

**The Claude Agent SDK exposes significantly more of the Claude Code configuration surface than the Copilot Coding Agent:**
The Copilot Coding Agent reads only `CLAUDE.md` (as flat instructions) and skills. The Claude Agent SDK (local session) reads all project-level and user-level Claude Code configuration: memory files, skills, sub-agents (`.claude/agents/`), custom commands (`.claude/commands/`), hooks (`.claude/settings.json`), settings/permissions, and MCP server configuration (`.mcp.json`). Cloud Agent SDK sessions read all project-level config from the repository but cannot access user-level (`~/.claude/`) directories. This makes the Claude Agent SDK mode the closest approximation to full Claude Code behaviour available within a Copilot subscription.

**Sub-agents, commands, and hooks are exclusive to the Claude Agent SDK mode within Copilot:**
Sub-agents (`.claude/agents/`), custom slash commands (`.claude/commands/`), and lifecycle hooks (`.claude/settings.json` hooks section) are fully supported in Claude Agent SDK sessions in VS Code but are entirely unsupported by the Copilot Coding Agent. Teams that build workflows relying on these Claude Code features should be aware that those workflows will not function in Copilot Coding Agent sessions.

**MCP configuration uses different formats for Copilot and Claude Agent SDK:**
Both Copilot and the Claude Agent SDK support MCP, but they use different configuration mechanisms. Copilot configures MCP servers through IDE settings (VS Code, JetBrains, etc.). The Claude Agent SDK is built on Claude Code, which uses `.mcp.json` as its project MCP configuration format; however, whether `.mcp.json` is loaded automatically by the VS Code Claude Agent SDK integration is not explicitly confirmed in the Agent SDK documentation. Teams integrating MCP servers for use across Copilot and Agent SDK modes should configure IDE-level MCP settings and verify `.mcp.json` behaviour separately.

**Data privacy nuances in preview:**
The zero data retention agreement between GitHub and Anthropic applies to generally available Anthropic features. Some aspects of the Claude Agent SDK that are in public preview — including tool search via the Messages API — may not be covered by this agreement.

**Local and cloud sessions available:**
Unlike some third-party agents, the Claude Agent supports both local (within VS Code on the developer's machine) and cloud (GitHub-hosted, creating a pull request) session modes, providing flexibility for both interactive and background workflows.

**Agent Skills compatibility with Claude Code:**
Skills following the Agent Skills open standard (shared between Copilot and Claude Code) can be stored in `.claude/skills/` to be automatically available to both systems. Basic skills using only `name`, `description`, and a Markdown body are fully cross-compatible without modification. Claude Code-specific frontmatter fields are ignored by Copilot rather than causing errors. Claude Code sub-agents (`.claude/agents/`) are a separate concept and are not compatible with the Copilot skill system.

**Agent skills not yet available in VS Code stable:**
At the time of writing (February 2026), agent skills are supported by the Copilot Coding Agent, GitHub Copilot CLI, and agent mode in VS Code Insiders — but not yet in the stable release of VS Code. Support for VS Code stable is listed as coming soon.

**Copilot Coding Agent dramatically underprices direct API compute for agentic sessions:**
At overage rates, a single Copilot Coding Agent feature ticket costs $0.01–$0.12 (depending on model and multiplier), compared to $0.375–$1.875 for equivalent direct Anthropic API usage. This represents a 16–38× cost advantage for Copilot. The session-based pricing model means all internal LLM calls within an agentic session are covered by a single premium request charge.

**Claude Agent SDK delegation is priced more favourably than native Copilot Coding Agent during preview:**
The Claude Agent SDK delegation mode (third-party coding agent) is documented as consuming one premium request per session with no model multiplier — a flat $0.04 at overage rates — compared to the native Copilot Coding Agent, which applies a model multiplier (for example, 3× for Opus 4.5). This pricing advantage may change at general availability.

**Copilot Pro is cost-effective for light-to-moderate Claude usage:**
A developer doing 20 feature tickets and 100 chat questions per month at Sonnet 4.6 consumes only 120 of the 300 premium requests included in the Copilot Pro plan ($10/month). Claude Code Pro ($20/month) is more appropriate for developers working intensively with Claude Code throughout the day, as its subscription covers all token usage without per-session metering.

**Citation:** About Anthropic Claude. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/anthropic-claude. Accessed 28 February 2026. About third-party agents. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents. Accessed 28 February 2026. Third-party agents in Visual Studio Code. Visual Studio Code Documentation. https://code.visualstudio.com/docs/copilot/agents/third-party-agents. Accessed 28 February 2026. Support for different types of custom instructions. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/custom-instructions-support. Accessed 28 February 2026. Hosting of models for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/ai-models/model-hosting. Accessed 28 February 2026. About agent skills. GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/about-agent-skills. Accessed 28 February 2026.

[↑ Back to top](#table-of-contents)

---

## 10. Completeness Checklist

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
- [x] Supported environments for CLAUDE.md tabulated (including Claude Agent SDK delegation mode)
- [x] Restrictions and limitations of CLAUDE.md support documented
- [x] Comparison of CLAUDE.md support between Claude Agent SDK mode and Copilot Coding Agent mode
- [x] Reverse compatibility: does Claude Agent SDK read Copilot instruction files? (Section 5.7)
- [x] Migration strategies for teams with existing Copilot instructions adding Claude Agent SDK
- [x] Master comparison table of all Claude configuration file types across Copilot modes
- [x] Sub-agents (`.claude/agents/`) support in Claude Agent SDK vs Copilot Coding Agent documented
- [x] Skills comparison between Claude Agent SDK mode and Copilot Coding Agent (including `allowed-tools` SDK limitation)
- [x] Custom slash commands (`.claude/commands/`) support comparison documented
- [x] Hooks (`.claude/settings.json`) support comparison documented
- [x] Settings and permissions (`.claude/settings.json`) support comparison documented
- [x] MCP server configuration (`.mcp.json`) support comparison documented
- [x] Subscription requirements for each feature documented
- [x] Agent skills open standard and Copilot/Claude Code shared compatibility documented
- [x] Supported environments for agent skills listed (with VS Code stable caveat)
- [x] Shared skill storage locations (`.claude/skills/`, `~/.claude/skills/`) documented
- [x] SKILL.md format differences between Copilot and Claude Code tabulated
- [x] Cross-compatibility analysis: can Claude Code skills be used in Copilot without modification?
- [x] Claude Code sub-agents distinguished from agent skills
- [x] Organisation and enterprise policy controls documented
- [x] GitHub Copilot plan allowances and overage pricing documented
- [x] Claude model multipliers for Haiku, Sonnet, and Opus documented
- [x] Anthropic API pricing reference provided for Haiku, Sonnet, and Opus
- [x] Per-request cost comparison (Copilot Chat vs direct API) provided with calculations
- [x] Per-session cost comparison (Copilot Coding Agent vs direct API) provided with calculations
- [x] Estimated premium request count per use case (chat question vs feature ticket) documented
- [x] Claude Code subscription tiers and session limits documented
- [x] Cost comparison table across Copilot plans, Claude Code, and direct API provided
- [x] Claude Agent SDK delegation pricing distinction (no model multiplier in preview) documented
- [x] Claude coding agent issue assignment workflow documented (entry points, plan requirements, differences vs Copilot Coding Agent)
- [x] All claims have citations to official documentation
- [x] All assumptions and estimates are explicitly labelled and sourced where possible
- [x] UK English used throughout

[↑ Back to top](#table-of-contents)

---

## 11. References

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

20. **Plans for GitHub Copilot.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/about-github-copilot/subscription-plans-for-github-copilot. Accessed 3 March 2026.

21. **Requests in GitHub Copilot.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/billing/copilot-requests. Accessed 3 March 2026.

22. **Supported AI models in GitHub Copilot (model multipliers).** GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/ai-models/supported-models. Accessed 3 March 2026.

23. **Pricing.** Anthropic Documentation. https://docs.anthropic.com/en/about-claude/pricing. Accessed 3 March 2026.

24. **Pricing.** Claude. https://claude.com/pricing. Accessed 3 March 2026.

25. **About billing for GitHub Copilot.** GitHub Copilot Documentation. https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-copilot/about-billing-for-github-copilot. Accessed 3 March 2026.

26. **USD to NZD Currency Converter.** XE.com. https://www.xe.com/currencyconverter/convert/?Amount=1&From=USD&To=NZD. Accessed 3 March 2026, 22:14 UTC. Rate used: 1 USD = NZ$1.6974 (mid-market rate).

27. **Sub-agents.** Claude Code Documentation. https://docs.anthropic.com/en/docs/claude-code/sub-agents. Accessed 3 March 2026.

28. **Subagents.** Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/subagents. Accessed 3 March 2026.

29. **About Copilot auto model selection.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/auto-model-selection. Accessed 3 March 2026.

30. **Changing the AI model for GitHub Copilot coding agent.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/changing-the-ai-model. Accessed 3 March 2026.

31. **Memory and system prompts.** Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/modifying-system-prompts. Accessed 3 March 2026.

32. **Skills.** Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/skills. Accessed 3 March 2026.

33. **Slash Commands.** Claude Agent SDK Documentation. https://platform.claude.com/docs/en/agent-sdk/slash-commands. Accessed 3 March 2026.

34. **Hooks.** Claude Code Documentation. https://code.claude.com/docs/en/hooks. Accessed 3 March 2026.

35. **Settings.** Claude Code Documentation. https://code.claude.com/docs/en/settings. Accessed 3 March 2026.

36. **MCP.** Claude Code Documentation. https://code.claude.com/docs/en/mcp. Accessed 3 March 2026.

37. **Model Context Protocol (MCP).** GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/context/mcp. Accessed 3 March 2026.

38. **Copilot customization cheat sheet.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/reference/customization-cheat-sheet. Accessed 3 March 2026.

39. **Asking GitHub Copilot to create a pull request.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-a-pr. Accessed 3 March 2026.

40. **Managing coding agents.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/manage-agents. Accessed 3 March 2026.

41. **About GitHub Copilot coding agent.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent. Accessed 3 March 2026.

42. **Creating custom agents for Copilot coding agent.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-custom-agents. Accessed 3 March 2026.

43. **Adding repository custom instructions for GitHub Copilot.** GitHub Copilot Documentation. https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions. Accessed 4 March 2026.

44. **February 2026 (version 1.110) — Visual Studio Code.** https://code.visualstudio.com/updates/v1_110. Accessed 8 March 2026.

[↑ Back to top](#table-of-contents)

---

## Changes in v1.110

The following changes were made to the Claude Agent SDK integration in VS Code v1.110 (February 2026):

- **Steering and queuing** (VS Code v1.110): You can now send follow-up messages mid-conversation to alter the Claude agent's approach, or queue up additional requests for after the current response completes. This feature was previously unavailable for third-party agents including Claude, and is now on a par with regular Copilot agent mode. See [Section 3.3](#33-local-vs-cloud-agent-sessions).
- **Session renaming** (VS Code v1.110): Claude agent sessions can now be renamed for easier tracking. See [Section 3.3](#33-local-vs-cloud-agent-sessions).
- **Context window rendering with compaction** (VS Code v1.110): The Claude agent now shows a context window control that indicates token usage. You can compact the conversation on demand using the `/compact` slash command or via the context window control. See [Section 3.3](#33-local-vs-cloud-agent-sessions) and [Section 3.4](#34-claude-agent-slash-commands).
- **`/compact` slash command** (VS Code v1.110): A new slash command for on-demand conversation compaction is now available within Claude agent sessions. See [Section 3.4](#34-claude-agent-slash-commands).
- **`getDiagnostics` tool** (VS Code v1.110): A new `getDiagnostics` tool has been added, allowing the Claude agent to access editor and workspace diagnostic information (problems, warnings, and errors from the Problems panel). This enables the agent to detect and respond to code issues without requiring manual sharing.
- **Significant performance improvements** (VS Code v1.110): The Claude agent integration has received unspecified performance improvements in this release.

**Citation:** February 2026 (version 1.110) — Visual Studio Code. https://code.visualstudio.com/updates/v1_110. Accessed 8 March 2026.

[↑ Back to top](#table-of-contents)

---

## Revision History

| Date | Version | Changes | Analyst |
|------|---------|---------|---------|
| 28 February 2026 | 1.0 | Initial analysis: Claude integration modes, delegation mode deep dive, CLAUDE.md support, restrictions and limitations | GitHub Copilot |
| 28 February 2026 | 1.1 | Added section 6: Agent Skills Support — open standard cross-compatibility, shared storage locations, SKILL.md format comparison, Claude Code sub-agents distinction, VS Code stable caveat | GitHub Copilot |
| 3 March 2026 | 1.2 | Added section 8: Cost Comparison — premium request allowances and overage pricing by plan, model multipliers for Haiku/Sonnet/Opus, Anthropic API pricing reference, per-request and per-session cost analysis with direct API equivalents, estimated premium requests per use case, Claude Code subscription comparison | GitHub Copilot |
| 3 March 2026 | 1.3 | Updated section 8: corrected citation URLs (Anthropic pricing page, Claude subscription pricing page), added explicit verification notes for model multiplier values and Business/Enterprise plan allowances, added caveat for Claude Max 20× price, added Reference 25 (GitHub Copilot billing documentation) | GitHub Copilot |
| 3 March 2026 | 1.4 | Updated section 8: added NZD prices (NZD first, USD in brackets) throughout all tables and prose, using mid-market rate NZ$1.6974/USD from XE.com at 22:14 UTC 3 March 2026; added currency conversion notice block; added Reference 26 (XE.com) | GitHub Copilot |
| 3 March 2026 | 1.5 | Added section 8.7: Claude Code and Claude Agent SDK internal multi-model architecture — confirmed Haiku usage for Explore and Claude Code Guide subagents, corrected "web searches" framing to codebase exploration, confirmed Claude Agent SDK shares the same subagent infrastructure, confirmed Copilot billing is unaffected (flat one premium request per session regardless of internal model selection); updated ToC; added References 27 (Claude Code sub-agents docs) and 28 (Agent SDK subagents docs) | GitHub Copilot |
| 3 March 2026 | 1.7 | Updated section 8.7: clarified when Opus may be auto-selected in Claude Code and Claude Agent SDK — no built-in subagent is hardcoded to Opus (inherit-subagents only use Opus when the user's main model is already Opus); documented that custom `model: opus` subagents can be auto-triggered as the only path to Opus appearing in a Sonnet session; updated direct API cost note in both 8.5 and 8.7 to be symmetric (costs may be lower via Haiku or higher via Opus, with ~1.7× quantification referencing the existing Section 8.5 Opus table row) | GitHub Copilot |
| 3 March 2026 | 1.8 | Added section 5.5: comparison of CLAUDE.md support in Claude Agent SDK delegation mode vs default Copilot agent mode — Claude Agent SDK natively supports project-level and user-level CLAUDE.md, /memory and /init slash commands; updated section 5.3 table with Claude Agent SDK rows for local and cloud sessions; updated section 9 key finding for CLAUDE.md; updated completeness checklist; added Reference 31 (Agent SDK memory documentation) | GitHub Copilot |
| 3 March 2026 | 1.9 | Expanded config file comparison to cover all Claude Code configuration types: added Section 5.6 (master comparison table for all config file types), renamed Section 6 to include commands/hooks/settings, updated Section 6.6 (sub-agents: added Agent SDK filesystem support), added Section 6.7 (skills Agent SDK comparison including `allowed-tools` limitation), Section 6.8 (custom commands), Section 6.9 (hooks), Section 6.10 (settings/permissions), Section 6.11 (MCP servers); added four new key findings to Section 9; expanded completeness checklist; added References 32–38 | GitHub Copilot |
| 3 March 2026 | 2.0 | Added Section 3.7: Assigning GitHub Issues to the Claude Coding Agent — confirmed the Claude coding agent supports all standard issue-assignment entry points (GitHub.com, Agents tab, VS Code cloud session); documented step-by-step workflow; added comparison table of capabilities vs Copilot Coding Agent; documented plan availability inconsistency (Pro+ / Enterprise noted in workflow docs); updated Section 4.2 feature comparison table and Section 4.3 use-case guidance; added References 39–41 | GitHub Copilot |
| 3 March 2026 | 2.1 | Corrected Section 3.7: clarified that Pro+ or Enterprise is strictly required (not just a recommendation to verify); added Troubleshooting subsection explaining that "Custom Agent" in the issue dialog creates a custom Copilot agent (`.agent.md`), not a third-party agent; fixed capability comparison table to show Pro+ / Enterprise plan requirement; added Reference 42 (create-custom-agents) | GitHub Copilot |
| 4 March 2026 | 2.2 | Revised Section 3.7 Troubleshooting: reordered checks to lead with the Partner agents toggle (most common cause for Pro+ users); expanded toggle instructions with explicit step-by-step navigation; added repository-level Copilot coding agent enablement as Step 2; demoted plan check to Step 3 | GitHub Copilot |
| 4 March 2026 | 2.3 | Added Section 5.7: Does the Claude Agent SDK Read Copilot Instruction Files? — documented that `.github/copilot-instructions.md` and `.github/instructions/*.instructions.md` are not read by the Claude Agent SDK; documented `AGENTS.md` caveat (not confirmed in official Anthropic docs); provided three migration strategies (duplicate in CLAUDE.md, @import bridge, AGENTS.md shared file); documented path-specific instruction format incompatibility (`applyTo` vs `paths`); added asymmetry summary; added Key Finding to Section 9; added Reference 43 | GitHub Copilot |
| 8 March 2026 | 2.4 | Updated with VS Code v1.110 changes (February 2026): added steering and queuing support for Claude agents (correcting prior limitation note in Section 3.3), added session renaming, context window rendering with compaction, and `getDiagnostics` tool information; added `/compact` slash command to Section 3.4 table; updated Section 4.2 feature comparison table (steering now supported); updated Section 4.3 when-to-use guidance; corrected Section 9 key finding on steering; updated Section 3.7 capability comparison table; added Changes in v1.110 section; added Reference 44 | GitHub Copilot |

[↑ Back to top](#table-of-contents)

---

## See Also

- [GitHub Copilot Chat](github-copilot-chat.md) - Main Copilot Chat analysis
- [GitHub Copilot Coding Agent](github-copilot-coding-agent.md) - Autonomous Copilot Coding Agent analysis
- [Claude Code](claude-code.md) - Anthropic's native Claude Code terminal agent

---

← [Previous: GitHub Codespaces](github-codespaces.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: GitHub Copilot Coding Agent](github-copilot-coding-agent.md) →
