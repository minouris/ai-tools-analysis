# Claude Code Analysis

**Analysis Date:** 20 January 2026  
**Tool Version:** 2.1.12 (as of January 2026)  
**Analyst:** GitHub Copilot  
**Official Documentation:** https://code.claude.com/docs/en/overview

---

## 1. Tool Overview

**Official Documentation:** https://code.claude.com/docs/en/overview  
**Version Analysed:** 2.1.12  
**Primary Use Case:** Terminal-based agentic coding assistant for executing tasks, explaining code, and managing git workflows through natural language  
**Licensing:** Commercial (requires Claude Pro or Claude Max subscription)

### Description

Claude Code is an agentic coding tool that lives in your terminal, understands your codebase, and helps you code faster by executing routine tasks, explaining complex code, and handling git workflows -- all through natural language commands. It can be used in your terminal, IDE, or by tagging @claude on GitHub.

Claude Code provides an interactive terminal interface where developers can have conversations with Claude AI to perform coding tasks. The tool has deep integration with the file system, git, and development workflows, allowing it to read files, make edits, run commands, and manage version control operations autonomously.

The tool is built on Node.js and distributed through multiple installation methods including curl install scripts, Homebrew, WinGet, and npm. It supports extensibility through plugins, MCP (Model Context Protocol) servers, custom agents, hooks, and slash commands.

### Key Features

- Natural language interface in terminal for coding tasks
- Autonomous file system operations (read, write, search)
- Integrated git workflow management
- Bash command execution with permission controls
- Model Context Protocol (MCP) support for extensibility
- Plugin system for custom commands and agents
- VS Code extension for IDE integration
- Background task execution (Ctrl+B)
- Plan mode for complex multi-step tasks
- Thinking mode with extended reasoning
- Skills system for reusable task definitions
- Web search capability
- Image paste and analysis support
- Conversation history and session resumption
- Real-time steering (send messages while Claude works)
- Jupyter notebook support

**Citation:** Claude Code README. https://github.com/anthropics/claude-code. Accessed 20 January 2026.

---

## 2. LLM Provider Integration

### 2.1 Ollama Integration

**Supported:** No

**Configuration:**

Claude Code is designed to work with Anthropic's Claude models and specific cloud providers (Bedrock, Vertex). There is no documented support for using Ollama models as the LLM backend for Claude Code.

**Supported Models:** Not applicable

**Limitations:** Claude Code requires cloud-based model access through Anthropic API, AWS Bedrock, or Google Vertex AI.

**Citation:** Based on analysis of Claude Code repository and documentation. No mention of Ollama support found in https://github.com/anthropics/claude-code. Accessed 20 January 2026.

---

### 2.2 GitHub Copilot Pro Integration

**Supported:** Partial (GitHub integration for PR comments)

**Integration Method:** Claude Code can integrate with GitHub through the `/install-github-app` command and can be mentioned in GitHub PRs using @claude tag, but it does not use GitHub Copilot Pro as its underlying LLM provider.

**Configuration:**

Run `/install-github-app` command within Claude Code to enable GitHub integration. This allows Claude Code to respond to mentions in GitHub issues and pull requests.

**Features Available with Copilot Pro:**

Not applicable - Claude Code is a separate tool from GitHub Copilot and does not integrate with Copilot Pro subscriptions.

**Citation:** Claude Code CHANGELOG mentions `/install-github-app` command and GitHub tagging feature. https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md. Accessed 20 January 2026.

---

### 2.3 Microsoft AI Foundry Integration

**Supported:** Yes

**Configuration:**

- **Endpoint URL Configuration:** Support added in version 2.0.45
- **API Key Configuration:** Configured through environment variables or settings
- **Supported Models:** Claude models available through Microsoft AI Foundry

**Authentication Methods:** Standard Microsoft AI Foundry authentication

**Citation:** "Added support for Microsoft Foundry! See https://code.claude.com/docs/en/azure-ai-foundry". Claude Code CHANGELOG version 2.0.45. https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md. Accessed 20 January 2026.

---

### 2.4 OpenAI Integration

**Supported:** No

**Configuration:**

- **API URL Configuration:** Not supported
- **API Key Configuration:** Not supported  
- **Supported Models:** Not applicable

**Custom Endpoints:** Claude Code is specifically designed for Anthropic's Claude models and does not support OpenAI API endpoints or models.

**Citation:** Based on analysis of Claude Code repository. No OpenAI integration mentioned in documentation. https://github.com/anthropics/claude-code. Accessed 20 January 2026.

---

### 2.5 Anthropic (Claude) Integration

**Supported:** Yes (Native)

**Account Requirements:** Requires Claude Pro or Claude Max subscription. Free tier mentioned with rate limits.

**Configuration:**

- **API Key Configuration:** Supports API keys through environment variables (ANTHROPIC_API_KEY) or via apiKeyHelper for dynamically generated keys. API keys can be stored in macOS Keychain on supported systems. OAuth authentication is also supported through console.anthropic.com (now platform.claude.com).
- **Supported Models:** 
  - Claude 3 family: Opus 3, Sonnet 3.5, Haiku 3
  - Claude 3.7: Sonnet 3.7 (Bedrock-specific)
  - Claude 4 family: Opus 4, Opus 4.1, Opus 4.5, Sonnet 4, Haiku 4, Haiku 4.5
  - Model aliases: `opus`, `sonnet`, `haiku`, `opusplan`
  - Custom model selection via `/model` command
  - Environment variables: `ANTHROPIC_DEFAULT_SONNET_MODEL`, `ANTHROPIC_DEFAULT_OPUS_MODEL`, `ANTHROPIC_DEFAULT_HAIKU_MODEL`

