# Instrucoes Para Agentes

Use a CLI do JurisHUB apenas para consultas read-only autorizadas pelo usuario.

## Setup

1. Verifique Node.js e npm.
2. Instale:

```bash
npm i -g @jurishub/cli
```

3. Peca para o usuario autenticar localmente:

```bash
jurishub login
```

4. Rode o diagnostico:

```bash
jurishub status
```

## Regras

- Nunca solicite a chave de API em chat se o usuario puder rodar `jurishub login`.
- Nunca salve a chave em repo, documento, log, print ou arquivo compartilhado.
- Nunca passe a chave como argumento de comando.
- Use somente comandos read-only.
- Prefira JSON para automacao.
- Use `--human` apenas para mostrar resultado para uma pessoa.

## Comandos permitidos

```bash
jurishub status
jurishub contatos listar
jurishub contatos buscar "<nome-ou-telefone>"
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

## Fluxo recomendado

```bash
jurishub status
jurishub contatos buscar "Nome do cliente"
jurishub casos listar
jurishub agenda listar
jurishub relatorio
```

Se `contatos buscar` retornar muitos itens, peca ao usuario mais contexto antes de abrir um detalhe por ID.

## Fora do escopo

- Criar, alterar ou excluir dados.
- Enviar mensagens.
- Consultar conversas, anexos ou midia.
- Consultar billing, faturas, assinatura ou checkout.
- Usar MCP.
- Tentar contornar permissao, tenant ou rate limit.
