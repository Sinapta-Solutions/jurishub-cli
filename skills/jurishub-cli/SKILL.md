---
name: jurishub-cli
description: "JurisHUB CLI: install @jurishub/cli, authenticate safely, and read or change authorized contacts, cases, pipeline, agenda, team, OmniChat state, and agent configuration."
---

# JurisHUB CLI

Use this skill to operate the public JurisHUB CLI safely for a single authorized organization.

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

`jurishub login` prompts the user locally for the API key. The key is hidden while the user pastes or types it; that is expected. Never ask the user to paste the key into chat or an agent prompt. Done when `jurishub status` succeeds.

The CLI uses the official JurisHUB API by default. Do not ask the user for an API URL. Set `JURISHUB_BASE_URL` only when JurisHUB support explicitly provides an alternate host.

## Rules

- Never save, print, log, commit, or screenshot the API key.
- Never pass the API key as a command argument.
- Treat request bodies and CLI output as client data.
- Never bypass permissions, tenant isolation, rate limits, delinquency, or authorization errors.
- Before delete or merge, summarize the affected resource and obtain user confirmation unless that exact action was already authorized.
- Use `--agent` only for the exact authorized mutation, never as standing permission.
- Prefer `--dados @file.json` or `--dados -` for sensitive or large inputs.
- Prefer JSON for automation. Use `--human` only for user-facing output.
- Preserve the reported `Idempotency-Key` when retrying an interrupted write. Do not create a fresh duplicate mutation.
- Do not recreate intentionally unavailable operations through raw HTTP or another tool.

## Read Commands

```bash
jurishub status
jurishub contatos listar
jurishub contatos buscar "<name-or-phone>"
jurishub contatos ver <id>
jurishub contatos duplicados listar
jurishub casos listar
jurishub casos ver <id>
jurishub casos parados
jurishub casos etapas
jurishub pipeline colunas listar
jurishub agenda listar
jurishub agenda ver <id>
jurishub agenda tipos
jurishub agenda responsaveis
jurishub equipe listar
jurishub equipe departamentos
jurishub integracoes status
jurishub webhooks status
jurishub omnichat conversas
jurishub omnichat mensagens <conversation-id>
jurishub agentes config
jurishub relatorio
```

## Write Commands

Writes require the exact scope on the API key.

```bash
jurishub contatos criar --dados @contato.json
jurishub contatos atualizar <id> --dados @contato.json
jurishub casos criar --dados @caso.json
jurishub casos atualizar <id> --dados @caso.json
jurishub casos mover <id> --dados '{"stage_id":"<column-id>"}'
jurishub pipeline colunas criar --dados @coluna.json
jurishub pipeline colunas renomear <id> --dados @coluna.json
jurishub pipeline colunas reordenar --dados @ordem.json
jurishub pipeline clientes criar --dados @cliente.json
jurishub agenda criar --dados @evento.json
jurishub agenda atualizar <id> --dados @evento.json
jurishub agenda cancelar <id>
jurishub equipe convidar --dados @convite.json
jurishub equipe atualizar <id> --dados @membro.json
jurishub omnichat estado <conversation-id> --estado closed
jurishub omnichat marcar-lida <conversation-id>
jurishub agentes config-atualizar --dados @configuracao.json
```

## Guarded Destructive Commands

Run only after exact authorization. The CLI obtains the required preview and concurrency values automatically.

```bash
jurishub contatos excluir <id> --yes
jurishub contatos duplicados mesclar --dados @merge.json --yes
jurishub pipeline colunas remover <id> --yes
jurishub agenda excluir <id> --yes
jurishub equipe excluir <id> --yes
```

If an interrupted destructive request must be retried, reuse the `Idempotency-Key`, `Preview-Fingerprint`, and `If-Match` values reported by the first attempt. Never fetch a new preview silently.

## Recommended Flow

1. Run `jurishub status`.
2. Read the target resource before changing it.
3. Confirm the API key has the required scope.
4. Show the intended change to the user.
5. Obtain confirmation for destructive work.
6. Execute once and report the JSON result without exposing private data.

Done when the requested operation succeeds, or when you report the exact safe error without bypassing it.

## Out Of Scope

- Sending OmniChat messages, attachments, or media.
- Connecting or disconnecting integrations or WhatsApp instances.
- Reconciling webhooks or resending invitations.
- Pausing, resuming, or escalating agent sessions.
- Reading or changing billing, invoices, subscriptions, or checkout.
- Accessing another organization.
- Using MCP.
- Running scraping, fuzzing, load, or abuse tests.

## Common Errors

- Expired or revoked key: ask the user to create a new key in JurisHUB.
- Missing login: ask the user to run `jurishub login` locally and paste the key only in the terminal prompt. The key will not appear on screen.
- `ORGANIZATION_DELINQUENT`: ask the user to regularize the organization. Do not recommend rotating a still-valid key.
- Missing scope: report the required permission. Never try another route to bypass it.
- Write endpoint temporarily unavailable: do not retry in a loop. Preserve the idempotency data and wait for the JurisHUB API V2 rollout or support guidance.
- Empty result: confirm name, phone, date range, or filters before assuming an error.
