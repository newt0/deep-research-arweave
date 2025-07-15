# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository is a documentation and research collection focused on Arweave ecosystem projects (AO, RedStone, ArFleet, etc.). It's designed for LLM-powered research storage and multi-language translation management.

## Architecture

### Core Structure
- **`deep-research/`** - English master research files (flat structure with tag-based categorization)
- **`translations/`** - Multi-language translations organized by language code directories
- **`docs/`** - Documentation and guides for research processes
- **`prompts/`** - Translation and research prompt templates

### File Organization
- All categorization is handled via YAML frontmatter `tags:` field only
- No directory-based categorization until >100 files threshold
- Identical filenames maintained between English and translated versions
- Single Markdown file format with YAML frontmatter + Markdown body

## Content Standards

### Research Files Format (`deep-research/`)
```yaml
---
title: [Research Title]
platform: [LLM Platform Used]
date: YYYY-MM-DD
url: [Source URL if applicable]
tags: [project, technology, usecase, audience]
---

[PROMPT]

```markdown
[Original prompt text]
```

---

# Output

```markdown
[Research output]
```
```

### Translation Files Format (`translations/[lang]/`)
```yaml
---
title: [Translated Title]
translation_tool: [Tool Used]
translation_prompt: [lang]/prompts/translation-v1.md
---

# [OUTPUT]

[Translated content]
```

## Key Guidelines

### Tagging System
Use multiple tag axes for flexible categorization:
- **Content type**: `project`, `ecosystem`, `dev-guide`
- **Technology**: `ao`, `arweave`, `redstone`, `arfleet`
- **Use case**: `oracle`, `nft`, `defi`, `wallet`, `ai`
- **Audience**: `builder`, `investor`, `user`

### Translation Standards
- Follow terminology guidelines in `prompts/translate-into-ja.md`
- Preserve markdown structure exactly
- Keep technical terms in English as specified
- Maintain consistent tone and terminology across languages

### Research Process
- Use prompt design guidelines from `docs/research-prompt-guide.md`
- Conduct research in English for optimal LLM performance
- Include source URLs and platform information in frontmatter
- Structure output with clear headings and bullet points

## Development Notes

- No build, lint, or test commands - this is a documentation repository
- Content management is manual with planned automation via Claude Code Hooks
- Git is used for translation history tracking
- Future tools planned for tag indexing and missing translation detection

## Workflow

1. Create English research in `deep-research/` with proper frontmatter
2. Use translation prompts to create language-specific versions
3. Maintain filename consistency across languages
4. Tag appropriately for future categorization and filtering