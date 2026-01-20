# Quick Reference Guide for AI Tool Analysis

## Getting Started

1. **Read** [analysis_plan.md](analysis_plan.md) for methodology
2. **Copy** [tool_analysis_template.md](tool_analysis_template.md) to `analyses/[tool-name].md`
3. **Fill in** each section using official documentation only
4. **Check** completeness using the checklist

## Essential Guidelines

| Do ✅ | Don't ❌ |
|------|---------|
| Use official documentation only | Make assumptions or guesses |
| Cite every claim with URL | Copy/paste without attribution |
| Use UK English (analyse, organisation, etc.) | Use US English (analyze, organization, etc.) |
| Mark missing info as "Not documented" | Skip sections or make up information |
| Include tool version being analysed | Analyse without version context |

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

## Citation Format

```markdown
**Citation:** [Feature Name]. [Tool Name] Documentation. [URL]. Accessed [Date].
```

**Example:**
```markdown
**Citation:** Ollama Integration. Continue Documentation. 
https://docs.continue.dev/reference/models#ollama. Accessed 16 January 2026.
```

## Common Phrases for Missing Information

Use these exact phrases when official documentation is lacking:

- "Not documented in official sources"
- "Not specified in official documentation"
- "Support status unclear from official documentation"
- "Not available according to official documentation"
- "Eclipse support not available"
- "CLI not available"

## Checklist Before Finalising

- [ ] All 7 main sections completed
- [ ] Every claim has a citation
- [ ] Tool version clearly stated at top
- [ ] UK English used throughout
- [ ] No assumptions or guesses made
- [ ] "Not documented" used where appropriate
- [ ] Completeness checklist filled in
- [ ] References section complete

## File Naming

Use lowercase with hyphens:
- ✅ `github-copilot.md`
- ✅ `cursor-editor.md`
- ✅ `amazon-codewhisperer.md`
- ❌ `GitHub Copilot.md`
- ❌ `cursor_editor.md`

## Directory Structure

```
ai-tools-analysis/
├── analysis_plan.md              ← Full methodology
├── tool_analysis_template.md     ← Copy this for new analyses
├── quick_reference.md            ← This file
└── analyses/                     ← Put completed analyses here
    ├── tool-name.md
    └── ...
```

## Tips for Efficient Analysis

1. **Start with official docs homepage** - Find the main documentation site
2. **Look for integration guides** - Check for "Integrations", "Setup", or "Configuration" sections
3. **Search for keywords** - Search docs for "Ollama", "OpenAI", "MCP", etc.
4. **Check GitHub repos** - Official repos may have additional setup info in READMEs
5. **Note version numbers** - Always record what version you're documenting
6. **Bookmark documentation** - Save all relevant doc pages for your references section

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

## Need Help?

1. Review [analysis_plan.md](analysis_plan.md) for detailed methodology
2. Look at completed analyses in `analyses/` directory for examples
3. Check the template structure in [tool_analysis_template.md](tool_analysis_template.md)

---

**Remember:** Quality over speed. A thorough, well-cited analysis is more valuable than a quick, incomplete one.
