# AI Tools Analysis

An analysis of available tools for AI-based coding.

## Overview

This repository provides a standardised methodology for analysing AI coding tools. It contains a reusable analysis plan and template that ensures comprehensive and consistent evaluation of different AI coding platforms.

## Documents

### 📋 [analysis_plan.md](analysis_plan.md)

The comprehensive guide for conducting tool analyses. This document contains:

- Detailed methodology for analysing AI coding tools
- Required information for each analysis section
- Guidelines for documentation and citations
- Quality standards and best practices
- Analysis checklist for completeness

**Use this document to understand the analysis process and requirements.**

### 📝 [tool_analysis_template.md](tool_analysis_template.md)

A ready-to-use template for creating new tool analyses. This template includes:

- Pre-formatted sections matching the analysis plan
- Placeholder text and examples
- Built-in citation fields
- Completeness checklist

**Use this template as a starting point for each new tool analysis.**

### ⚡ [quick_reference.md](quick_reference.md)

A concise guide for quick access while conducting analyses. Includes:

- Essential guidelines and checklist
- Section-by-section quick reference
- Citation format examples
- Common phrases for missing information
- UK vs US English reference
- Tips for efficient analysis

**Use this for quick lookups during the analysis process.**

## How to Analyse a New Tool

1. **Read the Analysis Plan**  
   Review [analysis_plan.md](analysis_plan.md) to understand the methodology and requirements.

2. **Copy the Template**  
   Create a copy of [tool_analysis_template.md](tool_analysis_template.md) for your new analysis:
   ```bash
   cp tool_analysis_template.md analyses/[tool-name].md
   ```

3. **Follow the Guidelines**  
   When conducting your analysis:
   - ✅ Rely entirely on official documentation
   - ❌ Make NO guesses or assumptions
   - 📚 Provide citations and links to official documentation
   - 🇬🇧 Use UK English
   - 📝 Complete all applicable sections

4. **Use the Checklist**  
   Before finalising, ensure all items in the completeness checklist are addressed.

## Analysis Sections

Each tool analysis covers:

1. **Tool Overview** - Description, primary use case, and key features
2. **LLM Provider Integration** - Ollama, Copilot Pro, Microsoft AI Foundry, OpenAI, Anthropic
3. **Policies and Rules** - Instruction files and configuration
4. **Custom Prompts** - Prompt storage and reuse capabilities
5. **Tools and MCP** - Model Context Protocol and extensions
6. **Development Workflow** - From design to code generation
7. **IDE Integration** - VSCode, JetBrains, Eclipse, Terminal/CLI, and others

## Directory Structure

```
ai-tools-analysis/
├── README.md                    # This file
├── analysis_plan.md            # Detailed analysis methodology
├── tool_analysis_template.md   # Template for new analyses
├── quick_reference.md          # Quick lookup guide
└── analyses/                   # Individual tool analyses
    ├── README.md
    ├── tool-name-1.md
    ├── tool-name-2.md
    └── ...
```

## Quality Standards

All analyses in this repository must:

- Be based on official documentation only
- Include citations for all claims
- Use UK English
- Follow the standard template structure
- Be kept up-to-date with tool versions
- Clearly mark undocumented features as such

## Contributing

When contributing an analysis:

1. Use the provided template
2. Follow the analysis plan methodology
3. Cite all sources
4. Use UK English
5. Complete the checklist before submission

## Licence

[To be determined based on repository needs] 
