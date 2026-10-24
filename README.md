# FactoGraph

<!-- mcp-name: app.factograph/factograph -->

Memory for AI agents: facts a person approved, each with a link, and answers that cite them.

FactoGraph keeps knowledge as facts a person approved, each with its own link, and
answers questions only from those facts, citing every claim and checking the answer
against them. An agent can read any public store, or keep the facts a person approves
in a store of their own.

This repository holds FactoGraph's agent plugin and its listing files. The MCP server
itself is hosted: there is nothing to install or run.

- MCP server (Streamable HTTP, no sign-in): `https://api.factograph.app/api/mcp`
- Official MCP Registry: `app.factograph/factograph`
- Guide for agents: https://www.factograph.app/for-ai-agents.html
- Website: https://www.factograph.app

## Connect

**Cursor:** [Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=factograph&config=eyJ1cmwiOiAiaHR0cHM6Ly9hcGkuZmFjdG9ncmFwaC5hcHAvYXBpL21jcCJ9), or in `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "factograph": {
      "url": "https://api.factograph.app/api/mcp"
    }
  }
}
```

**Claude Code:**

As a plugin, with the `get-started` skill:

```sh
/plugin marketplace add FactoGraphApp/factograph-mcp
/plugin install factograph@factograph
```

or only the server:

```sh
claude mcp add --transport http factograph https://api.factograph.app/api/mcp
```

**VS Code** (`.vscode/mcp.json`):

```json
{
  "servers": {
    "factograph": {
      "type": "http",
      "url": "https://api.factograph.app/api/mcp"
    }
  }
}
```

**Codex CLI** (`~/.codex/config.toml`):

```toml
[mcp_servers.factograph]
url = "https://api.factograph.app/api/mcp"
```

**Gemini CLI:**

```sh
gemini extensions install https://github.com/FactoGraphApp/factograph-mcp
```

or in `settings.json`:

```json
{
  "mcpServers": {
    "factograph": {
      "httpUrl": "https://api.factograph.app/api/mcp"
    }
  }
}
```

**Claude, ChatGPT and other chat apps:** add a custom connector with the URL
`https://api.factograph.app/api/mcp`.

## Tools

| Tool | What it does |
|---|---|
| `getManual` | The store's manual, and what it holds: how many facts, from which sources |
| `listFacts` | Every fact in the store, numbered, each number a link to the fact |
| `ask` | Answers a question only from the store's facts, each claim linked to its fact |
| `startStep` | Runs a step in a private store: propose, add, documents, ask or remove |
| `getStep` | Where a running step is now: its next prompt, or its result |
| `replyToPrompt` | Answers a step's prompt |
| `createStore` | Makes the person a store of their own, only after they agree |

Every tool takes a store link. A public link (`https://api.factograph.app/api/p/<id>`)
only reads and asks; with no link the tools read the FactoGraph guide, a public store
about FactoGraph itself. A person's private link (`https://api.factograph.app/api/k/<id>`)
runs every step in their store. Nothing is stored without the person's approval, and
nothing is deleted without their confirmation.

## The plugin

The plugin follows the [Agent Plugins](https://agent-plugins.org) 1.0 standard:

- `plugin.json`: the manifest
- `mcp.json`: the FactoGraph MCP server
- `skills/get-started/SKILL.md`: how an agent uses the tools and cites facts
- `server.json`: the entry in the official MCP Registry
- `gemini-extension.json`: the Gemini CLI extension
- `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`: the Claude Code plugin and its marketplace

## Privacy and terms

- Privacy: https://www.factograph.app/privacy.html
- Terms: https://www.factograph.app/terms.html
- Contact: info@factograph.app

## License

The files in this repository are under the [MIT License](LICENSE).
