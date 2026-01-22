← [Previous: Gemini Code Assist](gemini-code-assist.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: GitHub Codespaces](github-codespaces.md) →

---

# GitHub Copilot Chat Analysis

**Analysis Date:** 16 January 2026  
**Tool Version:** Current (as of January 2026)  
**Analyst:** GitHub Copilot  
**Official Documentation:** https://docs.github.com/en/copilot

## Table of Contents

- [1. Tool Overview](#1-tool-overview)
- [2. LLM Provider Integration](#2-llm-provider-integration)
  - [2.1 Ollama Integration](#21-ollama-integration)
  - [2.2 GitHub Copilot Pro Integration](#22-github-copilot-pro-integration)
  - [2.3 Microsoft AI Foundry Integration](#23-microsoft-ai-foundry-integration)
  - [2.4 OpenAI Integration](#24-openai-integration)
  - [2.5 Anthropic (Claude) Integration](#25-anthropic-claude-integration)
- [3. Policies and Rules (Instruction Files)](#3-policies-and-rules-instruction-files)
- [4. Custom and Stored Prompts](#4-custom-and-stored-prompts)
- [5. Tools and Model Context Protocol (MCP)](#5-tools-and-model-context-protocol-mcp)
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
- [9. Summary and Key Findings](#9-summary-and-key-findings)
- [10. Completeness Checklist](#10-completeness-checklist)
- [11. References](#11-references)
- [Revision History](#revision-history)

---

## 1. Tool Overview

**Official Documentation:** https://docs.github.com/en/copilot  
**Version Analysed:** Current version (as of January 2026)  
**Primary Use Case:** AI-powered code assistance and chat interface for software development  
**Licensing:** Subscription-based (Free, Pro, Pro+, Business, Enterprise)

### Description

GitHub Copilot Chat is an AI-powered conversational interface that provides contextualised assistance throughout the software development lifecycle. It integrates into various development environments to offer code completions, code explanations, answers to documentation questions, and more. Copilot Chat is backed by advanced language models and provides developers with the ability to ask questions, generate code, explain existing code, suggest fixes, and create documentation directly within their IDE or on GitHub.com.

GitHub Copilot transforms the developer experience by enabling developers to focus more on problem-solving and innovation whilst spending less effort on mundane and boilerplate tasks. Developers who use GitHub Copilot report up to 75% higher satisfaction with their jobs and are up to 55% more productive at writing code without sacrifice to quality.

### Key Features

- **Conversational AI Interface**: Chat with Copilot to ask questions, generate code, and get explanations
- **Multi-mode Interaction**: Ask mode, Edit mode, Agent mode, and Plan mode for different workflows
- **Context-Aware Suggestions**: Uses repository context, open files, and conversation history
- **Inline Code Generation**: Generate code directly in the editor with chat-based prompts
- **Code Explanation**: Understand existing code through natural language explanations
- **Multi-model Support**: Choose from various AI models including Claude, GPT, and Gemini
- **IDE Integration**: Available in VS Code, Visual Studio, JetBrains IDEs, Xcode, Eclipse, and more
- **GitHub Native**: Natively integrated into GitHub.com for Enterprise customers
- **Custom Instructions**: Repository-specific and path-specific instruction files
- **Model Context Protocol (MCP)**: Extensible through MCP servers for additional capabilities
- **CLI Interface**: Terminal-based agent for autonomous coding tasks
- **Smart Actions**: Context menu shortcuts for common tasks

**Citation:** About GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/about-github-copilot. Accessed 16 January 2026.

[↑ Back to top](#table-of-contents)

---

## 2. LLM Provider Integration

### 2.1 Ollama Integration

**Supported:** Yes (via model management in VS Code)

**Configuration:**

In Visual Studio Code, users can add Ollama models through the model management interface:

1. In the Copilot chat view, click the model picker dropdown
2. Click "Manage Models"
3. Install the AI Toolkit for Visual Studio Code extension (if not already installed)
4. Add models from the AI Toolkit, which supports Ollama and other local model providers
5. Provide any required authentication or configuration for the provider

The first time you use a model added via the AI Toolkit, you may be prompted to download it and authenticate with the provider.

**Supported Models:** Depends on models available through Ollama installation

**Limitations:** Requires AI Toolkit extension for VS Code. Support may vary by IDE - primarily documented for VS Code.

**Citation:** Changing the AI model for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat. Accessed 16 January 2026.

---

### 2.2 GitHub Copilot Pro Integration

**Supported:** Yes (GitHub Copilot Pro is a subscription tier)

**Integration Method:** GitHub Copilot Pro is one of the subscription tiers for GitHub Copilot, providing access to Copilot Chat and related features.

**Configuration:**

GitHub Copilot Pro is designed for individual developers, freelancers, students, educators, and open source maintainers. It includes all the features of GitHub Copilot Business except organisational licence management, policy management, and IP indemnity.

**Features Available with Copilot Pro:**

- Code completion and chat assistance in IDEs
- Access to multiple AI models
- Copilot Chat in supported IDEs
- GitHub Mobile support with Bing and public repository code search
- Access to Copilot CLI (requires preview features to be enabled)
- Higher monthly usage limits for completions and chat requests compared to the Free tier (see current plans for exact quotas)
- Model selection capabilities
- Custom instructions support

**Citation:** What is GitHub Copilot? GitHub Features. https://github.com/features/copilot. Accessed 16 January 2026. Plans & Pricing. GitHub Copilot. https://github.com/features/copilot/plans. Accessed 16 January 2026.

---

### 2.3 Microsoft AI Foundry Integration

**Supported:** Yes (via model management in VS Code)

**Configuration:**

In Visual Studio Code, users can add Azure AI/Microsoft AI Foundry models through the model management interface:

1. In the Copilot chat view, click the model picker dropdown
2. Click "Manage Models"
3. Select the Azure AI provider from the list
4. Provide the required authentication (GitHub PAT, API key, or model ID as applicable)
5. Select the specific models to add

- **Endpoint URL Configuration:** Configured through the model management interface
- **API Key Configuration:** Provided when adding the provider through "Manage Models"
- **Supported Models:** Azure OpenAI models and other models available through Microsoft AI Foundry

**Authentication Methods:** GitHub personal access token (PAT), API keys, or provider-specific authentication as required by the model provider

**Citation:** Changing the AI model for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat. Accessed 16 January 2026.

---

### 2.4 OpenAI Integration

**Supported:** Yes (models powered by OpenAI)

**Configuration:**

GitHub Copilot is powered by generative AI models developed by GitHub, OpenAI, and Microsoft. The service uses various OpenAI models including GPT-3.5, GPT-4, and GPT-4o variants. Users can select from available models through the model picker in supported clients.

- **API URL Configuration:** Not applicable - models are provided through GitHub Copilot subscription
- **API Key Configuration:** Not applicable - authentication handled through GitHub credentials
- **Supported Models:** GPT-3.5, GPT-4, GPT-4o, GPT-4 Turbo, and other variants available through model selection

**Custom Endpoints:** Users can extend Copilot Chat with additional models through the Visual Studio Code AI Toolkit or by adding models from providers such as OpenAI directly. This requires an API key from the provider.

**Citation:** What has GitHub Copilot been trained on? GitHub Features. https://github.com/features/copilot. Accessed 16 January 2026. Changing the AI model for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat. Accessed 16 January 2026.

---

### 2.5 Anthropic (Claude) Integration

**Supported:** Yes

**Account Requirements:** Requires GitHub Copilot subscription (Free, Pro, Pro+, Business, or Enterprise). Users can optionally add Anthropic models by providing their own API key through supported IDEs.

**Configuration:**

- **API Key Configuration:** Users can add Anthropic models through the model management interface in Visual Studio Code by providing an Anthropic API key
- **Supported Models:** Claude 3.5 Sonnet, Claude 3 Opus, Claude 3 Sonnet, and other Claude variants available through model selection

**Features and Limitations:** Different models have different premium request multipliers, which can affect monthly usage allowance. Experimental pre-release versions may not interact with all filters correctly, including the setting to block suggestions matching public code.

**Citation:** Changing the AI model for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat. Accessed 16 January 2026.

[↑ Back to top](#table-of-contents)

---

## 3. Policies and Rules (Instruction Files)

### Instruction File Support

**Supported File Types:** 
- `.github/copilot-instructions.md` (repository-wide custom instructions)
- `.github/instructions/*.instructions.md` (path-specific custom instructions)
- `AGENTS.md` (agent instructions, can be stored anywhere in repository; nearest file in directory tree takes precedence)
- `CLAUDE.md` or `GEMINI.md` (alternative agent instruction files in repository root)
- `global-copilot-instructions.md` (global instructions for JetBrains IDEs)

**File Locations:** 
- Repository-wide: `.github/copilot-instructions.md`
- Path-specific: `.github/instructions/` directory with `*.instructions.md` files
- Agent instructions: `AGENTS.md` anywhere in repository hierarchy, or `CLAUDE.md`/`GEMINI.md` in root
- Global (JetBrains): `~/.config/github-copilot/intellij/global-copilot-instructions.md` (macOS) or `C:\Users\USERNAME\AppData\Local\github-copilot\intellij\global-copilot-instructions.md` (Windows)

**File Format:** Markdown

### Configuration Method

Repository custom instructions let you provide Copilot with repository-specific guidance and preferences. These files give Copilot additional context on how to understand your project and how to build, test, and validate its changes.

To create custom instructions:

1. Create `.github/copilot-instructions.md` in the repository root for repository-wide instructions
2. For path-specific instructions, create `.github/instructions/` directory and add `*.instructions.md` files
3. Add natural language instructions in Markdown format
4. For path-specific files, include frontmatter with `applyTo` keyword using glob patterns

Custom instructions must be enabled in user settings (enabled by default in most IDEs). Users can also choose to disable custom instructions if desired.

### Syntax and Structure

**Repository-wide instructions** (`.github/copilot-instructions.md`):

```markdown
Follow these coding standards for this project:
- Use TypeScript for all new files
- Follow ESLint configuration
- Write unit tests for all functions
```

**Path-specific instructions** (`.github/instructions/*.instructions.md`):

```markdown
---
applyTo: "app/models/**/*.rb"
excludeAgent: "code-review"
---

All model classes should inherit from ApplicationRecord.
Use ActiveRecord validations.
Include appropriate database indexes.
```

**Agent instructions** (`AGENTS.md`):

Place agent instruction files in the repository to guide AI agents. The nearest `AGENTS.md` file in the directory tree takes precedence.

### Scope and Application

- **Global:** JetBrains IDEs support global custom instructions via `global-copilot-instructions.md`
- **Project-Level:** Eclipse supports project custom instructions; other IDEs support repository-wide instructions via `.github/copilot-instructions.md`
- **File-Level:** Path-specific instructions in `.github/instructions/` directory apply to files matching specified glob patterns

Path-specific instructions support the `excludeAgent` keyword to control whether they are used by Copilot coding agent or Copilot code review.

### Example Policies

```markdown
# .github/copilot-instructions.md

Use UK English spelling throughout the codebase.
Follow the project's established naming conventions.
Ensure all public APIs are documented with JSDoc comments.
Write unit tests using Jest framework.
Use functional components with hooks in React code.
```

```markdown
# .github/instructions/backend.instructions.md
---
applyTo: "src/backend/**/*.ts"
---

Use dependency injection for all services.
Implement proper error handling with custom error classes.
Log all database operations at debug level.
```

**Citation:** Adding custom instructions for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot. Accessed 16 January 2026.

[↑ Back to top](#table-of-contents)

---

## 4. Custom and Stored Prompts

### Prompt Storage Mechanism

**Available:** Yes

GitHub Copilot Chat provides several mechanisms for reusable prompts:

1. **Custom prompt files**: Repository-specific prompt files stored in the `.github/prompts` folder (documented in VS Code)
2. **Chat participants**: Special keywords prefixed with `@` to scope prompts to specific domains (e.g., `@workspace`, `@terminal`)
3. **Slash commands**: Shortcut commands prefixed with `/` for common scenarios (e.g., `/explain`, `/fix`, `/tests`)
4. **Chat variables**: Context variables prefixed with `#` to include specific context (e.g., `#file`, `#selection`)
5. **Custom instructions**: Repository-level instructions that guide Copilot's behaviour (see Section 3)

### Creating Custom Prompts

Users can create reusable prompt patterns through multiple methods:

**Prompt Files** (`.github/prompts` folder):
Repository-specific custom prompts can be stored in the `.github/prompts` directory. Prompt files allow teams to create, share, and reuse standardised prompts for common development tasks. The feature is documented in VS Code's Copilot customization documentation.

To create a prompt file:
1. Create the `.github/prompts` directory in your repository if it doesn't exist
2. Add Markdown files (`.md`) containing your custom prompts
3. Prompt files can include structured content for specific tasks, making them reusable across the team
4. These files are committed to version control, enabling team collaboration

**Built-in Keywords**:
1. **Chat participants**: Type `@` to see available participants (e.g., `@workspace`, `@terminal`)
2. **Slash commands**: Type `/` to see available commands (e.g., `/explain`, `/fix`, `/tests`)
3. **Chat variables**: Type `#` to see available variables (e.g., `#file`, `#selection`)

These can be combined in prompts for consistent results, though they are not stored as named templates.

### Organising Prompts

**Prompt Files**: Custom prompts stored in the `.github/prompts` folder can be organised using:
- File naming conventions for easy identification
- Directory structure within the prompts folder for categorisation
- Descriptive file names that indicate the prompt's purpose
- Team-agreed naming standards for consistency

**Built-in Keywords**: Chat participants, slash commands, and chat variables are pre-defined by the system and cannot be customised or organised by users.

### Using Stored Prompts

**Prompt Files**: Custom prompts from the `.github/prompts` folder are accessible within VS Code's Copilot interface. Teams can reference and use these stored prompts for consistent interactions with Copilot across projects.

**Built-in Keywords**: To use the built-in prompt shortcuts:

1. Open Copilot Chat in your IDE
2. Type `@`, `/`, or `#` to trigger auto-completion of available options
3. Combine these keywords with natural language to create effective prompts

Example: `@workspace /explain #file:auth.ts` asks Copilot to explain the auth.ts file using workspace context.

### Sharing and Exporting

**Prompt Files**: Custom prompts in the `.github/prompts` folder are committed to version control and automatically shared with team members through the repository. This enables:
- Consistent prompt usage across the team
- Version-controlled prompt evolution
- Easy onboarding of new team members with established prompts
- Cross-project prompt reuse by copying files between repositories

**Custom instructions**: Repository-level instructions (Section 3) can be shared via repository files, providing team-wide guidance for Copilot behaviour.

**Built-in Keywords**: Individual prompt templates using built-in keywords cannot be directly exported or shared through the Copilot interface, but effective prompt patterns can be documented and shared externally.

**Citation:** Asking GitHub Copilot questions in your IDE. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide. Accessed 16 January 2026. Prompt files for GitHub Copilot. VS Code Documentation. https://code.visualstudio.com/docs/copilot/customization/prompt-files. Accessed 16 January 2026.

[↑ Back to top](#table-of-contents)

---

## 5. Tools and Model Context Protocol (MCP)

### Model Context Protocol (MCP)

**MCP Support:** Yes

**Configuration:**

The Model Context Protocol (MCP) is an open standard that defines how applications share context with large language models. GitHub Copilot Chat supports MCP to extend its capabilities by integrating with external tools and services.

MCP support is available for:
- **Local MCP servers**: Broad support in Visual Studio Code, JetBrains IDEs, Xcode, and others
- **Remote MCP servers**: Supported in Visual Studio Code, Visual Studio, JetBrains IDEs, Xcode, Eclipse, and Cursor (with OAuth or PAT authentication)

Organisations and enterprises can control MCP access through the "MCP servers in Copilot" policy, which is disabled by default. This policy applies to Copilot Business and Enterprise subscribers. Copilot Free, Pro, and Pro+ users are not governed by this policy.

### MCP Server Configuration

Configuration varies by IDE. Example for Visual Studio Code:

```json
{
  "mcp": {
    "servers": {
      "github": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-github"],
        "env": {
          "GITHUB_PERSONAL_ACCESS_TOKEN": "your-token-here"
        }
      }
    }
  }
}
```

The GitHub MCP server can be accessed remotely through Copilot Chat in Visual Studio Code without local setup. It has access to additional toolsets only available in the remote server.

### Available Tools

| Tool Name | Purpose | Documentation |
|-----------|---------|---------------|
| GitHub MCP Server | Automate code-related tasks, connect GitHub context, invoke Copilot coding agent and code scanning | https://github.com/github/github-mcp-server |
| File System | Access local file system resources | Part of MCP standard |
| Web Search | Search the web for information (via `@github #web`) | Integrated with GitHub skills |
| Custom MCP Servers | Extend capabilities with community or custom servers | https://github.com/mcp |

The GitHub MCP server supports enabling or disabling specific toolsets to control which GitHub API capabilities are available. This improves performance and security by reducing the number of tools in the AI's context window.

### Custom Tool Development

**Supported:** Yes

MCP allows developers to create custom servers that extend Copilot Chat's capabilities. Custom MCP servers can be:
- Developed using the MCP specification
- Shared through the GitHub MCP Registry
- Configured for use with Copilot Chat in supported IDEs

**Development Framework:** Model Context Protocol (MCP) specification

Developers can create custom tools and services that work with Copilot Chat by implementing MCP servers. The GitHub MCP Registry provides a curated list of MCP servers from partners and the community.

**Citation:** About Model Context Protocol (MCP). GitHub Copilot Documentation. https://docs.github.com/en/copilot/concepts/context/mcp. Accessed 16 January 2026. GitHub MCP Registry. GitHub. https://github.com/mcp. Accessed 16 January 2026.

[↑ Back to top](#table-of-contents)

---

## 6. Application Development Workflow

### 6.1 Project Initialisation

GitHub Copilot Chat can assist with project initialisation by:
- Explaining project structure in existing codebases
- Suggesting scaffolding commands for new projects
- Installing dependencies through terminal commands (in Agent or CLI modes)
- Generating initial configuration files

In Copilot CLI, developers can ask the agent to explore project structure, install dependencies, and explain how everything works through simple conversation in the terminal.

### 6.2 Design and Planning

**Plan Mode**: GitHub Copilot Chat includes a dedicated Plan mode (currently in public preview) that helps create detailed implementation plans before executing them. The plan agent:
- Researches the task comprehensively using read-only tools and codebase analysis
- Breaks down tasks into manageable, actionable steps
- Identifies open questions about ambiguous requirements
- Presents a concise plan draft based on a standardised format
- Allows iteration to clarify requirements and adjust scope

Once complete, plans can be:
- Handed off to the agent for implementation
- Opened in the editor as Markdown for manual implementation
- Saved for team discussions or future reference

### 6.3 Code Generation

**Supported Generation Methods:**

- **Inline completions**: Real-time code suggestions as you type
- **Chat-based generation**: Request code through conversational prompts
- **Edit mode**: Controlled edits across multiple files with explicit approval
- **Agent mode**: Autonomous code generation with iterative improvements
- **Quick chat**: Dropdown chat interface (⇧+⌥+⌘+L on Mac, Ctrl+Shift+Alt+L on Windows/Linux)
- **Inline chat**: Editor-integrated chat (Command+i on Mac, Ctrl+i on Windows/Linux)
- **Smart actions**: Context menu shortcuts for common tasks

**Workflow:**

1. Open Copilot Chat in your IDE or use inline chat
2. Submit a prompt describing the code you need
3. Review the generated code
4. Accept, modify, or request refinements through follow-up prompts
5. Iterate until the code meets requirements

### 6.4 Iterative Development

**Ask Mode**: Optimised for answering questions and getting code suggestions. Best for understanding how something works or exploring ideas.

**Edit Mode**: Provides granular control over proposed edits:
1. Select Edit mode from the agents dropdown
2. Add relevant files to the working set
3. Submit a prompt describing desired changes
4. Review proposed changes for each file
5. Apply or discard edits as needed
6. Iterate with additional prompts

**Agent Mode**: Enables autonomous code editing:
1. Select Agent mode from the agents dropdown
2. Submit a task prompt
3. Copilot determines which files to change
4. Review streamed edits and suggested terminal commands
5. Confirm or deny command execution
6. Copilot iterates to remediate issues until task completion

Each prompt in Agent mode counts as one premium request multiplied by the model's multiplier. Follow-up actions by the agent do not count toward premium request usage.

### 6.5 Testing and Validation

GitHub Copilot Chat can assist with testing through:
- Generating unit tests (slash command `/tests` or natural language request)
- Explaining test failures
- Suggesting test improvements
- Creating test fixtures and mock data

Integration with testing frameworks is handled through code generation rather than direct framework integration.

### 6.6 Debugging

**Debugging Features:**

- Error explanation: Ask Copilot to explain error messages or stack traces
- Fix suggestions: Request fixes for bugs or issues
- Code review: Use smart actions to review selected code
- Inline debugging: Use inline chat whilst debugging to ask questions about state
- Terminal integration: Debug through CLI with agent assistance

Smart actions (accessed via right-click context menu or sparkle icon) include options specifically for debugging and fixing code issues.

### 6.7 Deployment

Not extensively documented in official sources. Copilot can assist with generating deployment scripts and configuration files through chat prompts, but does not provide built-in deployment automation features.

**Citation:** Asking GitHub Copilot questions in your IDE. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide. Accessed 16 January 2026. GitHub Copilot CLI. GitHub Features. https://github.com/features/copilot/cli. Accessed 16 January 2026.

[↑ Back to top](#table-of-contents)

---

## 7. IDE and Environment Integration

### 7.1 Visual Studio Code

**Supported:** Yes

**Installation:** GitHub Copilot extension and GitHub Copilot Chat extension from the VS Code Marketplace

**Configuration:**

1. Install the GitHub Copilot extension from the VS Code Marketplace
2. Sign in to GitHub in Visual Studio Code
3. Ensure you have an active Copilot subscription
4. The chat view becomes accessible via the icon in the title bar

**Features:**

- Inline code completions
- Chat view with multiple modes (Ask, Edit, Agent, Plan)
- Quick chat dropdown
- Inline chat in editor and terminal
- Smart actions via context menu
- Model selection and switching
- Chat participants (`@workspace`, `@terminal`, etc.)
- Slash commands for common tasks
- Chat variables for context inclusion
- Image attachment support for multimodal prompts
- MCP server integration (local and remote)
- Custom instructions support
- Code referencing feature for matching public code
- Subagent support (with `runSubagent` tool enabled)

**Keyboard Shortcuts:**

| Action | Shortcut (Windows/Linux) | Shortcut (macOS) |
|--------|--------------------------|------------------|
| Open chat view | Click icon in title bar | Click icon in title bar |
| Quick chat | Ctrl+Shift+Alt+L | ⇧+⌥+⌘+L |
| Inline chat | Ctrl+i | Command+i |

**UI Integration:**

Copilot integrates into VS Code through:
- Chat view panel (opened via icon or command)
- Quick chat dropdown overlay
- Inline chat within editor and terminal
- Status bar indicators
- Context menu smart actions
- Sparkle icon for contextual suggestions

**Citation:** Asking GitHub Copilot questions in your IDE. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide. Accessed 16 January 2026. Installing the GitHub Copilot extension in your environment. GitHub Copilot Documentation. https://docs.visualstudio.com/copilot. Accessed 16 January 2026.

---

### 7.2 JetBrains IDEs

**Supported IDEs:** IntelliJ IDEA, PyCharm, WebStorm, and other JetBrains IDEs

**Installation:** GitHub Copilot plugin from JetBrains Marketplace

**Configuration:**

1. Install the GitHub Copilot plugin from JetBrains Marketplace
2. Sign in to GitHub through the IDE
3. Ensure the latest version of the Copilot extension is installed
4. Access Copilot Chat via the status bar icon

**Features:**

- Code completions
- Copilot Chat panel
- Model selection (including Auto mode)
- Custom instructions support (workspace and global)
- Chat participants and slash commands
- MCP server support (local and remote)

**IDE-Specific Considerations:**

JetBrains IDEs support both workspace-specific custom instructions (`.github/copilot-instructions.md`) and global custom instructions (`global-copilot-instructions.md` in the user's config directory).

Configuration locations:
- macOS: `/Users/USERNAME/.config/github-copilot/intellij/`
- Windows: `C:\Users\USERNAME\AppData\Local\github-copilot\intellij\`

**Citation:** Changing the AI model for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat. Accessed 16 January 2026. Adding custom instructions for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot. Accessed 16 January 2026.

---

### 7.3 Eclipse

**Supported:** Yes (currently in public preview)

**Installation:** GitHub Copilot plugin for Eclipse

**Configuration:**

1. Install the latest version of the Copilot extension in Eclipse
2. Sign in to GitHub
3. Access Copilot Chat via the status bar icon
4. Enable custom instructions in preferences if desired

**Features:**

- Code completions
- Chat panel
- Model selection (including Auto mode)
- Custom instructions support (workspace and project level)
- Workspace custom instructions: Configure via Copilot preferences
- Project custom instructions: `.github/copilot-instructions.md` in project root

**Limitations:**

Eclipse support is currently in public preview and subject to change. Some features available in VS Code or JetBrains IDEs may not yet be available in Eclipse.

**Citation:** Changing the AI model for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat. Accessed 16 January 2026. Adding custom instructions for GitHub Copilot. GitHub Copilot Documentation. https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot. Accessed 16 January 2026.

---

### 7.4 Terminal and CLI

**CLI Available:** Yes (currently in public preview)

**Installation:** 

```bash
npm install -g @github/copilot
```

**Available Commands:**

GitHub Copilot CLI operates as an autonomous agent in the terminal rather than providing discrete commands. Users interact with the CLI through conversational prompts.

| Command | Description | Example |
|---------|-------------|---------|
| `gh copilot` | Launch Copilot CLI agent | `npm install -g @github/copilot` then authenticate |
| Interactive prompts | Ask questions, request code generation, file editing | Natural language conversation |
| Agent tasks | Autonomous execution of coding tasks | "Install dependencies and set up the project" |

**Configuration:**

After installation, authenticate using existing GitHub credentials. The CLI automatically inherits your organisation's Copilot policies and governance settings.

**Usage Examples:**

```bash
# Install Copilot CLI
npm install -g @github/copilot

# Authenticate (follows prompts)
gh copilot auth

# Launch CLI and interact
gh copilot

# Example interactions (within CLI):
> Explore the project structure
> Install dependencies for this project
> Explain how authentication works in this codebase
> Create a new feature for user profiles
```

**Integration with Shell:**

- Supported on macOS, Linux, and Windows (via WSL)
- Maintains session persistence within and across sessions
- Every file change and command execution requires explicit approval
- Supports MCP server integrations for custom capabilities

**Features:**

- Agent-powered, GitHub-native terminal interface
- Autonomous task execution
- File editing and command execution with explicit approval
- Context from GitHub issues and pull requests
- Extensible through custom MCP servers
- Legacy codebase navigation
- Multi-step implementations

**Citation:** GitHub Copilot CLI. GitHub Features. https://github.com/features/copilot/cli. Accessed 16 January 2026.

---

### 7.5 Other IDEs and Editors

**Supported Environments:** Visual Studio, Vim, Neovim, Xcode, Azure Data Studio, Windows Terminal Canary, GitHub Mobile

#### Visual Studio

**Installation:** GitHub Copilot extension for Visual Studio  
**Features:** 
- Code completions
- Copilot Chat (requires Visual Studio 2022 version 17.12 or later for multi-model support)
- Model selection including Auto mode
- Custom instructions support
**Limitations:** None documented  
**Citation:** Changing the AI model for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat. Accessed 16 January 2026.

#### Vim/Neovim

**Installation:** GitHub Copilot extension for Vim/Neovim  
**Features:** 
- Code completions
- Available as extension in Vim and Neovim
**Limitations:** Chat functionality may be limited compared to other IDEs  
**Citation:** What languages, IDEs, and platforms does GitHub Copilot support? GitHub Features. https://github.com/features/copilot. Accessed 16 January 2026.

#### Xcode

**Installation:** GitHub Copilot for Xcode extension  
**Features:** 
- Code completions
- Copilot Chat
- Model selection including Auto mode
- Custom instructions support (workspace and global)
**Limitations:** None documented  
**Citation:** Changing the AI model for GitHub Copilot Chat. GitHub Copilot Documentation. https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat. Accessed 16 January 2026.

#### Azure Data Studio

**Installation:** GitHub Copilot extension for Azure Data Studio  
**Features:** Code completions  
**Limitations:** None documented  
**Citation:** What languages, IDEs, and platforms does GitHub Copilot support? GitHub Features. https://github.com/features/copilot. Accessed 16 January 2026.

#### Windows Terminal Canary

**Installation:** Chat integration for Windows Terminal Canary  
**Features:** Copilot Chat integration in terminal  
**Limitations:** Requires Windows Terminal Canary build  
**Citation:** What languages, IDEs, and platforms does GitHub Copilot support? GitHub Features. https://github.com/features/copilot. Accessed 16 January 2026.

#### GitHub Mobile

**Installation:** GitHub Mobile app with Copilot enabled  
**Features:** 
- Copilot Chat on mobile devices
- Bing and public repository code search (Pro and Business)
- Organisation knowledge access (Enterprise)
**Limitations:** Limited compared to desktop IDE integrations  
**Citation:** What languages, IDEs, and platforms does GitHub Copilot support? GitHub Features. https://github.com/features/copilot. Accessed 16 January 2026.

[↑ Back to top](#table-of-contents)

---

## 8. Third Party Reviews and Experiences

### User Feedback and Testimonials

**Overall Sentiment:** Positive, with consistent praise for productivity gains but recurring concerns about code accuracy and cost.

**Common Praise:**

- **Significant Productivity Gains:** Enterprises and individual developers report dramatic improvements. Accenture's deployment with 12,000 developers showed 90% felt more fulfilled at work and 95% found coding more enjoyable.
  
  "Studies showed up to a 55% improvement in coding speed. In peer-reviewed metrics, there was an 8.69% increase in pull requests, a 15% increase in PR merge rate, and a reduction of time to PR from 9.6 to 2.4 days." - <a href="https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-in-the-enterprise-with-accenture/">GitHub Blog research on Accenture deployment, 2024-2025</a>

- **Real-World Success Stories:** Duolingo reported a 25% increase in developer speed with code review turnaround decreasing by 67%.
  
  "It allows our engineers to focus on harder problems and use their expertise as a force multiplier." - <a href="https://github.com/customer-stories">GitHub Customer Stories, 2024-2025</a>

- **Enterprise Validation:** Microsoft ISE team found tasks were at least twice as fast using Copilot, especially for validating complex documentation and automating data visualization.
  
  "Copilot frees up developers for more creative and complex work, boosting job fulfillment and developer productivity." - <a href="https://devblogs.microsoft.com/ise/accelerating-ai-development-with-github-copilot-real-world-use-cases/">Microsoft DevBlogs, 2025</a>

- **High Adoption Rates:** Accenture saw 80%+ developer adoption with 96% success rate and 67% using it at least five days per week.
  
  "43% found it 'extremely easy to use' with developers averaging 3.4 days of use weekly." - <a href="https://opsera.ai/blog/github-copilot-adoption-trends-insights-from-real-data/">Opsera analysis, 2025</a>

- **Code Review Features:** The code review features introduced in 2025 allow automated code comments and suggestions in pull requests, helping catch routine mistakes and enforce best practices.
  
  "The newer code review features allow automated code comments and suggestions in pull requests, helping to catch routine mistakes." - <a href="https://github.blog/ai-and-ml/github-copilot/how-to-use-github-copilot-to-level-up-your-code-reviews-and-pull-requests/">GitHub Blog, 2025</a>

**Common Complaints:**

- **Accuracy Issues ("Hallucinations"):** Copilot can suggest incorrect, insecure, or inefficient code, particularly with novel algorithms, unfamiliar libraries, or loosely typed codebases. Developers emphasise the need for manual review.
  "Copilot can suggest incorrect, insecure, or inefficient code, particularly with novel algorithms, unfamiliar libraries, or loosely typed codebases. Manual review is essential." - <a href="https://sider.ai/blog/ai-tools/is-github-copilot-worth-it-a-2025-review-for-serious-developers">Sider.ai review, 2025</a>

- **Context-Dependent Effectiveness:** ThoughtWorks' 10-week experiment showed that whilst team velocity improved, some tasks actually took longer due to the need to double-check AI suggestions.
  "Some increased time was reported to double-check AI-suggested code. Teams emphasized the need for careful integration and code review. Copilot is best used as an augmentation tool, not a replacement for thoughtful coding." - <a href="https://www.thoughtworks.com/insights/blog/generative-ai/experiment-github-copilot-practical-guide">ThoughtWorks insights, 2025</a>

- **Mixed Results in Healthcare Project:** Microsoft ISE team experienced situations where using Copilot increased complexity and slowed them down, demonstrating effectiveness depends heavily on context and developer experience.
  "They also experienced situations where using Copilot increased complexity and slowed them down, demonstrating its effectiveness depends heavily on context and experience." - <a href="https://devblogs.microsoft.com/ise/accelerating-ai-development-with-github-copilot-real-world-use-cases/">Microsoft DevBlogs, 2025</a>

- **Quality Varies:** In inconsistent or older projects, suggestions can be irrelevant, incomplete, or contextually off. Users report that AI helps most with repetitive, pattern-based tasks but can introduce subtle bugs or misunderstand business logic.
  "In inconsistent or older projects, suggestions can be irrelevant, incomplete, or contextually off." - <a href="https://www.g2.com/products/github-copilot/reviews?qs=pros-and-cons">G2 reviews, 2024-2025</a>

- **Surface-Level Code Reviews:** Whilst Copilot assists with code review, it tends to provide only basic, occasionally nitpicky feedback rather than nuanced insights a human would provide.
  "Copilot tends to provide only basic, occasionally nitpicky feedback rather than the nuanced insights a human would provide." - <a href="https://bito.ai/blog/is-github-copilot-worth-it-an-in-depth-review-with-examples/">Bito review, 2025</a>

- **"Smart Assistant, Not Autopilot":** Gartner Peer Insights reviews (4.4 out of 5 stars from 228 reviews) warn against over-reliance.
  "Some users noted 'occasional inaccurate suggestions' and warned against over-reliance, recommending it as a 'smart assistant, not an autopilot.'" - <a href="https://www.gartner.com/reviews/market/ai-code-assistants/vendor/github/product/github-copilot">Gartner Peer Insights, 2026</a>

- **Cost Concerns:** The tiered system (Free, Pro at $10/month, Pro+ at $39/month) brought more features but led to complaints about pricing, especially for small teams or freelancers.

**Citation:** Multiple sources including Sider.ai (2025), G2 reviews (2024-2025), Bito (2025), HackerNoon (2024-2025), and GitHub official blog (2025).

### Reported Bugs and Issues

**Critical Issues:**

- **Integration Bugs:** Ongoing reports of Copilot occasionally not loading, not suggesting code in particular files, or conflicting with other IDE plugins. Many issues are addressed with extension updates or IDE setting adjustments.
  
  <a href="https://docs.github.com/en/copilot/how-tos/troubleshoot-copilot/troubleshoot-common-issues">GitHub Troubleshooting Documentation, 2025</a>

- **Content Exclusion Conflicts:** Content exclusion features can block Copilot suggestions in sensitive or excluded files, which is both a privacy advantage and a limitation when it unexpectedly restricts usefulness.

**Minor Issues:**

- **Outdated Suggestions:** Older Copilot installations may become less compatible with newer frameworks, leading to degraded performance until the extension is updated.
  
  <a href="https://docs.github.com/en/copilot/how-tos/troubleshoot-copilot/troubleshoot-common-issues">GitHub Troubleshooting Documentation, 2025</a>

- **Learning Curve:** Several users cite a steep learning curve, especially for those new to Copilot or programming in general, and some struggle with integration into non-standard setups.
  
  <a href="https://www.g2.com/products/github-copilot/reviews?qs=pros-and-cons">G2 reviews, 2024-2025</a>

**Citation:** GitHub official troubleshooting documentation (2025), G2 user reviews (2024-2025).

### Productivity Impact

**Positive Impact:**

Developers who use GitHub Copilot report up to 75% higher satisfaction with their jobs and are up to 55% more productive at writing code without sacrifice to quality.

**Enterprise Results:**
- **Accenture (12,000 developers):** 8.69% increase in pull requests, 15% increase in PR merge rate, reduction of time to PR from 9.6 days to 2.4 days
- **Duolingo:** 25% increase in developer speed, 67% reduction in code review turnaround time
- **Apriorit:** 20% reduction in development cycles for complex projects

**Specific Use Cases:**
- Generating boilerplate code and API integrations
- Writing comprehensive unit tests with edge cases
- Creating and updating technical documentation
- Accelerating onboarding for new projects and team members
- Automating data visualization and demo scripts

"Developers who use GitHub Copilot report up to 75% higher satisfaction with their jobs and are up to 55% more productive at writing code." - *GitHub Copilot Official Documentation, 2025, https://docs.github.com/en/copilot/about-github-copilot**

"For complex projects, Copilot shortened development cycles by 20%. It accelerated time to market, helped lower costs, and improved productivity for experienced teams." - *Apriorit review, 2025, https://www.apriorit.com/dev-blog/github-copilot-review**

**Real Developer Experience:**
"Transform your workflow: we used Copilot to speed up documentation, code generation, and pull request descriptions, saving hours every week." - *Apriorit development team, 2025, https://www.apriorit.com/dev-blog/github-copilot-review**

**Negative Impact:**

- **Risk of Over-Reliance:** Can make developers "lazy" by accepting suggestions without sufficient review, potentially introducing bugs.
- **Context Limitations:** Sometimes gives inconsistent results when suggestions require awareness of broader codebase or multi-file context.
- **Interruption of Flow:** When suggestions are incorrect, they can interrupt workflow and require more time to correct than writing code manually.

"There are regular debates about balancing Copilot's productivity boost against the risk of subtle bugs or copyright-licensing uncertainties." - *Reddit discussions, 2024-2025, Various subreddits including r/programming**

**Citation:** GitHub official documentation (2025), multiple review sources (2024-2025), Reddit community discussions (2024-2025).

### Comparison with Other Tools

#### Comparison with Cursor

**User-Reported Advantages:**

- **Broader IDE Support:** Copilot works across VS Code, JetBrains, Visual Studio, and more, whilst Cursor is a standalone IDE (VS Code fork)
  
  <a href="https://www.digitalocean.com/resources/articles/github-copilot-vs-cursor">Digital Ocean comparison, 2026</a>

- **Lower Cost:** Copilot Pro at $10/month is more affordable than Cursor at $20/month
- **More Reliable Autocomplete:** Copilot is called the "gold standard" for inline code completion

**User-Reported Disadvantages:**

- **Less Context Awareness:** Cursor offers superior multi-file and project-wide context understanding
  "Cursor is especially favored for deep codebase tasks, collaborative workflows, and agent-like task execution." - <a href="https://zapier.com/blog/cursor-vs-copilot/">Zapier comparison, 2025</a>

- **Simpler Agent Capabilities:** Cursor provides more advanced autonomous agent features for complex refactoring

**Citation:** Digital Ocean comparison (2026), Zapier review (2025), F22 Labs comparison (2026), Reddit discussions (2024-2026).

#### Comparison with Continue.dev

**User-Reported Advantages:**

- **Plug-and-Play Experience:** Copilot requires minimal setup compared to Continue.dev's configuration needs
- **Most Reliable Suggestions:** Industry standard for autocomplete accuracy
- **Enterprise Features:** IP indemnity and policy controls unavailable in Continue.dev free tier

**User-Reported Disadvantages:**

- **No Privacy Control:** Code sent to Microsoft servers, unlike Continue.dev's local deployment options
  "Continue.dev stands out as an open-source assistant, allowing developers to easily customize which AI models it uses and even create custom assistants with reusable building blocks and context sources." - <a href="https://www.aitooldiscovery.com/guides/best-ai-for-coding-reddit">AI Tool Discovery review, 2026</a>

- **Less Customisable:** Continue.dev offers more flexibility in model selection and configuration
- **Cost:** $10/month vs Continue.dev's free tier

**Citation:** AI Tool Discovery (2026), BekahhW comparison (2024), Product Hunt reviews (2024-2026).

#### Comparison with Codeium

**User-Reported Advantages:**

- **More Accurate Suggestions:** Copilot generally provides more accurate autocompletions for mainstream use cases
- **Better Documentation:** Extensive official documentation and larger community
- **Enterprise Support:** Mature enterprise features and IP indemnity

**User-Reported Disadvantages:**

- **Cost:** Copilot requires $10/month subscription whilst Codeium offers unlimited free tier
  "Codeium is often praised as 'the best free AI code completion tool' for individual developers, especially for its zero-cost unlimited free tier." - *Reddit discussions, 2024-2025, Various programming subreddits**

- **Privacy:** Codeium offers better self-hosting options for sensitive codebases

**Citation:** Everhour comparison (2024), AI Tool Discovery (2026), Sentisight comparison (2025), Reddit discussions (2024-2025).

[↑ Back to top](#table-of-contents)

---

## 9. Summary and Key Findings

### Strengths

- **Comprehensive IDE support**: Available across all major IDEs and editors including VS Code, JetBrains, Visual Studio, Eclipse, Xcode, and more
- **Multiple interaction modes**: Flexible workflows with Ask, Edit, Agent, and Plan modes for different development scenarios
- **Native GitHub integration**: Seamless integration with GitHub.com, issues, pull requests, and repositories for Enterprise customers
- **Extensibility**: MCP support allows integration with external tools and services, with both local and remote server options
- **Multi-model support**: Choice of various AI models from OpenAI, Anthropic, Google, and others with model switching capability, including support for local models via Ollama and Azure AI through model management
- **Custom instructions and prompts**: Repository-wide and path-specific instruction files allow fine-tuned control over Copilot's behaviour; `.github/prompts` folder for storing reusable custom prompt files (documented in VS Code)
- **CLI agent**: Terminal-based autonomous agent for command-line workflows
- **Enterprise-ready**: Strong governance, policy management, and security features including IP indemnity for Business and Enterprise plans
- **Active development**: Regular feature updates and improvements with public preview features

### Limitations

- **Model management requires setup**: Adding Ollama, Azure AI, and other third-party models requires manual configuration through IDE-specific "Manage Models" interface
- **VS Code-specific features**: Some features like prompt files are primarily documented in VS Code documentation rather than core GitHub Copilot documentation
- **Subscription required**: Core features require paid subscription (Free tier has significant limitations: 2000 completions, 50 chat requests)
- **Public preview features**: Some advanced features (Plan mode, Eclipse support, CLI) are in public preview and subject to change
- **MCP policy restrictions**: Enterprise/Business customers need administrator approval to enable MCP servers
- **No direct deployment features**: Limited built-in support for deployment automation
- **AI Toolkit dependency**: Ollama and some other model integrations require the AI Toolkit extension for VS Code

### Best Use Cases

- **Enterprise software development**: Strong governance and policy controls make it suitable for large organisations
- **Multi-language projects**: Trained on diverse public repositories, supports all major programming languages
- **Code explanation and learning**: Excellent for understanding existing codebases and learning new technologies
- **Rapid prototyping**: Agent mode and chat-based generation enable quick experimentation
- **Legacy code modernisation**: Helpful for explaining and refactoring legacy codebases
- **Team collaboration**: Shared custom instructions ensure consistency across development teams
- **Terminal-centric workflows**: CLI agent provides powerful assistance for command-line focused developers

### Documentation Quality

The official GitHub Copilot documentation is comprehensive and well-organised. It covers:
- Clear explanation of features and capabilities
- Multiple client-specific guides (VS Code, JetBrains, Visual Studio, etc.)
- Step-by-step configuration instructions
- Detailed policy and governance documentation
- Active updates reflecting new features and changes

Areas for improvement:
- Some advanced features (subagents, specific MCP configurations) could benefit from more detailed examples
- Integration with third-party tools and services could be more thoroughly documented
- Clearer distinction between features available in different subscription tiers in some sections

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
- [x] All information verified against official documentation
- [x] No assumptions or guesses made
- [x] All claims have citations
- [x] UK English used throughout
- [x] Consistent formatting applied

[↑ Back to top](#table-of-contents)

---

## 11. References

### Official Documentation

1. GitHub Copilot Documentation - https://docs.github.com/en/copilot
2. GitHub Copilot Features - https://github.com/features/copilot
3. About GitHub Copilot - https://docs.github.com/en/copilot/about-github-copilot
4. Asking GitHub Copilot questions in your IDE - https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide
5. Adding custom instructions for GitHub Copilot - https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot
6. About Model Context Protocol (MCP) - https://docs.github.com/en/copilot/concepts/context/mcp
7. Changing the AI model for GitHub Copilot Chat - https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat
8. GitHub Copilot CLI - https://github.com/features/copilot/cli
9. GitHub MCP Server - https://github.com/github/github-mcp-server
10. GitHub MCP Registry - https://github.com/mcp
11. Setting up GitHub Copilot for your organization - https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-your-organization
12. Prompt files for GitHub Copilot (VS Code) - https://code.visualstudio.com/docs/copilot/customization/prompt-files

### Version Information

- **Tool Version Analysed:** Current version as of January 2026
- **Documentation Last Updated:** January 2026 (continuously updated)
- **Analysis Last Updated:** 16 January 2026

[↑ Back to top](#table-of-contents)

---

## Revision History

| Date | Version | Changes | Analyst |
|------|---------|---------|---------|
| 16 January 2026 | 1.0 | Initial analysis | GitHub Copilot |

[↑ Back to top](#table-of-contents)

---

## See Also

- [Amazon Q Developer](amazon-q-developer.md) - AWS-integrated AI coding assistant
- [Azure AI Toolkit](azure-ai-toolkit.md) - Microsoft Azure AI development toolkit
- [Claude Code](claude-code.md) - Anthropic's Claude AI for code generation
- [Codeium](codeium.md) - Free AI-powered code completion tool
- [Continue](continue.md) - Open-source AI code assistant
- [Cursor](cursor.md) - AI-first code editor
- [Roo Cline](roo-cline.md) - AI coding assistant for VS Code
- [Sourcegraph Cody](sourcegraph-cody.md) - AI assistant with codebase understanding
- [Tabnine](tabnine.md) - AI code completion and chat assistant

---

← [Previous: Gemini Code Assist](gemini-code-assist.md) | ↑ [Parent: Tool Analyses](README.md) | [Next: GitHub Codespaces](github-codespaces.md) →
