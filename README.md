# Qbyx Oneiros Skills

### Your AI agent's guide to local creation.

Qbyx Oneiros gives your AI agent a local creative engine. These Skills teach
it how to work with the **Qbyx Oneiros MCP**, from the first connection to a
finished image or video.

You describe the result you want. Your agent checks the models available in
Oneiros and helps you choose a plan. You approve the generation. Oneiros runs
the job through ComfyUI, and your agent helps you review the output.

## Start with your Oneiros dashboard

1. Open Oneiros and find **Create with your AI agent**.
2. Click **Copy connection message** and paste it into your AI agent.
3. Click **Install Oneiros Skills**, then copy the installation request into
   the agent. It will guide you through the setup for the agents you use.
4. Ask: **Use Oneiros to check what I can create.**

Your agent confirms the connection by calling `qbyx_oneiros_status`.
You need a running Qbyx Oneiros installation and an agent that supports MCP
and local Skills. Model availability comes from your Oneiros installation.

## Install from this repository

Copy this request into your agent:

```text
Install the Qbyx Oneiros Skills from https://github.com/qbyx-studio/oneiros
for the agents I use on this computer. Review the files first and use each
agent's supported user-level Skill folder. Preserve my existing settings
and ask before replacing customized Skills. Help me connect the Oneiros MCP
using the connection message from my dashboard, then verify readiness with
qbyx_oneiros_status.
```

With Node.js available, the Skills CLI also provides an interactive install:

```sh
npx skills add qbyx-studio/oneiros --global
```

Choose your agents and the Skills you want when prompted. The CLI supports
a defined set of agents. Each agent controls when installed Skills become
available, so you may need to start a new session.
See the [Skills CLI documentation](https://github.com/vercel-labs/skills).

## Choose your creative path

| Skill | Purpose |
| --- | --- |
| `oneiros` | Connect to Oneiros and guide the production workflow. Start here. |
| `oneiros-image` | Dream: create and review images using available image workflows. |
| `oneiros-video` | Dance: work with available video and audio workflows. |
| `qbyx-oneiros` | A compatible entry name that routes to `oneiros`. |

For example: **Use Oneiros Dream to help me plan a product image.**
Your agent checks the live catalogue before recommending a workflow.
Audio availability follows the capabilities installed in Oneiros.

## Where everything runs

The Skills live on the computer where your agent runs. Oneiros and ComfyUI
run on the computer providing your media tools. Both arrangements work:
everything on one computer, or an agent on a desktop connected to a separate
Oneiros machine.

With two computers, the agent needs an authenticated SSH connection for the
Oneiros MCP. The dashboard supplies the launch details for its own machine.
The agent's setup guide explains how to use those details remotely.

## Keep your setup current

The dashboard builds connection details from the current installation and
discovers the Skills included with that version. Revisit the connection
message after moving an installation. Download the current Skill bundle when
you update Oneiros, or rerun the repository installation to select newly
available Skills. Existing agent sessions may need to reload.

The `qbyx-oneiros` MCP identifier is the stable connection name. Each Skill
uses live tools and workflow information to guide production. Changes to the
MCP contract require compatibility review and a matching Skill release.

## Scope and release status

These Skills are written specifically for the Qbyx Oneiros MCP. The Oneiros
application provides the execution engine and manages your production state.
An application installer and model setup are separate parts of getting ready.
The public Windows installer is currently in development.

## Maintainer

[sean-cypher](https://github.com/sean-cypher) maintains Qbyx Oneiros Skills
under [Qbyx Studio](https://github.com/qbyx-studio).
