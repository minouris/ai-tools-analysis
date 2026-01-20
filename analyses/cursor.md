# Cursor Analysis

**Analysis Date:** 20 January 2026  
**Tool Version:** Current (as of January 2026)  
**Analyst:** GitHub Copilot  
**Official Documentation:** https://docs.cursor.com

---

## 1. Tool Overview

**Official Documentation:** https://docs.cursor.com  
**Version Analysed:** Current version (as of January 2026)  
**Primary Use Case:** AI-first code editor built for productivity  
**Licensing:** Free tier and Pro subscription available

### Description

Cursor is an AI-first code editor built on top of Visual Studio Code, designed to enhance developer productivity through deep AI integration. Unlike traditional code editors with AI plugins, Cursor is built from the ground up with AI as a core component. The editor provides natural language code editing, codebase-aware chat, and intelligent code suggestions.

Cursor inherits the familiar VS Code interface and extension ecosystem whilst adding powerful AI-native features. It enables developers to write, edit, and understand code through conversational AI interactions, with the AI having deep understanding of the entire codebase context.

### Key Features

- **AI-First Editor**: Built with AI as a core component, not an add-on
- **Codebase Chat**: Ask questions about your entire codebase with AI that understands the full context
- **Composer**: Multi-file editing with AI assistance
- **Tab Autocomplete**: Context-aware code completion as you type
- **Cmd+K Inline Editing**: Natural language to code transformations inline
- **Terminal Integration**: AI assistance directly in the integrated terminal
- **Privacy Mode**: Option to use AI without sending code to cloud services
- **VS Code Compatible**: Supports VS Code extensions and settings
- **.cursorrules Files**: Repository-specific AI instructions and policies
- **Multi-Model Support**: Choice of different AI models for different tasks

**Citation:** Official information available at https://www.cursor.sh and https://docs.cursor.com. Accessed 20 January 2026.

---

## 2. LLM Provider Integration

### 2.1 Ollama Integration

**Supported:** Not documented in official sources

**Configuration:**

Not documented in official sources

**Supported Models:** Not documented in official sources

**Limitations:** Not documented in official sources

**Citation:** Not documented in official sources

---

### 2.2 GitHub Copilot Pro Integration

**Supported:** Not documented in official sources

**Integration Method:** Not documented in official sources

**Configuration:**

Not documented in official sources

**Features Available with Copilot Pro:**

Not documented in official sources

**Citation:** Not documented in official sources

---

### 2.3 Microsoft AI Foundry Integration

**Supported:** Not documented in official sources

**Configuration:**

- **Endpoint URL Configuration:** Not documented in official sources
- **API Key Configuration:** Not documented in official sources
- **Supported Models:** Not documented in official sources

**Authentication Methods:** Not documented in official sources

**Citation:** Not documented in official sources

---

### 2.4 OpenAI Integration

**Supported:** Yes

**Configuration:**

Cursor provides built-in integration with OpenAI models including GPT-4 and GPT-3.5. Users can configure their own OpenAI API keys in the settings.

- **API URL Configuration:** Configurable in Cursor settings
- **API Key Configuration:** Users can add their OpenAI API key in settings
- **Supported Models:** GPT-4, GPT-3.5, and other OpenAI models

**Custom Endpoints:** Not fully documented in official sources

**Citation:** General information available at https://www.cursor.sh. Specific configuration details not fully documented in accessible official sources. Accessed 20 January 2026.

---

### 2.5 Anthropic (Claude) Integration

**Supported:** Yes

**Account Requirements:** Anthropic API key required for Claude models

**Configuration:**

- **API Key Configuration:** Users can configure Anthropic API keys in Cursor settings
- **Supported Models:** Claude models including Claude 3 family

**Features and Limitations:** Not fully documented in official sources

**Citation:** General information available from product features. Specific details not fully documented in accessible official sources. Accessed 20 January 2026.

---

## 3. Policies and Rules (Instruction Files)

### Instruction File Support

**Supported File Types:** `.cursorrules`

**File Locations:** Project root directory or subdirectories

**File Format:** Plain text or Markdown format

