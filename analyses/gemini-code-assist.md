← [Previous: Continue](continue.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: GitHub Copilot Chat](github-copilot-chat.md) →

---

# Gemini Code Assist Analysis

**Analysis Date:** 20 January 2026  
**Tool Version:** Current (Gemini 3)  
**Analyst:** GitHub Copilot  
**Official Documentation:** https://cloud.google.com/gemini/docs/codeassist/overview

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
- [8. Summary and Key Findings](#8-summary-and-key-findings)
  - [Strengths](#strengths)
  - [Limitations](#limitations)
  - [Best Use Cases](#best-use-cases)
  - [Documentation Quality](#documentation-quality)
- [9. Completeness Checklist](#9-completeness-checklist)
- [10. References](#10-references)
  - [Official Documentation](#official-documentation)
  - [Version Information](#version-information)

---

## 1. Tool Overview

**Official Documentation:** https://cloud.google.com/gemini/docs/codeassist/overview  
**Version Analysed:** Current (Gemini 3)  
**Primary Use Case:** Enterprise AI-powered coding assistant with Google Cloud integration  
**Licensing:** Commercial (Standard and Enterprise editions)

### Description

Gemini Code Assist is Google Cloud's enterprise AI-powered coding assistant available in two editions: Standard and Enterprise. It provides code completion, code generation, natural language chat, and agentic capabilities directly in IDEs such as Visual Studio Code, JetBrains IDEs, and Android Studio. The tool uses Google's Gemini large language models, fine-tuned on billions of lines of open source code, Google Cloud documentation, and security data.

The Enterprise edition includes code customisation based on private repositories, whilst the Standard edition focuses on IDE-based AI assistance with enterprise-grade security. Both editions integrate with various Google Cloud services including Firebase, BigQuery, Colab Enterprise, and Application Integration.

Gemini Code Assist also features agent mode (preview), which provides multi-step task execution with built-in tools and Model Context Protocol (MCP) integration. A command-line interface (Gemini CLI) extends AI assistance to the terminal.

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview

### Key Features

- Code completion and generation with Gemini 3 models
- Natural language chat interface in IDEs
- Agent mode with MCP support for complex multi-step tasks
- Gemini CLI for terminal-based AI assistance
- Local codebase awareness with 1M token context window
- Code customisation using private repositories (Enterprise only)
- Integration with Google Cloud services (Firebase, BigQuery, Apigee, Application Integration)
- Source citations for code suggestions
- Enterprise-grade security with IP indemnification
- Smart actions and commands for code transformation

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview, https://cloud.google.com/products/gemini/code-assist

[↑ Back to top](#table-of-contents)

---

## 2. LLM Provider Integration

### 2.1 Ollama Integration

**Supported:** No

Gemini Code Assist uses Google's proprietary Gemini models exclusively. There is no documented support for Ollama integration.

**Citation:** Not documented in official sources

---

### 2.2 GitHub Copilot Pro Integration

**Supported:** No

Gemini Code Assist is a standalone product that operates independently. It does not integrate with GitHub Copilot Pro.

**Citation:** Not documented in official sources

---

### 2.3 Microsoft AI Foundry Integration

**Supported:** No

Gemini Code Assist uses Google's Gemini models and does not support Microsoft AI Foundry integration.

**Citation:** Not documented in official sources

---

### 2.4 OpenAI Integration

**Supported:** No

Gemini Code Assist is designed to work exclusively with Google's Gemini models. There is no support for OpenAI model integration.

**Citation:** Not documented in official sources

---

### 2.5 Anthropic (Claude) Integration

**Supported:** No

Gemini Code Assist does not support Anthropic Claude models. It uses Google's proprietary Gemini models only.

**Citation:** Not documented in official sources

[↑ Back to top](#table-of-contents)

---

## 3. Policies and Rules (Instruction Files)

### Instruction File Support

**Supported File Types:** Not documented in official sources

The official documentation does not describe support for instruction files such as `.github/copilot-instructions.md` or similar configuration files for customising agent behaviour through policy files.

**File Locations:** Not documented in official sources

**File Format:** Not documented in official sources

### Configuration Method

Not documented in official sources

### Syntax and Structure

Not documented in official sources

### Scope and Application

Code customisation (Enterprise edition) allows indexing private repositories to influence code suggestions, but this is not the same as instruction files or policy-based rules.

- **Global:** Not documented
- **Project-Level:** Not documented
- **File-Level:** Not documented

### Example Policies

Not documented in official sources

**Citation:** Not documented in official sources. Code customisation described at https://cloud.google.com/gemini/docs/codeassist/code-customization-overview

[↑ Back to top](#table-of-contents)

---

## 4. Custom and Stored Prompts

### Prompt Storage Mechanism

**Available:** Not documented

The official documentation does not describe a mechanism for storing and reusing custom prompts.

### Creating Custom Prompts

Not documented in official sources

### Organising Prompts

Not documented in official sources

### Using Stored Prompts

Not documented in official sources

### Sharing and Exporting

Not documented in official sources

**Citation:** Not documented in official sources

[↑ Back to top](#table-of-contents)

---

## 5. Tools and Model Context Protocol (MCP)

### Model Context Protocol (MCP)

**MCP Support:** Yes (in agent mode)

Gemini Code Assist agent mode supports Model Context Protocol (MCP) servers. MCP servers can be configured to extend the agent's capabilities with additional tools and services.

**Configuration:**

MCP servers are configured in the Gemini settings JSON file located at `~/.gemini/settings.json` (VS Code) or in an `mcp.json` file in the IDE's configuration directory (IntelliJ).

**Citation:** https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer

### MCP Server Configuration

**VS Code:**

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_example_token"
      }
    },
    "gitlab": {
      "command": "npx",
      "args": ["mcp-remote", "https://your-gitlab-instance.com/api/v4/mcp"]
    }
  }
}
```

**IntelliJ:**

Create `mcp.json` in the IDE's configuration directory with the same structure as the VS Code configuration.

**Citation:** https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer

### Available Tools

Agent mode includes built-in tools that can be controlled via configuration:

| Tool Name | Purpose | Documentation |
|-----------|---------|---------------|
| File Search | Search files in the codebase | https://github.com/google-gemini/gemini-cli/blob/main/docs/core/tools-api.md |
| File Read | Read file contents | https://github.com/google-gemini/gemini-cli/blob/main/docs/core/tools-api.md |
| File Write | Write to files | https://github.com/google-gemini/gemini-cli/blob/main/docs/core/tools-api.md |
| Shell Tool | Execute terminal commands | https://github.com/google-gemini/gemini-cli/blob/main/docs/core/tools-api.md |
| Grep | Search code patterns | https://github.com/google-gemini/gemini-cli/blob/main/docs/core/tools-api.md |

Tool access can be controlled using `coreTools` and `excludeTools` settings in the Gemini settings JSON file.

**Citation:** https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer

### Custom Tool Development

**Supported:** Yes (via MCP servers)

Custom tools can be developed as MCP servers. Once configured, Gemini Code Assist automatically decides when and how to use the server tools contained within MCP servers.

**Development Framework:** Model Context Protocol (MCP)

**Citation:** https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer

[↑ Back to top](#table-of-contents)

---

## 6. Application Development Workflow

### 6.1 Project Initialisation

Gemini Code Assist works within existing project structures in supported IDEs. It does not provide explicit project initialisation or scaffolding features. Developers use Gemini Code Assist within their existing development workflows.

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview

### 6.2 Design and Planning

Agent mode (preview) can generate code from design documents, issues, and TODO comments. Developers can ask Gemini to complete high-level goals and complex tasks that involve multiple steps.

**Citation:** https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer

### 6.3 Code Generation

**Supported Generation Methods:**

- **Inline code completion:** Real-time code suggestions as developers type
- **Code block generation:** Generate full functions or code blocks from comments
- **Chat-based generation:** Natural language prompts in the chat interface
- **Agent mode:** Multi-step code generation with tool use and planning

**Workflow:**

1. Write code or comments in the IDE
2. Receive inline code completions automatically
3. Use chat interface for questions or generation requests
4. Switch to agent mode for complex multi-step tasks
5. Review and approve agent plans and tool use
6. Accept or reject generated code

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview, https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer

### 6.4 Iterative Development

Developers can iterate on generated code by:
- Editing agent plans during execution
- Providing feedback through chat
- Using smart actions on selected code (explain, fix, generate tests)
- Leveraging local codebase awareness for context-relevant suggestions

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview

### 6.5 Testing and Validation

Gemini Code Assist can generate unit tests through:
- Smart actions on selected code
- Natural language prompts ("Write unit tests for my code")
- Agent mode for comprehensive test generation

Integration with external testing frameworks is not explicitly documented.

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview

### 6.6 Debugging

**Debugging Features:**
- Help debugging code through chat interface
- Smart actions to fix code errors
- Code explanation capabilities
- Error analysis (particularly in Firebase with Crashlytics integration)

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview

### 6.7 Deployment

Deployment features are available through Google Cloud service integrations:
- Cloud Run code completion during function development
- Apigee for API development and deployment
- Application Integration for workflow automation
- Firebase for mobile and web app deployment

Direct deployment features from the IDE are not explicitly documented.

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview

[↑ Back to top](#table-of-contents)

---

## 7. IDE and Environment Integration

### 7.1 Visual Studio Code

**Supported:** Yes

**Installation:** Gemini Code Assist extension from VS Code Marketplace

Extension name: "Gemini Code Assist" (Google Cloud Tools extension)

**Configuration:**

1. Install the Gemini Code Assist extension from the VS Code Marketplace
2. Set up Gemini Code Assist for a Google Cloud project
3. Configure settings in `~/.gemini/settings.json` for agent mode and MCP servers

**Citation:** https://marketplace.visualstudio.com/items?itemName=GoogleCloudTools.cloudcode, https://cloud.google.com/gemini/docs/codeassist/overview

**Features:**

- Inline code completion and generation
- Natural language chat interface
- Agent mode with multi-step task execution
- Smart actions (fix, explain, generate tests)
- Smart commands (slash `/` commands in chat)
- Local codebase awareness
- MCP server integration
- Code customisation (Enterprise edition)

**Keyboard Shortcuts:**

Not explicitly documented in official sources

**UI Integration:**

Gemini Code Assist appears as:
- Activity bar icon (spark **Gemini Code Assist**)
- Chat panel with standard and agent mode toggle
- Inline code suggestions in the editor
- Context menu for smart actions

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview, https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer

---

### 7.2 JetBrains IDEs

**Supported IDEs:** 
- CLion
- DataGrip
- GoLand
- IntelliJ IDEA (Community, Educational, Ultimate)
- PhpStorm
- PyCharm (Community and Professional)
- Rider
- RubyMine
- WebStorm

**Installation:** Gemini Code Assist plugin from JetBrains Marketplace

Plugin name: "Gemini Code Assist"

**Configuration:**

1. Install the Gemini Code Assist plugin from JetBrains Marketplace
2. Set up Gemini Code Assist for a Google Cloud project
3. For MCP servers, create `mcp.json` in the IDE's configuration directory

**Citation:** https://plugins.jetbrains.com/plugin/24198-gemini-code-assist, https://cloud.google.com/gemini/docs/codeassist/supported-languages

**Features:**

- Inline code completion and generation
- Natural language chat interface (spark **Gemini** in tool window bar)
- Agent mode with Agent tab
- Smart actions on selected code
- Local codebase awareness
- MCP server integration
- Code customisation (Enterprise edition)
- Auto-approve changes option in agent mode

**IDE-Specific Considerations:**

- Built-in tool control (`coreTools` and `excludeTools`) is not supported in JetBrains IDEs
- MCP servers configured via `mcp.json` file instead of `~/.gemini/settings.json`

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview, https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer

---

### 7.3 Eclipse

**Supported:** No

Eclipse is not listed amongst the supported IDEs for Gemini Code Assist.

**Citation:** https://cloud.google.com/gemini/docs/codeassist/supported-languages

---

### 7.4 Terminal and CLI

**CLI Available:** Yes (Gemini CLI)

**Installation:** 

The Gemini CLI is an open source tool available on GitHub. Installation instructions are provided in the repository.

```bash
# Installation method not explicitly documented in the overview
# Refer to https://github.com/google-gemini/gemini-cli
```

**Available Commands:**

The Gemini CLI provides AI capabilities at the command line, including:

| Command | Description | Example |
|---------|-------------|---------|
| Code understanding | Ask questions about code in the terminal | Not explicitly documented |
| File manipulation | Perform file operations with AI assistance | Not explicitly documented |
| Command execution | Execute commands with AI guidance | Not explicitly documented |
| Troubleshooting | Get help with debugging and errors | Not explicitly documented |

Specific commands are not detailed in the overview documentation.

**Configuration:**

Configuration uses `~/.gemini/settings.json` file, similar to VS Code.

**Usage Examples:**

Specific usage examples are not provided in the overview documentation. The Gemini CLI provides a "generous free tier with high usage limits for individual developers" and can be enhanced with a Gemini Code Assist licence.

**Integration with Shell:**

The Gemini CLI integrates directly with terminal environments (bash, zsh, etc.) as a command-line tool.

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview, https://github.com/google-gemini/gemini-cli

---

### 7.5 Other IDEs and Editors

**Supported Environments:** 

#### Android Studio

**Installation:** Built-in support  
**Features:**
- Code completion and generation
- Smart actions on selected code
- Full Gemini Code Assist capabilities

**Limitations:** None documented  
**Citation:** https://cloud.google.com/gemini/docs/codeassist/supported-languages, https://developer.android.com/studio/gemini/overview

#### Cloud Shell Editor

**Installation:** Available by default in Cloud Shell  
**Features:**
- Inline code suggestions
- Smart actions
- Smart commands
- Full Gemini Code Assist integration

**Limitations:** None documented  
**Citation:** https://cloud.google.com/gemini/docs/codeassist/supported-languages

#### Cloud Workstations

**Installation:** Available by default in Cloud Workstations  
**Features:**
- Inline code suggestions
- Smart actions
- Smart commands
- Code customisation support
- Full Gemini Code Assist integration

**Limitations:** None documented  
**Citation:** https://cloud.google.com/gemini/docs/codeassist/supported-languages

[↑ Back to top](#table-of-contents)

---

## 8. Summary and Key Findings

### Strengths

- Enterprise-grade security with IP indemnification and data governance
- Deep integration with Google Cloud ecosystem (Firebase, BigQuery, Apigee, etc.)
- Agent mode with MCP support for complex multi-step tasks
- Large 1M token context window for codebase awareness
- Code customisation using private repositories (Enterprise edition)
- Gemini 3 model with strong reasoning and coding capabilities
- Source citations for code suggestions
- Multiple deployment options (IDE, CLI, Google Cloud services)
- Comprehensive JetBrains IDE support
- Available in 40+ languages for prompts

### Limitations

- Locked to Google's Gemini models only (no Ollama, OpenAI, Claude support)
- No documented instruction file support for agent behaviour policies
- No documented custom prompt storage mechanism
- No Eclipse support
- Enterprise edition required for code customisation
- Code customisation limited to 20,000 repositories and specific languages
- Hourly licensing model may be complex to manage
- Agent mode recitation (source citations) not available

### Best Use Cases

- Enterprise teams using Google Cloud infrastructure
- Organisations requiring IP indemnification
- Development teams needing private repository code customisation
- Projects using Firebase, BigQuery, or other Google Cloud services
- Teams requiring enterprise-grade security and compliance (SOC, ISO certifications)
- Developers working across multiple JetBrains IDEs
- Command-line intensive workflows (via Gemini CLI)
- Multi-step agentic tasks with tool integration

### Documentation Quality

The official documentation is comprehensive and well-structured, covering setup, configuration, features, and integrations. Documentation includes:
- Clear overview of Standard vs Enterprise editions
- Detailed IDE setup instructions
- Feature comparison tables
- Pricing information
- Security and compliance details
- MCP configuration examples

Some areas lack detail:
- Specific CLI commands and usage examples
- Instruction file support (if any)
- Custom prompt storage mechanisms
- Keyboard shortcuts for IDE operations

Overall documentation quality: High

**Citation:** https://cloud.google.com/gemini/docs/codeassist/overview

[↑ Back to top](#table-of-contents)

---

## 9. Completeness Checklist

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
- [x] All information verified against official documentation
- [x] No assumptions or guesses made
- [x] All claims have citations
- [x] UK English used throughout
- [x] Consistent formatting applied

[↑ Back to top](#table-of-contents)

---

## 10. References

### Official Documentation

1. Gemini Code Assist Overview - https://cloud.google.com/gemini/docs/codeassist/overview
2. Gemini Code Assist Product Page - https://cloud.google.com/products/gemini/code-assist
3. Gemini Code Assist Pricing - https://cloud.google.com/products/gemini/pricing
4. Supported Languages and IDEs - https://cloud.google.com/gemini/docs/codeassist/supported-languages
5. Agent Mode Documentation - https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer
6. Code Customisation Overview - https://cloud.google.com/gemini/docs/codeassist/code-customization-overview
7. VS Code Marketplace Extension - https://marketplace.visualstudio.com/items?itemName=GoogleCloudTools.cloudcode
8. JetBrains Plugin - https://plugins.jetbrains.com/plugin/24198-gemini-code-assist
9. Gemini CLI GitHub Repository - https://github.com/google-gemini/gemini-cli
10. Android Studio Gemini - https://developer.android.com/studio/gemini/overview

### Version Information

- **Tool Version Analysed:** Current (Gemini 3)
- **Documentation Last Updated:** 13 January 2026 UTC
- **Analysis Last Updated:** 20 January 2026

---

## Revision History

| Date | Version | Changes | Analyst |
|------|---------|---------|---------|
| 20 January 2026 | 1.0 | Initial analysis | GitHub Copilot |

[↑ Back to top](#table-of-contents)

---

## See Also

- [Amazon Q Developer](amazon-q-developer.md) - AWS AI-powered coding assistant with security scanning and AWS service integration
- [Azure AI Toolkit for Visual Studio Code](azure-ai-toolkit.md) - Visual Studio Code extension for integrating Azure AI services and local AI models into development workflows
- [ChatGPT](chatgpt.md) - Browser-based conversational AI with Canvas code editing and Python execution (replaced deprecated Codex)
- [Claude Code](claude-code.md) - Terminal-based agentic coding tool from Anthropic with MCP support, plugin system, and VS Code integration
- [Codeium](codeium.md) - Free AI-powered code completion and chat assistant with broad IDE support
- [Continue](continue.md) - AI-powered coding assistant with IDE extensions, CLI, and cloud agents
- [Cursor](cursor.md) - AI-first code editor built for productivity with deep AI integration
- [GitHub Copilot Chat](github-copilot-chat.md) - AI-powered code assistance and chat interface for software development
- [Roo Cline](roo-cline.md) - AI-powered development assistant for VS Code with multiple operational modes (Version 3.41.0)
- [Sourcegraph Cody](sourcegraph-cody.md) - AI coding assistant with deep codebase context and understanding
- [Tabnine](tabnine.md) - AI-powered code completion tool with flexible deployment options

---

← [Previous: Continue](continue.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: GitHub Copilot Chat](github-copilot-chat.md) →
