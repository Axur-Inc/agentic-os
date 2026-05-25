# Agentic OS Starter Kit

A working seed of the architecture described in *Restructuring Knowledge Work for Human-Agent Teams* (the manifesto) and *An Agentic Operating System: Seven Weeks of Practice* (the field report). Fork it, populate the knowledge base with your own context, and you have a working agentic operating system for your team in under an hour.

## What this is

A minimal, opinionated, tool-agnostic file structure for running an LLM agent against your company's knowledge as the substrate. Two layers (commons + workshop), five concrete surfaces, six conventions. Written to be forked, not just read.

## Quickstart

1. Fork or clone this repository.
2. Open the workspace in any agentic tool (Claude Code, Cowork, Cursor, GitHub Copilot, OpenCode, AntiGravity, or anything else that reads files and follows instructions).
3. Tell the agent: **"Set me up."** The agent will run `knowledge-base/_starter/setup-interview.md`, ask you a few questions, and generate your personal context files.

That is it. From there, populate `knowledge-base/` with what your company knows, and start using the agent against it.

## Structure

```
agentic-os-starter/
├── README.md                              # This file
├── .gitignore                             # What stays out of the shared repo
│
├── knowledge-base/                        # COMMONS — what the company knows
│   ├── README.md
│   └── _starter/
│       ├── setup-interview.md             # Agent-addressed onboarding script
│       ├── CLAUDE-template.md             # Personal manifest template
│       ├── PRINCIPLES.md                  # The six principles
│       ├── STATUS-MARKERS.md              # Behavioral gates reference
│       └── SENSITIVE-CONTENT.md           # Open question on hard segregation
│
├── shared-projects/                       # COMMONS — work in flight
│   └── README.md
│
├── tools/                                 # COMMONS — executable capabilities
│   └── README.md
│
├── memory/                                # WORKSHOP — personal context (gitignored)
│   └── README.md
│
└── skills/                                # WORKSHOP — procedural workflows
    └── session-review/                     # (move to .claude/skills/ for Claude tools)
        └── SKILL.md
```

After running `Set me up`, the following will exist in your local workspace (gitignored):

```
├── CLAUDE.md                              # Your personal manifest
├── TASKS.md                               # Your personal task list
└── memory/
    ├── people/                            # One file per collaborator
    ├── projects/                          # One file per active project
    ├── context/                           # Your role, communication patterns
    ├── drafts/                            # Work in progress
    └── glossary.md                        # Personal shorthand decoder
```

## How it works

Two layers:

- **COMMONS** (`knowledge-base/`, `shared-projects/`, `tools/`) — shared, versioned in Git, reviewed before merge. Everyone reads from it; everyone contributes to it.
- **WORKSHOP** (`memory/`, `.claude/skills/`, your personal `CLAUDE.md` and `TASKS.md`) — autonomous, fast-moving, gitignored. Each contributor manages their own.

Six conventions do most of the operational work:

1. **Knowledge is Markdown** — everything in plain text files, version controlled, parseable by any LLM.
2. **Progressive disclosure** — thin index at the top, modular files below, agent loads only what the current question needs.
3. **Shared truth, personal workspace** — strict separation between commons and workshop.
4. **Tool agnosticism** — works with any agent that reads files. Switch tools without touching the substrate.
5. **Status markers as behavioral gates** — `[TBD]`, `[NEEDS-UPDATE]`, `[DRAFT]` change agent behavior.
6. **Skills as reusable intent** — encode workflows once, use them everywhere.

See `knowledge-base/_starter/PRINCIPLES.md` for the full version.

## What to do after setup

1. Add one or two domain files to `knowledge-base/`. Whatever your team gets asked about most often — product descriptions, internal terms, processes. Markdown only. If you have legacy material in PDFs or slide decks, convert it to Markdown first and ask the agent to distill the result before committing. The distillation is a quality gate: anything that does not survive the agent's summary did not belong in the substrate to begin with.
2. Use the agent for a real task: drafting a stakeholder update, summarizing a meeting, comparing two product capabilities, preparing for a customer call. Watch what the agent gets right and what it gets wrong.
3. Update the knowledge base based on what you learned. The first failure modes are also the first signals of what is missing.

## What to expect

Three frictions are real in week one. Naming them upfront so they do not surprise you.

- **Git is the toll gate.** For contributors who do not come from engineering, branching, committing, and pulling are not muscle memory. They are learnable in an afternoon, and the agent will help — natural-language Git commands, narrated diffs, branch naming suggestions. Plan for the cliff anyway. This is the most universal friction we observed, and the one we expect tooling to absorb fastest.
- **Model choice is not obvious.** Most agentic tools expose multiple model tiers. Pricing is opaque. The default is usually the most expensive option, and most tasks do not need it. Surface the choice to the team explicitly, early. A higher-capability model belongs on planning and architecture work; a faster, cheaper tier handles execution and recurring workflows at the same quality.
- **Tokens are working capital.** Long sessions accumulate context, and that context is paid for on every turn. Reset between distinct tasks. Compact long sessions before switching focus. The field report's section on *Tokens are the new working capital* is the operating manual.

## Common pitfalls

- Do not put too much in `CLAUDE.md`. Keep it around fifty lines. Push everything else to dedicated files under `memory/` and `knowledge-base/`.
- Do not treat the knowledge base as documentation for humans. It is operating context for agents. It should answer "what does the agent need to know to act on my behalf", not "what should a new hire read on day one".
- Watch token consumption. See the field report's section on *Tokens are the new working capital*.
- Start with two people, ideally two who already tinker with their own tools — call them the evangelists. Each function in our pilot had one contributor who tried the substrate first, hit the friction, and built something useful. The rest of the function joined only after seeing the evangelist's productivity change visibly. Two evangelists will pull a function. Twenty mandated participants will not.

## Tool-specific notes

- **Claude Code / Cowork**: the personal manifest is `CLAUDE.md`. Use the template at `knowledge-base/_starter/CLAUDE-template.md` directly.
- **Cursor**: rename to `.cursorrules` or place under `.cursor/rules/`. Same content, different filename.
- **OpenCode / GitHub Copilot / AntiGravity**: the cross-tool open standard is `AGENTS.md`. Rename the template accordingly.

The substrate (`knowledge-base/`, `shared-projects/`, `tools/`, `memory/`) is identical across tools. Only the manifest filename changes.

## What this kit is not

- A polished product. It is a working seed.
- A complete framework. It is the minimum that makes the architecture real.
- Specific to any company. Replace placeholders with your own context.

## License

MIT (proposed — finalize before public release).

## Origin

Built by Jônadas Techio and Fábio Ramos at Axur, based on a seven-week internal pilot. The full account is in the [field report]. The argument is in the [manifesto].
