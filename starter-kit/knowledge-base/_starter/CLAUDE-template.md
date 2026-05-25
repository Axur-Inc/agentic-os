# Memory

> **First time here?** If this file still has placeholders like `[Your name]`, do not fill it in manually. Open this folder in your agentic tool of choice and say: **"Set me up."** The agent will run the onboarding script at `knowledge-base/_starter/setup-interview.md` and generate this file for you. The interview takes about five minutes.

---

## Me
[Your name], [Your role] at [Your company]. [One sentence about what you do.]

## People
| Who | Role | Notes |
|-----|------|-------|
| **[Name]** | [Role] | [How you interact with them] |
→ Full list: `memory/glossary.md`, profiles: `memory/people/`

## Terms
| Term | Meaning |
|------|---------|
→ Full glossary: `memory/glossary.md`
→ Company glossary: `knowledge-base/` (shared)

## Active Projects
| Name | What | Status |
|------|------|--------|
→ Details: `memory/projects/`

## Preferences
- [Your delivery style preferences]
- [Language preferences]
- [Communication style]
- [Tool and format preferences]

## Critical Rules
- [Any rules specific to your role]
→ Company-wide rules: `knowledge-base/`

## Where to find things
→ Shared company knowledge (stable reference): `knowledge-base/`
→ Active collaborative work (in-flight): `shared-projects/`
→ Tools and executable code: `tools/`
→ Personal memory (gitignored): `memory/`
→ Personal skills: `.claude/skills/` (or `skills/` in tool-agnostic starter kits)
→ This file is PERSONAL and gitignored

Read the relevant file before responding about a person, term, or project you are unsure about. Do not guess from this file alone — check the source.

When you observe a correction, learn something new about a person, project, or preference, or notice that existing memory is outdated during a session, flag it and propose updating the relevant memory file. Do not update silently; propose the change and confirm first.

## Status Markers
- `[TBD]` → Do not present as fact. Propose a value or ask.
- `[NEEDS-UPDATE]` → Do not cite as current truth. Flag uncertainty.
- `[DRAFT]` → Do not use in final outputs. Treat as work in progress.
- `[CONFIDENTIAL]` → Internal use only. Extra care required.

→ Full reference: `knowledge-base/_starter/STATUS-MARKERS.md`

## Personal vs Shared Memory
Personal or sensitive info → `memory/` (gitignored). Active collaborative work → `shared-projects/` (git-tracked). Stable reference → `knowledge-base/` (git-tracked). Only add to shared folders when explicitly asked. When in doubt, ask.

## Session Review
At the end of a working session, run the `session-review` skill to update memory files based on what happened. The next session begins with better context than this one had.
