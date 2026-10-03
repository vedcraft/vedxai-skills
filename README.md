# VedXAI skills

Skills and MCP connection that let AI agents (Claude Code, Claude Cowork, Codex) manage social media through [VedXAI](https://vedxai.com). The skills are generated from the skill packs in `vedcraft/vedxai-mcp-server` (`yarn plugin:build`); do not edit `skills/` by hand.

Skills: automations, brand, compliance, connectors, content-creation, documents, images, insights, jobs, library, post-management, wordpress.

## You need

1. `VEDXAI_MCP_URL`: the VedXAI MCP server URL (ends in `/mcp`).
2. `VEDXAI_TOKEN`: a personal token (`vxm_...`) from VedXAI Settings > Chat assistant. It carries your own plan and limits and can be revoked there.

```
export VEDXAI_MCP_URL="https://<server>/mcp"
export VEDXAI_TOKEN="vxm_..."
```

## Install

**Skills only (any agent that supports `npx skills`)**

```
npx skills add vedcraft/vedxai-skills
npx skills add vedcraft/vedxai-skills --skill post-management   # one skill
```

This installs the SKILL.md guidance only. Also add the MCP server:

```
claude mcp add --transport http vedxai "$VEDXAI_MCP_URL" --header "Authorization: Bearer $VEDXAI_TOKEN"
```

**Claude Code plugin (skills and MCP connection together)**

```
/plugin marketplace add vedcraft/vedxai-skills
/plugin install vedxai-social@vedxai
```

**Claude Cowork**: add `VEDXAI_MCP_URL` as a custom connector with the bearer token, and upload the `skills/*` folders as skills. Menu names differ by version.

**Codex**: copy `skills/*` into your Codex skills folder and add to `config.toml`:

```toml
[mcp_servers.vedxai]
url = "<VEDXAI_MCP_URL>"
bearer_token_env_var = "VEDXAI_TOKEN"
```

## Safety

These tools act on your real social accounts under your own plan and role. Tools that publish, schedule, delete or disconnect are marked "asks first" in each SKILL.md; the agent must get your explicit yes before calling them.
