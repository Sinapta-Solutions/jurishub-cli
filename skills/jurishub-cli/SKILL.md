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

`jurishub login` prompts the user locally for the API key. The key is hidden while the user pastes or types it; that is expected. Never ask the user to paste the key into chat or an agent prompt. `jurishub status` checks local configuration and API reachability; validate the key end to end with one read command allowed by its scopes.

The CLI uses the official JurisHUB API by default. Do not ask the user for an API URL. Set `JURISHUB_BASE_URL` only when JurisHUB support explicitly provides an alternate host.

## Rules

- Never save, print, log, commit, or screenshot the API key.
- Never pass the API key as a command argument.
- Treat request bodies and CLI output as client data.
- Never bypass permissions, tenant isolation, rate limits, delinquency, or authorization errors.
- Before delete or merge, summarize the affected resource and obtain user confirmation unless that exact action was already authorized.
- Use `--agent` only for the exact authorized mutation, never as standing permission.
- Prefer `--dados @file.json` or `--dados -` for sensitive or large inputs.
- Delete protected local input files after use. Never put names, phone numbers, case notes, or private payloads directly in shell history.
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
jurishub contatos duplicados prever --telefone <telefone>
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
jurishub relatorio funil
jurishub relatorio receita
jurishub relatorio fontes
```

## Write Commands

Writes require the exact scope on the API key.

```bash
jurishub contatos criar --dados @contato.json
jurishub contatos atualizar <id> --dados @contato.json
jurishub casos criar --dados @caso.json
jurishub casos atualizar <id> --dados @caso.json
jurishub casos mover <id> --dados @movimentacao.json
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

## Permission Matrix

| Commands | Required scope(s) | Destructive | Special lifetime |
| --- | --- | --- | --- |
| `status` | No API scope; checks local configuration and API reachability | No | Not applicable |
| `contatos listar`, `buscar`, `ver`, `duplicados listar`, `duplicados prever` | `contacts:read` | No | Read-only: up to 180 days |
| `casos listar`, `ver`, `etapas` | `cases:read` | No | Read-only: up to 180 days |
| `casos parados` | `analytics:read` | No | Read-only: up to 180 days |
| `pipeline colunas listar` | Any one of `cases:write`, `pipeline:cards:create`, `pipeline:columns:write`, `pipeline:columns:update`, `pipeline:columns:delete` | No | Follows the selected write scope |
| `agenda listar`, `ver`, `tipos`, `responsaveis` | `agenda:read` | No | Read-only: up to 180 days |
| `equipe listar`, `departamentos` | `team:members:read` | No | Optional read: up to 180 days |
| `integracoes status` | `integrations:read` | No | Optional read: up to 180 days |
| `webhooks status` | `webhooks:read` | No | Optional read: up to 180 days |
| `omnichat conversas`, `mensagens` | `omnichat:read` | No | Optional read: up to 180 days |
| `agentes config` | `agents:read` | No | Read-only: up to 180 days |
| `relatorio`, `relatorio funil` | `dashboard:read` | No | Read-only: up to 180 days |
| `relatorio receita`, `relatorio fontes` | `analytics:read` | No | Read-only: up to 180 days |
| `contatos criar`, `atualizar` | `contacts:write` | No | Ordinary write: up to 30 days |
| `casos criar`, `atualizar`, `mover` | `cases:write` | No | Ordinary write: up to 30 days |
| `pipeline colunas criar` | `pipeline:columns:write` | No | Ordinary write: up to 30 days |
| `pipeline colunas renomear`, `reordenar` | `pipeline:columns:update` | No | Ordinary write: up to 30 days |
| `pipeline clientes criar` | `contacts:write` and `pipeline:cards:create` | No | Ordinary write: up to 30 days |
| `agenda criar`, `atualizar`, `cancelar` | `agenda:write` | No | Ordinary write: up to 30 days |
| `equipe convidar` | `team:members:invite` | No | Ordinary write: up to 30 days |
| `equipe atualizar` | `team:members:write` | No | Ordinary write: up to 30 days |
| `omnichat estado`, `marcar-lida` | `omnichat:write` | No | Ordinary write: up to 30 days |
| `agentes config-atualizar` | `agents:config:write` | No | Ordinary write: up to 30 days |
| `contatos excluir` | `contacts:delete` only | Yes | Exclusive key: up to 24 hours |
| `contatos duplicados mesclar` | `contacts:merge` only | Yes | Exclusive key: up to 24 hours |
| `pipeline colunas remover` | `pipeline:columns:delete` only | Yes | Exclusive key: up to 24 hours |
| `agenda excluir` | `agenda:delete` only | Yes | Exclusive key: up to 24 hours |
| `equipe excluir` | `team:members:delete` only | Yes | Exclusive key: up to 24 hours |

The default read-only key includes `contacts:read`, `cases:read`, `agenda:read`, `dashboard:read`, `analytics:read`, `agents:read`, and `organization:read`. Optional read scopes must be selected explicitly. Only an organization owner can issue write scopes. Privileged destructive scopes cannot be combined with another scope. An organization can have at most two active API keys.

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
