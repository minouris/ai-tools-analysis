# Quick Reference Guide for AI Tool Analysis

## Table of Contents

- [Getting Started](#getting-started)
- [Essential Guidelines](#essential-guidelines)
- [Section Quick Reference](#section-quick-reference)
- [Citation Format](#citation-format)
- [Common Phrases for Missing Information](#common-phrases-for-missing-information)
- [Checklist Before Finalising](#checklist-before-finalising)
- [File Naming](#file-naming)
- [Directory Structure](#directory-structure)
- [Tips for Efficient Analysis](#tips-for-efficient-analysis)
- [UK English vs US English Quick Reference](#uk-english-vs-us-english-quick-reference)
- [Questions to Ask for Each Section](#questions-to-ask-for-each-section)
- [Need Help?](#need-help)

---

## Getting Started

1. **Read** [ANALYSIS_INSTRUCTIONS.md](ANALYSIS_INSTRUCTIONS.md) for methodology
2. **Copy** [templates/TOOL_ANALYSIS_TEMPLATE.md](templates/TOOL_ANALYSIS_TEMPLATE.md) to `../analyses/[tool-name].md`
3. **Fill in** each section using official documentation only
4. **Check** completeness using the checklist

[↑ Back to top](#table-of-contents)

---

## Essential Guidelines

| Do ✅ | Don't ❌ |
|------|---------|
| Use official documentation only | Make assumptions or guesses |
| Cite every claim with URL | Copy/paste without attribution |
| Use UK English (analyse, organisation, etc.) | Use US English (analyze, organization, etc.) |
| Mark missing info as "Not documented" | Skip sections or make up information |
| Include tool version being analysed | Analyse without version context |

[↑ Back to top](#table-of-contents)

---

## Section Quick Reference

### 1. Tool Overview
- Name, vendor, version
- Primary use case
- Key features
- Licensing model

### 2. LLM Provider Integration

| Provider | What to Document |
|----------|------------------|
| **Ollama** | Support status, configuration, models, limitations |
| **Copilot Pro** | Integration method, features, configuration |
| **Microsoft AI Foundry** | Endpoint/API key setup, supported models |
| **OpenAI** | API URL/key config, supported models (GPT-3.5, GPT-4, etc.) |
| **Anthropic** | Account requirements, API key setup, Claude models |

### 3. Policies and Rules
- Instruction file types (`.cursorrules`, `.github/copilot-instructions.md`, etc.)
- File locations and formats
- Syntax and examples
- Scope (global, project, file-level)

### 4. Custom Prompts
- Storage mechanism (local, cloud, etc.)
- Creating and organising prompts
- Invoking saved prompts
- Sharing/exporting

### 5. Tools and MCP
- MCP support (Yes/No/Partial)
- Configuration method
- Available tools
- Custom tool development

### 6. Development Workflow
1. Project initialisation
2. Design and planning
3. Code generation
4. Iterative development
5. Testing and validation
6. Debugging
7. Deployment

### 7. IDE Integration

| IDE/Editor | What to Document |
|------------|------------------|
| **VS Code** | Extension name, installation, features, shortcuts, UI |
| **JetBrains** | Supported IDEs, plugin, features |
| **Eclipse** | Support status, plugin, features, limitations |
| **Terminal/CLI** | Commands, configuration, shell integration |
| **Others** | Vim, Emacs, Sublime, etc. |

### 8. Third Party Reviews and Experiences
- Overall user sentiment (Positive/Mixed/Negative)
- Common praise from user reviews
- Common complaints and pain points
- Reported bugs and issues (critical and minor)
- Productivity impact (positive and negative)
- Comparisons with other tools
- **Sources:** Reddit, Stack Overflow, G2, Gartner, tech blogs, YouTube
- **Always include:** Dated citations, direct quotes where possible
- **Note:** When newer information contradicts older accounts, explicitly state this

[↑ Back to top](#table-of-contents)

---

## Citation Format

```markdown
**Citation:** [Feature Name]. [Tool Name] Documentation. [URL]. Accessed [Date].
```

### For Third Party Reviews

```markdown
**Citation:** [Platform/Publication]. [Month Year]. [URL]

Example: Reddit discussion. January 2025. https://reddit.com/...
Example: "GitHub Copilot Review". TechCrunch. March 2024. https://...
```

**Example:**
```markdown
**Citation:** Ollama Integration. Continue Documentation. 
https://docs.continue.dev/reference/models#ollama. Accessed 16 January 2026.
```

[↑ Back to top](#table-of-contents)

---

## Common Phrases for Missing Information

Use these exact phrases when official documentation is lacking:

- "Not documented in official sources"
- "Not specified in official documentation"
- "Support status unclear from official documentation"
- "Not available according to official documentation"
- "Eclipse support not available"
- "CLI not available"

[↑ Back to top](#table-of-contents)

---

## Checklist Before Finalising

- [ ] All 8 main sections completed
- [ ] Third party reviews section included with dated citations
- [ ] Every claim has a citation
- [ ] Tool version clearly stated at top
- [ ] UK English used throughout
- [ ] No assumptions or guesses made
- [ ] "Not documented" used where appropriate
- [ ] Completeness checklist filled in
- [ ] References section complete

[↑ Back to top](#table-of-contents)

---

## File Naming

Use lowercase with hyphens:
- ✅ `github-copilot.md`
- ✅ `cursor-editor.md`
- ✅ `amazon-codewhisperer.md`
- ❌ `GitHub Copilot.md`
- ❌ `cursor_editor.md`

[↑ Back to top](#table-of-contents)

---

## Directory Structure

```
ai-tools-analysis/
├── doc/
│   ├── ANALYSIS_INSTRUCTIONS.md      ← Full methodology
│   ├── QUICK_REFERENCE.md            ← This file
│   └── templates/
│       └── TOOL_ANALYSIS_TEMPLATE.md ← Copy this for new analyses
└── analyses/                         ← Put completed analyses here
    ├── tool-name.md
    └── ...
```

[↑ Back to top](#table-of-contents)

---

## Tips for Efficient Analysis

1. **Start with official docs homepage** - Find the main documentation site
2. **Look for integration guides** - Check for "Integrations", "Setup", or "Configuration" sections
3. **Search for keywords** - Search docs for "Ollama", "OpenAI", "MCP", etc.
4. **Check GitHub repos** - Official repos may have additional setup info in READMEs
5. **Note version numbers** - Always record what version you're documenting
6. **Bookmark documentation** - Save all relevant doc pages for your references section

[↑ Back to top](#table-of-contents)

---

## UK English vs US English Quick Reference

| UK English ✅ | US English ❌ |
|---------------|---------------|
| analyse | analyze |
| organisation | organization |
| licence | license (noun) |
| behaviour | behavior |
| customise | customize |
| recognised | recognized |
| optimise | optimize |
| colour | color |

[↑ Back to top](#table-of-contents)

---

## Questions to Ask for Each Section

### Tool Overview
- What problem does this tool solve?
- Who is the target user?
- What makes it different from competitors?

### LLM Integration
- How do I configure [provider]?
- What models are supported?
- Are there any costs or limits?

### Policies and Rules
- Where do I put instruction files?
- What syntax do they use?
- What can I control with them?

### Custom Prompts
- Can I save prompts for reuse?
- How do I organise them?
- Can I share them with my team?

### Tools and MCP
- Does it support MCP?
- What tools are available?
- Can I create custom tools?

### Workflow
- How do I start a project?
- How does code generation work?
- What about testing and debugging?

### IDE Integration
- Which IDEs are supported?
- How do I install it?
- What features work in each IDE?

[↑ Back to top](#table-of-contents)

---

## Need Help?

1. Review [ANALYSIS_INSTRUCTIONS.md](ANALYSIS_INSTRUCTIONS.md) for detailed methodology
2. Look at completed analyses in `../analyses/` directory for examples
3. Check the template structure in [templates/TOOL_ANALYSIS_TEMPLATE.md](templates/TOOL_ANALYSIS_TEMPLATE.md)

[↑ Back to top](#table-of-contents)

---

**Remember:** Quality over speed. A thorough, well-cited analysis is more valuable than a quick, incomplete one.

[↑ Back to top](#table-of-contents)
