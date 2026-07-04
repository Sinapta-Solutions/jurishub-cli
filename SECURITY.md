# Security

The JurisHUB CLI authenticates with an organization API key managed in JurisHUB.

## API Key Handling

- Authenticate with `jurishub login`.
- The user enters the key locally; agents should not receive it in chat.
- Do not print, log, store, commit, screenshot, or paste API keys into prompts.
- Do not pass the key as a command argument.
- If a key may be exposed, ask the user to revoke it in JurisHUB and create a new one.

## Client Data

- Treat CLI output as client data.
- Do not publish client data, command output, screenshots, or private payloads in public issues or logs.
- Share only the minimum excerpt needed for support, with sensitive values removed.

## Reporting

Report security issues through your organization's JurisHUB support channel.