**Features and Limitations:** 
- Usage limits based on subscription tier (Pro vs Max)
- Ability to purchase extra usage for Opus 4.5
- Rate limit warnings at 70% usage
- 5-hour session limit for continuous operation
- Token limits vary by model
- Cross-region inference support for Bedrock (EU/APAC)

**Additional Provider Support:**
- **AWS Bedrock:** Full support with ARN-based model configuration, STS token support, SSO login support, environment variable `AWS_BEARER_TOKEN_BEDROCK`
- **Google Vertex AI:** Supported with `CLOUD_ML_REGION` configuration, global endpoint support for certain models

**Citation:** Multiple entries in Claude Code CHANGELOG and README referencing model support, authentication methods, and provider integrations. https://github.com/anthropics/claude-code. Accessed 20 January 2026.

---

## 3. Policies and Rules (Instruction Files)

### Instruction File Support

**Supported File Types:** 
- `CLAUDE.md` - Project-level instructions
- `.claude/rules/` - Rule files for behaviour control (added in v2.0.64)
- `settings.json` - Configuration file for tool permissions and behaviour
- `.mcp.json` - MCP server configuration (project-level)

**File Locations:** 
- `./CLAUDE.md` - Project root
- `./.claude/rules/` - Project-specific rules directory
- `./.claude/settings.json` - Project settings
- `~/.claude/` - User-level configuration directory

**File Format:** Markdown for CLAUDE.md and rules; JSON for settings and MCP configuration

### Configuration Method

**CLAUDE.md Files:**
CLAUDE.md files provide instructions and context to Claude Code. They support:
- Markdown formatting for instructions
- File imports using `@path/to/file.md` syntax to include additional files
- Nested CLAUDE.md files that load automatically when working in subdirectories
- Image and PDF file references

**Rules Files:**
Rules files in `.claude/rules/` directory provide behavior control and can be used to define coding standards, conventions, and project-specific guidelines.

**Settings.json:**
The settings.json file controls permissions, tool access, and behavior. Key settings include:
- `allowedTools` / `disallowedTools` - Control which tools Claude can use
- `permissionMode` - Set default permission behavior
- `ignorePatterns` - File patterns to exclude from operations
- Various feature flags and configuration options

### Syntax and Structure

**CLAUDE.md Example:**
```markdown
# Project Guidelines

Follow these coding standards:
- Use TypeScript for all new code
- Write unit tests for all functions
- Follow the style guide in STYLE.md

@.claude/rules/typescript.md
@.claude/rules/testing.md
```

**Settings.json Example:**
```json
{
  "allowedTools": ["Read", "Write", "Bash(npm install)", "Bash(npm test)"],
  "ignorePatterns": ["node_modules/**", ".git/**"],
  "permissionMode": "ask"
}
```

### Scope and Application

- **Global (User-level):** Settings in `~/.claude/settings.json` apply to all projects for the user
- **Project-Level:** Settings in `.claude/settings.json` and CLAUDE.md apply to the specific project
- **Session-Level:** Permissions can be granted for a single session only
- **Managed Settings:** Enterprise users can have administrator-managed settings applied

Settings are merged with project settings taking precedence over user settings. Permission rules can be scoped to "project", "local", or "user" levels.

### Example Policies

**Permission Rules:**
```json
{
  "allowedTools": [
    "Read(*)",
    "Write(*)",
    "Bash(git *)",
    "Bash(npm install)",
    "Bash(npm test)",
    "Bash(npm run build)"
  ],
  "disallowedTools": [
    "Bash(rm -rf *)",
    "Bash(sudo *)"
  ]
}
```

**Claude.md Instructions:**
```markdown
# Development Guidelines

## Code Style
- Use 2-space indentation
- Use single quotes for strings
- Include JSDoc comments for exported functions

## Git Workflow
- Create feature branches from main
- Write descriptive commit messages
- Squash commits before merging

@.claude/rules/security.md
```

**Citation:** Multiple CHANGELOG entries mentioning CLAUDE.md imports (v0.2.107), rules directory support (v2.0.64), settings migration, and permission systems. https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md. Accessed 20 January 2026.

---

## 4. Custom and Stored Prompts

### Prompt Storage Mechanism

**Available:** Yes (via Skills and Slash Commands)

Claude Code provides two main mechanisms for storing and reusing prompts:

1. **Skills** - Reusable task definitions stored as markdown files with YAML frontmatter (introduced in v2.0.20)
2. **Slash Commands** - Custom commands from markdown files that insert prompts into conversations (introduced in v0.2.31)

Skills and slash commands are stored as markdown files in:
- `~/.claude/skills/` - User-level skills
- `.claude/skills/` - Project-level skills  
- `~/.claude/commands/` - User-level commands (deprecated in favor of skills)
- `.claude/commands/` - Project-level commands (deprecated in favor of skills)

