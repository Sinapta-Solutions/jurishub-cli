# Security

The JurisHUB CLI uses an organization API key for authenticated queries.

## API Keys

- The key belongs to the client's organization.
- The full key value is shown only once when it is created.
- The key must stay only in the authorized local environment.
- The key must never be sent in chat, public issues, agent prompts, screenshots, or versioned files.
- If exposure is suspected, revoke the key in JurisHUB and create a new one.

## For Agents

If authentication is needed, ask the user to run:

```bash
jurishub login
```

Do not ask for the key directly unless the user explicitly chooses that flow and accepts the risk.

## Reporting

Report security issues through your organization's JurisHUB support channel.

Do not publish API keys, client data, sensitive screenshots, or private payloads in public issues.
