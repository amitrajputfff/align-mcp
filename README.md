<p align="center"><img src="logo.png" width="72" alt="Align"></p>

# Align MCP server

Ask Claude, ChatGPT, Cursor or any MCP client about your team's meetings: what was decided, who owns what, what's due this week, and what you got done yesterday. Answers come with citations back to the meeting.

[Align](https://meet-align.com) turns meetings into decisions and tickets synced with Jira and Linear. This is its hosted MCP server. There's nothing to install or run: connect to the URL and sign in with OAuth.

```
https://api.meet-align.com/mcp
```

Listed in the official MCP Registry as [`com.meet-align/align`](https://registry.modelcontextprotocol.io/v0/servers?search=com.meet-align).

## Connect

| Client | How |
|---|---|
| **Claude** (web/desktop) | Settings → Connectors → **Add custom connector** → paste the URL |
| **Claude Code** | `claude mcp add --transport http align https://api.meet-align.com/mcp`, then `/mcp` → Authenticate |
| **ChatGPT** | Settings → Apps & Connectors → Advanced → Developer mode → **Create** → paste the URL, auth **OAuth** |
| **Cursor** | `~/.cursor/mcp.json` → `{"mcpServers": {"align": {"url": "https://api.meet-align.com/mcp"}}}` |
| **VS Code** | `.vscode/mcp.json` → `{"servers": {"align": {"type": "http", "url": "https://api.meet-align.com/mcp"}}}` |
| **Windsurf / others** | Any client that supports remote Streamable HTTP servers with OAuth |

The first call opens a browser to sign in to Align and approve the client. You need an Align account (free at [meet-align.com](https://meet-align.com)).

## Tools

| Tool | What it does |
|---|---|
| `ask_align` | Cited answer from your meetings, decisions, docs, chat and tasks |
| `list_meetings` | Recent meetings with summary, participants, decision/action counts |
| `get_meeting` | One meeting: summary, decisions + rationale, action items, risks, optional transcript |
| `list_decisions` | Decisions captured in meetings, filterable by keyword or status |
| `my_standup` | Today's standup from what actually happened: tickets, PRs, commits, blockers |
| `list_my_tasks` | Your tasks and action items (today / open / all) |
| `get_task` | One work item by key (e.g. `ALI-12`), with its synced Jira/Linear issue |
| `find_ticket` | Find the ticket a commit or branch belongs to |
| `update_task` | Change stage, title, description, priority or due date (syncs to Jira/Linear) |
| `comment_task` | Add a progress note (posted to the synced issue too) |
| `create_task` | Log a new work item, optionally in a Jira/Linear-synced project |

Reading tools are marked `readOnlyHint`. Task tools act as the signed-in user and never delete anything.

## Example prompts

- "What did we decide about pricing last week?"
- "Write my standup for today."
- "What's due for me this week, and what's blocked?"
- "I just pushed the checkout fix. Move its ticket to review."

## Auth and data

- Transport: Streamable HTTP (stateless, JSON responses).
- Auth: OAuth 2.1 with dynamic client registration + PKCE. Discovery via [RFC 9728](https://www.rfc-editor.org/rfc/rfc9728) metadata at `https://api.meet-align.com/.well-known/oauth-protected-resource/mcp`.
- An assistant sees exactly what you see in Align, nothing more.

Docs: [docs.meet-align.com/guide/mcp](https://docs.meet-align.com/guide/mcp) · Privacy: [meet-align.com/privacy](https://meet-align.com/privacy) · Security: [meet-align.com/security](https://meet-align.com/security) · Contact: hello@meet-align.com

This repo holds the listing and docs. The server itself is hosted by Align.
