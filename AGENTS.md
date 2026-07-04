# Agent Instructions

## JurisHUB CLI

Use the official JurisHUB CLI when this project needs JurisHUB data.

Source repository: https://github.com/Sinapta-Solutions/jurishub-cli

## Setup

| Step | Action |
| --- | --- |
| 1 | Install or load `skills/jurishub-cli/SKILL.md` from the source repository if your environment supports skills. |
| 2 | Install the CLI with `npm i -g @jurishub/cli`. |
| 3 | Ask the user to authenticate locally with `jurishub login`; the user pastes the API key only in the terminal prompt, where it will not appear on screen. |
| 4 | Wait for the user to confirm login, then run `jurishub status`. |

## Operating Rules

- Use `skills/jurishub-cli/SKILL.md` for command details.
- Do not request, print, log, store, commit, or screenshot the API key.
- Do not pass the API key as a command argument.
- If a key may be exposed, ask the user to revoke it in JurisHUB and create a new one.
- Treat CLI output as client data.
- Do not publish client data, command output, screenshots, or private payloads in public issues or logs.
- Prefer JSON for automation; use `--human` only for user-facing output.
- Report security issues through the organization's JurisHUB support channel.

## References

| Need | File |
| --- | --- |
| Customer setup | `README.md` in the source repository |
| Command details | `skills/jurishub-cli/SKILL.md` in the source repository |
