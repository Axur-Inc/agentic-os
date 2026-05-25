# Tools

Executable code: scripts, MCP server implementations, Python and Node tools the agent can call.

## Conventions

- One subdirectory per tool.
- Each tool has its own `README.md` describing what it does, how to install dependencies, how to configure credentials, and how to run it.
- Each tool that requires credentials includes a `.env.example` showing the variables it needs. The actual `.env` is gitignored.
- Tools should be invokable from the command line as well as from the agent. The agent calls them through MCP or direct shell when authorized.

## Why tools live alongside knowledge

Knowledge tells the agent what your company knows. Tools let the agent act on that knowledge — query a database, send a message, generate a report, parse a file, run an analysis. The agent reading both as part of the same operation is what turns the substrate from a reference library into an executable operating system.

## Examples of what goes here

- A tool that queries your BI platform via API and returns formatted results.
- An MCP server that exposes a specific data source (tickets, leads, telemetry) as a queryable surface for the agent.
- A script that takes a structured input and produces a branded PDF using your company's templates.
- A connector to your messaging platform (Slack, Teams) that lets the agent post drafts for review.

## Anti-patterns

- One-off scripts that only one person uses and that nobody else can rerun. If a tool lives here, anyone on the team should be able to invoke it after reading its README.
- Hardcoded credentials. Always use `.env` for secrets and `.env.example` for the schema.
- Tools without READMEs. The README is the tool's interface for everyone other than the original author.
