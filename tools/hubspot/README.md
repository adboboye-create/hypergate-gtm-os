# HubSpot MCP

Server `hubspot`: HubSpot's official remote MCP server (https://mcp.hubspot.com), signed in with OAuth. It lives in this project's local Claude Code config (`~/.claude.json`), not in `.mcp.json`, so nothing about it is committed.

- Portal: EU1 data hosting (checked 2026-11-27). HubSpot reports the portal has not completed onboarding.
- Covers CRM records (contacts, companies, deals, leads, custom objects), properties, segments (lists), campaigns, marketing emails, pages, social and AEO.
- Sign in or re-authenticate: run `/mcp` in an interactive Claude Code session and pick `hubspot`.

## Rules

- Ask before any write: creating or changing records, properties, lists, emails or pages (CLAUDE.md rule 4).
- Log every change in this week's work log.

## History

- 2026-11-27: a second server, `hubspot-crm` (`@hubspot/mcp-server@0.4.0` with a private app token), was tried and removed. The token was valid but never reached the server process (401 every time), and the official server already covers the same work. If the private app still exists in HubSpot, delete it or rotate its token (Settings > Integrations > Private Apps).
