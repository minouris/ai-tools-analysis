↑ [Parent: Tool Analyses](README.md) | [Next: Claude Code](claude-code.md) →

---

# AI Coding Tools: Overview

**Analysis Date:** 20 January 2026  
**Tools Analysed:** 12 AI coding assistants  
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

---

## 1. Executive Summary

This document provides a comprehensive comparison of 12 AI coding tools analysed in this repository. The tools represent different approaches to AI-assisted development, ranging from cloud-based subscription services to open-source agentic frameworks, including historical platforms.

### Tools Included

1. **Amazon Q Developer** - AWS-focused AI assistant with security scanning
2. **Azure AI Toolkit** - Local and Azure model management for VS Code
3. **ChatGPT** - Browser-based AI chat with Canvas code editing (replaced deprecated Codex)
4. **Claude Code** - Terminal-based agentic coding with MCP support
5. **Codeium** - Free unlimited code completion and chat
6. **Continue** - Open-source multi-provider platform with MCP
7. **Cursor** - AI-first standalone code editor
8. **Gemini Code Assist** - Google Cloud enterprise AI assistant with agent mode
9. **GitHub Copilot Chat** - GitHub-native multi-mode assistant
10. **Roo Cline** - Open-source autonomous VS Code agent
11. **Sourcegraph Cody** - Deep codebase context via Sourcegraph
12. **Tabnine** - Privacy-focused with local deployment options

### Key Insights

- **Model Flexibility:** Continue and Roo Cline support 20-40+ LLM providers, whilst Amazon Q is AWS-only and Gemini Code Assist is Google-only
- **MCP Adoption:** 5 tools (Claude Code, Continue, Gemini Code Assist, GitHub Copilot, Roo Cline) offer full MCP support
- **Total Cost of Ownership:** Codeium ($0) and GitHub Copilot Pro ($10 USD ≈ $17 NZD) offer best value. "Free" tools like Continue/Roo Cline require separate LLM subscriptions ($20-30 USD ≈ $33-50 NZD/month) or local deployment (hardware-intensive, lower model quality)
- **IDE Coverage:** VS Code has universal support (100%); JetBrains (58%); Eclipse and Neovim limited
- **Customisation:** 6 tools support custom instruction files; 7 support custom prompts/commands

