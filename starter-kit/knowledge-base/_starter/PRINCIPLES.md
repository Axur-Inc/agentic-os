# The Six Principles

The architecture rests on six principles. They emerged from constraints encountered in practice, not from upfront design. Each one is a one-line rule that the agent applies to every operation.

## 1. Knowledge is Markdown

The canonical format for everything the company knows is plain Markdown files in a Git repository. Not a database, not a SaaS platform, not a proprietary format. Markdown is human-readable, version-controlled, portable across tools, and natively parseable by every major LLM. If a piece of knowledge cannot be expressed as a Markdown file, it either needs to be restructured or it belongs somewhere else. The constraint is productive: it forces clarity on what counts as durable knowledge versus what counts as ephemera.

## 2. Progressive disclosure

No agent and no human should need to load the entire knowledge base to answer a question. The system is organized as a thin index at the top — a root instruction file (`CLAUDE.md`, `AGENTS.md`, or equivalent) of about fifty lines — that points to topic-specific directories, each with its own focused files. The agent reads the index first, then loads only what the current task requires. The repository can grow to thousands of files without slowing the agent down, because at any given moment the agent operates on a small, relevant subset.

The corollary worth naming: you do not need to know where each piece of information lives. Asking the agent "where is X?" or "which file should I update?" is the model's job, not yours. The structure exists for the agent to navigate. The natural-language interface exists for the human. This is one of the harder shifts for new contributors to internalize, because every prior file system trained you to know where things are.

## 3. Shared truth, personal workspace

There is a single source of truth that everyone reads from and contributes to (`knowledge-base/`, `shared-projects/`, `tools/`). There is also a personal layer that each contributor manages on their own (`memory/`, the personal manifest, `TASKS.md`, `.claude/skills/`). The shared layer is governed (reviewed before merge). The personal layer is autonomous (gitignored, each person manages their own). This separation prevents the two failure modes of knowledge systems: the wiki nobody updates (too heavy to contribute), and the wiki nobody trusts (too open).

## 4. Tool agnosticism

The knowledge base does not depend on any specific AI tool, editor, or platform. Git is the transport layer. Markdown is the storage format. Any LLM agent that can read files and follow instructions can operate on this substrate. Tool-specific configuration exists as a thin adapter on top of the portable base. Switch tools — Claude Code, Cursor, GitHub Copilot, OpenCode, AntiGravity, anything — and the substrate is unchanged. Only the manifest filename differs.

## 5. Status markers as behavioral gates

Documents contain machine-readable signals about their own reliability. `[TBD]` means the agent should not present adjacent content as fact. `[NEEDS-UPDATE]` means flag uncertainty. `[DRAFT]` means do not appear in final outputs. `[CONFIDENTIAL]` means extra care. These markers turn passive documents into active instructions. Constraints travel with the knowledge, not with the chat session or tool configuration. Once you have markers, the document is no longer a description of state. It is a participant in the workflow.

## 6. Skills as reusable intent

Agent workflows should be encoded as reusable skills rather than one-off prompts. A skill is a Markdown file that defines a specific workflow, its trigger, the tools it should use, and its expected output. Skills are version-controlled alongside the knowledge base, shareable across contributors, and composable with each other. A skill for generating a quarterly business review can call a skill for applying brand identity, which can call live data connectors, producing a complete branded document from a single natural-language command. Skills are how the knowledge base stops being a reference library and becomes an executable operating system.

---

These six did not exist on day one of our pilot. They emerged as failure modes appeared, got formalized, and stuck because removing any one of them brought the failures back. They are the shortest version of the architecture you can adopt and still have it work.
