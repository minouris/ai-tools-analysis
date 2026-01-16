# Reusable Analysis Plan for AI Coding Tools

## Overview

This document provides a standardised methodology for analysing AI coding tools. When creating an analysis of a new AI coding tool, follow this plan to ensure comprehensive and consistent evaluation.

## Important Guidelines

**When conducting an analysis using this plan:**

- ✅ **Rely entirely on official documentation** for the tool being analysed
- ❌ **Make NO guesses or assumptions** about functionality
- 📚 **Provide citations and links** to official documentation for every claim
- 🇬🇧 **Use UK English** throughout the analysis
- 📝 **Create a dedicated page** for each tool analysis in a consistent format

---

## Analysis Structure

Each tool analysis should follow this structure and address each section thoroughly.

### 1. Tool Overview

**Purpose:** Provide a clear introduction to the tool.

**Required Information:**
- Tool name and vendor/maintainer
- Official website and documentation links
- Primary use case and target audience
- Key distinguishing features
- Current version/release information
- Licensing model (open-source, commercial, freemium, etc.)

**Documentation to Reference:**
- Official product page
- README or introduction documentation
- Release notes or changelog

**Template:**
```markdown
## [Tool Name] Overview

**Official Documentation:** [Link]
**Version Analysed:** [Version Number]
**Primary Use Case:** [Description]

[Detailed description of the tool, its purpose, and key features]

**Citation:** [Official documentation links]
```

---

### 2. LLM Provider Integration

**Purpose:** Document how the tool integrates with various LLM providers and services.

#### 2.1 Local LLM (Ollama)

**Required Information:**
- Whether Ollama is supported
- Configuration steps required
- Which models can be used
- Performance considerations
- Any limitations or constraints

**Template:**
```markdown
### Ollama Integration

**Supported:** [Yes/No/Partial]

**Configuration:**
[Step-by-step configuration instructions from official docs]

**Supported Models:** [List of models]

**Citation:** [Official documentation links]
```

#### 2.2 GitHub Copilot Pro Subscription

**Required Information:**
- Whether Copilot Pro is supported or required
- Integration method
- Features available with Copilot Pro
- Configuration requirements

**Template:**
```markdown
### GitHub Copilot Pro Integration

**Supported:** [Yes/No/Partial]

**Integration Method:** [Description]

**Configuration:**
[Step-by-step configuration instructions]

**Citation:** [Official documentation links]
```

#### 2.3 Microsoft AI Foundry

**Required Information:**
- Support for Azure AI services
- How to configure endpoint URL
- How to configure API keys
- Supported Azure AI models
- Authentication methods

**Template:**
```markdown
### Microsoft AI Foundry Integration

**Supported:** [Yes/No/Partial]

**Configuration:**
- **Endpoint URL Configuration:** [Instructions]
- **API Key Configuration:** [Instructions]
- **Supported Models:** [List]

**Citation:** [Official documentation links]
```

#### 2.4 OpenAI Integration

**Required Information:**
- OpenAI API support
- Configuration of custom OpenAI URLs
- Supported models (GPT-3.5, GPT-4, etc.)
- API key configuration

**Template:**
```markdown
### OpenAI Integration

**Supported:** [Yes/No/Partial]

**Configuration:**
- **API URL Configuration:** [Instructions]
- **API Key Configuration:** [Instructions]
- **Supported Models:** [List]

**Citation:** [Official documentation links]
```

#### 2.5 Anthropic Integration

**Required Information:**
- Claude API support
- Account setup requirements
- API key configuration
- Supported Claude models
- Any specific features or limitations

**Template:**
```markdown
### Anthropic (Claude) Integration

**Supported:** [Yes/No/Partial]

**Account Requirements:** [Description]

**Configuration:**
- **API Key Configuration:** [Instructions]
- **Supported Models:** [List]

**Citation:** [Official documentation links]
```

---

### 3. Policies and Rules (Instruction Files)

**Purpose:** Document how to configure policies, rules, and instructions that guide the tool's behaviour.

