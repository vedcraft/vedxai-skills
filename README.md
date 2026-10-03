# VedXAI Skills

Let your AI assistant manage your social media through [VedXAI](https://vedxai.com): list and write posts, schedule and publish, check insights, and more. This repo holds the skills (instructions for the assistant) and the connection to the VedXAI MCP server. It works with Claude Code, Claude Cowork and Codex.

The skills are generated from the skill packs in `vedcraft/vedxai-mcp-server` (`yarn plugin:build`); do not edit `skills/` by hand.

## Before you start

1. **A VedXAI account** with the assistant feature enabled.
2. **A personal token.** In VedXAI go to **Settings > Chat assistant > Create token** and copy the value (it starts with `vxm_`). It carries your own plan and limits, and you can revoke it there at any time. Treat it like a password.
3. **Set it in your environment:**

   macOS or Linux:
   ```
   export VEDXAI_TOKEN="vxm_..."
   ```
   Windows (PowerShell):
   ```
   $env:VEDXAI_TOKEN = "vxm_..."
   ```
   Add it to your shell profile to keep it between sessions.

The server address defaults to `https://mcp.vedxai.com/mcp`. Set `VEDXAI_MCP_URL` only if you want to use a different server (for example a local or staging one).

## Install in Claude Code

**Option 1: plugin (recommended).** Installs the skills and the server connection together.

```
/plugin marketplace add vedcraft/vedxai-skills
/plugin install vedxai-social@vedxai
```

Restart Claude Code, then run `/mcp` and check that `vedxai` shows as connected.

**Option 2: skills and server separately.**

```
npx skills add vedcraft/vedxai-skills
claude mcp add --transport http vedxai "${VEDXAI_MCP_URL:-https://mcp.vedxai.com/mcp}" --header "Authorization: Bearer $VEDXAI_TOKEN"
```

To install a single skill, add `--skill post-management` to the first command. Using only the second command gives you the tools without the skill guidance (such as "ask first before publishing").

## Install in Claude Cowork

1. Add `https://mcp.vedxai.com/mcp` as a custom connector and give it your token as a bearer token.
2. Upload the folders in `skills/` as skills.

Menu names differ between versions; see Cowork's own help for the exact steps.

## Install in Codex

Copy the folders in `skills/` into your Codex skills folder, then add this to `config.toml`:

```toml
[mcp_servers.vedxai]
url = "https://mcp.vedxai.com/mcp"
bearer_token_env_var = "VEDXAI_TOKEN"
```

## Try it

Ask your assistant: "List my drafts", or "What is my usage this month?".

## Skills

automations, brand, compliance, connectors, content-creation, documents, images, insights, jobs, library, post-management.

## Safety

These tools act on your real social accounts under your own plan and role. Tools that publish, schedule, delete or disconnect are marked "asks first" in each `SKILL.md`; the assistant must get your explicit yes before calling them. Check what it is about to do before you approve.

## Troubleshooting

| Problem | Likely cause |
| --- | --- |
| `/mcp` shows `vedxai` as failed, or a 401 | The token is wrong, revoked, or `VEDXAI_TOKEN` is not set in the shell that started Claude Code. Create a new token and restart. |
| A skill mentions a tool you cannot see | The server hides tools your plan or feature flags do not allow. |
| No tools at all | The assistant feature is not enabled on your account. |

## Notices

See `THIRD_PARTY_NOTICES.md`.
