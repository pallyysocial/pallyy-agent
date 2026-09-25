# Pallyy for AI agents

Connect [Pallyy](https://pallyy.com) to your AI assistant and schedule social media posts from a conversation. This repo packages Pallyy's hosted MCP server as a plugin for Cursor, Grok Build, Grok Bot and Claude, plus a skill that teaches the agent Pallyy's workflow.

The server lives at `https://app.pallyy.com/mcp` and is included on every Pallyy plan, the free plan included. Docs: https://pallyy.com/docs/api/mcp

## What the agent can do

- List your social sets and their connected accounts (Instagram, Facebook, LinkedIn, TikTok, YouTube, Pinterest, Threads, Bluesky, X, Google Business Profile)
- List, create and update draft or scheduled posts, including approval state
- Import images and videos into the media library from a URL, or from the conversation in ChatGPT
- Read and pin calendar notes

## Sign in

The plugin points the agent at the server; on first use the agent asks you to sign in to Pallyy and approve which social sets and permissions it gets. Nothing runs locally and no token is stored by the plugin. Any MCP client that supports OAuth or a bearer header works; for clients without OAuth, create an API key at [Settings > API Keys](https://app.pallyy.com/settings/api-keys) in Pallyy and send it as `Authorization: Bearer pallyy_...`.

## Install

- **Cursor**: search for Pallyy in the Cursor Marketplace and install.
- **Grok Bot**: Settings, Plugins, search Pallyy.
- **Grok Build**: `plugin install pallyy` from the xAI marketplace.
- **Claude Code**: `claude mcp add --transport http pallyy https://app.pallyy.com/mcp`, or add this repo as a plugin marketplace.
- **Anything else**: point the client at `https://app.pallyy.com/mcp`.

## Layout

| Path | For |
| --- | --- |
| `.cursor-plugin/` | Cursor Marketplace manifest and MCP config |
| `.grok-plugin/` | Grok Build catalog manifest and MCP config |
| `.claude-plugin/` | Claude Code plugin manifest |
| `.mcp.json` | The server, for hosts that read it from the repo root |
| `skills/pallyy/` | The skill: how to work with sets, media, drafts and scheduling |

## License

MIT. Pallyy itself is a hosted service, see https://pallyy.com/terms.
