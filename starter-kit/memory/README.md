# Memory

Personal context layer. Each contributor's working notes, profiles of people they work with, project-specific context, drafts in progress, glossary of personal shorthand, and reusable anecdotes.

This entire folder is gitignored except this README. Personal memory does not get committed to the shared repository.

## Expected substructure

The setup interview creates these as needed. You can add or remove subfolders to match your work.

- **`people/`** — one file per collaborator. Name, role, communication style, what they care about, history of how you have worked together. Loaded by the agent when relevant.
- **`projects/`** — active project files. Scope, status, decisions, open questions, blockers. One file per project.
- **`context/`** — your role, your communication patterns, anything contextual about you the agent should know across all sessions. Files like `my-role.md`, `communication-patterns.md`.
- **`drafts/`** — work in progress that does not belong in `shared-projects/` yet. Talking points, exploratory notes, half-finished analyses.
- **`glossary.md`** — personal shorthand decoder. Internal acronyms, nicknames, codenames you use that are not yet in the shared knowledge base.
- **`story-bank.md`** — reusable anecdotes for talks, demos, presentations.

## How memory works

Memory files are loaded by the agent on demand, not all at once. When you ask the agent about a person, it reads `memory/people/[name].md`. When you ask about a project, it reads the project file. The personal manifest at the workspace root (`CLAUDE.md` or equivalent) tells the agent where to look.

Keep each file focused and small. Long files with multiple unrelated topics make progressive disclosure harder.

## How memory grows

When you observe a correction, learn something new about a person, project, or preference, or notice that existing memory is outdated during a session, the agent should propose updating the relevant memory file. The `session-review` skill in `.claude/skills/` does this automatically at session end.

Memory compounds. Each session ends with updates that the next session begins by reading. Over weeks, the agent operates against a richer and richer model of your work.

## What never goes here

- Information that should be shared with the team. That goes in `knowledge-base/` or `shared-projects/`.
- Production secrets. Use a proper secret manager.
- Anything subject to retention or compliance rules in your organization. Memory is convenience, not a record system.