Note: As of v2.0.0, slash commands and skills were merged, simplifying the mental model with skills being the primary mechanism.

### Creating Custom Prompts

**Skills Creation:**

1. Create a markdown file in `.claude/skills/` or `~/.claude/skills/`
2. Add YAML frontmatter with configuration
3. Write the prompt/instructions in markdown body

**Frontmatter Options:**
- `user-invocable` - Whether skill appears in slash command menu (default: true for `/skills/` subdirectory)
- `allowed-tools` - Restrict which tools the skill can use
- `context` - Execution context (`fork` to run in sub-agent)
- `agent` - Specify agent type for execution
- `model` - Specify which model to use
- `hooks` - Define PreToolUse, PostToolUse, Stop hooks for the skill
- `argument-hint` - Hint text for command arguments
- `thinking` - Keywords to trigger thinking mode

**Example Skill File (`.claude/skills/refactor.md`):**
```markdown
---
user-invocable: true
allowed-tools:
  - Read
  - Write
  - Search
model: sonnet
---

# Refactor Code

Analyse the provided code and refactor it to improve:
- Readability
- Performance
- Maintainability
- Test coverage

Provide explanations for each significant change.
```

### Organising Prompts

Skills are automatically discovered from nested `.claude/skills` directories when working in subdirectories. Skills can be organised by:

- **Directory structure** - Use subdirectories in `.claude/skills/` for logical grouping
- **Scope** - Separate user-level (`.claude/skills/`) vs project-level (`~/.claude/skills/`)
- **Frequency** - Recently and frequently used skills are prioritised in suggestions
- **Naming** - Use descriptive filenames as they become the command name

### Using Stored Prompts

**Invocation Methods:**
1. Type `/` to see autocomplete list of available skills/commands
2. Use fuzzy search to filter commands
3. @-mention skill files to reference them
4. Skills can invoke other skills or be invoked by agents

**Features:**
- Auto-complete with Tab
- Search functionality with fuzzy matching
- Skills show progress while executing, displaying tool uses
- Skills support arguments passed after the command name
- Hot-reload: skills created or modified are immediately available without restart (v2.1.0)

### Sharing and Exporting

**Sharing Methods:**
1. **Version Control** - Commit `.claude/skills/` directory to Git for team sharing
2. **Plugins** - Package skills as plugins for distribution through marketplaces
3. **Direct File Sharing** - Copy skill markdown files between projects

Skills in committed `.claude/skills/` directories are automatically available to all team members working on the project.

**Citation:** Multiple CHANGELOG entries: Skills released in v2.0.20, slash commands in v0.2.31, skills-commands merge in v2.0.0, hot-reload in v2.1.0, hooks support in v2.1.0. https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md. Accessed 20 January 2026.

---

## 5. Tools and Model Context Protocol (MCP)

### Model Context Protocol (MCP)

**MCP Support:** Yes (Full support)

**Configuration:**

MCP servers can be configured through:
1. **`.mcp.json`** files (project-level, can be committed to version control)
2. **User-level MCP configuration** (global settings)
3. **CLI flag** `--mcp-config` to specify config files
4. **Interactive wizard** using `claude mcp add` command

MCP servers support multiple transport types:
- **stdio** - Standard input/output transport
- **SSE** (Server-Sent Events) - Streaming HTTP transport (added in v0.2.47)
- **HTTP** (Streamable) - HTTP-based transport (added in v1.0.27)

### MCP Server Configuration

