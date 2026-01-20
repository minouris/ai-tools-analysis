# Tool Analyses

This directory contains individual analyses of AI coding tools, each following the standardised methodology defined in [ANALYSIS_PLAN.md](../ANALYSIS_PLAN.md).

## Current Analyses

- [Azure AI Toolkit for Visual Studio Code](azure-ai-toolkit.md) - Visual Studio Code extension for integrating Azure AI services and local AI models into development workflows
- [Roo Cline](roo-cline.md) - AI-powered development assistant for VS Code with multiple operational modes (Version 3.41.0)
- [GitHub Copilot Chat](github-copilot-chat.md) - AI-powered code assistance and chat interface for software development
- [Continue](continue.md) - AI-powered coding assistant with IDE extensions, CLI, and cloud agents
- [GitHub Copilot Chat](github-copilot-chat.md) - AI-powered code assistance and chat interface for software development

## Creating a New Analysis

To analyse a new tool:

1. Copy the template:
   ```bash
   cp ../TOOL_ANALYSIS_TEMPLATE.md [tool-name].md
   ```

2. Follow the [Analysis Plan](../ANALYSIS_PLAN.md) methodology

3. Complete all applicable sections with information from official documentation

4. Verify completeness using the checklist in the template

## Naming Convention

Analysis files should be named using lowercase with hyphens:
- ✅ `github-copilot.md`
- ✅ `cursor-editor.md`
- ✅ `jetbrains-ai-assistant.md`
- ❌ `GitHub Copilot.md`
- ❌ `cursor_editor.md`

## File Organisation

Each analysis is a single Markdown file containing all sections. For very large analyses, consider splitting into multiple files in a subdirectory:

```
analyses/
├── tool-name.md                    # Simple single-file analysis
└── complex-tool/                   # Multi-file analysis
    ├── overview.md
    ├── llm-integration.md
    ├── policies-rules.md
    ├── prompts.md
    ├── tools-mcp.md
    ├── workflow.md
    └── ide-integration.md
```

## Quality Checklist

Before considering an analysis complete:

- [ ] All sections from the template are addressed
- [ ] Every claim has a citation to official documentation
- [ ] No assumptions or guesses are made
- [ ] UK English is used throughout
- [ ] The tool version is clearly stated
- [ ] Undocumented features are marked as "Not documented in official sources"
- [ ] The completeness checklist in the analysis is filled out

## Maintenance

Analyses should be reviewed and updated when:
- A new major version of the tool is released
- Significant features are added or changed
- Official documentation is substantially updated

When updating an analysis:
1. Update the "Analysis Date" and "Tool Version" at the top
2. Add an entry to the "Revision History" section at the bottom
3. Review all citations to ensure they are still valid
