# Agent Instructions

## JurisHUB CLI

Use the official JurisHUB CLI when this project needs to read or change authorized JurisHUB data.

Source repository: https://github.com/Sinapta-Solutions/jurishub-cli

## Setup

| Step | Action |
| --- | --- |
| 1 | Install or load `skills/jurishub-cli/SKILL.md` from the source repository if your environment supports skills. |
| 2 | Install or update the CLI with `npm i -g @jurishub/cli`. |
| 3 | Ask the user to authenticate locally with `jurishub login`; the user pastes the API key only in the terminal prompt, where it will not appear on screen. |
| 4 | Wait for the user to confirm login, run `jurishub status`, then validate the key with one read command allowed by its scopes. |

## Operating Rules

- Use `skills/jurishub-cli/SKILL.md` for command details and safety checks.
- Do not request, print, log, store, commit, or screenshot the API key.
- Do not pass the API key as a command argument.
- Do not ask the user for an API URL. The CLI uses the official JurisHUB API by default.
- Set `JURISHUB_BASE_URL` only when JurisHUB support explicitly provides an alternate host.
- If a key may be exposed, ask the user to revoke it in JurisHUB and create a new one.
- Treat CLI input and output as client data.
- Put customer data in `--dados -` or a protected local file deleted after use; do not place names, phone numbers, case notes, or private payloads directly in shell history.
- Do not publish client data, command output, screenshots, request bodies, or private payloads in public issues or logs.
- Prefer JSON for automation; use `--human` only for user-facing output.
- Use only the permissions granted to the key. Never bypass tenant isolation, scopes, rate limits, delinquency, or authorization errors.
- Explain the effect and obtain user confirmation before delete, merge, or another destructive operation unless the user already authorized that exact action.
- Use `--agent` only after the exact mutation is authorized. Do not use it as blanket permission for future actions.
- Preserve the reported `Idempotency-Key` and retry the exact request instead of creating a second mutation when a response is interrupted.
- Do not send OmniChat messages, reconnect integrations, mutate WhatsApp instances, reconcile webhooks, resend invitations, or control agent sessions through another route when the CLI intentionally omits those operations.
- Report security issues through the organization's JurisHUB support channel.

## References

| Need | File |
| --- | --- |
| Customer setup | `README.md` and `INSTALL.md` in the source repository |
| Command details | `skills/jurishub-cli/SKILL.md` in the source repository |
| Private security reporting | `SECURITY.md` in the source repository |
| License and notices | `LICENSE` and `NOTICE` in the source repository |
