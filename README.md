# n8n Tidy Up

An agent skill that arranges existing n8n workflows into compact, readable box-shaped layouts through MCP: wrapped rows, clear branches, and AI helpers grouped under their agent. It changes node positions only and preserves behavior, including n8n's position-dependent branch execution order.

Works with any agent that reads `SKILL.md` skills (Claude Code, Codex, opencode, Copilot CLI and others).

## Requirements

An n8n MCP server connected to your agent that can read a full workflow and update node positions.

## Install

Clone into your agent's skills folder.

Claude Code:

```bash
git clone https://github.com/sys-nat-ai/n8n-tidy-up ~/.claude/skills/n8n-tidy-up
```

Codex:

```bash
git clone https://github.com/sys-nat-ai/n8n-tidy-up ~/.codex/skills/n8n-tidy-up
```

Other agents:

```bash
git clone https://github.com/sys-nat-ai/n8n-tidy-up ~/.agents/skills/n8n-tidy-up
```

Start a new session so the agent picks it up.

## Use

Ask the agent to tidy a workflow and give it the workflow URL, ID or name:

> Tidy up the layout of my "Lead intake" workflow.

Ask for a preview only if you do not want the layout saved.

## License

[MIT](LICENSE)
