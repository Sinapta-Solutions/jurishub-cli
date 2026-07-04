---
name: jurishub-cli
description: "CLI JurisHUB publica: use para instalar @jurishub/cli, autenticar com jurishub login, rodar status e consultar contatos, casos, agenda ou relatorios sem expor chave de API."
---

# JurisHUB CLI

Use esta skill para operar a CLI publica do JurisHUB em modo somente leitura.

## Instalacao

```bash
npm i -g @jurishub/cli
jurishub login
jurishub status
```

Feito quando `jurishub status` retorna sucesso. Se o pacote npm ou a release ainda nao existir, pare e informe que a publicacao da CLI esta pendente.

## Regras

- Use somente comandos read-only.
- Nunca salve ou imprima a chave de API.
- Nunca passe a chave como argumento de comando.
- Nunca tente contornar permissao, tenant, rate limit ou erro de autorizacao.
- Prefira JSON para automacao.
- Use `--human` apenas para leitura humana.

## Comandos

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

Feito quando a resposta necessaria foi obtida em JSON ou quando voce informou um erro operacional claro. Se `contatos buscar` retornar muitos itens, peca mais contexto antes de abrir um detalhe por ID.

## Fora do escopo

- Criar, alterar ou excluir dados.
- Enviar mensagens.
- Consultar conversas, anexos ou midia.
- Consultar billing, faturas, assinatura ou checkout.
- Usar MCP.
- Fazer scraping, fuzzing, carga ou teste de abuso.

## Erros comuns

- Chave expirada ou revogada: peça ao usuario para gerar uma nova chave no JurisHUB.
- Falta de login: peça ao usuario para rodar `jurishub login`.
- Resultado vazio: confirme nome, telefone, periodo ou filtros antes de assumir erro.
