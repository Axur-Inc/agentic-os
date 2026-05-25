# Status Markers — Reference

Status markers are machine-readable signals embedded in documents that change the agent's behavior. They are not formatting. They are instructions.

## The four standard markers

| Marker | Meaning | Agent behavior |
|--------|---------|----------------|
| `[TBD]` | Value is unknown | Do not present adjacent content as fact. Propose a value or ask the user. |
| `[NEEDS-UPDATE]` | Content may be outdated | Flag uncertainty when citing. Propose updating the source. |
| `[DRAFT]` | Work in progress | Do not include in final outputs. Treat as exploratory only. |
| `[CONFIDENTIAL]` | Internal use only | Do not include in shareable outputs. Flag if user asks to share. |

## How to use them

Embed markers inline near the affected content. Examples:

> Estimated arrival: [TBD] — waiting on logistics confirmation.

> Annual revenue: $42M [NEEDS-UPDATE] — last verified Q3 2025.

> [DRAFT] Section to be reviewed by legal before publication.

> Customer roster: [CONFIDENTIAL] — do not include in external decks.

The agent reads these markers as behavioral gates. The constraint travels with the knowledge, not with the chat session or tool configuration.

## Why this matters

Without markers, the agent has no way to distinguish a verified fact from a guess, a current value from a stale one, a final draft from a working one. It treats everything as equally authoritative, and the result is confident hallucination.

With markers, the agent can reason about the reliability of its own context. It will hedge where you have hedged, defer where you have deferred, and exclude where you have excluded.

## Adding new markers

If your team needs additional markers (for example, `[REVIEW-REQUIRED]`, `[EXTERNAL]`, `[LEGAL-CHECK]`), document them here and reference the convention in your personal manifest so the agent enforces them consistently. Keep the set small. Five to seven markers is usually enough; more becomes hard to remember and inconsistent in practice.

## Anti-patterns

- Marking everything. If most content is `[NEEDS-UPDATE]`, the marker stops carrying signal. Use sparingly.
- Marking without explanation. `[TBD]` alone is weaker than `[TBD] — waiting on Q4 numbers from finance`.
- Removing markers without addressing the underlying issue. The marker is a placeholder for resolution, not a UI element.
