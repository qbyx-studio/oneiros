---
name: qbyx-oneiros
description: Product-qualified alias that routes Qbyx Oneiros requests to the canonical Oneiros Skill.
---

# Qbyx Oneiros alias

Use `$oneiros` for the current MCP workflow. The canonical MCP server ID is
`qbyx-oneiros`; no client-specific profile is required. When the connection is
missing, follow `$oneiros` and its `references/connect.md` contract using the
client's documented configuration paths.

This alias inherits `$oneiros` project isolation and later-user-turn
submission lock. It never selects project 1 or exposes project-wide asset history.
