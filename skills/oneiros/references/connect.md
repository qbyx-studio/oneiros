# Connect Qbyx Oneiros

Use this guide when the user asks to connect Oneiros or the readiness check
finds that setup is needed. Codex, Claude, DeepseekHarness, Hermes, and other
MCP clients each provide their own supported connection settings.

## Get this installation's details

Ask the user for the connection message from the Oneiros dashboard's first
box. With an accessible, user-provided dashboard address, read
`/api/oneiros/control/connection`. Schema version 1 provides `server_id`,
`command`, `args`, `config`, and the currently bundled `skills`.
Use these current values. A moved installation can produce new paths.

## Choose the correct computer

The launch command belongs to the computer running Oneiros. When the agent
runs there, register the command and arguments through the client's supported
MCP settings, preserving existing entries. The stable server ID is `qbyx-oneiros`.

When the agent runs on another computer, use the user's confirmed SSH
destination with `ssh -T` to launch the supplied command on the Oneiros host.
Quote remote paths correctly, including paths with spaces. Keep host-key
verification enabled. The dashboard's browser tunnel carries HTTP traffic;
the MCP connection carries stdio over its own SSH process. Verify SSH access
before changing the agent configuration. Ask for the specific missing host
or authentication setup when required. Keep credentials out of Skill files.

The installed Windows package supplies `QbyxOneirosMCP.exe`. Source
installations supply the governed `agent/mcp/launcher.py` command. Preserve
that governed entrypoint and its production approval lifecycle.

## Install Skills

Use the dashboard's Install Oneiros Skills button to obtain an installation
request and a ZIP of the bundled Skills. The download route is
`/api/oneiros/control/skills.zip`. If the agent cannot reach the browser's
address, ask the user to attach the downloaded ZIP.

Inspect the bundle and discover its `SKILL.md` folders. Install them into the
chosen agent's documented user-level Skill directory on the agent's computer.
Preserve unrelated files. Ask before replacing locally customized Skills.
Each agent controls its discovery rules; a new session or reload may be needed.

For source installations, the bundled installer accepts an explicit target:

```text
python3 agent/install_skills.py --target <supported-skill-root>
python3 agent/install_skills.py --check --target <supported-skill-root>
```

## Verify

Reconnect the MCP client, confirm the governed tools are visible, and call
`qbyx_oneiros_status` once. Report the observed result. Production begins
with the Oneiros Skill's plan and approval flow. A setup request authorizes
connection work; a GPU render requires the user's approval of its specific plan.
