# [Tool Name] Analysis

**Analysis Date:** [Date]  
**Tool Version:** [Version]  
**Analyst:** [Name]  
**Official Documentation:** [Primary documentation URL]

---

## 1. Tool Overview

**Official Documentation:** [Link]  
**Version Analysed:** [Version Number]  
**Primary Use Case:** [Brief description]  
**Licensing:** [Open-source/Commercial/Freemium/etc.]

### Description

[Detailed description of the tool, its purpose, target audience, and key features]

### Key Features

- [Feature 1]
- [Feature 2]
- [Feature 3]

**Citation:** [Official documentation links]

---

## 2. LLM Provider Integration

### 2.1 Ollama Integration

**Supported:** [Yes/No/Partial]

**Configuration:**

[Step-by-step configuration instructions from official docs, or "Not documented in official sources"]

**Supported Models:** [List of models, or "Not specified"]

**Limitations:** [Any known limitations]

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

### 2.2 GitHub Copilot Pro Integration

**Supported:** [Yes/No/Partial]

**Integration Method:** [Description]

**Configuration:**

[Step-by-step configuration instructions, or "Not documented in official sources"]

**Features Available with Copilot Pro:**

- [Feature 1]
- [Feature 2]

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

### 2.3 Microsoft AI Foundry Integration

**Supported:** [Yes/No/Partial]

**Configuration:**

- **Endpoint URL Configuration:** [Instructions, or "Not documented"]
- **API Key Configuration:** [Instructions, or "Not documented"]
- **Supported Models:** [List, or "Not specified"]

**Authentication Methods:** [Description]

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

### 2.4 OpenAI Integration

**Supported:** [Yes/No/Partial]

**Configuration:**

- **API URL Configuration:** [Instructions, or "Not documented"]
- **API Key Configuration:** [Instructions, or "Not documented"]
- **Supported Models:** [List (e.g., GPT-3.5, GPT-4, GPT-4o, etc.)]

**Custom Endpoints:** [Whether custom OpenAI-compatible endpoints are supported]

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

### 2.5 Anthropic (Claude) Integration

**Supported:** [Yes/No/Partial]

**Account Requirements:** [Description of account/subscription requirements]

**Configuration:**

- **API Key Configuration:** [Instructions, or "Not documented"]
- **Supported Models:** [List (e.g., Claude 3 Opus, Claude 3 Sonnet, etc.)]

**Features and Limitations:** [Any specific features or constraints]

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

## 3. Policies and Rules (Instruction Files)

### Instruction File Support

**Supported File Types:** [List (e.g., `.github/copilot-instructions.md`, `.cursorrules`, etc.) or "Not documented"]

**File Locations:** [Paths where instruction files should be placed]

**File Format:** [Supported formats: Markdown, YAML, JSON, etc.]

### Configuration Method

[Detailed explanation of how to create and configure instruction files, or "Not documented in official sources"]

### Syntax and Structure

```
[Example instruction file syntax]
```

### Scope and Application

- **Global:** [How global rules are applied]
- **Project-Level:** [How project-level rules are applied]
- **File-Level:** [How file-level rules are applied, if supported]

### Example Policies

```
[Example instruction file content]
```

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

## 4. Custom and Stored Prompts

### Prompt Storage Mechanism

**Available:** [Yes/No/Partial]

[Description of how prompts are stored: local files, cloud sync, database, etc.]

### Creating Custom Prompts

[Step-by-step instructions for creating custom prompts, or "Not documented in official sources"]

### Organising Prompts

[Instructions for categorisation, tagging, and management, or "Not documented in official sources"]

### Using Stored Prompts

[Instructions for invoking and using saved prompts, including keyboard shortcuts or commands]

### Sharing and Exporting

[Information about sharing prompt collections with team members or exporting prompts]

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

## 5. Tools and Model Context Protocol (MCP)

### Model Context Protocol (MCP)

**MCP Support:** [Yes/No/Partial]

**Configuration:**

[How to configure MCP servers and tools, or "Not documented in official sources"]

### MCP Server Configuration

```json
[Example MCP configuration, if applicable]
```

### Available Tools

| Tool Name | Purpose | Documentation |
|-----------|---------|---------------|
| [Tool 1] | [Purpose] | [Link] |
| [Tool 2] | [Purpose] | [Link] |

### Custom Tool Development

**Supported:** [Yes/No]

[Information about creating custom tools or plugins, or "Not documented in official sources"]

**Development Framework:** [If custom development is supported, what framework/API is used]

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

## 6. Application Development Workflow

### 6.1 Project Initialisation

[How to start a new project with the tool, including any scaffolding or template features]

### 6.2 Design and Planning

[Features for architecture design, planning, or requirements gathering]

### 6.3 Code Generation

**Supported Generation Methods:**

- [Method 1: e.g., inline completions]
- [Method 2: e.g., chat-based generation]
- [Method 3: e.g., command-based generation]

**Workflow:**

1. [Step 1]
2. [Step 2]
3. [Step 3]

### 6.4 Iterative Development

[How to refine and iterate on generated code, including editing and regeneration features]

### 6.5 Testing and Validation

[Integration with testing frameworks, test generation capabilities]

### 6.6 Debugging

[Debugging features: error explanation, fix suggestions, debugging assistance]

### 6.7 Deployment

[Deployment-related features, if any, or "Not applicable"]

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

## 7. IDE and Environment Integration

### 7.1 Visual Studio Code

**Supported:** [Yes/No]