[↑ Back to top](#table-of-contents)

---

## 2. Tools Overview

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

---

### Cursor

**Type:** Standalone Code Editor  
**Licence:** Free tier available, Pro subscription for advanced features  
**Key Focus:** AI-first editor experience

AI-first code editor built on VS Code with deep AI integration. Features composer mode, chat interface, and inline suggestions. Supports Claude and OpenAI models. Custom rules via `.cursorrules` files.

**Official Documentation:** https://cursor.sh/

---

### Gemini Code Assist

**Type:** IDE Plugin + CLI  
**Licence:** Commercial (Standard and Enterprise editions, hourly billing)  
**Key Focus:** Enterprise Google Cloud integration with agent mode

Google Cloud's enterprise AI coding assistant using Gemini 3 models. Available in Standard and Enterprise editions with code completion, chat, and agent mode (MCP support). Features 1M token context window, Gemini CLI for terminal, and integration with Google Cloud services (Firebase, BigQuery, Apigee). Enterprise edition includes code customisation using private repositories. Supports VS Code, JetBrains IDEs, Android Studio, and Cloud environments.

**Official Documentation:** https://cloud.google.com/gemini/docs/codeassist/overview

---

### GitHub Copilot Chat

**Type:** Multi-IDE Plugin  
**Licence:** Subscription-based (Free, Pro, Pro+, Business, Enterprise)  
**Key Focus:** GitHub-native integration with multiple modes

AI-powered conversational interface integrated across multiple IDEs (VS Code, JetBrains, Eclipse, Xcode, Neovim) and GitHub.com. Features Ask, Edit, Agent, and Plan modes. Supports Claude, GPT, and Gemini models. Custom instructions via `.github/copilot-instructions.md` and MCP server support.

**Official Documentation:** https://docs.github.com/en/copilot

---

### Roo Cline

**Type:** VS Code Extension  
**Licence:** Open Source (Apache 2.0)  
**Key Focus:** Autonomous multi-mode agent

Open-source autonomous development assistant for VS Code supporting 20+ LLM providers. Features multiple operational modes (Ask, Architect, Code, Test, Debug), MCP integration via McpHub, and cross-compatible rules (`.clinerules`, `.cursorrules`, `CLAUDE.md`).

**Official Documentation:** https://github.com/RooVetGit/Roo-Cline

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

[↑ Back to top](#table-of-contents)

---

## 3. Feature Comparison Charts

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
| **GitHub Copilot** | ✅ | ✅ Native | ✅ (Toolkit) | ✅ (Toolkit) | ❌ | ✅ | Multi-provider |
| **Roo Cline** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | **20+ providers** |
| **Sourcegraph Cody** | ✅ | ✅ | ✅ | Not doc. | ❌ | ✅ | Multi-provider |
| **Tabnine** | Not doc. | Not doc. | Not doc. | Not doc. | ❌ | Not doc. | Proprietary |

**Key Finding:** Continue and Roo Cline offer the most provider flexibility with 20-40+ integrations, whilst Amazon Q (AWS-only) and Gemini Code Assist (Google-only) are locked to their respective cloud ecosystems.

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
| **GitHub Copilot** | ✅ **Supported** | IDE-specific config | stdio, SSE | GitHub MCP |
| **Roo Cline** | ✅ **Full** | `.roomodes` config | Multiple | McpHub |
| **Sourcegraph Cody** | ❌ Not documented | Built-in tools | N/A | N/A |
| **Tabnine** | ❌ Not documented | N/A | N/A | N/A |

**Key Finding:** 5 tools (Claude Code, Continue, Gemini Code Assist, GitHub Copilot, Roo Cline) have documented MCP support, representing 42% of analysed tools. MCP adoption is growing but not yet universal.

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

**IDE Support Count:**
- **VS Code:** 11/12 tools (92%)
- **JetBrains:** 7/12 tools (58%)
- **Eclipse:** 3/12 tools (25%)
- **Neovim:** 4/12 tools (33%)
- **Terminal/CLI:** 4/12 tools (33%)
- **Standalone:** 2/12 tools (17%) - Cursor (editor), ChatGPT (browser/app)

**Key Finding:** VS Code has near-universal support amongst IDE-integrated tools. ChatGPT and Cursor operate as standalone applications without IDE integration. Gemini Code Assist supports Cloud-native environments (Cloud Shell, Cloud Workstations, Android Studio).

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

**Supported Rule Formats:**
1. `.github/copilot-instructions.md` (GitHub Copilot)
2. `.clinerules` (Roo Cline)
3. `.cursorrules` (Cursor, Roo Cline)
4. `.claude/rules/` (Claude Code)
5. `.continue/rules/` (Continue)
6. `.cody/instructions` (Sourcegraph Cody)
7. `CLAUDE.md` (Claude Code, Roo Cline cross-compat)

**Key Finding:** 6 out of 10 tools (60%) support custom instruction files, but formats are fragmented. Roo Cline offers the most cross-compatibility by supporting 3 different formats.

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
| **Tabnine** | ❌ Not documented | N/A | N/A | N/A |

**Key Finding:** 7 out of 12 tools (58%) support some form of custom prompts or commands. Continue and Claude Code offer the most sophisticated prompt management with Hub sharing and skills systems respectively.

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
> "Copilot can suggest incorrect, insecure, or inefficient code, particularly with novel algorithms, unfamiliar libraries, or loosely typed codebases. Manual review is essential."
> 
> *Source: Sider.ai review. 2025.*

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
- Gemini Code Assist: "completely unusable during some weeks in 2025-2026"
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
> "Use Copilot for autocomplete and simple suggestions. Use Cursor for architectural advice and in-depth code walkthroughs."
> 
> *Source: Reddit discussions. 2024-2026.*

**GitHub Copilot vs Continue.dev:**
- Copilot: Plug-and-play, most reliable, enterprise features
- Continue.dev: Open source, privacy control, customisable, free
> "Continue.dev is lauded for 'letting me create my workflow instead of forcing one on me,' though this comes with some additional upfront effort."
> 
> *Source: AI Tool Discovery. 2026.*

**GitHub Copilot vs Codeium:**
- Copilot: More accurate, better documentation, mature ecosystem
- Codeium: Free unlimited, good privacy options, self-hosting available
> "Codeium is often praised as 'the best free AI code completion tool' for individual developers."
> 
> *Source: Reddit discussions. 2024-2025.*

**Cursor vs Cline/Roo Cline:**
- Cursor: More autonomous, better project intelligence, higher cost
- Cline: More cautious, human-in-the-loop safety, free (requires LLM)
- Roo Cline: Maximum automation, multi-role AI, steeper learning curve
> "Roo Code is the pro's tool; Cline is the 'safe default'."
> 
> *Source: MyAIVerdict. 2025.*

**Amazon Q vs GitHub Copilot:**
- Amazon Q: AWS-specific excellence, infrastructure code, security scanning
- GitHub Copilot: General-purpose, multi-cloud, broader language support
> "For teams or developers already live on AWS, Amazon Q Developer is increasingly recognised as the top productivity booster. For everyone else (multi-cloud, front-end, cross-language), Copilot remains the 'gold standard'."
> 
> *Source: Multiple sources. 2024-2026.*

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

### Market Landscape

1. **Consolidation Around Key Models:** Claude and OpenAI dominate LLM provider integration, with Ollama growing as local alternative
2. **VS Code Dominance:** 100% of tools support VS Code; other IDEs have lower coverage (JetBrains 60%, Eclipse 30%)
3. **Emerging MCP Standard:** 40% of tools support MCP, suggesting growing standardisation for extensibility
4. **Fragmented Instruction Formats:** 6 different instruction file formats exist, limiting cross-tool compatibility
5. **Open Source Growth:** 2 major open-source options (Continue, Roo Cline) provide full-featured alternatives to commercial tools

### User Experience Insights (Based on Third-Party Reviews)

**Consistent Patterns Across All Tools:**

1. **Productivity Gains Are Real:** Users consistently report 40-55% productivity improvements, with GitHub Copilot (55%), Tabnine (45%), and Sourcegraph Cody (5-6 hours/week saved) leading reported gains

2. **Accuracy Requires Vigilance:** All tools experience "hallucinations" and generate incorrect code. Manual review is essential regardless of tool choice
   > "Copilot can suggest incorrect, insecure, or inefficient code, particularly with novel algorithms, unfamiliar libraries, or loosely typed codebases. Manual review is essential."
   > 
   > *Source: Multiple user reviews. 2024-2026.*

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

**MCP Adoption:** Model Context Protocol support growing but not universal. Tools with MCP (Claude Code, Continue, GitHub Copilot, Roo Cline) demonstrate extensibility advantages.

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
8. **Roo Cline.** RooVetGit. https://github.com/RooVetGit/Roo-Cline
9. **Sourcegraph Cody.** Sourcegraph. https://sourcegraph.com/cody
10. **Tabnine.** Tabnine. https://www.tabnine.com/

### Analysis Files

All detailed tool analyses are available in this directory:

- [Amazon Q Developer Analysis](amazon-q-developer.md)
- [Azure AI Toolkit Analysis](azure-ai-toolkit.md)
- [Claude Code Analysis](claude-code.md)
- [Codeium Analysis](codeium.md)
- [Continue Analysis](continue.md)
- [Cursor Analysis](cursor.md)
- [GitHub Copilot Chat Analysis](github-copilot-chat.md)
- [Roo Cline Analysis](roo-cline.md)
- [Sourcegraph Cody Analysis](sourcegraph-cody.md)
- [Tabnine Analysis](tabnine.md)

### Methodology

Analysis methodology detailed in: [ANALYSIS_PLAN.md](../ANALYSIS_PLAN.md)

Tool analysis template: [TOOL_ANALYSIS_TEMPLATE.md](../TOOL_ANALYSIS_TEMPLATE.md)

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
- [Roo Cline](roo-cline.md) - AI-powered development assistant for VS Code with multiple operational modes
- [Sourcegraph Cody](sourcegraph-cody.md) - AI coding assistant with deep codebase context and understanding
- [Tabnine](tabnine.md) - AI-powered code completion tool with flexible deployment options

---

↑ [Parent: Tool Analyses](README.md) | [Next: Claude Code](claude-code.md) →
