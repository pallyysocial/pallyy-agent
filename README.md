# Pallyy for AI agents

Connect [Pallyy](https://pallyy.com) to your AI assistant and schedule social media posts from a conversation. This repo packages Pallyy's hosted MCP server as a plugin for Cursor, Grok Build, Grok Bot, Claude and Gemini CLI, a skill that teaches any agent Pallyy's workflow, and the one-line setup for agents that take a custom MCP connector, such as Cue, Muse and ChatGPT.

The server lives at `https://app.pallyy.com/mcp` and is included on every Pallyy plan, the free plan included. Docs: https://pallyy.com/docs/api/mcp

## What the agent can do

- List your social sets and their connected accounts (Instagram, Facebook, LinkedIn, TikTok, YouTube, Pinterest, Threads, Bluesky, X, Google Business Profile)
- List, create and update draft or scheduled posts, including approval state
- Import images and videos into the media library from a URL, or from the conversation in ChatGPT
- Read and pin calendar notes

## Sign in

The plugin points the agent at the server; on first use the agent asks you to sign in to Pallyy and approve which social sets and permissions it gets. Nothing runs locally and no token is stored by the plugin. Any MCP client that supports OAuth or a bearer header works; for clients without OAuth, create an API key at [Settings > API Keys](https://app.pallyy.com/settings/api-keys) in Pallyy and send it as `Authorization: Bearer pallyy_...`.

## Install

Plugins and marketplaces:

- **Claude** (web, desktop, mobile): connect Pallyy from the [connector directory](https://claude.ai/directory/connectors/pallyy).
- **Claude Code**: `claude plugin marketplace add pallyysocial/pallyy-agent` then `claude plugin install pallyy@pallyy-agent`. Or just the server: `claude mcp add --transport http pallyy https://app.pallyy.com/mcp`.
- **Cursor**: search for Pallyy in the Cursor Marketplace and install.
- **Grok Bot**: Settings, Plugins, search Pallyy.
- **Grok Build**: `plugin install pallyy` from the xAI marketplace.
- **Gemini CLI**: `gemini extensions install https://github.com/pallyysocial/pallyy-agent`.
- **Codex, OpenClaw, Hermes Agent, GitHub Copilot and other agents that install skills**: `npx skills add pallyysocial/pallyy-agent`, then create an API key at [Settings > API Keys](https://app.pallyy.com/settings/api-keys) and give it to the agent when it asks.

Agents that take a custom MCP connector:

- **Cue** (Manus): send your Cue agent this message. *Add Pallyy as a custom MCP connector over HTTP with OAuth: https://app.pallyy.com/mcp. Sign in to Pallyy when it asks and approve the social sets it may use.*
- **Muse** (Meta): the same message works in Muse. *Add my Pallyy connector: https://app.pallyy.com/mcp. Setup: standard MCP over HTTP with OAuth.*
- **Manus**: Settings, Integrations, Custom MCP Servers, Add Server, with `https://app.pallyy.com/mcp` as the URL.
- **ChatGPT**: Settings, Connectors, Create, name it Pallyy and paste `https://app.pallyy.com/mcp`. Keep OAuth as the authentication method. Full steps in the [docs](https://pallyy.com/docs/api/mcp).
- **Anything else**: point the client at `https://app.pallyy.com/mcp`. It signs in with OAuth; clients without OAuth send an API key as a bearer header.

## Layout

| Path | For |
| --- | --- |
| `.cursor-plugin/` | Cursor Marketplace manifest and MCP config |
| `.grok-plugin/` | Grok Build catalog manifest and MCP config |
| `.claude-plugin/` | Claude Code plugin manifest and the marketplace that lists it |
| `gemini-extension.json` | Gemini CLI extension manifest |
| `.mcp.json` | The server, for hosts that read it from the repo root |
| `skills/pallyy/` | The skill: how to work with sets, media, drafts and scheduling |

## License

MIT. Pallyy itself is a hosted service, see https://pallyy.com/terms.