**Required Information:**
- Types of instruction files supported (e.g., `.github/copilot-instructions.md`, `.cursorrules`, etc.)
- File formats and locations
- Syntax and structure of instruction files
- Scope of rules (global, project-level, file-level)
- Examples of common policies
- How the tool interprets and applies these rules

**Template:**
```markdown
## Policies and Rules Configuration

### Instruction File Support

**Supported File Types:** [List]
**File Locations:** [Paths]

### Configuration Method

[Detailed explanation of how to create and configure instruction files]

### Syntax and Structure

[Examples and syntax rules]

### Scope and Application

[How the tool applies these rules]

**Citation:** [Official documentation links]
```

---

### 4. Custom and Stored Prompts

**Purpose:** Document how users can create, store, and reuse custom prompts.

**Required Information:**
- Prompt library or storage mechanisms
- How to create custom prompts
- How to organise and categorise prompts
- How to invoke stored prompts
- Sharing and exporting prompt collections
- Template or snippet functionality

**Template:**
```markdown
## Custom and Stored Prompts

### Prompt Storage Mechanism

[Description of how prompts are stored]

### Creating Custom Prompts

[Step-by-step instructions]

### Organising Prompts

[Instructions for categorisation and management]

### Using Stored Prompts

[Instructions for invoking and using saved prompts]

**Citation:** [Official documentation links]
```

---

### 5. Tools and Model Context Protocol (MCP)

**Purpose:** Document the tool's support for extensions, plugins, and MCP.

**Required Information:**
- Support for MCP (Model Context Protocol)
- How to configure MCP servers
- Available MCP tools and their purposes
- Custom tool/plugin development
- Tool marketplace or registry
- How tools extend functionality

**Template:**
```markdown
## Tools and MCP Support

### Model Context Protocol (MCP)

**MCP Support:** [Yes/No/Partial]

**Configuration:**
[How to configure MCP servers and tools]

### Available Tools

[List of available tools and their functions]

### Custom Tool Development

[Information about creating custom tools, if supported]

**Citation:** [Official documentation links]
```

---

### 6. Application Development Workflow

**Purpose:** Document the complete workflow from design to code generation.

**Required Information:**
- Project initialisation process
- Design and planning features
- Code generation workflow
- Iterative development process
- Code review and refinement
- Testing integration
- Debugging support
- Deployment considerations

**Template:**
```markdown
## Application Development Workflow

### 1. Project Initialisation

[How to start a new project]

### 2. Design and Planning

[Features for design and architecture planning]

### 3. Code Generation

[How to generate code from requirements or prompts]

### 4. Iterative Development

[How to refine and iterate on generated code]

### 5. Testing and Validation

[Integration with testing frameworks]

### 6. Debugging

[Debugging features and workflow]

### 7. Deployment

[Deployment-related features, if any]

**Citation:** [Official documentation links]
```

---

### 7. IDE and Environment Integration

**Purpose:** Document how the tool integrates with various development environments.

#### 7.1 Visual Studio Code

**Required Information:**
- Installation method (extension, plugin, etc.)
- Configuration steps
- Available features in VS Code
- Keyboard shortcuts and commands
- UI integration points

**Template:**
```markdown
### Visual Studio Code Integration

**Installation:** [Method and link]

**Configuration:**
[Setup instructions]

**Features:**
[List of available features]

**Usage:**
[How to use the tool within VS Code]

**Citation:** [Official documentation links]
```

#### 7.2 JetBrains IDEs

**Required Information:**
- Supported JetBrains IDEs (IntelliJ IDEA, PyCharm, WebStorm, etc.)
- Installation method
- Configuration steps
- Available features
- IDE-specific considerations

**Template:**
```markdown
### JetBrains IDEs Integration

**Supported IDEs:** [List]

**Installation:** [Method and link]

**Configuration:**
[Setup instructions]

**Features:**
[List of available features]

**Citation:** [Official documentation links]
```

#### 7.3 Eclipse

**Required Information:**
- Eclipse support availability
- Installation method
- Configuration steps
- Available features
- Limitations compared to other IDEs