**Installation:** [Extension name and installation method]

**Configuration:**

[Setup instructions with links to marketplace or official setup guide]

**Features:**

- [Feature 1]
- [Feature 2]
- [Feature 3]

**Keyboard Shortcuts:**

| Action | Shortcut (Windows/Linux) | Shortcut (macOS) |
|--------|--------------------------|------------------|
| [Action 1] | [Shortcut] | [Shortcut] |
| [Action 2] | [Shortcut] | [Shortcut] |

**UI Integration:**

[Description of how the tool appears in VS Code: sidebar, panel, inline, etc.]

**Citation:** [Official documentation links]

---

### 7.2 JetBrains IDEs

**Supported IDEs:** [List: IntelliJ IDEA, PyCharm, WebStorm, etc., or "Not supported"]

**Installation:** [Plugin name and installation method]

**Configuration:**

[Setup instructions with links to plugin marketplace or official setup guide]

**Features:**

- [Feature 1]
- [Feature 2]
- [Feature 3]

**IDE-Specific Considerations:**

[Any specific considerations or limitations for JetBrains IDEs]

**Citation:** [Official documentation links, or "Not documented in official sources"]

---

### 7.3 Eclipse

**Supported:** [Yes/No/Partial]

**Installation:** [Plugin name and installation method, if available]

**Configuration:**

[Setup instructions, or "Not documented in official sources"]

**Features:**

[List of available features, or "Eclipse support not available"]

**Limitations:**

[Any known limitations compared to other IDEs]

**Citation:** [Official documentation links, or "Not supported"]

---

### 7.4 Terminal and CLI

**CLI Available:** [Yes/No]

**Installation:** [Installation command or method]

```bash
[Installation command example]
```

**Available Commands:**

| Command | Description | Example |
|---------|-------------|---------|
| [command1] | [Description] | `[example]` |
| [command2] | [Description] | `[example]` |

**Configuration:**

[CLI configuration file location and options]

**Usage Examples:**

```bash
# Example 1: [Description]
[command example]

# Example 2: [Description]
[command example]
```

**Integration with Shell:**

[How the tool integrates with bash, zsh, fish, PowerShell, etc.]

**Citation:** [Official documentation links, or "CLI not available"]

---

### 7.5 Other IDEs and Editors

**Supported Environments:** [List all other supported environments]

#### [Editor/IDE Name 1]

**Installation:** [Method]  
**Features:** [List]  
**Limitations:** [Any known limitations]  
**Citation:** [Official documentation links]

#### [Editor/IDE Name 2]

**Installation:** [Method]  
**Features:** [List]  
**Limitations:** [Any known limitations]  
**Citation:** [Official documentation links]

---

## 8. Third Party Reviews and Experiences

### User Feedback and Testimonials

**Overall Sentiment:** [Positive/Mixed/Negative]

**Common Praise:**

- [Commonly mentioned positive aspect 1 with quotation if available]
- [Commonly mentioned positive aspect 2 with quotation if available]
- [Commonly mentioned positive aspect 3 with quotation if available]

**Common Complaints:**

- [Pain point 1 with quotation if available]
- [Pain point 2 with quotation if available]
- [Pain point 3 with quotation if available]

**Citation:** [Review source with date, e.g., "Reddit discussion. January 2025. https://..."]

### Reported Bugs and Issues

**Critical Issues:**

- [Bug/issue 1 with description and citation]
- [Bug/issue 2 with description and citation]

**Minor Issues:**

- [Bug/issue 1 with description and citation]
- [Bug/issue 2 with description and citation]

**Citation:** [Issue tracker, Stack Overflow, or forum posts with dates]

### Productivity Impact

**Positive Impact:**

[Quote or summary of productivity improvements reported by users]

**Negative Impact:**

[Quote or summary of productivity hindrances reported by users]

**Citation:** [Review source with date]

### Comparison with Other Tools

#### Comparison with [Tool Name 1]

**Advantages over [Tool Name 1]:**

- [Advantage 1]
- [Advantage 2]

**Disadvantages compared to [Tool Name 1]:**

- [Disadvantage 1]
- [Disadvantage 2]

**Citation:** [Comparison source with date, e.g., "Comparative review. February 2025. https://..."]

#### Comparison with [Tool Name 2]

[Similar structure as above]

**Citation:** [Comparison source with date]

---

## 9. Summary and Key Findings

### Strengths

- [Strength 1]
- [Strength 2]
- [Strength 3]

### Limitations

- [Limitation 1]
- [Limitation 2]
- [Limitation 3]

### Best Use Cases

[Description of scenarios where this tool excels]

### Documentation Quality

[Assessment of the official documentation quality and completeness]

---

## 10. Completeness Checklist

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
- [ ] Third party reviews and experiences documented with dated citations
- [ ] Comparisons with other tools included where available
- [ ] All information verified against official documentation
- [ ] No assumptions or guesses made
- [ ] All claims have citations
- [ ] UK English used throughout
- [ ] Consistent formatting applied

---

## 11. References

### Official Documentation

1. [Primary documentation source] - [URL]
2. [Secondary documentation source] - [URL]
3. [Additional resource] - [URL]

### Version Information

- **Tool Version Analysed:** [Version]
- **Documentation Last Updated:** [Date]
- **Analysis Last Updated:** [Date]

---

## Revision History

| Date | Version | Changes | Analyst |
|------|---------|---------|---------|
| [Date] | 1.0 | Initial analysis | [Name] |