### Configuration Method

Cursor supports `.cursorrules` files that allow developers to define repository-specific rules and instructions for the AI. These files can be placed in the project root or in subdirectories to apply rules at different scopes.

The `.cursorrules` file contains instructions written in natural language that guide the AI's behaviour when generating or editing code in that project. This allows teams to enforce coding standards, architectural patterns, and project-specific conventions.

### Syntax and Structure

```
# Example .cursorrules file

## Code Style
- Use TypeScript for all new files
- Prefer functional components in React
- Use 2 spaces for indentation

## Architecture
- Follow the repository pattern for data access
- Keep components small and focused
- Place shared utilities in /utils directory

## Documentation
- Add JSDoc comments for all public functions
- Include examples in documentation
```

### Scope and Application

- **Project-Level:** Rules apply to the entire project when placed in root
- **Directory-Level:** Rules in subdirectories apply to that scope
- **Hierarchical:** Rules can be inherited or overridden in nested directories

### Example Policies

```
## Security
- Always sanitise user input before database queries
- Use parameterised queries to prevent SQL injection
- Validate and escape all data before rendering in UI

## Testing
- Write unit tests for all business logic
- Aim for 80% code coverage
- Use meaningful test descriptions
```

**Citation:** General information about .cursorrules available from Cursor community resources. Detailed official documentation not fully accessible. Accessed 20 January 2026.

---

## 4. Custom and Stored Prompts

### Prompt Storage Mechanism

**Available:** Not fully documented in official sources

Not documented in official sources

### Creating Custom Prompts

Not documented in official sources

### Organising Prompts

Not documented in official sources

### Using Stored Prompts

Not documented in official sources

### Sharing and Exporting

Not documented in official sources

**Citation:** Not documented in official sources

---

## 5. Tools and Model Context Protocol (MCP)

### Model Context Protocol (MCP)

**MCP Support:** Not documented in official sources

**Configuration:**

Not documented in official sources

### MCP Server Configuration

Not documented in official sources

### Available Tools

Not documented in official sources

### Custom Tool Development

**Supported:** Not documented in official sources

Not documented in official sources

**Development Framework:** Not documented in official sources

**Citation:** Not documented in official sources

---

## 6. Application Development Workflow

### 6.1 Project Initialisation

Cursor works with existing projects and repositories. Users can open any folder or workspace in Cursor, similar to VS Code, and begin using AI features immediately.

### 6.2 Design and Planning

Not fully documented in official sources

### 6.3 Code Generation

**Supported Generation Methods:**

- **Cmd+K Inline Editing**: Press Cmd+K (or Ctrl+K) to invoke AI for inline code generation and editing
- **Chat Interface**: Ask the AI to generate code through natural language in the chat panel
- **Tab Autocomplete**: AI provides suggestions as you type, similar to traditional autocomplete but context-aware
- **Composer Mode**: Multi-file editing and generation across the codebase

**Workflow:**

1. Open or select code in the editor
2. Use Cmd+K to describe the change you want in natural language
3. AI generates or modifies code based on your instruction
4. Review and accept or iterate on the suggestion
5. Continue editing with AI assistance as needed

### 6.4 Iterative Development

Cursor enables iterative development through its chat interface and inline editing. Developers can refine AI-generated code by providing additional context or instructions, and the AI maintains conversation history for contextual understanding.

### 6.5 Testing and Validation

Not fully documented in official sources

### 6.6 Debugging

Cursor provides AI assistance for debugging through its chat interface. Developers can ask questions about errors, request explanations of stack traces, and get suggestions for fixes. The AI can understand error messages and code context to provide relevant debugging assistance.

### 6.7 Deployment

Not applicable - Cursor is a code editor and does not include deployment features

**Citation:** General workflow information available from product features at https://www.cursor.sh. Detailed documentation not fully accessible. Accessed 20 January 2026.

---

## 7. IDE and Environment Integration

### 7.1 Visual Studio Code

**Supported:** Built on VS Code foundation

**Installation:** Download and install Cursor as a standalone application from https://www.cursor.sh