**Template:**
```markdown
### Eclipse Integration

**Supported:** [Yes/No/Partial]

**Installation:** [Method and link, if available]

**Configuration:**
[Setup instructions, if available]

**Features:**
[List of available features, if any]

**Citation:** [Official documentation links]
```

#### 7.4 Terminal and CLI

**Required Information:**
- Command-line interface availability
- Installation method
- Available commands
- Configuration options
- Use cases for CLI usage
- Integration with shell environments

**Template:**
```markdown
### Terminal and CLI Integration

**CLI Available:** [Yes/No]

**Installation:** [Method]

**Available Commands:**
[List of commands with descriptions]

**Configuration:**
[CLI configuration options]

**Usage Examples:**
[Common use cases and examples]

**Citation:** [Official documentation links]
```

#### 7.5 Other IDEs and Editors

**Required Information:**
- Support for other editors (Vim, Emacs, Sublime Text, etc.)
- Installation methods
- Features and limitations
- Alternative integration methods (LSP, plugins, etc.)

**Template:**
```markdown
### Other IDE and Editor Support

**Supported Environments:** [List]

[For each supported environment:]

#### [Environment Name]

**Installation:** [Method]
**Features:** [List]
**Limitations:** [Any known limitations]

**Citation:** [Official documentation links]
```

---

## Analysis Checklist

Use this checklist to ensure completeness when analysing a tool:

- [ ] Tool overview completed with all required information
- [ ] Ollama integration documented with citations
- [ ] GitHub Copilot Pro integration documented with citations
- [ ] Microsoft AI Foundry integration documented with citations
- [ ] OpenAI integration documented with citations
- [ ] Anthropic integration documented with citations
- [ ] Policies and rules configuration documented with citations
- [ ] Custom and stored prompts documented with citations
- [ ] Tools and MCP support documented with citations
- [ ] Application development workflow documented with citations
- [ ] VS Code integration documented with citations
- [ ] JetBrains IDEs integration documented with citations
- [ ] Eclipse integration documented with citations
- [ ] Terminal/CLI integration documented with citations
- [ ] Other applicable IDEs documented with citations
- [ ] All information verified against official documentation
- [ ] No assumptions or guesses made
- [ ] All claims have citations
- [ ] UK English used throughout
- [ ] Consistent formatting applied

---

## Document Organisation

**Recommended File Structure:**

```
/analyses
  /[tool-name]
    - overview.md          # Section 1
    - llm-integration.md   # Section 2
    - policies-rules.md    # Section 3
    - prompts.md           # Section 4
    - tools-mcp.md         # Section 5
    - workflow.md          # Section 6
    - ide-integration.md   # Section 7
```

**Alternative (Single File):**

```
/analyses
  /[tool-name].md         # All sections in one file
```

---

## Notes for Analysts

1. **Documentation Gaps:** If official documentation does not address a section, explicitly state "Not documented in official sources" rather than making assumptions.

2. **Version Specificity:** Always note the version of the tool being analysed, as features may change between versions.

3. **Update Frequency:** Consider adding a "Last Updated" date to each analysis to track currency.

4. **Community Resources:** While official documentation is the primary source, community resources (Stack Overflow, GitHub issues, etc.) can be noted separately but should not replace official documentation.

5. **Verification:** When possible, verify claims by testing the tool directly, but always cite the official documentation that describes the feature.

6. **Incomplete Information:** If a section cannot be completed due to lack of documentation, document this explicitly and note what information is missing.

---

## Citation Format

Use the following format for citations:

```markdown
**Citation:** [Feature/Topic Name]. [Tool Name] Official Documentation. [URL]. Accessed [Date].
```

**Example:**
```markdown
**Citation:** OpenAI Integration. Cursor Documentation. https://docs.cursor.com/integrations/openai. Accessed 16 January 2026.
```

---

## Revision History

| Date | Version | Changes |
|------|---------|---------|
| 16 January 2026 | 1.0 | Initial creation of reusable analysis plan |

