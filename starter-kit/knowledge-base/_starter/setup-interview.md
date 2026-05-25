# New User Setup — Agent Instruction File

> **This file is written for the agent, not for the human.** When a user invokes setup, follow the steps below. The goal is to generate their personal context layer (CLAUDE.md or equivalent manifest, plus memory files) through a guided conversation, so they never have to fill in a blank template.

---

## When to run this

Run this when:
- The user says "set me up", "configure my workspace", or "I'm new here"
- You detect that the workspace manifest at the root still contains unfilled placeholders like `[Your name]`
- The user explicitly asks to run setup

## Step 1 — Orient the user (one message)

Tell them in plain language:
- What you are about to do (ask a few questions, then generate their personal context files)
- What files will be created (the personal manifest at the root, a few memory files, `TASKS.md`)
- That they can correct anything afterward — nothing is final
- Estimated time: 5 to 10 minutes

## Step 2 — Interview (one question at a time, wait for real answers)

Ask these in order. Do not batch questions. Wait for a complete answer before moving on.

1. **Name and role.** "What's your full name and your role at your company? For example, Staff PM, Designer, Sales Engineer."

2. **Team and company.** "Which team or function do you work in, and at what company?"

3. **Working language.** "Do you work mainly in one language, or multiple? If multiple, any rule of thumb for when you use each?"

4. **Frequent collaborators.** "Who are the three to five people you work with most? For each one, tell me their name, their role, and one sentence about how you interact with them."

5. **Active projects.** "What are the one or two projects you are currently most involved in? Just a name and a one-liner on what each is."

6. **Communication preferences.** "Any strong preferences for how you want me to communicate with you? Think tone, format, how long responses should be, anything you hate or love."

7. **Critical rules (optional).** "Is there anything I should never do in your context — a guardrail, a constraint from your role, or a topic to always flag before acting on?"

## Step 3 — Generate the files

Using the answers, create the following files. Be precise — use the person's actual words where possible, not paraphrases.

### Personal manifest at the workspace root

Take `knowledge-base/_starter/CLAUDE-template.md`, fill in every `[placeholder]` with the user's answers, and save it as the appropriate manifest filename for the user's tool. Defaults: `CLAUDE.md` for Claude tools, `AGENTS.md` for the cross-tool open standard, `.cursorrules` for Cursor. If unsure, ask the user which tool they are using and use the appropriate filename. Preserve the structure of the template. Remove the "First time here?" banner from the top of the saved file.

### `memory/people/[firstname-lastname].md` for each collaborator mentioned

One file per person, named in lowercase with hyphens. Format:

```
# [Full Name]
**Role:** [their role]
**How we work together:** [one sentence from the user's answer]
**Notes:** [anything else mentioned]
```

### `memory/context/my-role.md`

```
# My Role Context
**Role:** [role]
**Team:** [team or function]
**Company:** [company]
**Primary language:** [language rule]
**Scope:** [brief description, synthesized from answers]
```

### `memory/projects/[project-slug].md` for each active project

```
# [Project Name]
**What it is:** [the user's one-liner]
**Status:** [if mentioned, otherwise leave for the user to add]
```

### `TASKS.md` at the workspace root

```
# Tasks

## Active
- [ ] Review CLAUDE.md and correct anything I got wrong

## Waiting On
(nothing yet)

## Someday
(nothing yet)

## Done
(nothing yet)
```

### `memory/glossary.md`

If the user mentioned any internal acronyms, nicknames, or codenames during the interview, capture them here. Otherwise leave it as an empty stub with a header.

## Step 4 — Confirm and hand off

After creating the files:

1. Tell the user what was created and where each file lives.
2. Ask them to open the personal manifest and correct anything that does not look right.
3. Suggest their first real task: "Once you are happy with the setup, try asking me something you would normally ask a colleague — and see if I answer it as if I already know your context."

## Step 5 — Offer ingestion of existing material (optional)

After hand-off, if the user mentions they already have context written down somewhere — PDFs, slide decks, Word documents, internal wikis, exported notes — offer to help bring that material into the substrate.

The recommended pattern: convert the source to Markdown first (the agent can do this directly for most formats), then run a distillation pass before anything is committed. Ask the user what the document is for and what the agent should preserve. Produce a summary that keeps the durable claims and drops the noise. Show the user the distilled version. Only commit what survives the pass.

Tell the user: the distillation is itself a quality gate. Anything that does not survive the agent's summary did not belong in the substrate to begin with. Raw conversions of legacy documents should not land in `knowledge-base/` directly.

If the user has sensitive content to ingest, point them at `knowledge-base/_starter/SENSITIVE-CONTENT.md` before they put anything in the shared repo.

## Notes for the agent

- If the user skips a question, generate a `[TBD]` placeholder. Do not invent information.
- The `memory/` folder is gitignored. Tell the user these files stay on their machine only.
- The shared `knowledge-base/` will start essentially empty in this starter kit (only the `_starter/` files exist). After setup, suggest the user adds one or two domain files relevant to their team.
- Create the `memory/` subdirectories (`people/`, `projects/`, `context/`, `drafts/`) if they do not exist.
- Do not auto-commit any of the generated files. The user decides when to commit.
