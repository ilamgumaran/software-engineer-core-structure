# Prompts: Recreate This Framework From Scratch

This directory contains the structured prompts used to generate the entire multi-role software engineering agent framework. Feed these prompts to an AI coding agent (Claude Code, or any capable LLM with file-writing access) to recreate the framework from an empty directory.

---

## Why These Exist

1. **Reproducibility**: Anyone can regenerate the framework from these prompts
2. **Customization**: Modify the prompts before running to get a customized framework
3. **Learning**: Study the prompt structure to understand how to instruct AI agents effectively
4. **Evolution**: Update prompts and re-run to evolve the framework

---

## Prompt Architecture

```
00-master.md              ← Run this first (or run it alone — it orchestrates everything)
  |
  +-- 01-scaffold.md      ← Creates the directory structure and root files
  |
  +-- 02-roles.md         ← Generates all 9 role definitions
  |
  +-- 03-domains.md       ← Generates the domain extension system + reference domain
  |
  +-- 04-plan.md          ← Generates the master plan and all plan documents
  |
  +-- 05-tools.md         ← Generates AI tool guides and workflow recipes
  |
  +-- 06-org.md           ← Generates organizational configuration templates
  |
  +-- 07-templates.md     ← Generates document generation templates
  |
  +-- 08-agent-config.md  ← Generates CLAUDE.md and agent configuration
  |
  +-- 09-documentation.md ← Generates README, DIRECTORY_GUIDE, CUSTOMIZATION
```

---

## How to Use

### Option A: Run the Master Prompt (Recommended)

Feed `00-master.md` to an AI agent in an empty git repository. It contains the full context and instructions to generate everything. This is the single-prompt approach.

```bash
mkdir my-engineering-agent && cd my-engineering-agent && git init
claude < prompts/00-master.md
# Or paste the content of 00-master.md into your AI tool
```

### Option B: Run Prompts Individually

Run each numbered prompt in sequence. Each prompt is self-contained — it includes all the context needed to generate its part of the framework.

```bash
mkdir my-engineering-agent && cd my-engineering-agent && git init
# Run each prompt in order:
claude < prompts/01-scaffold.md
claude < prompts/02-roles.md
claude < prompts/03-domains.md
claude < prompts/04-plan.md
claude < prompts/05-tools.md
claude < prompts/06-org.md
claude < prompts/07-templates.md
claude < prompts/08-agent-config.md
claude < prompts/09-documentation.md
```

### Option C: Customize Before Running

Edit the prompts to change the framework:
- Change roles in `02-roles.md` (add, remove, or modify roles)
- Change the reference domain in `03-domains.md` (swap relevancy for your domain)
- Change tools in `05-tools.md` (different AI tools, different workflow platforms)
- Change organizational defaults in `06-org.md`

Then run as Option A or B.

---

## Prompt Design Principles

These prompts follow a consistent structure:

1. **Context**: What exists so far and what this prompt builds on
2. **Objective**: What to generate and why
3. **Specifications**: Exact structure, content depth, and quality criteria
4. **Output format**: File paths, markdown structure, section requirements
5. **Verification**: How to validate the output is correct

Each prompt is detailed enough to produce high-quality output on the first run, without requiring follow-up clarification.

---

## Modifying These Prompts

| I want to... | Modify this prompt |
|--------------|-------------------|
| Change the agent's roles | `02-roles.md` |
| Use a different domain | `03-domains.md` |
| Change the implementation plan | `04-plan.md` |
| Use different AI tools | `05-tools.md` |
| Change org defaults/policies | `06-org.md` |
| Change document templates | `07-templates.md` |
| Change agent behavior | `08-agent-config.md` |
| Change the README/docs | `09-documentation.md` |
| Change everything at once | `00-master.md` |
