# Tool Analyses

This directory contains individual analyses of AI coding tools, each following the standardised methodology defined in [analysis_plan.md](../analysis_plan.md).

## Current Analyses

- [Claude Code](claude_code.md) - Terminal-based agentic coding tool from Anthropic with MCP support, plugin system, and VS Code integration
- [Azure AI Toolkit for Visual Studio Code](azure_ai_toolkit.md) - Visual Studio Code extension for integrating Azure AI services and local AI models into development workflows
- [Continue](continue.md) - AI-powered coding assistant with IDE extensions, CLI, and cloud agents
- [GitHub Copilot Chat](github_copilot_chat.md) - AI-powered code assistance and chat interface for software development
- [Roo Cline](roo_cline.md) - AI-powered development assistant for VS Code with multiple operational modes (Version 3.41.0)

## Other

- [Amazon Q Developer](amazon_q_developer.md) - AWS AI-powered coding assistant with security scanning and AWS service integration
- [Codeium](codeium.md) - Free AI-powered code completion and chat assistant with broad IDE support
- [Cursor](cursor.md) - AI-first code editor built for productivity with deep AI integration
- [Sourcegraph Cody](sourcegraph_cody.md) - AI coding assistant with deep codebase context and understanding
- [Tabnine](tabnine.md) - AI-powered code completion tool with flexible deployment options

## Creating a New Analysis

To analyse a new tool:

1. Copy the template:
   ```bash
   cp ../tool_analysis_template.md [tool-name].md
   ```

2. Follow the [Analysis Plan](../analysis_plan.md) methodology

3. Complete all applicable sections with information from official documentation

4. Verify completeness using the checklist in the template

## Naming Convention

Analysis files should be named using lowercase with underscores (lower-snake-case):
- ✅ `github_copilot.md`
- ✅ `cursor_editor.md`
- ✅ `jetbrains_ai_assistant.md`
- ❌ `GitHub Copilot.md`
- ❌ `github-copilot.md` (kebab-case not allowed)
- ❌ `cursor_Editor.md` (mixed case not allowed)

## File Organisation

Each analysis is a single Markdown file containing all sections. For very large analyses, consider splitting into multiple files in a subdirectory:

```
analyses/
├── tool_name.md                    # Simple single-file analysis
└── complex_tool/                   # Multi-file analysis
    ├── overview.md
    ├── llm_integration.md
    ├── policies_rules.md
    ├── prompts.md
    ├── tools_mcp.md
    ├── workflow.md
    └── ide_integration.md
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
