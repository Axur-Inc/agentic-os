# Sensitive Content — A Note

The substrate as described in the manifesto and field report assumes a single shared repository, with project folders for relevance. That works for content that does not need hard access boundaries.

It does not work, on its own, for content that does need hard boundaries: financial planning, HR records, M&A material, customer data under regulatory constraints, security-sensitive operational data. Project folders give coarse separation by relevance, but the access boundary in this setup is the repository itself, not the folder. Anyone with read access to the repo can read every project under it.

## What teams do today

For non-sensitive content: one shared repository, project folders for relevance, the `[CONFIDENTIAL]` status marker (see `STATUS-MARKERS.md`) where extra care is required. The agent treats `[CONFIDENTIAL]` as a behavioral gate — it will not include marked content in shareable outputs without confirmation. A marker is a soft constraint, not a hard one. It changes agent behavior, not file system permissions.

For sensitive content: keep it out of the shared repository. Most teams running this architecture today maintain one or two parallel knowledge bases for sensitive material, accessed by a smaller subset of contributors. The personal `memory/` layer (already gitignored) is appropriate for individually sensitive notes; group-sensitive content needs its own private repository.

## What is not solved

The likely path forward as a team scales is multiple repositories, each with its own access boundary, each with its own substrate. The cost of that path is unclear:

- Cross-repository references would need to resolve cleanly. The agent has to know which substrate to load for which question, without leaking context between them.
- Knowledge that legitimately sits in both worlds — a glossary, a style guide, a brand voice, basic product descriptions — would either need to duplicate across repos or live in a third public reference both can read.
- Governance overhead grows. Two repos require twice the review discipline; ten require a coordination model the substrate does not yet specify.

We have not chosen between those tradeoffs. The field report's *What we don't yet know → How sensitive content scales* covers the same gap from the experiment side. This file is a placeholder for the conventions and tooling once we have them.

## Practical advice for now

If you are starting this kit and you know you will have sensitive content from day one:

1. Decide what is sensitive before populating `knowledge-base/`. Do not put it in the shared repo and try to retract later — Git history persists.
2. Use the `[CONFIDENTIAL]` marker for content that is shareable internally but needs care on outputs.
3. For content that is not shareable across the team, set up a second private repository and treat it as a parallel substrate. Accept that the agent will need explicit pointers to switch between them.
4. Plan for redundancy on cross-cutting references (glossary, conventions). Either duplicate them or maintain a public reference both substrates can load.

If you find a workable pattern for multi-repo segregation before we do, we would like to hear about it.
