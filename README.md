# SignalPilot Agent plugin for Codex and ChatGPT

Delegate a data analysis to a SignalPilot agent from Codex. The plugin bundles the
SignalPilot MCP server (OAuth sign-in, no API key) and two skills:

- `signalpilot`: launch the agent, share the chat link, watch progress, collect the report.
- `signalpilot-artifacts`: download the files the agent saved and check them.

Codex plugins work in the Codex CLI and the ChatGPT apps. They are not available in the
IDE extension at the time of writing.

## Install

```bash
codex plugin marketplace add SignalPilot-Labs/signalpilot-chatgpt-work-plugin
codex plugin add signalpilot-agent@signalpilot-agent
```

Some Codex versions name the second command `codex plugin install`. Run `codex plugin --help`
to check. The marketplace policy asks you to sign in to SignalPilot during install. If it
does not, run:

```bash
codex mcp login signalpilot
```

The MCP server is `https://gateway.signalpilot.ai/mcp`.

## Downloads and the sandbox

MCP tool calls run outside the shell sandbox and always work. The artifact download in the
`signalpilot-artifacts` skill is a shell `curl` command. In `workspace-write` mode the
sandbox blocks network access by default, so Codex asks for approval to run it outside the
sandbox. To skip the prompt:

```toml
[sandbox_workspace_write]
network_access = true
```

## Try it

```
$signalpilot Run a SignalPilot agent for a simple chart of the past year of revenue and write a report.
```

Codex shares the chat link at once, watches the run, downloads the chart and data, and
writes `signalpilot-reports/<date>-<task>/report.md`.

## Requirements

- Codex CLI 0.131 or newer (plugin marketplaces).
- A SignalPilot account with a default project and connection set under Settings, then
  MCP Connect.
