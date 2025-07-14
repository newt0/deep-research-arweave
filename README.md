# deep-research-arweave

## ✅ Overview

| Item       | Description                                                                                                                        |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Repository | `deep-research-arweave`                                                                                                            |
| Scope      | Deep research on Arweave and related projects (AO, RedStone, ArFleet, etc.)                                                        |
| Purpose    | To perform and store LLM-powered research (ChatGPT, Grok, Gemini etc.) in English, and manage translations into multiple languages |
| Structure  | All content is stored as flat files in `deep-research/` and categorized using the `tags:` field only                               |

## 📁 Directory Structure (Initial)

```plaintext
deep-research-arweave/
├── README.md
├── deep-research/                         # English master research files (flat structure)
│   ├── ao-executor-security.md
│   ├── redstone-oracle.md
│   ├── ao-defi-usecase.md
│   └── ...
├── translations/                          # Multilingual translations
│   ├── ja/
│   │   ├── ao-executor-security.md
│   │   └── prompts/
│   │       └── translate.md
│   ├── zh/
│   │   ├── ...
│   │   └── prompts/
│   │       └── translate.md
│   ├── ko/
│   │   └── prompts/
│   │       └── translate.md
│   ├── de/
│   │   └── prompts/
│   │       └── translate.md
│   ├── fr/
│   │   └── prompts/
│   │       └── translate.md
│   └── es/
│       └── prompts/
│           └── translate.md
└── tools/                                  # Optional scripts/utilities
    ├── generate-tag-index.ts
    └── check-missing-translations.ts
```

## 📝 `deep-research/` File Format (English master files)

These files contain original research output, including the prompt, LLM-generated result, and metadata.
All content is stored in a single Markdown file using **YAML front matter + Markdown body**.
All research is conducted in English for LLM performance and ecosystem relevance (especially in Web3 contexts).

````markdown
---
title: AO Executor Security Model
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-10
url: https://chat.openai.com/share/abc123
tags: [ao, project, developer, security, wasm]
---

[PROMPT]

```markdown
Please investigate...
```

---

# Output

```markdown
[出力全文]
```
````

## 📝 `translations/` File Format (Multilingual)

```markdown
---
title: AOのExecutorセキュリティモデル
translation_tool: ChatGPT (GPT-4o)
translation_prompt: ja/prompts/translation-v1.md
---

# [OUTPUT]

...

## Translation

...
```

> 📝 `source_file:` is omitted because filenames are kept identical to the English master files.

## ✅ Tagging Policy

All file categorization is handled via the `tags:` field only.
Multiple axes can be used together for flexible filtering.

| Axis         | Examples                                |
| ------------ | --------------------------------------- |
| Content type | `project`, `ecosystem`, `dev-guide`     |
| Technology   | `ao`, `arweave`, `redstone`, `arfleet`  |
| Use case     | `oracle`, `nft`, `defi`, `wallet`, `ai` |
| Audience     | `builder`, `investor`, `user`           |

## ✅ When to Split Directories

| Trigger condition                     | Action to take                                |
| ------------------------------------- | --------------------------------------------- |
| Over 100 total files                  | Split into subdirectories by tag (e.g. `ao/`) |
| A category has multiple related files | Create a dedicated subdirectory (e.g. `ao/`)  |

## ❌ Metadata You Should Not Include

| Field              | Reason                                     |
| ------------------ | ------------------------------------------ |
| `language:`        | Inferred from directory name (`ja/`, etc.) |
| `translator:`      | Available via Git commit logs              |
| `date_translated:` | Tracked via Git history                    |
| `source_file:`     | Unnecessary if filenames match exactly     |

## ✅ Additional Notes

- Tools to generate tag indexes or filter by tags (`Node.js`, `Python`, etc.) are planned
- Translation automation will be implemented using Claude Code Hooks, combining static processing with LLM output