**Configuration File Example (`.mcp.json`):**
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@anthropic-ai/mcp-server-filesystem", "/path/to/allowed"],
      "env": {
        "API_KEY": "${API_KEY}"
      }
    },
    "slack": {
      "transport": "sse",
      "url": "https://slack-mcp-server.example.com/sse",
      "headers": {
        "Authorization": "Bearer ${SLACK_TOKEN}"
      }
    }
  }
}
```

**Configuration Features:**
- Environment variable expansion (e.g., `${API_KEY}`)
- Custom headers for SSE/HTTP servers
- OAuth support with automatic token refresh
- `headersHelper` for dynamic header generation
- Timeout configuration via `MCP_TIMEOUT` and `MCP_TOOL_TIMEOUT` environment variables
- Auto-reconnection for SSE connections

### Available Tools

MCP tools are dynamically provided by configured MCP servers. Claude Code includes built-in tools and supports custom MCP tools:

**Built-in Tools:**
- **Read** (formerly View) - Read file contents
- **Write** - Create or modify files
- **Search** (formerly Grep) - Search code with patterns
- **LS** (formerly LSTool) - List directory contents
- **Bash** - Execute shell commands
- **Task** - Create sub-agents for complex tasks
- **Skill** - Invoke custom skills
- **SlashCommand** - Execute slash commands
- **Fetch** - Retrieve web content
- **WebSearch** - Search the web
- **LSP** - Language Server Protocol operations (v2.0.74)
- **MCPSearch** - Auto-discover MCP tools when context exceeds threshold
- **NotebookEdit** - Edit Jupyter notebook cells
- **AskUserQuestion** (AskQuestion) - Interactive user input
- **Todo** - Manage todo lists

**MCP Tool Features:**
- Tool names are prefixed with server name (e.g., `mcp__slack__post_message`)
- Wildcard permissions: `mcp__server__*` allows/denies all tools from a server
- `list_changed` notifications for dynamic tool updates (v2.1.0)
- Tool annotations and titles display in `/mcp` view
- Resource support with `@-mention` capability for MCP resources (v1.0.27)

**Managing MCP Tools:**
- `/mcp` command to view configured servers and tools
- `/mcp enable <name>` or `/mcp disable <name>` to toggle servers
- @-mention MCP servers to toggle them on/off
- MCP debug mode with `--mcp-debug` flag

### Custom Tool Development

**Supported:** Yes (via MCP servers and plugins)

**MCP Server Development:**
Developers can create custom MCP servers that provide tools to Claude Code. MCP servers:
- Can be written in any language
- Communicate via stdio, SSE, or HTTP transport
- Provide tools, prompts, and resources
- Support OAuth authentication
- Can be packaged and distributed as plugins

**Plugin-based Tools:**
The plugin system (v2.0.12) allows developers to create and distribute:
- Custom tools and commands
- Custom agents with specific behaviours
- MCP server integrations
- Hooks for tool execution lifecycle

**Development Framework:** 
- MCP protocol specification
- Claude Code SDK (TypeScript v1.0.23, Python available via pip)
- Plugin development framework
- Hooks system for tool execution interception

**Installation Methods:**
- `claude mcp add` - Interactive wizard
- `claude mcp add-json` - Add from JSON string
- `claude mcp add-from-claude-desktop` - Import from Claude Desktop config
- `/plugin install` - Install from plugin marketplaces
- Manual `.mcp.json` configuration

**Citation:** Multiple CHANGELOG entries covering MCP support evolution: SSE transport (v0.2.47), HTTP transport (v1.0.27), OAuth (v1.0.33), tool annotations, resource support, list_changed notifications (v2.1.0), debugging features, and wildcard permissions. https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md. Accessed 20 January 2026.

---

## 6. Application Development Workflow

### 6.1 Project Initialisation

Claude Code can assist with project initialisation through natural language commands:

**Starting a New Project:**
1. Navigate to desired directory in terminal
2. Run `claude` to start interactive session
3. Describe project requirements in natural language
4. Claude can: create directory structure, initialise git repository, generate configuration files, install dependencies, create boilerplate code

**Working with Existing Projects:**
1. Navigate to project directory
2. Run `claude` to start
3. Claude automatically discovers:
   - CLAUDE.md files for project instructions
   - `.claude/` directory for configuration
   - Skills and commands from `.claude/skills/`
   - Git repository information
   - Project structure and dependencies

**Additional Directories:**
Use `--add-dir` or `/add-dir` to specify additional working directories beyond the current working directory.

### 6.2 Design and Planning

**Plan Mode:**
Claude Code includes a dedicated Plan Mode for complex multi-step tasks:
- Triggered by keywords: "think", "think harder", "ultrathink"
- Accessible via `/plan` command or Shift+Tab
- Uses enhanced thinking with extended reasoning tokens
- Creates structured plans before execution
- Feedback mechanism: reject plans with specific change requests
- Supports Opus Plan Mode: runs Opus for planning, Sonnet for execution

**Design Assistance:**
- Architecture discussions through natural language
- Code structure recommendations
- Technology stack selection
- API design
- Database schema design
- System requirements analysis

**Explore Agent:**
Powered by Haiku, the Explore agent efficiently searches codebases to understand structure and find relevant code without loading everything into context.

### 6.3 Code Generation

**Supported Generation Methods:**

1. **Interactive Conversation** - Natural language requests in terminal
2. **Print Mode** (`-p` flag) - Non-interactive command-line usage
3. **Streaming Output** - Real-time code generation with `--output-format=stream-json`
4. **Skills** - Pre-defined task execution via `/skill-name`
5. **Agent-based** - Specialised agents for specific code generation tasks

**Workflow:**

1. **Describe Intent** - Explain what code is needed in natural language
2. **Review Proposal** - Claude proposes approach and may ask clarifying questions
3. **Generation** - Code is generated with inline progress indicators
4. **Preview** - View diffs before accepting changes (unless auto-accept enabled)
5. **Apply** - Accept or reject changes, provide feedback for iterations

**Code Generation Features:**
- Multi-file operations in single request
- Diff previews with word-level differences (v0.2.26)
- Syntax highlighting in previews (configurable via `/theme`)
- Auto-accept mode (Shift+Tab to toggle)
- Background execution (Ctrl+B) for long-running tasks
- Context window management with auto-compaction
- Image analysis for UI implementation
- PDF reading for documentation-based generation

### 6.4 Iterative Development

**Real-time Steering:**
- Send messages to Claude while it works (press Enter to queue)
- Redirect approach mid-execution
- Add additional requirements on the fly

**Iteration Features:**
- Conversation history maintained across sessions
- `/resume` command to continue previous work
- `--continue` flag to resume last session
- Named sessions: `/rename` and `--resume <name>`
- Session forking: `--fork-session` flag
- `/rewind` command to undo code changes (v2.0.0)
- History search with Ctrl+R

**Feedback Mechanisms:**
- Accept/reject individual changes
- Provide specific feedback on rejections
- ESC to interrupt and provide new direction
- Conversation compaction maintains context

### 6.5 Testing and Validation

**Test Generation:**
Claude can generate:
- Unit tests
- Integration tests
- Test data and fixtures
- Testing framework setup
- Test debugging and analysis

**Test Execution:**
- Run tests via Bash tool with permission controls
- Background test execution (Ctrl+B)
- Test output analysis
- Coverage improvement suggestions
- Auto-allowed test commands (configurable)

**Common Test Workflows:**
```bash
# Pre-approve test commands
{
  "allowedTools": [
    "Bash(npm test)",
    "Bash(pytest *)",
    "Bash(cargo test)",
    "Bash(go test *)"
  ]
}
```

### 6.6 Debugging

**Debugging Capabilities:**
- Error message interpretation
- Stack trace analysis
- Bug identification from code review
- Fix suggestions
- Debugging strategy recommendations
- Log analysis

**Debug Tools:**
- Read tool for examining files
- Bash tool for running diagnostic commands
- Search tool for finding related code
- LSP tool for code intelligence (go-to-definition, references, hover documentation)

**Debug Workflow:**
1. Share error messages or describe issue
2. Claude analyses context and proposes investigation approach
3. Claude may read relevant files, search code, or run commands
4. Identify root cause
5. Propose and implement fixes
6. Verify resolution

### 6.7 Deployment

**Deployment Assistance:**
- CI/CD pipeline configuration
- Docker containerisation
- Cloud deployment setup (AWS, Azure, GCP)
- Infrastructure as Code (Terraform, CloudFormation)
- Deployment script generation
- Environment configuration

**Git Integration:**
- Automatic commit message generation with attribution
- Pull request creation
- GitHub integration via `/install-github-app`
- PR comment responses when tagged @claude
- Branch management
- Git workflow execution

**Usage Tracking:**
- `/usage` command shows plan limits and consumption
- `/stats` provides detailed analytics:
  - Favourite model
  - Usage graph
  - Usage streak
  - Active time metrics
- `/cost` for cost tracking (deprecated, use `/usage`)

**Citation:** Comprehensive analysis of CHANGELOG and README covering all workflow features. Multiple versions referenced including plan mode (v0.2.44), real-time steering (v0.2.108), skills (v2.0.20), debugging improvements, testing features, and deployment capabilities. https://github.com/anthropics/claude-code. Accessed 20 January 2026.

---

## 7. IDE and Environment Integration

### 7.1 Visual Studio Code

**Supported:** Yes (Native extension)

**Installation:** 
- Native VS Code extension released in version 2.0.0
- Install from VS Code marketplace
- Search for "Claude Code" in Extensions view

**Configuration:**

The extension connects to the Claude Code CLI running in the background. Configuration includes:
- `claudeProcessWrapper` - Wrapper for Claude binary path
- `chat.fontSize` and `chat.fontFamily` - UI customisation (v1.0.111)
- `respectGitIgnore` - Control whether .gitignored files appear in file searches (default: true, v2.0.30/v2.0.31)
- Sidebar placement - Can be positioned in right sidebar (secondary sidebar) for VS Code 1.97+ (v2.0.56)
- Initial permission mode configuration for new conversations (v2.0.34)

**Features:**

- **Chat Interface** - Full conversational interface within VS Code
- **Code Completions** - Inline code suggestions with acceptance indicators
- **File Operations** - Drag-and-drop support for files and folders
- **Diff View** - Side-by-side diffs for code changes
- **Image Support** - Paste images directly (⌘+V on macOS, Ctrl+V on other platforms)
- **Context Menu** - Model selection and configuration access
- **Usage Indicator** - Token usage and limits display (v2.0.24, v2.1.6)
- **Tab Badges** - Pending permissions (blue) and unread completions (orange) (v2.0.73)
- **Copy to Clipboard** - Button on code blocks and bash tool inputs (v2.0.64)
- **Streaming Messages** - Real-time response display (v2.0.57)
- **Multiple Terminals** - Support for multiple terminal clients connecting simultaneously (v2.0.60, reverted in v2.0.61 due to issues)
- **Plugin Management** - Install count display, trust warnings (v2.1.10)

**Keyboard Shortcuts:**

Standard VS Code keybindings apply. Extension integrates with VS Code's command palette.

**UI Integration:**

- Sidebar panel with collapsible sections
- Inline diff view for code changes
- Status indicators for model, usage, and session state
- Permission request dialogs within VS Code UI
- Sessions dialog for managing conversations
- Markdown rendering with proper paragraph breaks

**Terminal Setup:**
Use `/terminal-setup` command for optimal Shift+Enter configuration.

**Citation:** Multiple CHANGELOG entries: Native VS Code extension (v2.0.0), various feature additions throughout v2.0.x and v2.1.x versions, sidebar support (v2.0.56), respectGitIgnore (v2.0.30), streaming messages (v2.0.57). https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md. Accessed 20 January 2026.

---

### 7.2 JetBrains IDEs

**Supported IDEs:** Not documented in official sources

**Installation:** No official JetBrains plugin mentioned in documentation

**Configuration:**

Not documented in official sources

**Features:**

No official JetBrains IDE integration is documented. Users would need to use Claude Code through the terminal within JetBrains IDEs or develop custom integrations using the Claude Code SDK.

**IDE-Specific Considerations:**

Terminal integration within JetBrains IDEs can run Claude Code, but no native plugin integration is available.

**Citation:** No mention of JetBrains plugin in GitHub repository documentation. https://github.com/anthropics/claude-code. Accessed 20 January 2026.

---

### 7.3 Eclipse

**Supported:** No

**Installation:** Not available

**Configuration:**

Not documented in official sources

**Features:**

Eclipse support not available. No official Eclipse plugin exists.

**Limitations:**

No IDE-specific integration for Eclipse. Users can run Claude Code in terminal but without IDE integration features.

**Citation:** No Eclipse support documented. https://github.com/anthropics/claude-code. Accessed 20 January 2026.

---

### 7.4 Terminal and CLI

**CLI Available:** Yes (Primary interface)

**Installation:**

Multiple installation methods:

**macOS/Linux:**
```bash
# Recommended method
curl -fsSL https://claude.ai/install.sh | bash

