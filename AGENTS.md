# Agent Instructions

## JurisHUB CLI

Use the official JurisHUB CLI when this project needs JurisHUB data.

Source repository: https://github.com/Sinapta-Solutions/jurishub-cli

## Setup

| Step | Action |
| --- | --- |
| 1 | Install or load `skills/jurishub-cli/SKILL.md` from the source repository if your environment supports skills. |
| 2 | Install the CLI with `npm i -g @jurishub/cli`. |
| 3 | Ask the user to authenticate locally with `jurishub login`. |
| 4 | Wait for the user to confirm login, then run `jurishub status`. |

## Operating Rules

- Use `skills/jurishub-cli/SKILL.md` for command details.
- Do not request, print, log, store, commit, or screenshot the API key.
- Do not pass the API key as a command argument.
- Treat CLI output as client data.
- Prefer JSON for automation; use `--human` only for user-facing output.

## References

| Need | File |
| --- | --- |
| Customer setup | `README.md` in the source repository |
| Command details | `skills/jurishub-cli/SKILL.md` in the source repository |
| Security handling | `SECURITY.md` in the source repository |
