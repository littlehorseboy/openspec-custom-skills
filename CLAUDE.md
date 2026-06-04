# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

This is a **Claude Code Custom Skills Library** that extends the OpenSpec spec-driven workflow system. It packages 7 skills (4 native OpenSpec skills + 3 custom extensions) for distribution via npm (`@littlehorseboy/openspec-custom-skills`) or by manually copying `.claude/skills/` into a target project.

The 3 custom skills add:
- Interactive Mermaid HTML design visualizations (`openspec-propose-design-mermaid-html`, `openspec-design-html`)
- One-step production finalization without prompts (`openspec-complete-archive-change`)

## Distribution

```bash
npm publish   # Publish to npm with public access
```

Users install skills by copying `.claude/skills/<skill-name>/` into their project's `.claude/skills/` directory, or referencing the npm package.

## Architecture

### Skill Structure

Each skill lives in `.claude/skills/<skill-name>/SKILL.md`. The format is YAML frontmatter (name, description, trigger phrases) followed by Markdown instructions that Claude Code executes step-by-step. There is no compiled code — skills are pure instruction documents.

Custom skills that generate HTML use an `assets/page-shell.html` template alongside their `SKILL.md`. This template holds the full CSS, layout scaffolding, and Mermaid CDN reference. Skills read this file and inject generated diagram sections into it.

### OpenSpec Workflow

The OpenSpec workflow is configured in `openspec/config.yaml` with `schema: spec-driven`. Active work lives in `openspec/changes/<change-name>/` (proposal.md, design.md, tasks.md, optional design.html). Completed changes are archived to `openspec/archive/YYYY-MM-DD-<name>/`. Main specs are tracked in `openspec/specs/`.

### Language Rules (openspec/config.yaml)

All artifact text (titles, descriptions, requirements, risks) must be in **Traditional Chinese (zh-TW)**. Technical identifiers — API names, function names, file paths, CLI commands, code symbols — stay in English. This rule applies to all skills when generating OpenSpec artifacts.

### Custom Skill Relationships

- `openspec-propose-design-mermaid-html` = `openspec-propose` steps 1–5 + HTML generation step
- `openspec-design-html` = HTML generation step only (requires an existing change with design.md)
- `openspec-complete-archive-change` = mark all tasks `[x]` + sync delta specs + archive, with no confirmation prompts

The HTML generation step reads the change's design.md, proposal.md, and tasks.md, then writes a `design.html` that renders Before/After comparisons, entry-point cards, data-flow and mapping tables, and risk panels as interactive Mermaid diagrams.