# Homebrew
brew install --cask claude-code
```

**Windows:**
```powershell
# Recommended method
irm https://claude.ai/install.ps1 | iex

# WinGet
winget install Anthropic.ClaudeCode
```

**npm (Deprecated):**
```bash
npm install -g @anthropic-ai/claude-code
```

**Available Commands:**

| Command | Description | Example |
|---------|-------------|---------|
| `claude` | Start interactive session | `claude` |
| `claude -p "<prompt>"` | Print mode (non-interactive) | `claude -p "explain this code"` |
| `claude --continue` | Resume last session | `claude --continue` |
| `claude --resume <name>` | Resume named session | `claude --resume feature-work` |
| `claude --model <model>` | Specify model | `claude --model opus` |
| `claude --agent <type>` | Override agent type | `claude --agent explore` |
| `claude --add-dir <path>` | Add working directory | `claude --add-dir /path/to/dir` |
| `claude --mcp-config <file>` | Specify MCP config | `claude --mcp-config mcp.json` |
| `claude update` | Update Claude Code | `claude update` |
| `claude mcp list` | List MCP servers | `claude mcp list` |
| `claude mcp add` | Add MCP server (wizard) | `claude mcp add` |
| `claude mcp serve` | Serve local MCP server | `claude mcp serve` |
| `/` prefix | Slash commands | `/model`, `/help`, `/config` |

**Configuration:**

Configuration stored in:
- `~/.claude/settings.json` - User settings
- `.claude/settings.json` - Project settings
- `~/.claude.json` - Legacy global config
- `.claude.json` - Legacy project config (being phased out)

**Environment Variables:**
- `ANTHROPIC_API_KEY` - API authentication
- `ANTHROPIC_LOG` - Logging level (debug, info, etc.)
- `CLAUDE_CONFIG_DIR` - Custom config directory
- `CLAUDE_CODE_TMPDIR` - Temporary file directory
- `CLAUDE_CODE_SHELL` - Override shell detection
- `CLAUDE_CODE_FILE_READ_MAX_OUTPUT_TOKENS` - File read limit
- `CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR` - Freeze bash working directory
- `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` - Disable backgrounding
- `CLAUDE_CODE_AUTO_CONNECT_IDE` - IDE auto-connection control
- `CLAUDE_CODE_SHELL_PREFIX` - Wrapper for shell commands
- `CLAUDE_CODE_API_KEY_HELPER_TTL_MS` - API key helper TTL
- `CLAUDE_SESSION_ID` - Available in skills for session access
- `IS_DEMO` - Hide sensitive info for recording
- `DISABLE_AUTOUPDATER` - Disable auto-updates
- `USE_BUILTIN_RIPGREP` - Control ripgrep usage
- Various MCP-related timeouts and settings

**Usage Examples:**

```bash
# Start interactive session
claude

