---
name: jurishub-cli
description: "JurisHUB CLI: use to install @jurishub/cli, authenticate with jurishub login, run status, and query contacts, cases, agenda items, or reports without exposing an API key."
---

# JurisHUB CLI

Use this skill to operate the public JurisHUB CLI.

## Project Setup

When onboarding a project from https://github.com/Sinapta-Solutions/jurishub-cli:

1. Install or load this skill from `skills/jurishub-cli/SKILL.md`.
2. Add the concise CLI instructions from `AGENTS.md` to the target project's agent-instructions file.

Done when future agent runs can find both the skill and the project instruction.

## Install

```bash
npm i -g @jurishub/cli
jurishub login
jurishub status
```

Done when `jurishub status` succeeds.

## Rules

- Never save or print the API key.
- Never pass the API key as a command argument.
- Never try to bypass permissions, tenant isolation, rate limits, or authorization errors.
- Prefer JSON for automation.
- Use `--human` only for human-readable output.

## Commands

```bash
jurishub status
jurishub contatos listar
jurishub contatos buscar "<name-or-phone>"
jurishub contatos ver <id>
jurishub casos listar
jurishub casos ver <id>
jurishub casos parados
jurishub casos etapas
jurishub agenda listar
jurishub agenda ver <id>
jurishub agenda tipos
jurishub relatorio
jurishub relatorio funil
jurishub relatorio receita
jurishub relatorio fontes
```

## Recommended Flow

```bash
jurishub status
jurishub contatos buscar "Client name"
jurishub casos listar
jurishub agenda listar
jurishub relatorio
```

Done when the needed response is obtained as JSON, or when you report a clear operational error. If `contatos buscar` returns many items, ask for more context before opening a detail by ID.

## Out Of Scope

- Creating, changing, or deleting data.
- Sending messages.
- Reading conversations, attachments, or media.
- Reading billing, invoices, subscriptions, or checkout data.
- Using MCP.
- Running scraping, fuzzing, load, or abuse tests.

## Common Errors

- Expired or revoked key: ask the user to create a new key in JurisHUB.
- Missing login: ask the user to run `jurishub login`.
- Empty result: confirm name, phone, date range, or filters before assuming an error.
