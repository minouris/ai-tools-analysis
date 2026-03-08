↑ [Parent: Tool Analyses](README.md) | [Next: Claude Code](claude-code.md) →

---

# AI Coding Tools: Overview

**Analysis Date:** 25 February 2026  
**Tools Analysed:** 17 AI coding assistants and development platforms  
**Methodology:** Based on official documentation and tool analysis files in this repository

## Table of Contents

- [1. Executive Summary](#1-executive-summary)
- [2. Tools Overview](#2-tools-overview)
- [3. Feature Comparison Charts](#3-feature-comparison-charts)
  - [3.1 LLM Provider Support](#31-llm-provider-support)
  - [3.2 Model Context Protocol (MCP) Integration](#32-model-context-protocol-mcp-integration)
  - [3.3 IDE and Environment Support](#33-ide-and-environment-support)
  - [3.4 Custom Instructions and Rules](#34-custom-instructions-and-rules)
  - [3.5 Custom Prompts and Commands](#35-custom-prompts-and-commands)
  - [3.6 Pricing Models](#36-pricing-models)
  - [3.7 Core Capabilities Matrix](#37-core-capabilities-matrix)
- [4. User Reviews and Feedback](#4-user-reviews-and-feedback)
- [5. Comparative Analysis](#5-comparative-analysis)
  - [5.1 By Use Case](#51-by-use-case)
  - [5.2 By Deployment Model](#52-by-deployment-model)
  - [5.3 By Customisation Level](#53-by-customisation-level)
- [6. Key Findings](#6-key-findings)
- [7. References](#7-references)
- [Changes Since January 2026](#changes-since-january-2026)

---

## 1. Executive Summary

This document provides a comprehensive comparison of 17 AI coding tools and development platforms analysed in this repository. The tools represent different approaches to AI-assisted development, ranging from cloud-based subscription services to open-source agentic frameworks, cloud development environments, and historical platforms.

### Tools Included

1. **[Claude Code](claude-code.md)** - Terminal-based agentic coding with MCP support
2. **[Claude SDK](claude-sdk.md)** - Programmatic API access to Claude models (Python, TypeScript, Java, Go, Ruby, C#, PHP)
3. **[Azure AI Toolkit](azure-ai-toolkit.md)** - Local and Azure model management for VS Code
4. **[Continue](continue.md)** - Open-source multi-provider platform with MCP
5. **[Gemini Code Assist](gemini-code-assist.md)** - Google Cloud enterprise AI assistant with agent mode
6. **[GitHub Copilot Chat](github-copilot-chat.md)** - GitHub-native multi-mode assistant
7. **[GitHub Copilot Coding Agent](github-copilot-coding-agent.md)** - Autonomous AI developer working independently in background
8. **[GitHub Codespaces](github-codespaces.md)** - Cloud-hosted development environment platform
9. **[Roo Cline](roo-cline.md)** - Open-source autonomous VS Code agent
10. **[Amazon Q Developer](amazon-q-developer.md)** - AWS-focused AI assistant with security scanning
11. **[ChatGPT](chatgpt.md)** - Browser-based AI chat with Canvas code editing (replaced deprecated Codex)
12. **[Codeium](codeium.md)** - Free unlimited code completion and chat
13. **[Cursor](cursor.md)** - AI-first standalone code editor
14. **[Sourcegraph Cody](sourcegraph-cody.md)** - Deep codebase context via Sourcegraph
15. **[Tabnine](tabnine.md)** - Privacy-focused with local deployment options
16. **[Windsurf](windsurf.md)** - AI-first IDE with Cascade agentic assistant and in-house SWE models
17. **[OpenAI Codex](openai-codex.md)** - OpenAI's coding agent available as CLI, cloud service, and IDE extension (2026)

### Key Insights

- **Model Flexibility:** Continue and Roo Cline support 20-40+ LLM providers, whilst Amazon Q is AWS-only and Gemini Code Assist is Google-only
- **MCP Adoption:** 7 tools (Claude Code, Continue, Gemini Code Assist, GitHub Copilot Chat, OpenAI Codex, Roo Cline, Windsurf) offer full MCP support
- **Total Cost of Ownership:** Codeium ($0) and GitHub Copilot Pro ($10 USD ≈ $17 NZD) offer best value. "Free" tools like Continue/Roo Cline require separate LLM subscriptions ($20-30 USD ≈ $33-50 NZD/month) or local deployment (hardware-intensive, lower model quality)
- **IDE Coverage:** VS Code is supported by almost all tools; JetBrains by around half; Eclipse and Neovim have limited support
- **Customisation:** 8 tools support custom instruction files; 9 support custom prompts/commands

[↑ Back to top](#table-of-contents)

---

## 2. Tools Overview

### Changes Since January 2026

The following tools have notable updates since 22 January 2026. Detailed changes are documented within each tool's section below.

- **Roo Code (formerly Roo Cline):** Rebranded to Roo Code as of v3.2.0, now at v3.48.0 with new worktree selector, Smart Code Folding, and wider model support.
- **GitHub Copilot Chat:** Multi-agent development focus in VS Code v1.109, Claude Agent SDK (public preview), GPT-5.3-Codex GA, Agent Skills, Copilot Memory. In VS Code v1.110: Edit Mode deprecated, context compaction (`/compact`), fork chat sessions, session memory for plans, Claude agent improvements (steering/queuing, `/compact`, `getDiagnostics`), background agent improvements, Agent Debug panel, agent plugins, agentic browser tools, create agent customizations from chat, Explore subagent, redesigned model picker, long-distance NES.
- **GitHub Copilot Coding Agent:** Now accessible from Visual Studio 2026; SKILL.md support for agent skills. In VS Code v1.110: background agents (Copilot CLI in VS Code) now support context compaction, slash commands, and session renaming.
- **Gemini Code Assist:** Agent mode now generally available (stable) in VS Code and IntelliJ.
- **Claude Code:** Now at v2.1.47; Sonnet 4.6 added; Opus 4/4.1 deprecated; agent hooks and message queueing.
- **Cursor:** Now at v2.5 with Plugins/Marketplace, async subagents, and Cursor Blame (Enterprise).
- **Tabnine:** v5.28.0 with Context Engine GA, BYOAI, predefined slash commands, Visual Studio 2022/2026 support.
- **Continue:** Reached stable v1.0; OpenRouter provider added.
- **New: Windsurf** — AI-first IDE with Cascade agent, in-house SWE-1.5 model, MCP support, and rules/workflows system. Now at Wave 13 / v1.13.3.
- **New: OpenAI Codex (2026)** — OpenAI's new coding agent (not the deprecated 2021-2023 Codex API) available as CLI, cloud service, and IDE extension. Open-source CLI included in ChatGPT Plus/Pro/Business/Enterprise plans.

---

### Amazon Q Developer

**Type:** IDE Plugin + Chat  
**Licence:** Commercial (Free tier available, Pro tier paid)  
**Key Focus:** AWS service integration and security scanning

AWS-powered AI assistant that specialises in AWS service integration, security vulnerability scanning, and code transformation. Includes inline code completion, chat interface, and command-line support. Limited to AWS models only.

**Official Documentation:** https://aws.amazon.com/q/developer/

---

### Azure AI Toolkit

**Type:** VS Code Extension  
**Licence:** Free (Azure services charged separately)  
**Key Focus:** Local and cloud model management

Visual Studio Code extension for managing both local AI models and Azure AI services. Supports model playground, prompt experimentation, and integration with GitHub Copilot. Primarily focused on Azure ecosystem with multi-cloud model support.

**Official Documentation:** https://marketplace.visualstudio.com/items?itemName=ms-windows-ai-studio.windows-ai-studio

---

### ChatGPT

**Type:** Browser-Based Chat Interface  
**Licence:** Free tier, Plus ($20/month), Pro ($200/month)  
**Key Focus:** Conversational AI with Canvas code editing and execution

Browser-based conversational AI platform from OpenAI for code generation, debugging, and development assistance. Features Canvas (dedicated code editing interface), Python code execution, file upload/download, web browsing, and memory across sessions. Uses GPT-4o and o1 models. Replaced deprecated Codex (March 2023) as OpenAI's consumer coding platform. No IDE integration; operates standalone via chatgpt.com.

**Official Documentation:** https://help.openai.com/  
**Historical Note:** Uses models that replaced OpenAI Codex (deprecated March 2023)

---

### Claude Code

**Type:** Terminal + VS Code Extension  
**Licence:** Commercial (Claude Pro/Max subscription required)  
**Key Focus:** Agentic terminal-based coding with plugins

Terminal-based agentic coding tool from Anthropic with native Claude integration. Features skills system for reusable prompts, MCP server support, plugin architecture, and VS Code integration. Supports multiple transport protocols and cloud providers (Azure, Bedrock, Vertex AI).

**Official Documentation:** https://docs.claude.ai/docs/claude-code

#### Changes Since January 2026

- **Version:** Now at v2.1.47 (February 2026), up from v2.1.12 at time of original analysis. (Source: [Claude Code Releases](https://github.com/anthropics/claude-code/releases). Accessed 21 February 2026.)
- **Claude Sonnet 4.6:** Support added on 17 February 2026. (Source: [Claude Code Releases](https://github.com/anthropics/claude-code/releases). Accessed 21 February 2026.)
- **Model Deprecations:** Opus 4 and Opus 4.1 have been deprecated from Claude Code. (Source: [Claude Code Releases](https://github.com/anthropics/claude-code/releases). Accessed 21 February 2026.)
- **New Features:** Agent hooks and message queueing added. (Source: [Claude Code Releases](https://github.com/anthropics/claude-code/releases). Accessed 21 February 2026.)

---

### Codeium

**Type:** Multi-IDE Plugin  
**Licence:** Free for individuals, Teams/Enterprise tiers available  
**Key Focus:** Free unlimited AI assistance

Free AI-powered code completion and chat assistant with broad IDE support (VS Code, JetBrains, Eclipse, Neovim). Offers unlimited completions and chat on free tier. Uses proprietary models with unspecified LLM backend.

**Official Documentation:** https://codeium.com/

---

### Continue

**Type:** IDE Extension + CLI + Cloud Agents  
**Licence:** Open Source (Apache 2.0)  
**Key Focus:** Multi-provider flexibility with MCP

Open-source AI coding assistant supporting 40+ LLM providers including Claude, OpenAI, Ollama, Azure, and Bedrock. Features Mission Control dashboard, terminal user interface, headless CLI mode, and full MCP support. Hub-based sharing of prompts and rules.

**Official Documentation:** https://docs.continue.dev/

#### Changes Since January 2026

- **Version 1.0:** Continue has reached its stable v1.0 release. (Source: [Continue Changelog](https://changelog.continue.dev/). Accessed 21 February 2026.)
- **OpenRouter Provider:** OpenRouter has been added as a supported LLM provider, expanding the available provider count. (Source: [Continue Changelog](https://changelog.continue.dev/). Accessed 21 February 2026.)

---

### Cursor

**Type:** Standalone Code Editor  
**Licence:** Free tier available, Pro subscription for advanced features  
**Key Focus:** AI-first editor experience

AI-first code editor built on VS Code with deep AI integration. Features composer mode, chat interface, and inline suggestions. Supports Claude and OpenAI models. Custom rules via `.cursorrules` files.

**Official Documentation:** https://cursor.sh/

#### Changes Since January 2026

- **Version v2.5:** Released February 2026. (Source: [Cursor Changelog](https://cursor.com/changelog). Accessed 21 February 2026.)
- **Plugins and Marketplace:** New Plugins/Marketplace with support for skills, subagents, and hooks. Partners include Amplitude, AWS, Figma, Linear, and Stripe. (Source: [Cursor Changelog](https://cursor.com/changelog). Accessed 21 February 2026.)
- **Async Subagents:** Asynchronous subagent execution support added. (Source: [Cursor Changelog](https://cursor.com/changelog). Accessed 21 February 2026.)
- **Cursor Blame (Enterprise):** New Cursor Blame feature available for Enterprise tier. (Source: [Cursor Changelog](https://cursor.com/changelog). Accessed 21 February 2026.)

---

### Gemini Code Assist

**Type:** IDE Plugin + CLI  
**Licence:** Commercial (Standard and Enterprise editions, hourly billing)  
**Key Focus:** Enterprise Google Cloud integration with agent mode

Google Cloud's enterprise AI coding assistant using Gemini 3 models. Available in Standard and Enterprise editions with code completion, chat, and agent mode (MCP support). Features 1M token context window, Gemini CLI for terminal, and integration with Google Cloud services (Firebase, BigQuery, Apigee). Enterprise edition includes code customisation using private repositories. Supports VS Code, JetBrains IDEs, Android Studio, and Cloud environments.

**Official Documentation:** https://cloud.google.com/gemini/docs/codeassist/overview

#### Changes Since January 2026

- **Agent Mode Generally Available:** Agent mode is now widely available in both VS Code and IntelliJ as a stable release, no longer in preview. An auto-approve option has been added in IntelliJ. (Source: [Gemini Code Assist Overview](https://cloud.google.com/gemini/docs/codeassist/overview). Accessed 21 February 2026.)

---

### GitHub Copilot Chat

**Type:** Multi-IDE Plugin  
**Licence:** Subscription-based (Free, Pro, Pro+, Business, Enterprise)  
**Key Focus:** GitHub-native integration with multiple modes

AI-powered conversational interface integrated across multiple IDEs (VS Code, JetBrains, Eclipse, Xcode, Neovim) and GitHub.com. Features Ask, Agent, and Plan modes. Supports Claude, GPT, and Gemini models. Custom instructions via `.github/copilot-instructions.md` and MCP server support. Edit mode is deprecated from VS Code v1.110.

**Official Documentation:** https://docs.github.com/en/copilot

#### Changes Since January 2026

- **Multi-Agent Development:** VS Code v1.109 (released 4 February 2026) positions VS Code as the platform for multi-agent development, with multi-agent workflows as a primary focus. (Source: [GitHub Copilot in VS Code v1.109 January Release](https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/). Accessed 21 February 2026.)
- **Claude Agent SDK (Public Preview):** Claude Agent support in public preview enables delegation to Anthropic's Claude Agent SDK. (Source: [VS Code v1.109 Release Notes](https://code.visualstudio.com/updates/v1_109). Accessed 21 February 2026.)
- **New Capabilities (v1.109):** Agent orchestrations, Agent Skills, Copilot Memory, and parallel subagents. (Source: [GitHub Copilot in VS Code v1.109 January Release](https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/). Accessed 21 February 2026.)
- **GPT-5.3-Codex:** Generally available for GitHub Copilot from 9 February 2026. (Source: [GPT-5.3-Codex is now generally available for GitHub Copilot](https://github.blog/changelog/2026-02-09-gpt-5-3-codex-is-now-generally-available-for-github-copilot/). Accessed 21 February 2026.)
- **Edit Mode deprecated (v1.110):** Edit mode is hidden from the agent picker by default and officially deprecated; will be removed in v1.125. (Source: [February 2026 (version 1.110) — VS Code](https://code.visualstudio.com/updates/v1_110). Accessed 8 March 2026.)
- **Context compaction (v1.110):** Conversation history can be compacted automatically or on demand with the `/compact` slash command. (Source: [February 2026 (version 1.110) — VS Code](https://code.visualstudio.com/updates/v1_110). Accessed 8 March 2026.)
- **Fork chat sessions (v1.110):** `/fork` creates a new independent session inheriting conversation history. (Source: [February 2026 (version 1.110) — VS Code](https://code.visualstudio.com/updates/v1_110). Accessed 8 March 2026.)
- **Claude agent improvements (v1.110):** Steering/queuing, session renaming, `/compact`, `getDiagnostics` tool, and performance improvements added for Claude agents. (Source: [February 2026 (version 1.110) — VS Code](https://code.visualstudio.com/updates/v1_110). Accessed 8 March 2026.)
- **Agent Debug panel, agent plugins, agentic browser tools (v1.110):** New tooling for agent development and debugging. (Source: [February 2026 (version 1.110) — VS Code](https://code.visualstudio.com/updates/v1_110). Accessed 8 March 2026.)

---

### GitHub Copilot Coding Agent

**Type:** Cloud-Based Autonomous Agent  
**Licence:** Subscription-based (Pro, Pro+, Business, Enterprise)  
**Key Focus:** Asynchronous autonomous development

GitHub-hosted autonomous AI developer that works independently in GitHub Actions environment to complete development tasks. Assign issues to `@copilot` or delegate from VS Code. Creates pull requests, runs builds and tests, responds to review feedback. Supports custom instructions and Copilot Memory. Model selection available for Pro/Pro+ users (Claude Sonnet 4.5 default).

**Official Documentation:** https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent

#### Changes Since January 2026

- **Visual Studio 2026 Support:** The Coding Agent is now accessible from Visual Studio 2026 (released 17 February 2026), in addition to VS Code and GitHub.com. (Source: [Delegate tasks to Copilot coding agent from Visual Studio](https://github.blog/changelog/2026-02-17-delegate-tasks-to-copilot-coding-agent-from-visual-studio/). Accessed 21 February 2026.)
- **Agent Skills System:** SKILL.md files enable definition of custom agent skills. (Source: [GitHub Copilot in VS Code v1.109 January Release](https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/). Accessed 21 February 2026.)
- **Background agent improvements (v1.110):** Background agents (Copilot CLI in VS Code) now support context compaction with `/compact`, slash commands for prompt files/hooks/skills, and session renaming. (Source: [February 2026 (version 1.110) — VS Code](https://code.visualstudio.com/updates/v1_110). Accessed 8 March 2026.)

---

### GitHub Codespaces

**Type:** Cloud Development Environment  
**Licence:** Usage-based billing (free tier included)  
**Key Focus:** Consistent cloud-hosted workspaces

Cloud-hosted development environments running in Docker containers on GitHub infrastructure. Provides instant, reproducible workspaces via devcontainer configurations. Supports 2 to 32-core VMs with browser or desktop VS Code/JetBrains access. Native GitHub Copilot integration. Not an AI tool itself but a platform that supports AI coding tools.

**Official Documentation:** https://docs.github.com/en/codespaces

---

### Roo Cline

**Type:** VS Code Extension  
**Licence:** Open Source (Apache 2.0)  
**Key Focus:** Autonomous multi-mode agent

Open-source autonomous development assistant for VS Code supporting 20+ LLM providers. Features multiple operational modes (Ask, Architect, Code, Test, Debug), MCP integration via McpHub, and cross-compatible rules (`.clinerules`, `.cursorrules`, `CLAUDE.md`).

**Official Documentation:** https://docs.roocode.com/ (repository: https://github.com/RooCodeInc/Roo-Code; previously published as Roo Cline at https://github.com/RooVetGit/Roo-Cline)

#### Changes Since January 2026

- **Rebrand to Roo Code:** The extension has been officially rebranded from "Roo Cline" to "Roo Code" as of v3.2.0. The repository has moved to https://github.com/RooCodeInc/Roo-Code and official documentation is now at https://docs.roocode.com/. (Source: [Roo Code Update Notes](https://docs.roocode.com/update-notes/). Accessed 21 February 2026.)
- **Current Version:** v3.48.0 (released 17 February 2026). (Source: [Roo Code Update Notes](https://docs.roocode.com/update-notes/). Accessed 21 February 2026.)
- **New Features:** Worktree selector, Smart Code Folding (context condensation), and wider model support added since January 2026. (Source: [Roo Code Update Notes](https://docs.roocode.com/update-notes/). Accessed 21 February 2026.)

---

### Sourcegraph Cody

**Type:** IDE Plugin  
**Licence:** Free tier, Pro, and Enterprise  
**Key Focus:** Deep codebase understanding via Sourcegraph

AI coding assistant with deep codebase context powered by Sourcegraph's code intelligence. Supports VS Code, JetBrains, and Neovim. Features custom commands, autocomplete, and chat. Supports Claude, OpenAI, Gemini, and Ollama models.

**Official Documentation:** https://sourcegraph.com/cody

---

### Tabnine

**Type:** Multi-IDE Plugin  
**Licence:** Free tier, Pro, and Enterprise  
**Key Focus:** Privacy-first with local deployment

Privacy-focused AI code completion tool supporting 15+ IDEs including VS Code, JetBrains, Eclipse, and Neovim. Offers local-only execution and on-premises deployment options. Enterprise features include custom model training on organisation codebases.

**Official Documentation:** https://www.tabnine.com/

#### Changes Since January 2026

- **Version v5.28.0** (released 10 February 2026): Context Engine is now generally available. (Source: [Tabnine Release Notes](https://docs.tabnine.com/main/administering-tabnine/release-notes). Accessed 21 February 2026.)
- **BYOAI (Bring Your Own AI):** Support for bringing external models including Claude, GPT-4o, Gemini, and Codestral via BYOAI, replacing the previous proprietary-only model approach. (Source: [Tabnine Release Notes](https://docs.tabnine.com/main/administering-tabnine/release-notes). Accessed 21 February 2026.)
- **Predefined Slash Commands:** New predefined slash commands including `/code-review`. (Source: [Tabnine Release Notes](https://docs.tabnine.com/main/administering-tabnine/release-notes). Accessed 21 February 2026.)
- **Visual Studio Support:** Added support for Visual Studio 2022 and Visual Studio 2026. (Source: [Tabnine Release Notes](https://docs.tabnine.com/main/administering-tabnine/release-notes). Accessed 21 February 2026.)
- **Image Context:** Image context support added for Gemini models. (Source: [Tabnine Release Notes](https://docs.tabnine.com/main/administering-tabnine/release-notes). Accessed 21 February 2026.)

---

### Windsurf

**Type:** Standalone AI-First Code Editor  
**Licence:** Free tier, Pro ($15/month), Teams ($30/user/month), Enterprise  
**Key Focus:** Agentic AI IDE with in-house SWE models

AI-first code editor built on a VS Code fork by Windsurf Inc. (formerly Codeium). Features Cascade, an agentic AI assistant with Code and Chat modes, real-time awareness of developer actions, and the ability to remember context across sessions. Includes in-house SWE model family (SWE-1, SWE-1.5) optimised for software engineering tasks, plus support for third-party models (Claude 4 Sonnet/Opus, Gemini). Supports MCP, rules system, workflows, and JetBrains plugin. **Note:** This is a separate product from the Codeium extension (analysed separately). Windsurf was launched in November 2024 and has grown to over 1 million users.

**Official Documentation:** https://docs.windsurf.com

---

### OpenAI Codex (2026)

**Type:** CLI + Cloud Agent + IDE Extension  
**Licence:** Included with ChatGPT Plus/Pro/Business/Enterprise; API access available separately  
**Key Focus:** Cloud and local coding agent with open-source CLI

**Note:** This is the new 2026 Codex, not the deprecated Codex API (models `codex-001`, `code-davinci-002`) which was discontinued in March 2023.

OpenAI's coding agent with three delivery modes: Codex CLI (open source, Rust, npm), Codex Web/Cloud (runs tasks in isolated OpenAI-managed containers), and Codex IDE Extension (VS Code, Cursor, Windsurf, JetBrains). Included in ChatGPT Plus, Pro, Business, Edu, and Enterprise plans. Uses GPT-5.3-Codex and GPT-5.1-Codex-Mini models. Features AGENTS.md instruction system, full MCP support, OS-level sandboxing, and GitHub integration for automated code reviews.

**Official Documentation:** https://developers.openai.com/codex  
**GitHub (CLI):** https://github.com/openai/codex

---

[↑ Back to top](#table-of-contents)

---

## 3. Feature Comparison Charts

### Changes Since January 2026

Updates to feature comparison data since 22 January 2026 are noted within each relevant subsection below with detailed citations.

---

### 3.1 LLM Provider Support

| Tool | Claude | OpenAI | Ollama | Azure AI | AWS Bedrock | Google Gemini | Multi-Provider |
|------|--------|--------|--------|----------|-------------|---------------|----------------|
| **Amazon Q Developer** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | AWS only |
| **Azure AI Toolkit** | Not doc. | ✅ (via Azure) | ✅ | ✅ Native | ❌ | Not doc. | Multi-cloud |
| **ChatGPT** | ❌ | ✅ Native | ❌ | ❌ | ❌ | ❌ | OpenAI only |
| **Claude Code** | ✅ Native | ❌ | ❌ | ✅ | ✅ | ✅ (Vertex) | 4 providers |
| **Codeium** | Not doc. | Not doc. | Not doc. | Not doc. | Not doc. | Not doc. | Proprietary |
| **Continue** | ✅ | ✅ | ✅ | ✅ (Azure) | ✅ | ✅ | **40+ providers** |
| **Cursor** | ✅ | ✅ | Not doc. | Not doc. | ❌ | Not doc. | Limited |
| **Gemini Code Assist** | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ Native | Google only |
| **GitHub Copilot Chat** | ✅ + Agent SDK† | ✅ Native | ✅ (Toolkit) | ✅ (Toolkit) | ❌ | ✅ | Multi-provider |
| **GitHub Copilot Coding Agent** | ✅ (via GitHub) | ✅ (via GitHub) | ❌ | ❌ | ❌ | ✅ (via GitHub) | GitHub-managed |
| **GitHub Codespaces** | N/A | N/A | ✅ (via tools) | N/A | N/A | N/A | Via installed tools |
| **Roo Cline** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | **20+ providers** |
| **Sourcegraph Cody** | ✅ | ✅ | ✅ | Not doc. | ❌ | ✅ | Multi-provider |
| **Tabnine** | ✅ BYOAI | ✅ BYOAI | Not doc. | Not doc. | ❌ | ✅ BYOAI | Proprietary + BYOAI |
| **Windsurf** | ✅ BYOK | ✅ (via service) | ❌ | ❌ | ❌ | ✅ | Proprietary (SWE) + BYOK |
| **OpenAI Codex** | ❌ | ✅ **Native** | ❌ | ❌ | ❌ | ❌ | OpenAI only |

† Claude Agent SDK integration for GitHub Copilot Chat is in public preview (VS Code v1.109, February 2026). In VS Code v1.110, steering/queuing and additional slash commands were added to the Claude agent experience. Source: [VS Code v1.109 Release Notes](https://code.visualstudio.com/updates/v1_109). Accessed 21 February 2026. Source: [VS Code v1.110 Release Notes](https://code.visualstudio.com/updates/v1_110). Accessed 8 March 2026.

**Key Finding:** Continue and Roo Cline offer the most provider flexibility with 20-40+ integrations, whilst Amazon Q (AWS-only), Gemini Code Assist (Google-only), and OpenAI Codex (OpenAI-only) are locked to their respective ecosystems. Windsurf uses proprietary in-house SWE models by default with BYOK support for Claude 4 models.

#### Changes Since January 2026

- **GitHub Copilot Chat:** Claude Agent SDK integration added in public preview (VS Code v1.109, 4 February 2026). (Source: [GitHub Copilot in VS Code v1.109](https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/). Accessed 21 February 2026.)
- **Tabnine:** BYOAI (Bring Your Own AI) feature in v5.28.0 (10 February 2026) adds support for Claude, GPT-4o, Gemini, and Codestral, replacing the previous proprietary-only model approach. (Source: [Tabnine Release Notes](https://docs.tabnine.com/main/administering-tabnine/release-notes). Accessed 21 February 2026.)
- **New Models in GitHub Copilot:** GPT-5.3-Codex became generally available on 9 February 2026. (Source: [GPT-5.3-Codex is now generally available for GitHub Copilot](https://github.blog/changelog/2026-02-09-gpt-5-3-codex-is-now-generally-available-for-github-copilot/). Accessed 21 February 2026.)
- **New Tool — Windsurf:** In-house SWE-1.5 model family, Claude 4 Sonnet/Opus via BYOK, Gemini 3.1 Pro available. (Source: [Windsurf Models](https://docs.windsurf.com/windsurf/models). Accessed 25 February 2026.)
- **New Tool — OpenAI Codex:** Uses GPT-5.3-Codex and GPT-5.1-Codex-Mini; OpenAI models only; API key access available at standard rates. (Source: [OpenAI Codex Pricing](https://developers.openai.com/codex/pricing). Accessed 25 February 2026.)

[↑ Back to top](#table-of-contents)

---

### 3.2 Model Context Protocol (MCP) Integration

| Tool | MCP Support | Configuration Method | Transport Types | MCP Servers |
|------|-------------|---------------------|-----------------|-------------|
| **Amazon Q Developer** | ❌ Not documented | N/A | N/A | N/A |
| **Azure AI Toolkit** | ❌ Not documented | N/A | N/A | N/A |
| **ChatGPT** | ❌ Not supported | N/A | N/A | N/A |
| **Claude Code** | ✅ **Full** | YAML/JSON config | stdio, SSE, HTTP | Multiple |
| **Codeium** | ❌ Not documented | N/A | N/A | N/A |
| **Continue** | ✅ **Full** | `.continue/mcpServers/` | Multiple | Extensive |
| **Cursor** | ❌ Not documented | N/A | N/A | N/A |
| **Gemini Code Assist** | ✅ **Full** (Agent mode) | `~/.gemini/settings.json` or `mcp.json` | stdio, SSE | Multiple |
| **GitHub Copilot Chat** | ✅ **Supported** | IDE-specific config | stdio, SSE | GitHub MCP |
| **GitHub Copilot Coding Agent** | ❌ Not documented | N/A | N/A | N/A |
| **GitHub Codespaces** | ✅ (via installed tools) | Via AI tool configs | N/A | Via tools |
| **Roo Cline** | ✅ **Full** | `.roomodes` config | Multiple | McpHub |
| **Sourcegraph Cody** | ❌ Not documented | Built-in tools | N/A | N/A |
| **Tabnine** | ❌ Not documented | N/A | N/A | N/A |
| **Windsurf** | ✅ **Full** | `~/.codeium/windsurf/mcp_config.json` | stdio, Streamable HTTP, SSE | MCP Marketplace |
| **OpenAI Codex** | ✅ **Full** | `~/.codex/config.toml` | stdio, Streamable HTTP | Multiple |

**Key Finding:** 7 AI tools (Claude Code, Continue, Gemini Code Assist, GitHub Copilot Chat, OpenAI Codex, Roo Cline, Windsurf) have documented MCP support. GitHub Codespaces supports MCP indirectly through installed AI tools. MCP adoption is growing and becoming a standard for extensibility.

[↑ Back to top](#table-of-contents)

---

### 3.3 IDE and Environment Support

| Tool | VS Code | JetBrains | Eclipse | Neovim | Xcode | Terminal/CLI | Standalone |
|------|---------|-----------|---------|--------|-------|--------------|------------|
| **Amazon Q Developer** | ✅ | ✅ | Not doc. | ❌ | Not doc. | Limited | ❌ |
| **Azure AI Toolkit** | ✅ **Native** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **ChatGPT** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ **Browser/App** |
| **Claude Code** | ✅ Extension | Not doc. | ❌ | ❌ | ❌ | ✅ **Primary** | ❌ |
| **Codeium** | ✅ | ✅ | ✅ | ✅ | Not doc. | ❌ | ❌ |
| **Continue** | ✅ | ✅ | ❌ | ❌ | ❌ | ✅ TUI/Headless | ❌ |
| **Cursor** | Built-in | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ **Editor** |
| **Gemini Code Assist** | ✅ | ✅ | ❌ | ❌ | ❌ | ✅ **Gemini CLI** | Cloud native |
| **GitHub Copilot** | ✅ | ✅ | ✅ Preview | ✅ | ✅ | ✅ CLI | ❌ |
| **Roo Cline** | ✅ **Native** | ❌ | ❌ | ❌ | ❌ | Partial | Cursor compat. |
| **Sourcegraph Cody** | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ |
| **Tabnine** | ✅ | ✅ | ✅ | ✅ | Not doc. | ❌ | ❌ |
| **Windsurf** | ✅ (fork) | ✅ Plugin | ✅ (maintenance) | ✅ (maintenance) | ❌ | ❌ | ✅ **Editor** |
| **OpenAI Codex** | ✅ Extension | ✅ | ❌ | ❌ | ❌ | ✅ **CLI** | ❌ |

**IDE Support Count:**
- **VS Code:** 13/14 table entries (93%) — near-universal
- **JetBrains:** 9/14 table entries (64%)
- **Eclipse:** 4/14 table entries (29%)
- **Neovim:** 5/14 table entries (36%)
- **Terminal/CLI:** 5/14 table entries (36%)
- **Standalone:** 3/14 table entries (21%) — Cursor (editor), ChatGPT (browser/app), Windsurf (editor)

> **Note on denominator:** The IDE table contains 14 entries. Of the 17 tools analysed, GitHub Copilot Chat and GitHub Copilot Coding Agent are combined as a single "GitHub Copilot" row, and the GitHub Codespaces row is retained separately, giving 14 distinct entries in this table. Counts above reflect the 14-entry table, not the full 17-analysis count.

**Key Finding:** VS Code has near-universal support amongst IDE-integrated tools. ChatGPT, Cursor, and Windsurf operate as standalone applications. OpenAI Codex offers both a CLI and IDE extension. Windsurf's VS Code extension is in maintenance mode with new features only available in the native Windsurf Editor.

#### Changes Since January 2026

- **GitHub Copilot Coding Agent in Visual Studio 2026:** The Coding Agent is now accessible from Visual Studio 2026 (released 17 February 2026). This adds Microsoft's full IDE to the supported access methods alongside VS Code and GitHub.com. (Source: [Delegate tasks to Copilot coding agent from Visual Studio](https://github.blog/changelog/2026-02-17-delegate-tasks-to-copilot-coding-agent-from-visual-studio/). Accessed 21 February 2026.)
- **Tabnine in Visual Studio:** Tabnine v5.28.0 (10 February 2026) added support for Visual Studio 2022 and Visual Studio 2026. (Source: [Tabnine Release Notes](https://docs.tabnine.com/main/administering-tabnine/release-notes). Accessed 21 February 2026.)

[↑ Back to top](#table-of-contents)

---

### 3.4 Custom Instructions and Rules

| Tool | Instruction Files | File Location | Cross-Tool Compatibility | Organisation-Wide |
|------|-------------------|---------------|--------------------------|-------------------|
| **Amazon Q Developer** | ❌ Not documented | N/A | N/A | N/A |
| **Azure AI Toolkit** | Partial (via Copilot) | Via Copilot | GitHub Copilot | N/A |
| **ChatGPT** | ✅ Custom Instructions | Settings UI | N/A | ❌ |
| **Claude Code** | ✅ `.claude/rules/` | Project root | `CLAUDE.md` | ❌ |
| **Codeium** | ❌ Not documented | N/A | N/A | N/A |
| **Continue** | ✅ `.continue/rules/` | `.continue/` | Hub sharing | Via Hub |
| **Cursor** | ✅ `.cursorrules` | Project root | Cursor-native | ❌ |
| **Gemini Code Assist** | ❌ Not documented | N/A | N/A | Code customisation (Enterprise) |
| **GitHub Copilot** | ✅ `.github/copilot-instructions.md` | `.github/` | Multi-format | Enterprise |
| **Roo Cline** | ✅ `.clinerules` + 6 variants | Project root | `.cursorrules`, `CLAUDE.md` | ❌ |
| **Sourcegraph Cody** | ✅ `.cody/instructions` | `.cody/` | Project-level | Enterprise |
| **Tabnine** | ❌ Not documented | N/A | N/A | N/A |
| **Windsurf** | ✅ `global_rules.md` + `.windsurf/rules/` | Home dir + project | Windsurf-native | ✅ System-level (Enterprise) |
| **OpenAI Codex** | ✅ `AGENTS.md` + `AGENTS.override.md` | `~/.codex/` + project | `AGENTS.md` (standard) | ✅ System config |

**Supported Rule Formats:**
1. `.github/copilot-instructions.md` (GitHub Copilot)
2. `.clinerules` (Roo Cline)
3. `.cursorrules` (Cursor, Roo Cline)
4. `.claude/rules/` (Claude Code)
5. `.continue/rules/` (Continue)
6. `.cody/instructions` (Sourcegraph Cody)
7. `CLAUDE.md` (Claude Code, Roo Cline cross-compat)
8. `.windsurf/rules/` (Windsurf)
9. `AGENTS.md` / `AGENTS.override.md` (OpenAI Codex)

**Key Finding:** 8 out of 14 tools (57%) support custom instruction files, but formats are fragmented. Roo Cline offers the most cross-compatibility by supporting 3 different formats. Both Windsurf and OpenAI Codex support enterprise/system-level deployment of rules for organisation-wide enforcement.

[↑ Back to top](#table-of-contents)

---

### 3.5 Custom Prompts and Commands

| Tool | Storage Method | Management Interface | Sharing Mechanism | Slash Commands |
|------|----------------|---------------------|-------------------|----------------|
| **Amazon Q Developer** | ❌ Not documented | N/A | N/A | N/A |
| **Azure AI Toolkit** | Partial (Playground) | Playground UI | ❌ | ❌ |
| **ChatGPT** | Partial (History/Memory) | Web UI | Share links | ❌ |
| **Claude Code** | ✅ Skills system | `.claude/skills/` | Version control | ✅ Auto-complete |
| **Codeium** | Partial (History) | Session-based | ❌ | ✅ |
| **Continue** | ✅ Prompts + Slash | `.continue/` or Hub | Hub sharing | ✅ CLI/IDE |
| **Cursor** | ❌ Not documented | N/A | N/A | N/A |
| **Gemini Code Assist** | ❌ Not documented | N/A | N/A | ✅ Smart commands |
| **GitHub Copilot** | ✅ Prompt files | `.github/prompts/` | Via repository | ✅ Built-in |
| **Roo Cline** | ✅ Custom Modes | `.roomodes` config | Text-based | Via modes |
| **Sourcegraph Cody** | ✅ Custom Commands | JSON/settings | Enterprise org-wide | ✅ Via commands |
| **Tabnine** | ✅ Predefined Slash | Not documented | N/A | ✅ /code-review |
| **Windsurf** | ✅ Workflows | `.windsurf/workflows/` | Via repository | ✅ `/workflow-name` |
| **OpenAI Codex** | Partial (via AGENTS.md) | `~/.codex/config.toml` (profiles) | Via AGENTS.md | ✅ `/model`, `/status` |

**Key Finding:** 9 out of 14 tools (64%) support some form of custom prompts or commands. Continue and Claude Code offer the most sophisticated prompt management. Windsurf's Workflows system provides structured multi-step automation via slash commands.

#### Changes Since January 2026

- **Tabnine:** v5.28.0 (10 February 2026) introduced predefined slash commands including `/code-review`, updating the previous "Not documented" status. (Source: [Tabnine Release Notes](https://docs.tabnine.com/main/administering-tabnine/release-notes). Accessed 21 February 2026.)

[↑ Back to top](#table-of-contents)

---

### 3.6 Pricing Models

**Currency Note:** All prices are in USD. Approximate NZD conversions provided (1 USD ≈ 1.65 NZD, subject to exchange rate fluctuations).

| Tool | Free Tier | Pro/Individual | Teams/Business | Enterprise | Open Source |
|------|-----------|----------------|----------------|------------|-------------|
| **Amazon Q Developer** | ✅ Limited | $19/month (≈$31 NZD) | $25/user/month (≈$41 NZD) | Custom | ❌ |
| **Azure AI Toolkit** | ✅ (Azure costs) | Via Azure | Via Azure | Via Azure | ❌ |
| **ChatGPT** | ✅ Limited | $20/month (≈$33 NZD) (Plus) | Not available | $200/month (≈$330 NZD) (Pro) | ❌ |
| **Claude Code** | ❌ | $20/month (≈$33 NZD) (Pro) | Not separate | $30/month (≈$50 NZD) (Max) | ❌ |
| **Codeium** | ✅ **Unlimited** | ✅ Free | $12/user/month (≈$20 NZD) | Custom | ❌ |
| **Continue** | ✅ **Full** | ✅ Free | ✅ Free | ✅ Free | ✅ Apache 2.0 |
| **Cursor** | ✅ Limited | $20/month (≈$33 NZD) | Not specified | Not specified | ❌ |
| **Gemini Code Assist** | ❌ | $22/month (≈$36 NZD) Standard | Not separate | $54/month (≈$89 NZD) Enterprise | ❌ |
| **GitHub Copilot** | ✅ Limited | $10/month (≈$17 NZD) (Pro) | $19/user/month (≈$31 NZD) | $39/user/month (≈$64 NZD) | ❌ |
| **Roo Cline** | ✅ **Full** | ✅ Free | ✅ Free | ✅ Free | ✅ Apache 2.0 |
| **Sourcegraph Cody** | ✅ Limited | $9/month (≈$15 NZD) | $19/user/month (≈$31 NZD) | Custom | ❌ |
| **Tabnine** | ✅ Limited | $12/month (≈$20 NZD) | $39/user/month (≈$64 NZD) | Custom | ❌ |
| **Windsurf** | ✅ (limited credits) | $15/month (≈$25 NZD) | $30/user/month (≈$50 NZD) | Custom | ❌ |
| **OpenAI Codex** | ✅ (via ChatGPT Free) | Included with ChatGPT Plus ($20/month ≈ $33 NZD) | Included with Business | Custom (Enterprise) | ✅ CLI (Apache-2.0) |

**Note:** Gemini Code Assist pricing is based on hourly usage with monthly/yearly commitments. Approximate monthly cost calculated assuming 720 hours/month (Standard: $0.031/hr × 720 = ~$22/month with monthly commitment; Enterprise: $0.074/hr × 720 = ~$54/month with monthly commitment).

**Pricing Categories:**
- **Tool Free, LLM Required:** Continue, Roo Cline (open source, user provides LLM access)
- **All-Inclusive Free:** Codeium (includes proprietary models)
- **Freemium Model:** GitHub Copilot, Sourcegraph Cody, Cursor, Amazon Q, Tabnine
- **Subscription Required:** Claude Code (requires Claude Pro/Max subscription), Gemini Code Assist (hourly billing)

**Tool Cost Range (Pro/Individual):**
- Tool free: $0 (Continue, Roo Cline, Codeium)
- Low-cost: $9-12/month (≈$15-20 NZD) (Sourcegraph Cody, Tabnine, Codeium Teams)
- Mid-cost: $19-22/month (≈$31-36 NZD) (Amazon Q, Claude Code, Cursor, Gemini Code Assist Standard)
- High-cost: $54/month (≈$89 NZD) (Gemini Code Assist Enterprise)

**Total Cost of Ownership Considerations:**

Tools that appear "free" may require separate LLM subscriptions:

- **Continue/Roo Cline + Cloud LLM:** $0 tool + $20-30/month (≈$33-50 NZD) (Claude Pro, GPT-4) = **$20-30/month (≈$33-50 NZD) total**
- **Continue/Roo Cline + Local LLM:** $0 tool + $0 LLM = **$0/month** (but requires high-spec hardware, limited model quality)
- **Codeium:** $0 tool + $0 LLM (included) = **$0/month total**
- **GitHub Copilot Pro:** $10/month (≈$17 NZD) (includes access to Claude, GPT-4, Gemini) = **$10/month (≈$17 NZD) total**
- **Claude Code:** Requires Claude Pro ($20/month ≈ $33 NZD) or Max ($30/month ≈ $50 NZD) = **$20-30/month (≈$33-50 NZD) total**
- **Cursor Pro:** $20/month (≈$33 NZD) (includes model access) = **$20/month (≈$33 NZD) total**

**Key Finding:** Whilst Continue and Roo Cline have no tool cost, total cost of ownership matches or exceeds commercial alternatives when factoring in LLM subscriptions. Codeium offers the lowest true total cost ($0), whilst GitHub Copilot Pro offers the best value for cloud-hosted, high-quality models ($10/month ≈ $17 NZD).

[↑ Back to top](#table-of-contents)

---

### 3.7 Core Capabilities Matrix

| Tool | Code Completion | Multi-line Gen | Chat/Q&A | Refactoring | Bug Fixing | Test Gen | Doc Gen | Code Review |
|------|-----------------|----------------|----------|-------------|------------|----------|---------|-------------|
| **Amazon Q** | ✅ | ✅ | ✅ | ✅ | ✅ Security | ✅ | ✅ | ✅ Security |
| **Azure AI Toolkit** | Via Copilot | Via Copilot | ✅ Playground | ❌ | ❌ | ❌ | ❌ | ❌ |
| **ChatGPT** | ❌ | ✅ Canvas | ✅ Primary | ✅ Canvas | ✅ | ✅ | ✅ | ✅ |
| **Claude Code** | ✅ | ✅ | ✅ | ✅ Agentic | ✅ Agentic | ✅ | ✅ | ✅ |
| **Codeium** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | Not doc. |
| **Continue** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | Not doc. |
| **Cursor** | ✅ | ✅ Composer | ✅ | ✅ | ✅ | Not doc. | Not doc. | Not doc. |
| **Gemini Code Assist** | ✅ | ✅ | ✅ | ✅ Smart actions | ✅ Smart actions | ✅ | ✅ | ✅ |
| **GitHub Copilot** | ✅ | ✅ | ✅ | ✅ Agent | ✅ | ✅ | ✅ | ✅ PR reviews |
| **Roo Cline** | ✅ | ✅ | ✅ | ✅ Code mode | ✅ Debug mode | ✅ Test mode | ✅ | Not doc. |
| **Sourcegraph Cody** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | Not doc. |
| **Tabnine** | ✅ Primary | ✅ | ✅ | Not doc. | Not doc. | Not doc. | Not doc. | Not doc. |
| **Windsurf** | ✅ (Tab) | ✅ Cascade | ✅ Cascade | ✅ Cascade | ✅ Cascade | ✅ Cascade | ✅ Cascade | Not doc. |
| **OpenAI Codex** | ❌ | ✅ | ✅ | ✅ Agentic | ✅ Agentic | ✅ | ✅ | ✅ (GitHub PR) |

**Key Finding:** All tools except ChatGPT (browser-based) provide code completion. All tools support multi-line generation and chat capabilities. GitHub Copilot and Amazon Q offer specialised security scanning and PR review features. Roo Cline, Claude Code, and Gemini Code Assist emphasise agentic workflows. ChatGPT focuses on conversational coding via Canvas without IDE integration.

[↑ Back to top](#table-of-contents)

---

## 4. User Reviews and Feedback

This section consolidates third-party user reviews and experiences from multiple sources including Reddit, Stack Overflow, G2, Gartner, TrustRadius, tech blogs, and trade publications. Full details for each tool are available in their individual analysis documents.

### Overall Sentiment by Tool

| Tool | Overall Sentiment | Key Strengths | Key Weaknesses |
|------|------------------|---------------|----------------|
| **GitHub Copilot** | Positive | Productivity boost (55%), reliable autocomplete, broad IDE support | Accuracy issues, cost ($10-39/month), surface-level reviews |
| **Cursor** | Positive | Best-in-class context, multi-file refactoring | Higher cost ($20/month), IDE lock-in, edit_file bugs |
| **Continue.dev** | Positive | Open source, flexible, privacy control | Steeper learning curve, less polished UI |
| **Codeium** | Positive | Free unlimited tier, good performance | Newer tool, less mature ecosystem |
| **Tabnine** | Positive | Privacy-first, 45% productivity boost | Resource intensive, free tier limited, Vue.js issues |
| **Roo Cline** | Mixed | High autonomy, multi-role AI | Steep learning curve, heavy resources |
| **Claude Code** | Positive | Outstanding reasoning, project mapping | Verbosity, Q4 2025 bugs (mostly fixed) |
| **Sourcegraph Cody** | Positive | Deep codebase context, saves 5-6 hours/week | Suggestions quality varies, high cost ($59/month) |
| **Amazon Q** | Positive (AWS users) | AWS integration, security scanning | Only useful for AWS workflows |
| **Gemini Code Assist** | Mixed | Free (180k completions/month) | Reliability issues, performance problems |
| **ChatGPT Canvas** | Mixed | Collaborative coding interface | No IDE integration, cuts off code |
| **Azure AI Toolkit** | Positive | Unified AI workflows, model catalog | Learning curve, not for simple completion |
| **Windsurf** | Positive (with caveats) | Agentic UX, SWE models, free tier generosity | Pricing changes upset users, Cascade looping, credit limits changed |
| **OpenAI Codex** | Mixed | Open-source CLI, ChatGPT bundle, sandbox security | Rate limits frustrating, Windows support experimental, API key feature gaps |

*Source: Aggregated from reviews published 2024-2026 across multiple platforms*

### Common Praise Across Tools

**Productivity Gains:**
- GitHub Copilot users report up to 55% productivity increase and 75% higher job satisfaction
- Tabnine users report 45% productivity improvements with 90% acceptance rates for single-line completions
- Sourcegraph Cody users save 5-6 hours per week
- Multiple tools report significant time savings on boilerplate code and documentation

**Context Awareness:**
- Cursor leads with "best-in-class project context" and multi-file understanding
- Sourcegraph Cody praised for "deep understanding of entire codebases"
- Claude Code excels at "project mapping and architectural analysis"
- GitHub Copilot improving workspace-wide context (2025-2026)

**Cost Efficiency:**
- Codeium offers unlimited free tier, praised as "best free AI code completion tool"
- Continue.dev open-source model eliminates vendor lock-in
- GitHub Copilot Free tier (2000 completions/month) for students
- Gemini Code Assist free tier (180,000 completions/month)

### Common Complaints Across Tools

**Accuracy and Reliability:**
"Copilot can suggest incorrect, insecure, or inefficient code, particularly with novel algorithms, unfamiliar libraries, or loosely typed codebases. Manual review is essential." - *Sider.ai review, 2025*

- All tools experience "hallucinations" or incorrect code suggestions
- Quality varies significantly with codebase consistency
- Edge cases and niche frameworks poorly supported across most tools
- Requires careful human review to avoid introducing bugs

**Cost Concerns:**
- GitHub Copilot Pro+ at $39/month seen as expensive for freelancers
- Sourcegraph Cody Enterprise at $59/user/month a barrier for small teams
- "Free" tools (Continue, Roo Cline) require separate LLM subscriptions ($20-50/month)
- Cursor at $20/month compared to Copilot at $10/month

**Learning Curves:**
- Continue.dev requires setup and configuration knowledge
- Roo Cline has "steep learning curve" for advanced features
- Claude Code's verbosity can overwhelm new users
- Azure AI Toolkit "overkill for simple AI completion"

**Performance Issues:**
- Gemini Code Assist: Severe reliability issues reported during parts of 2025-2026, with official acknowledgement from Google
- Tabnine: Resource intensive, can slow IDE on large codebases
- Cursor: edit_file errors if not launched from project root
- ChatGPT Canvas: cuts off long files, auto-switching frustration

### Reported Bug Patterns

**Integration Issues:**
- IDE extension conflicts and crashes (GitHub Copilot, Gemini Code Assist)
- Authentication and setup problems (multiple tools)
- Content exclusion blocking legitimate use (GitHub Copilot)
- Slow syncing and indexing (Amazon Q, Claude Code)

**Context Limitations:**
- Context window "forgetfulness" in large projects (Roo Cline, Claude Code)
- Multi-file context loss (GitHub Copilot pre-2025)
- Prompt specificity issues (Sourcegraph Cody, Gemini Code Assist)
- "There was a problem getting a response" errors (Gemini Code Assist)

**Code Quality:**
- Outdated suggestions requiring extension updates
- Framework-specific bugs (Tabnine with Vue.js, Gemini with Amplify)
- Incomplete code generation requiring manual completion
- Overwrites adjacent lines unexpectedly (ChatGPT Canvas)

### Productivity Impact Analysis

**High-Impact Use Cases (Positive):**
1. **Boilerplate Generation:** All tools excel at repetitive code (95%+ satisfaction)
2. **Documentation:** Automated docstrings and README generation widely praised
3. **Test Writing:** Unit test generation saves significant time
4. **Code Explanation:** Helps with onboarding and legacy code understanding
5. **Refactoring:** Cursor and Claude Code particularly strong for large refactors

**Low-Impact or Negative Cases:**
1. **Novel Algorithms:** AI struggles with unique or complex logic
2. **Security-Critical Code:** Requires extensive manual review
3. **Niche Frameworks:** Poor performance with less common libraries
4. **Large Codebases:** Context limitations affect accuracy
5. **Creative Problem-Solving:** AI better at implementation than design

### Tool Comparison Insights

**GitHub Copilot vs Cursor:**
- Copilot: Better autocomplete, broader IDE support, lower cost
- Cursor: Superior context awareness, better refactoring, more autonomous
"Use Copilot for autocomplete and simple suggestions. Use Cursor for architectural advice and in-depth code walkthroughs." - *Reddit discussions, 2024-2026.*

**GitHub Copilot vs Continue.dev:**
- Copilot: Plug-and-play, most reliable, enterprise features
- Continue.dev: Open source, privacy control, customisable, free
"Continue.dev is lauded for 'letting me create my workflow instead of forcing one on me,' though this comes with some additional upfront effort." - *AI Tool Discovery, 2026.*

**GitHub Copilot vs Codeium:**
- Copilot: More accurate, better documentation, mature ecosystem
- Codeium: Free unlimited, good privacy options, self-hosting available
"Codeium is often praised as 'the best free AI code completion tool' for individual developers." - *Reddit discussions, 2024-2025.*

**Cursor vs Cline/Roo Cline:**
- Cursor: More autonomous, better project intelligence, higher cost
- Cline: More cautious, human-in-the-loop safety, free (requires LLM)
- Roo Cline: Maximum automation, multi-role AI, steeper learning curve
"Roo Code is the pro's tool; Cline is the 'safe default'." - *MyAIVerdict, 2025.*

**Amazon Q vs GitHub Copilot:**
- Amazon Q: AWS-specific excellence, infrastructure code, security scanning
- GitHub Copilot: General-purpose, multi-cloud, broader language support
"For teams or developers already live on AWS, Amazon Q Developer is increasingly recognised as the top productivity booster. For everyone else (multi-cloud, front-end, cross-language), Copilot remains the 'gold standard'." - *Multiple sources, 2024-2026.*

### Community Recommendations (2024-2026)

**For Individual Developers:**
1. **Free/Budget:** Codeium or Continue.dev
2. **Best Overall:** GitHub Copilot Pro ($10/month)
3. **AWS Focus:** Amazon Q Developer
4. **Privacy:** Tabnine or Continue.dev with local models

**For Teams:**
1. **Enterprise (General):** GitHub Copilot Enterprise
2. **AWS-Heavy:** Amazon Q Developer
3. **Large Codebases:** Sourcegraph Cody or Cursor
4. **Privacy/Compliance:** Tabnine Enterprise or Continue.dev

**For Specific Workflows:**
1. **Deep Refactoring:** Cursor
2. **Architectural Planning:** Claude Code
3. **Learning/Onboarding:** GitHub Copilot or Gemini (free tier)
4. **Autonomous Coding:** Roo Cline or Claude Code

### Citation Summary

This section consolidates reviews and user experiences from:
- Reddit (r/programming, r/vscode, r/webdev, tool-specific subreddits): 2024-2026
- Stack Overflow discussions and questions: 2024-2026
- G2, Gartner, TrustRadius review platforms: 2024-2026
- Tech publications (Sider.ai, Bito, Digital Ocean, Zapier, etc.): 2024-2026
- YouTube reviews and community forums: 2024-2026
- Hacker News and Slashdot discussions: 2024-2026

Full citations and detailed reviews are available in individual tool analysis documents.

[↑ Back to top](#table-of-contents)

---

## 5. Comparative Analysis

### Changes Since January 2026

The "Best for Agentic Workflows" recommendation has been updated to include GitHub Copilot Coding Agent following VS Code v1.109 (February 2026) positioning VS Code as the platform for multi-agent development. See [Best for Agentic Workflows](#best-for-agentic-workflows) for details.

---

### 5.1 By Use Case

#### Best for Individual Developers

**Recommendation: Codeium (lowest total cost) or GitHub Copilot Pro (best value)**

- **Codeium:** Free unlimited completions and chat with proprietary models included. No LLM subscription required. **Total cost: $0/month**
- **GitHub Copilot Pro:** $10/month (≈$17 NZD) includes access to multiple high-quality models (Claude, GPT-4, Gemini). **Total cost: $10 USD (≈$17 NZD)/month**
- **Continue/Roo Cline:** Free tool but requires separate LLM subscription ($20-30 USD ≈ $33-50 NZD/month for Claude/GPT-4) or local models (hardware-intensive, lower quality). **Total cost: $0-30 USD (≈$0-50 NZD)/month**

**Rationale:** Codeium offers genuinely free AI assistance with no hidden costs. GitHub Copilot Pro provides the best value for cloud-hosted, high-quality models. Continue and Roo Cline appear free but require LLM access, making total cost comparable to commercial alternatives unless using local models.

---

#### Best for AWS Environments

**Recommendation: Amazon Q Developer**

- **Strengths:** Native AWS service integration, AWS-specific code generation, security scanning for AWS resources
- **Limitations:** AWS-only (no multi-cloud support), requires AWS ecosystem

**Rationale:** Purpose-built for AWS development workflows with deep service integration.

---

#### Best for Privacy-Sensitive Organisations

**Recommendation: Tabnine Enterprise or Continue (self-hosted)**

- **Tabnine:** Local-only execution, on-premises deployment, custom model training on organisation code
- **Continue:** Open source, self-hostable, bring-your-own-models (including local Ollama)

**Rationale:** Both support local-only execution preventing code transmission to external services.

---

#### Best for Multi-Provider Flexibility

**Recommendation: Continue or Roo Cline**

- **Continue:** 40+ provider support, open source, MCP integration, Hub sharing
- **Roo Cline:** 20+ provider support, multiple operational modes, cross-compatible rules

**Rationale:** Highest number of supported LLM providers, allowing switching between models based on task requirements.

**Cost Consideration:** Whilst tools are free, each provider requires separate subscription or API access. Total monthly cost depends on chosen provider(s): $0 for local models (Ollama), $20-30 USD (≈$33-50 NZD)/month for cloud providers (Claude, GPT-4), or pay-per-use API pricing.

---

#### Best for Agentic Workflows

**Recommendation: Claude Code or Roo Cline**

- **Claude Code:** Terminal-based autonomous agent, skills system, MCP support, plugin architecture
- **Roo Cline:** Multiple operational modes (Ask, Architect, Code, Test, Debug), MCP via McpHub

**Rationale:** Both designed for autonomous task execution with minimal manual intervention.

#### Changes Since January 2026

**GitHub Copilot Coding Agent** has become a strong option for background autonomous development tasks. VS Code v1.109 (4 February 2026) explicitly positions VS Code as "the home for multi-agent development", with agent orchestrations, Agent Skills (SKILL.md files), and parallel subagents. The Coding Agent can be delegated tasks from VS Code, GitHub.com, and now Visual Studio 2026 (17 February 2026). (Sources: [VS Code v1.109 Release Notes](https://code.visualstudio.com/updates/v1_109); [Delegate tasks from Visual Studio](https://github.blog/changelog/2026-02-17-delegate-tasks-to-copilot-coding-agent-from-visual-studio/). Accessed 21 February 2026.)

---

#### Best for GitHub Integration

**Recommendation: GitHub Copilot**

- **Strengths:** Native GitHub.com integration (Enterprise), PR reviews, multiple modes (Ask, Edit, Agent, Plan)
- **Limitations:** Subscription required, primarily GitHub-centric

**Rationale:** Deepest integration with GitHub platform and workflows.

---

#### Best for Enterprise Deployment

**Recommendation: GitHub Copilot Enterprise or Sourcegraph Cody Enterprise**

- **GitHub Copilot:** Organisation-wide custom instructions, GitHub.com integration, compliance features
- **Sourcegraph Cody:** Organisation-wide commands, deep codebase context via Sourcegraph, custom models

**Rationale:** Both offer enterprise-specific features including organisation-wide customisation and compliance controls.

---

### 5.2 By Deployment Model

#### Cloud-Only Services
- **Amazon Q Developer** (AWS infrastructure)
- **Cursor** (proprietary cloud)
- **Codeium** (proprietary cloud)

**Trade-offs:** Easier setup, no infrastructure management, but requires internet connectivity and code transmission to external services.

---

#### Hybrid (Cloud + Local Options)
- **GitHub Copilot** (cloud with Ollama support via AI Toolkit)
- **Azure AI Toolkit** (cloud and local models)
- **Continue** (multi-provider including local)
- **Roo Cline** (multi-provider including local)
- **Sourcegraph Cody** (cloud with Ollama support)

**Trade-offs:** Flexibility to choose deployment model based on privacy and cost requirements.

---

#### Local-First Options
- **Tabnine** (local-only execution available)
- **Continue** (with Ollama)
- **Roo Cline** (with Ollama)

**Trade-offs:** Maximum privacy and control, but requires local infrastructure and model management.

---

### 5.3 By Customisation Level

#### Minimal Customisation
- **Tabnine** (primarily completion-focused)
- **Cursor** (`.cursorrules` only)
- **Amazon Q** (no documented customisation)
- **Codeium** (no documented customisation)

**Use Case:** Quick setup, standardised workflows, minimal configuration overhead.

---

#### Moderate Customisation
- **GitHub Copilot** (custom instructions, prompts, MCP)
- **Sourcegraph Cody** (custom commands, instructions)
- **Azure AI Toolkit** (model configuration)

**Use Case:** Project-specific customisation whilst maintaining standardised base functionality.

---

#### High Customisation
- **Continue** (rules, prompts, MCP servers, Hub integration)
- **Claude Code** (skills, rules, plugins, MCP servers)
- **Roo Cline** (custom modes, rules, MCP via McpHub)

**Use Case:** Complex workflows, specialised domains, organisation-specific requirements, extensive automation.

[↑ Back to top](#table-of-contents)

---

## 6. Key Findings

### Changes Since January 2026

**Multi-Agent Development Platforms:** VS Code v1.109 (4 February 2026) explicitly positions VS Code as "the home for multi-agent development". Features added include agent orchestrations, parallel subagents, Agent Skills (SKILL.md files), and Copilot Memory. (Source: [VS Code v1.109 Release Notes](https://code.visualstudio.com/updates/v1_109). Accessed 21 February 2026.)

**Claude Agent SDK Integration:** Claude Agent support in public preview in VS Code expands the agent ecosystem by enabling delegation to Anthropic's Claude Agent SDK. (Source: [GitHub Copilot in VS Code v1.109 January Release](https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/). Accessed 21 February 2026.)

**Open-Source Ecosystem Maturity:** The Roo Cline rebrand to "Roo Code" (v3.2.0) and Continue reaching v1.0 reflect increasing maturity of open-source agentic tooling.

---

### Market Landscape

1. **Consolidation Around Key Models:** Claude and OpenAI dominate LLM provider integration, with Ollama growing as local alternative
2. **VS Code Dominance:** VS Code is supported by almost all tools analysed (13 of 14 IDE table entries); other IDEs have lower coverage (JetBrains ~64%, Eclipse ~29%)
3. **Emerging MCP Standard:** 40% of tools support MCP, suggesting growing standardisation for extensibility
4. **Fragmented Instruction Formats:** 6 different instruction file formats exist, limiting cross-tool compatibility
5. **Open Source Growth:** 2 major open-source options (Continue, Roo Cline) provide full-featured alternatives to commercial tools

### User Experience Insights (Based on Third-Party Reviews)

**Consistent Patterns Across All Tools:**

1. **Productivity Gains Are Real:** Users consistently report 40-55% productivity improvements, with GitHub Copilot (55%), Tabnine (45%), and Sourcegraph Cody (5-6 hours/week saved) leading reported gains

2. **Accuracy Requires Vigilance:** All tools experience "hallucinations" and generate incorrect code. Manual review is essential regardless of tool choice
   "Copilot can suggest incorrect, insecure, or inefficient code, particularly with novel algorithms, unfamiliar libraries, or loosely typed codebases. Manual review is essential." - *Multiple user reviews, 2024-2026.*

3. **Context Awareness Varies Dramatically:** Cursor leads with "best-in-class project context," followed by Sourcegraph Cody's "deep codebase understanding." Traditional autocomplete tools lag significantly in multi-file scenarios

4. **Cost vs Value Trade-offs:**
   - Users consistently praise Codeium's unlimited free tier
   - GitHub Copilot seen as "best value" at $10/month
   - Cursor at $20/month justified only for power users needing superior context
   - "Free" tools (Continue, Roo Cline) require separate LLM subscriptions, making total cost $20-50/month

5. **Bug Patterns:** Integration issues (IDE crashes, conflicts), context loss, performance degradation on large codebases, and framework-specific bugs common across all tools

**Tool-Specific User Feedback:**

- **GitHub Copilot:** "Industry standard" for reliability but criticized for surface-level reviews and tiered pricing
- **Cursor:** Praised for refactoring but "edit_file bugs" frustrate users requiring specific workflow
- **Continue.dev:** "Maximum control" appreciated by power users but "steeper learning curve" deters casual users
- **Codeium:** "Best free option" but "less mature ecosystem" compared to Copilot
- **Tabnine:** "Privacy-first" approach valued but "resource intensive" on older hardware
- **Claude Code:** "Outstanding reasoning" praised but Q4 2025 bugs damaged trust (mostly resolved)
- **Gemini Code Assist:** Free tier attractive but "completely unusable during some weeks" undermines reliability
- **Amazon Q:** "Top productivity booster for AWS" but "only useful for AWS workflows"
- **Roo Cline:** "Pro's tool" for maximum automation but "steep learning curve"
- **ChatGPT Canvas:** "Collaborative coding" interesting but "no IDE integration" limits professional use

**Key User Decision Factors (in priority order):**

1. **Reliability over features** (consistent suggestions more valuable than cutting-edge capabilities)
2. **Cost** (free tools gaining adoption despite requiring separate LLM subscriptions)
3. **Context awareness** (multi-file understanding increasingly essential for complex projects)
4. **Privacy** (local deployment or self-hosting critical for sensitive codebases)
5. **IDE support** (VS Code universal, but JetBrains and CLI access matter for some workflows)

**Common User Recommendations (Reddit, Forums, 2024-2026):**

- **Starting out?** GitHub Copilot or Codeium (lowest friction, reliable)
- **AWS-heavy?** Amazon Q (specialized for AWS, significant time savings)
- **Privacy concerns?** Tabnine or Continue.dev (local deployment options)
- **Large codebase?** Cursor or Sourcegraph Cody (superior context awareness)
- **Maximum control?** Continue.dev or Roo Cline (open source, customizable)
- **Budget constrained?** Codeium (unlimited free) or GitHub Copilot Free tier
- **Learning/experimenting?** Gemini Code Assist free tier (180k completions/month)

### Feature Gaps

**Across All Tools:**
- Limited Eclipse support (only 3/10 tools)
- Inconsistent test generation capabilities (not documented for several tools)
- Code review features limited to specific tools (GitHub Copilot, Amazon Q, Claude Code)
- Organisation-wide customisation limited to enterprise tiers

**Tool-Specific Gaps:**
- **Amazon Q:** AWS-only, no multi-cloud support
- **Azure AI Toolkit:** Limited to model management, lacks full coding features
- **Tabnine:** Documentation gaps for advanced features
- **Codeium:** Proprietary models, unclear LLM backend

### Pricing Insights

**Currency Note:** All prices are in USD. Approximate NZD conversions provided in parentheses (1 USD ≈ 1.65 NZD, subject to exchange rate fluctuations).

**Free Options (Tool Cost Only):**
- **Tool Free, LLM Required:** Continue, Roo Cline (open source, user provides LLM access)
- **All-Inclusive Free:** Codeium (proprietary models included)
- **Freemium:** GitHub Copilot Free tier (limited features)

**Total Cost of Ownership Analysis:**

When factoring in LLM access costs, the true pricing picture changes significantly:

| Tool | Tool Cost (USD) | LLM Cost (USD) | Total Monthly Cost |
|------|-----------------|----------------|-------------------|
| Codeium | $0 | $0 (included) | **$0** |
| Continue/Roo Cline (local) | $0 | $0 | **$0** (requires high-spec hardware) |
| GitHub Copilot Pro | $10 (≈$17 NZD) | $0 (included) | **$10 (≈$17 NZD)** |
| Continue/Roo Cline (cloud) | $0 | $20-30 (≈$33-50 NZD) | **$20-30 (≈$33-50 NZD)** |
| Cursor Pro | $20 (≈$33 NZD) | $0 (included) | **$20 (≈$33 NZD)** |
| Claude Code | $0 (tool) | $20-30 (≈$33-50 NZD) (Claude Pro/Max) | **$20-30 (≈$33-50 NZD)** |
| Amazon Q Pro | $19 (≈$31 NZD) | $0 (included) | **$19 (≈$31 NZD)** |
| Sourcegraph Cody Pro | $9 (≈$15 NZD) | Varies | **$9+ (≈$15+ NZD)** |
| Tabnine Pro | $12 (≈$20 NZD) | $0 (included) | **$12 (≈$20 NZD)** |

**Cost Considerations:**
- **Codeium** offers the only truly free option with proprietary models included
- **GitHub Copilot Pro** offers best value for high-quality cloud models at $10 USD (≈$17 NZD)/month
- **Continue and Roo Cline** appear free but require LLM subscriptions ($20-30 USD ≈ $33-50 NZD/month) or local deployment
- **Local LLM deployment** eliminates ongoing costs but requires:
  - High-specification hardware (16GB+ RAM, powerful GPU for optimal performance)
  - Reduced model quality compared to cloud-hosted alternatives (Claude, GPT-4)
  - Technical expertise for setup and maintenance
- Enterprise features (org-wide customisation) typically require top-tier subscriptions ($19-39 USD ≈ $31-64 NZD/user/month)

**Value Assessment:**
- **Best Total Value:** GitHub Copilot Pro ($10 USD ≈ $17 NZD/month for multiple high-quality models)
- **Lowest Total Cost:** Codeium ($0/month, models included)
- **Most Flexible:** Continue/Roo Cline (40+ providers, but cost varies by choice)
- **Hidden Costs:** "Free" tools requiring separate LLM access can exceed commercial all-in-one solutions

### Technology Trends

**MCP Adoption:** Model Context Protocol support growing but not universal. Tools with MCP (Claude Code, Continue, Gemini Code Assist, GitHub Copilot Chat, OpenAI Codex, Roo Cline, Windsurf) demonstrate extensibility advantages.

**Multi-Provider Support:** Increasing recognition that single-model approach limits flexibility. Continue (40+) and Roo Cline (20+) lead in provider diversity.

**Agentic Workflows:** Shift from completion-only to autonomous agents evident in Claude Code, Roo Cline, and GitHub Copilot Agent mode.

**Cross-Tool Compatibility:** Emerging standards like `CLAUDE.md` and `.cursorrules` enable sharing of instructions across tools, though adoption remains limited.

### Selection Criteria Summary

| Priority | Recommended Tool(s) | Rationale |
|----------|---------------------|-----------|
| **Lowest Total Cost** | Codeium | $0/month (models included) |
| **Best Value** | GitHub Copilot Pro | $10/month for multiple high-quality models |
| **AWS Integration** | Amazon Q Developer | Native AWS service integration |
| **Privacy/Compliance** | Tabnine Enterprise, Continue (local) | Local-only execution options |
| **Provider Flexibility** | Continue, Roo Cline | 20-40+ provider support (requires LLM subscriptions) |
| **GitHub Integration** | GitHub Copilot | Native platform integration |
| **Enterprise Features** | GitHub Copilot Enterprise, Sourcegraph Cody | Org-wide customisation |
| **Autonomous Agents** | Claude Code, Roo Cline | Agentic workflow focus |
| **IDE Breadth** | Codeium, GitHub Copilot, Tabnine | Widest IDE support |

[↑ Back to top](#table-of-contents)

---

## 7. References

### Tool Documentation

1. **Amazon Q Developer.** AWS. https://aws.amazon.com/q/developer/
2. **Azure AI Toolkit for Visual Studio Code.** Microsoft. https://marketplace.visualstudio.com/items?itemName=ms-windows-ai-studio.windows-ai-studio
3. **Claude Code.** Anthropic. https://docs.claude.ai/docs/claude-code
4. **Codeium.** Codeium. https://codeium.com/
5. **Continue.** Continue Dev. https://docs.continue.dev/
6. **Cursor.** Cursor. https://cursor.sh/
7. **GitHub Copilot.** GitHub. https://docs.github.com/en/copilot
8. **OpenAI Codex (2026).** OpenAI. https://developers.openai.com/codex
9. **Roo Cline.** RooVetGit. https://github.com/RooVetGit/Roo-Cline
10. **Sourcegraph Cody.** Sourcegraph. https://sourcegraph.com/cody
11. **Tabnine.** Tabnine. https://www.tabnine.com/
12. **Windsurf.** Windsurf Inc. https://docs.windsurf.com

### Analysis Files

All detailed tool analyses are available in this directory:

- [Amazon Q Developer Analysis](amazon-q-developer.md)
- [Azure AI Toolkit Analysis](azure-ai-toolkit.md)
- [Claude Code Analysis](claude-code.md)
- [Codeium Analysis](codeium.md)
- [Continue Analysis](continue.md)
- [Cursor Analysis](cursor.md)
- [GitHub Copilot Chat Analysis](github-copilot-chat.md)
- [OpenAI Codex Analysis](openai-codex.md)
- [Roo Cline Analysis](roo-cline.md)
- [Sourcegraph Cody Analysis](sourcegraph-cody.md)
- [Tabnine Analysis](tabnine.md)
- [Windsurf Analysis](windsurf.md)

### Methodology

Analysis methodology detailed in: [ANALYSIS_PLAN.md](../ANALYSIS_PLAN.md)

Tool analysis template: [TOOL_ANALYSIS_TEMPLATE.md](../doc/templates/TOOL_ANALYSIS_TEMPLATE.md)

[↑ Back to top](#table-of-contents)

---

## Changes Since January 2026

**Update Date:** 25 February 2026

This section summarises all changes identified since the original analysis date of 22 January 2026.

### New Tools Analysed

#### Windsurf

Windsurf is an AI-first code editor launched in November 2024 by Windsurf Inc. (formerly Codeium) and now at Wave 13 / v1.13.3 (February 2026). It is a separate product from the Codeium extension (analysed separately at [codeium.md](codeium.md)). Windsurf features the Cascade AI agent, in-house SWE-1.5 frontier model, a rules and workflows system, full MCP support, and JetBrains integration. Over 1 million users as of February 2026. (Source: [Windsurf Documentation](https://docs.windsurf.com). Accessed 25 February 2026.)

#### OpenAI Codex (2026)

The new OpenAI Codex (2026) is a coding agent distinct from the deprecated Codex API (discontinued March 2023). It is available as an open-source CLI (Apache-2.0, Rust), a cloud-based agent at chatgpt.com/codex, and an IDE extension for VS Code, Cursor, Windsurf, and JetBrains IDEs. Included with ChatGPT Plus, Pro, Business, Edu, and Enterprise plans. Uses GPT-5.3-Codex and GPT-5.1-Codex-Mini models. Features AGENTS.md instruction system, full MCP support, and OS-level sandboxing. (Source: [OpenAI Codex Documentation](https://developers.openai.com/codex). Accessed 25 February 2026.)

### Tool Updates

#### Roo Code (formerly Roo Cline)

The extension has been officially rebranded from "Roo Cline" to "Roo Code" as of v3.2.0. Current version is v3.48.0 (17 February 2026). Documentation has moved to https://docs.roocode.com/ (repository: https://github.com/RooCodeInc/Roo-Code). New features include a worktree selector, Smart Code Folding (context condensation), and wider model support. (Source: [Roo Code Update Notes](https://docs.roocode.com/update-notes/). Accessed 21 February 2026.)

#### GitHub Copilot Chat

VS Code v1.109 (4 February 2026) added multi-agent development as a primary focus, including Claude Agent SDK integration (public preview), agent orchestrations, Agent Skills, Copilot Memory, and parallel subagents. GPT-5.3-Codex became generally available for GitHub Copilot on 9 February 2026. (Sources: [VS Code v1.109 Release Notes](https://code.visualstudio.com/updates/v1_109); [GitHub Copilot in VS Code v1.109](https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/); [GPT-5.3-Codex GA](https://github.blog/changelog/2026-02-09-gpt-5-3-codex-is-now-generally-available-for-github-copilot/). Accessed 21 February 2026.)

For a detailed analysis of Claude integration in GitHub Copilot — including the Claude Agent SDK delegation mode, how it differs from regular agent mode, and restrictions on CLAUDE.md config file support — see [GitHub Copilot: Claude Integration Deep Dive](github-copilot-claude-integration.md).

#### GitHub Copilot Coding Agent

The Coding Agent is now accessible from Visual Studio 2026 (17 February 2026), in addition to VS Code and GitHub.com. SKILL.md files enable definition of custom agent skills. (Sources: [Delegate tasks from Visual Studio](https://github.blog/changelog/2026-02-17-delegate-tasks-to-copilot-coding-agent-from-visual-studio/); [GitHub Copilot in VS Code v1.109](https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/). Accessed 21 February 2026.)

#### Gemini Code Assist

Agent mode is now widely available in VS Code and IntelliJ as a stable release, no longer in preview. An auto-approve option has been added in IntelliJ. (Source: [Gemini Code Assist Overview](https://cloud.google.com/gemini/docs/codeassist/overview). Accessed 21 February 2026.)

#### Claude Code

Current version is v2.1.47 (February 2026), up from v2.1.12 at the time of original analysis. Claude Sonnet 4.6 support was added on 17 February 2026. Opus 4 and Opus 4.1 have been deprecated from Claude Code. New features include agent hooks and message queueing. (Source: [Claude Code Releases](https://github.com/anthropics/claude-code/releases). Accessed 21 February 2026.)

#### Cursor

Current version is v2.5 (February 2026). A new Plugins/Marketplace enables skills, subagents, and hooks, with partners including Amplitude, AWS, Figma, Linear, and Stripe. Async subagents and Cursor Blame (Enterprise) were added. (Source: [Cursor Changelog](https://cursor.com/changelog). Accessed 21 February 2026.)

#### Tabnine

Version v5.28.0 (10 February 2026): Context Engine is now generally available. BYOAI (Bring Your Own AI) enables use of Claude, GPT-4o, Gemini, and Codestral models. New predefined slash commands (`/code-review`) are available. Support added for Visual Studio 2022 and Visual Studio 2026. Image context support added for Gemini models. (Source: [Tabnine Release Notes](https://docs.tabnine.com/main/administering-tabnine/release-notes). Accessed 21 February 2026.)

#### Continue

Continue has reached its stable v1.0 release. OpenRouter has been added as a supported LLM provider. (Source: [Continue Changelog](https://changelog.continue.dev/). Accessed 21 February 2026.)

### Feature Comparison Updates

- **LLM Provider Support (§3.1):** GitHub Copilot Chat now includes Claude Agent SDK integration (public preview). Tabnine's BYOAI feature adds Claude, GPT-4o, Gemini, and Codestral support. GPT-5.3-Codex is now generally available in GitHub Copilot (9 February 2026). Windsurf and OpenAI Codex added as new entries.
- **MCP Support (§3.2):** Windsurf and OpenAI Codex both added with full MCP support, increasing tools count from 5 to 7.
- **IDE Support (§3.3):** GitHub Copilot Coding Agent is now accessible from Visual Studio 2026. Tabnine added Visual Studio 2022 and 2026 support. Windsurf added as standalone editor with JetBrains plugin.
- **Custom Instructions (§3.4):** Windsurf (`.windsurf/rules/`) and OpenAI Codex (`AGENTS.md`) added, increasing documented tools from 6 to 8.
- **Custom Prompts (§3.5):** Tabnine now supports predefined slash commands. Windsurf (Workflows) and OpenAI Codex (profiles/AGENTS.md) added. GitHub Copilot Chat v1.110 adds `/create-prompt`, `/create-instruction`, `/create-skill`, `/create-agent`, and `/create-hook` commands.
- **Pricing (§3.6):** Windsurf Pro at $15/month, Teams at $30/user/month. OpenAI Codex included with ChatGPT plans.

### Technology Trends

- **Multi-Agent Development:** VS Code is positioning itself as the platform for multi-agent development (v1.109, February 2026), with agent orchestrations, parallel subagents, and Agent Skills now available. In v1.110, agent plugins, agentic browser tools, and the Agent Debug panel further deepen multi-agent capabilities. (Source: [VS Code v1.109 Release Notes](https://code.visualstudio.com/updates/v1_109). Accessed 21 February 2026. [VS Code v1.110 Release Notes](https://code.visualstudio.com/updates/v1_110). Accessed 8 March 2026.)
- **Claude Agent SDK:** Integration of Anthropic's Claude Agent SDK into VS Code (public preview) expands the agent ecosystem beyond proprietary implementations. In v1.110, steering/queuing, `/compact`, and `getDiagnostics` have been added, closing the capability gap between Claude agents and native Copilot agents. (Source: [GitHub Copilot in VS Code v1.109](https://github.blog/changelog/2026-02-04-github-copilot-in-visual-studio-code-v1-109-january-release/). Accessed 21 February 2026.)
- **Edit Mode Deprecation:** GitHub Copilot Chat's Edit mode is deprecated in v1.110 and will be removed in v1.125. Agent mode and Ask mode handle all previous Edit mode use cases, signalling that interactive multi-file editing is now considered a standard agentic task rather than a separate mode. (Source: [VS Code v1.110 Release Notes](https://code.visualstudio.com/updates/v1_110). Accessed 8 March 2026.)
- **Context Management:** Context compaction (available in v1.110 for local, background, and Claude agents via `/compact`) and session memory for plans represent growing investment in managing long-running agentic sessions more effectively.
- **Open-Source Ecosystem Maturity:** Roo Cline rebranded to Roo Code (v3.2.0) with a dedicated documentation site, and Continue reached stable v1.0, reflecting increased maturity of open-source agentic tooling.
- **Proprietary In-House Models:** Windsurf's SWE-1.5 model demonstrates the trend of coding-tool vendors building their own fine-tuned models rather than relying solely on third-party providers. (Source: [Windsurf Models](https://docs.windsurf.com/windsurf/models). Accessed 25 February 2026.)
- **Open-Source CLI Agents:** OpenAI's Codex CLI (Apache-2.0) represents a trend towards open-source coding agents that can run locally with OS-level sandboxing. (Source: [OpenAI Codex GitHub](https://github.com/openai/codex). Accessed 25 February 2026.)
- **Subscription Bundling:** The inclusion of Codex in existing ChatGPT plans without extra cost signals a trend of bundling agentic coding capabilities into existing AI subscription tiers.

[↑ Back to top](#table-of-contents)

---

## See Also

- [Amazon Q Developer](amazon-q-developer.md) - AWS AI-powered coding assistant with security scanning and AWS service integration
- [Azure AI Toolkit](azure-ai-toolkit.md) - Visual Studio Code extension for integrating Azure AI services and local AI models into development workflows
- [Claude Code](claude-code.md) - Terminal-based agentic coding tool from Anthropic with MCP support, plugin system, and VS Code integration
- [Codeium](codeium.md) - Free AI-powered code completion and chat assistant with broad IDE support
- [Continue](continue.md) - AI-powered coding assistant with IDE extensions, CLI, and cloud agents
- [Cursor](cursor.md) - AI-first code editor built for productivity with deep AI integration
- [GitHub Copilot Chat](github-copilot-chat.md) - AI-powered code assistance and chat interface for software development
- [GitHub Copilot: Claude Integration Deep Dive](github-copilot-claude-integration.md) - Detailed analysis of Claude integration in GitHub Copilot, including delegation mode and CLAUDE.md support
- [Roo Cline](roo-cline.md) - AI-powered development assistant for VS Code with multiple operational modes
- [Sourcegraph Cody](sourcegraph-cody.md) - AI coding assistant with deep codebase context and understanding
- [Tabnine](tabnine.md) - AI-powered code completion tool with flexible deployment options
- [Windsurf](windsurf.md) - AI-first IDE with Cascade agentic assistant and in-house SWE models
- [OpenAI Codex](openai-codex.md) - OpenAI's coding agent available as CLI, cloud service, and IDE extension (2026)

---

↑ [Parent: Tool Analyses](README.md) | [Next: Claude Code](claude-code.md) →