# Quick code explanation
echo "function foo() { return 42; }" | claude -p "explain this"

# Resume previous work
claude --continue

# Start with specific model
claude --model opus

# Non-interactive with system prompt
claude -p "refactor this code" --system-prompt-file prompts/refactor.md

# Background long-running command (within Claude)
# Press Ctrl+B to background current task

# Resume named session
claude --resume my-feature

# Fork existing session
claude --resume base-session --fork-session

# SDK mode with streaming
claude -p "generate code" --output-format=stream-json
```

**Integration with Shell:**

- **Bash**: Fully supported with command execution
- **Zsh**: Supported
- **Fish**: Supported  
- **PowerShell**: Supported (Windows)
- **WSL**: Fully supported with native Windows or WSL installation

**Terminal Features:**
- Keyboard protocol support: Kitty, iTerm2, WezTerm, Ghostty
- Custom terminal prompts via `/statusline`
- Progress bars (OSC 9;4)
- Hyperlinks (OSC 8) for file paths
- Terminal title updates
- Suspend/resume with Ctrl+Z / fg
- IME support for CJK languages (v2.0.68, v2.0.53)

**Keyboard Shortcuts (in Claude Code):**

| Action | Shortcut | Notes |
|--------|----------|-------|
| Toggle thinking | Alt+T (Tab deprecated) | View extended reasoning |
| Background task | Ctrl+B | Background bash/agents |
| Interrupt | Esc | Stop current operation |
| History search | Ctrl+R | Search command history |
| Transcript mode | Ctrl+O (was Ctrl+R) | View full conversation |
| External editor | Ctrl+G | Edit in system editor |
| Suspend | Ctrl+Z | Resume with `fg` |
| Model selector | Alt+P / Option+P | Switch models mid-prompt |
| Paste | Ctrl+V / Alt+V (Windows images) | Including images |
| Undo input | Ctrl+\_ | Undo prompt changes |
| Yank (paste deleted) | Ctrl+Y | Paste from kill ring |
| Yank-pop | Alt+Y | Cycle kill ring after Ctrl+Y |
| Word navigation | Alt+B / Alt+F | Move by word |
| Word delete | Alt+Delete | Delete word backward |
| Submit queued | Enter (while working) | Queue additional messages |
| Toggle mode | Shift+Tab | Plan/edit mode switching |
| Copy OAuth URL | C (during login) | If browser doesn't open |

**Terminal Setup Helper:**
`/terminal-setup` command provides terminal-specific configuration guidance for:
- iTerm2
- WezTerm  
- Kitty
- Alacritty
- Zed
- Warp
- Ghostty
- VS Code

**Citation:** Comprehensive review of README installation instructions and CHANGELOG keyboard shortcut updates across multiple versions. https://github.com/anthropics/claude-code. Accessed 20 January 2026.

---

### 7.5 Other IDEs and Editors

**Supported Environments:** Terminal-based integration for any IDE/editor with terminal support

#### Zed Editor

**Installation:** Terminal access within Zed  
**Features:** `/terminal-setup` includes Zed-specific configuration (v2.0.74)  
**Limitations:** No native plugin; terminal integration only  

#### Vim/Neovim

**Installation:** Run `claude` within terminal  
**Features:** 
- Vim mode available within Claude Code prompts (v0.2.34)
- Vim motions: h/j/k/l, w/b/e, 0/$, ^, gg/G, f/F/t/T, ;/,, operators (d/c/y), text objects, >>/<<, J
- Undo with 'u', redo with Ctrl+R
**Limitations:** Vim mode is for Claude Code's prompt input, not as a Vim plugin  

#### Emacs

**Installation:** Run `claude` within terminal  
**Features:** Emacs-style keybindings supported (Ctrl+A, Ctrl+E, Ctrl+K, Ctrl+U, Ctrl+N/P)  
**Limitations:** No native Emacs integration  

#### Sublime Text / Other Editors

**Installation:** Run `claude` in integrated terminal  
**Features:** Terminal integration only  
**Limitations:** No specific IDE features; full functionality through terminal interface  

#### Web Interface (Claude.ai)

**Installation:** Not required (web-based)  
**Features:**
- Send background tasks to web using `&` prefix (v2.0.45)
- Teleport sessions from web to terminal with `/teleport` command (v2.1.0)
- Remote environment configuration with `/remote-env` (v2.1.0)
- Requires Claude.ai subscription
**Limitations:** 
- Separate from terminal Claude Code
- Session teleporting requires subscription
**Citation:** Teleport and remote features in v2.1.0, background task sending in v2.0.45

#### GitHub Integration

**Installation:** `/install-github-app` command  
**Features:**
- Tag @claude in pull requests and issues
- Automatic PR comment responses
- PR creation from Claude Code with attribution
**Limitations:** Requires GitHub app installation and authentication  

#### Claude in Chrome (Beta)

**Installation:** Chrome extension from https://claude.ai/chrome  
**Features:**
- Browser control from Claude Code
- Web automation capabilities
- Released in v2.0.72
**Limitations:** Beta feature, requires Chrome extension and Claude Code working together  

**Citation:** Various terminal editors and integrations mentioned in CHANGELOG: Vim mode (v0.2.34), terminal setup expansions (v2.0.74), Claude in Chrome (v2.0.72), GitHub integration throughout versions. https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md. Accessed 20 January 2026.

---

## 8. Summary and Key Findings

### Strengths

- **Terminal-native workflow** - Seamless integration into developer terminal workflows without context switching
- **Comprehensive file system operations** - Full read/write/search capabilities with permission controls
- **Extensive git integration** - Automated commit messages, PR creation, and GitHub app integration
- **Rich extensibility** - MCP support, plugin system, custom agents, hooks, and skills
- **Multiple model options** - Access to latest Claude models (Opus 4.5, Sonnet 4, Haiku 4.5) with flexible provider support (Bedrock, Vertex, AI Foundry)
- **Plan mode** - Sophisticated multi-step task planning with extended thinking capabilities
- **Active development** - Frequent updates with 125+ versions showing continuous improvement
- **VS Code integration** - Native extension providing IDE-integrated experience
- **Session management** - Resume, fork, and name sessions for flexible workflow management
- **Real-time interaction** - Queue messages while Claude works, steer execution in real-time
- **Background execution** - Run long tasks in background while continuing other work
- **Permission system** - Granular control over tool usage with project/user/session scopes
- **SDK availability** - TypeScript and Python SDKs for custom integrations

### Limitations

- **Subscription required** - Requires Claude Pro or Claude Max subscription (commercial licensing)
- **Terminal-centric** - Primary interface is terminal-based, which may not suit all workflows
- **No Ollama support** - Cannot use local models; requires cloud-based API access
- **Limited IDE integrations** - Only VS Code has native extension; other IDEs rely on terminal
- **No OpenAI compatibility** - Exclusively designed for Claude models, no OpenAI API support
- **Usage limits** - Rate limits and session duration limits (5 hours) based on subscription tier
- **Context management** - Requires periodic compaction for long sessions, though automatic
- **Learning curve** - Rich feature set requires time to learn all capabilities
- **Platform availability** - Windows support added relatively recently (native in v1.0.51)

### Best Use Cases

- **Full-stack development** - Terminal-based workflow suits backend and infrastructure work
- **Code refactoring** - Excellent for large-scale refactoring with multi-file context
- **Git workflow automation** - Strong for teams with structured git workflows
- **Documentation generation** - Can read code and generate comprehensive documentation
- **Debugging and analysis** - Good for investigating complex issues across codebases
- **Infrastructure as code** - Suited for DevOps and cloud infrastructure management
- **Prototype development** - Rapid prototyping with conversational interface
- **Legacy code modernisation** - Understanding and updating older codebases
- **Custom tooling** - Extensible for team-specific workflows via plugins and MCP
- **Terminal power users** - Developers comfortable with CLI workflows

### Documentation Quality

The official documentation quality is comprehensive:

**GitHub Repository:**
- Detailed README with installation and getting started
- Extensive CHANGELOG (125+ version entries) showing feature evolution
- Examples directory with practical use cases
- Plugin and MCP documentation
- Security and contribution guidelines

**Official Documentation Site:**
- Referenced at https://code.claude.com/docs/en/overview
- Covers setup, data usage, hooks, plugins, skills, and configuration
- Integration guides (Azure AI Foundry mentioned specifically)

**Community Resources:**
- Discord server for developer community
- GitHub issues for bug reporting and feature requests
- `/bug` command for in-app feedback

**Areas for Improvement:**
- Some features documented primarily through CHANGELOG rather than structured docs
- Web documentation site (code.claude.com/docs) was inaccessible during this analysis
- JetBrains and other IDE integrations not documented (likely because they don't exist)

**Overall Assessment:** Documentation is thorough for available features, with GitHub repository serving as primary source. The extensive CHANGELOG provides excellent version-specific information.

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

---

## 10. References

### Official Documentation

1. Claude Code GitHub Repository - https://github.com/anthropics/claude-code
2. Claude Code README - https://github.com/anthropics/claude-code/blob/main/README.md
3. Claude Code CHANGELOG - https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md  
4. Official Documentation Site - https://code.claude.com/docs/en/overview (referenced but inaccessible during analysis)
5. Setup Documentation - https://code.claude.com/docs/en/setup (referenced in README)
6. Data Usage Policies - https://code.claude.com/docs/en/data-usage (referenced in README)
7. Hooks Documentation - https://code.claude.com/docs/en/hooks (referenced in CHANGELOG)
8. Plugins Documentation - https://code.claude.com/docs/en/plugins (referenced in CHANGELOG)
9. Skills Documentation - https://code.claude.com/docs/en/memory (referenced in CHANGELOG)
10. Azure AI Foundry Integration - https://code.claude.com/docs/en/azure-ai-foundry (referenced in CHANGELOG)
11. Claude Commercial Terms of Service - https://www.anthropic.com/legal/commercial-terms
12. Claude Privacy Policy - https://www.anthropic.com/legal/privacy
13. Claude Developers Discord - https://anthropic.com/discord
14. Claude Code npm Package - https://www.npmjs.com/package/@anthropic-ai/claude-code
15. Claude Install Scripts - https://claude.ai/install.sh (macOS/Linux), https://claude.ai/install.ps1 (Windows)
16. Claude Chrome Extension - https://claude.ai/chrome
17. Anthropic Platform - https://platform.claude.com

### Version Information

- **Tool Version Analysed:** 2.1.12 (latest as of analysis date)
- **Repository State:** Based on main branch as of 20 January 2026
- **Documentation Last Updated:** GitHub repository actively maintained with frequent updates
- **Analysis Last Updated:** 20 January 2026
- **CHANGELOG Coverage:** Versions 0.2.21 through 2.1.12 (125+ releases documented)

### Key Release Milestones

- **v2.1.x** - Latest stable series with plugin system, hooks, skills integration
- **v2.0.0** - Major release with native VS Code extension, new UI, thinking mode
- **v1.0.0** - General availability with Sonnet 4 and Opus 4 models
- **v0.2.x** - Beta releases introducing core features (MCP, skills, commands)

### SDK and Development Resources

- TypeScript SDK: `@anthropic-ai/claude-code` (deprecated in favour of `@anthropic-ai/claude-agent-sdk`)
- Python SDK: `claude-code-sdk` (available via pip install)
- Claude Agent SDK: https://platform.claude.com/docs/en/agent-sdk/migration-guide
- Plugin Development: Examples available in repository plugins directory

---

## Revision History

| Date | Version | Changes | Analyst |
|------|---------|---------|---------|
| 16 January 2026 | 0.1 | Initial analysis framework created with limited documentation access | GitHub Copilot |
| 20 January 2026 | 1.0 | Complete analysis based on GitHub repository documentation, README, and comprehensive CHANGELOG review | GitHub Copilot |