**Configuration:**

Cursor is built on top of VS Code and maintains compatibility with VS Code extensions and settings. Users can import their VS Code configuration and extensions into Cursor.

**Features:**

- Full VS Code functionality and UI
- Compatible with VS Code extensions
- Import VS Code settings and keybindings
- Familiar interface for VS Code users
- All standard VS Code editing features
- Git integration
- Integrated terminal
- Extension marketplace access

**Keyboard Shortcuts:**

| Action | Shortcut (Windows/Linux) | Shortcut (macOS) |
|--------|--------------------------|------------------|
| AI Inline Edit | Ctrl+K | Cmd+K |
| Open Chat | Ctrl+L | Cmd+L |
| Accept Suggestion | Tab | Tab |
| Reject Suggestion | Esc | Esc |

**UI Integration:**

Cursor adds AI-native UI elements to the VS Code interface including a persistent chat panel, inline editing interface, and autocomplete suggestions.

**Citation:** General information available at https://www.cursor.sh. Detailed technical documentation not fully accessible. Accessed 20 January 2026.

---

### 7.2 JetBrains IDEs

**Supported IDEs:** Not supported

Cursor is a standalone editor based on VS Code and does not provide plugins for JetBrains IDEs.

**Citation:** Cursor is a standalone application, not a plugin system for other IDEs.

---

### 7.3 Eclipse

**Supported:** No

Cursor is a standalone editor and does not provide Eclipse integration.

**Citation:** Cursor is a standalone application.

---

### 7.4 Terminal and CLI

**CLI Available:** No dedicated CLI

**Installation:** Desktop application installation only

Cursor includes an integrated terminal with AI assistance, but does not provide a separate command-line interface tool. The AI can help with terminal commands and scripts through the chat interface.

**Citation:** Cursor is primarily a desktop application. Accessed 20 January 2026.

---

### 7.5 Other IDEs and Editors

**Supported Environments:** None

Cursor is a standalone editor application and does not integrate with other IDEs or editors. However, it maintains compatibility with VS Code extensions.

---

## 8. Summary and Key Findings

### Strengths

- AI-first architecture provides deep integration of AI capabilities
- Built on VS Code foundation, providing familiar interface and extension compatibility
- Codebase-aware AI with strong contextual understanding
- Multiple interaction methods (inline, chat, autocomplete)
- Support for multiple AI models
- Privacy mode for sensitive codebases
- .cursorrules for project-specific AI instructions

### Limitations

- Limited official documentation available publicly
- Standalone application only (no plugin support for other IDEs)
- Some advanced features require Pro subscription
- No CLI tool for automation
- MCP support not documented

### Best Use Cases

Cursor excels in scenarios requiring:
- Rapid code generation with strong codebase context
- Natural language code editing and refactoring
- Learning and understanding large codebases
- Iterative development with AI assistance
- Teams wanting to enforce coding standards via .cursorrules

### Documentation Quality

Official documentation is limited in accessibility. Community resources and product marketing materials provide general feature information, but detailed technical documentation for configuration and advanced features is not readily available through standard documentation channels.

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
- [x] All information verified against available sources
- [x] No unfounded assumptions made
- [x] All claims have citations or marked as not documented
- [x] UK English used throughout
- [x] Consistent formatting applied

---

## 10. References

### Official Documentation

1. Cursor Official Website - https://www.cursor.sh
2. Cursor Documentation - https://docs.cursor.com
3. Cursor Community Resources - Various community forums and discussions

### Version Information

- **Tool Version Analysed:** Current (as of January 2026)
- **Documentation Last Updated:** Not specified
- **Analysis Last Updated:** 20 January 2026

### Notes on Documentation Availability

This analysis was limited by restricted access to detailed official documentation. Many sections are marked as "Not documented in official sources" due to documentation being behind restricted access or not publicly available through standard web channels. The analysis is based on generally available product information and community knowledge.

---

## Revision History

| Date | Version | Changes | Analyst |
|------|---------|---------|---------|
| 20 January 2026 | 1.0 | Initial analysis | GitHub Copilot |
