---
name: pallyy
description: Schedule, review and publish social media posts through the user's Pallyy account via the Pallyy MCP server. Use when the user asks to plan, draft, schedule, list or update social media posts, import media into their library, or pin notes to their content calendar.
---

# Pallyy

Pallyy is a social media scheduler for agencies and brands. Each client or brand is a **social set** holding that brand's connected accounts. Posts are **post sets**: one piece of content with a version per network. The MCP server at `https://app.pallyy.com/mcp` exposes the same capabilities as Pallyy's REST API, under the same rules: every connection can read, writes need the matching scope, and the user can limit a connection to specific social sets.

## Workflow

1. **Find the set.** Call `list_social_sets` first and confirm with the user which set to work in when they have more than one. Every other tool takes a `socialSetId`.
2. **Media first.** A post with an image or video references media already in the set's library. Use `list_media` to find existing items, or `create_media_upload` to import from a public URL, then poll `get_media_upload` until its status is `READY` and use the returned `mediaLibraryId`.
3. **Draft, then schedule.** `create_post_set` with `status: "DRAFT"` lets the user review before anything goes out. Scheduling (`status: "SCHEDULED"`) needs the `post-sets:publish` scope; if it's missing, save a draft and tell the user it's ready to schedule in Pallyy.
4. **Link back.** Every post set opens in Pallyy at `https://app.pallyy.com/dashboard/scheduling/calendar/month?set=<socialSetId>&post=<postSetId>`. Give the user that link after creating or changing a post.

## Tools

| Tool | Use it to | Scope |
| --- | --- | --- |
| `list_social_sets`, `get_social_set` | Find the brand and its connected accounts | read |
| `list_post_sets`, `get_post_set` | See what's scheduled, drafted, or awaiting approval | read |
| `create_post_set`, `update_post_set` | Draft or schedule posts, change time, status, approval | `post-sets:write`, plus `post-sets:publish` to schedule |
| `list_media`, `get_media` | Browse the media library | read |
| `create_media_upload`, `get_media_upload` | Import a file from a URL and wait for it | `media:write` |
| `list_notes`, `get_note`, `create_note`, `update_note` | Calendar notes and reminders | `notes:write` |

## Rules of thumb

- Never schedule to a network the user didn't name; each post set lists its target accounts explicitly.
- Respect approval: a post set with `approval` other than `NONE` is in a review workflow, so don't flip its status without asking.
- Dates are ISO 8601 in UTC. Convert from the user's timezone before sending.
- Tool results are the same JSON the REST API returns; the field reference is at https://pallyy.com/docs/api/mcp-tools.
- If the client can't sign in with OAuth, the user can create an API key at https://app.pallyy.com/settings/api-keys and configure it as a bearer header.
