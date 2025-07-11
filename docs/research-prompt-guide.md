# Deep Research Prompt Design Guide

This document outlines **best practices for designing prompts** that produce high-quality Deep Research outputs, especially for emerging Web3 protocols such as AO. When using tools like ChatGPT or other LLMs, careful prompt design is essential to obtain reliable results.

## Design Principles

### Write Prompts in English (but plan in your native language)

LLMs are optimized for English. Therefore, prompts should be written and executed in English.
However, during the planning or requirement-gathering phase, it's better to think and draft in your native language (e.g., Japanese). This helps prevent misunderstandings and preserves nuance.

### Specify Output Format

Always define the output format clearly, like this:

- `Markdown`
- `Clear headings and bullet points`

This ensures the response is structured and easy to read. Avoid emojis, decorative characters, or other visual elements that don’t contribute to content structure.

### Define Scope and Restrictions

To improve accuracy and reduce noise, apply strict boundaries to the research scope. For example:

- Limit sources to **English-language content** only
  _(e.g., “Only include English-language sources”)_
- Set a **starting date** based on the project’s launch
  _(e.g., “Only include sources published after February 2024”)_
- **Exclude unrelated general information**
  _(e.g., “Exclude general Arweave content unless directly relevant”)_

### Keep Prompts Concise

LLMs tend to lose focus with long or redundant prompts. To avoid this:

- Use short and clear sentences
- Avoid long paragraphs
- Eliminate unnecessary flourishes, such as emojis or exclamations

### Design Clear Focus Areas

Focus Areas should be expressed as **specific questions or checklist items**, not vague or abstract topics.
For example:

- What is AO? Core design principles and execution model.
- Core components: Executors, Actors, Messages.
- Release history and notable milestones.

Make sure to clearly cover all key aspects of the target project.

### Specify Trusted Information Sources

In early-stage Web3 projects, **defining trusted sources in advance** greatly improves output quality. Suggested categories include:

- Core Docs (e.g., official website, whitepaper, cookbooks)
- GitHub repositories
- Blogs / Medium / Journals
- Twitter (by core developers or official accounts)
- Explorers / IDEs / sample projects

To cover important use cases or implementations that AI might not find on its own, you should **manually prepare a source list** when possible.
Of course, you can also use AI to assist in this pre-listing step.

Also, many popular tools, protocols, and L1/L2 chains have curated `awesome-xxx` GitHub repositories. Start there, filter out irrelevant links, and add newer updates if needed.

### Define the Target Audience

Mentioning the intended audience at the beginning of the prompt helps the LLM adjust tone and vocabulary accordingly. For example:

```
Please conduct a technical investigation into [Project Name] from the perspective of Web3 developers.
```

### Split Tasks

Avoid assigning multiple unrelated tasks in a single prompt (e.g., research + writing + translation).
Instead, **split tasks** and execute them step-by-step with separate prompts.

## Prompt Template

Here’s a reusable template for writing Deep Research prompts:

```markdown
Please conduct a technical investigation into [Project Name] from the perspective of [Target Audience].

## Focus Areas

- [Question / Area 1]
- [Question / Area 2]
- [Question / Area 3]

## Restrictions

- Only include English-language sources published after [Launch Date]
- Exclude [Unrelated Content]

## Output Format

- Markdown
- Clear headings, bullet points

## Prioritized Sources

### Core Docs

- [...]

### Key GitHub Repositories

- [...]

### Developer Blogs / Explorers

- [...]

### Twitter (X) — Core Accounts

- [...]
```
