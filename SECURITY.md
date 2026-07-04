# Seguranca

A CLI do JurisHUB usa uma chave de API da organizacao para consultas read-only.

## Chaves de API

- A chave pertence a organizacao do cliente.
- O valor bruto da chave aparece uma unica vez na criacao.
- A chave deve ficar apenas no ambiente local autorizado.
- A chave nunca deve ser enviada em chat, issue publica, prompt de agente, print ou arquivo versionado.
- Se houver suspeita de vazamento, revogue a chave no JurisHUB e gere outra.

## Para agentes

Se precisar autenticar, peca para o usuario executar:

```bash
jurishub login
```

Nao solicite a chave diretamente, a menos que o usuario tenha escolhido explicitamente esse fluxo e aceite o risco.

## Reporte

Reporte problemas de seguranca pelo canal de suporte JurisHUB usado pela sua organizacao.

Nao publique chaves, dados de clientes, prints com informacao sensivel ou payloads privados em issues publicas.
