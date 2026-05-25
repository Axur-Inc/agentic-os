# Knowledge Base

The shared, stable reference layer. What your company knows, expressed as Markdown files in a Git repository.

Organize by domain. Use a thin `_index.md` at the top of each subdirectory pointing to the focused files inside. Examples of what lives here: product descriptions, customer context, processes, narrative rules, internal glossary, market context, brand assets, integration guides.

## Conventions

- Add files as needed. One topic per file, named clearly.
- Mark unverified content with `[TBD]`, outdated content with `[NEEDS-UPDATE]`, in-progress content with `[DRAFT]`. The agent reads these markers as behavioral gates. See `_starter/STATUS-MARKERS.md`.
- Include a `Last updated: YYYY-MM-DD` line at the top of any file likely to age.
- Prefer specifics over generalities. The agent operates better against `Annual revenue: $42M (Q4 2025)` than against `revenue is significant`.

## What goes here vs. shared-projects/

`knowledge-base/` is for stable reference — knowledge that has settled. `shared-projects/` is for work in flight — drafts, plans, deliverables under construction. When a project finishes and its output is useful as long-term reference, promote the final artifact here.

## Do not delete

The `_starter/` subdirectory contains the onboarding script, the personal manifest template, and reference docs for principles and conventions. These are loaded by the agent during setup and cited by the workspace manifest. Keep them.
