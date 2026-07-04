# Instrucoes Para Agentes

Voce esta operando a CLI publica do JurisHUB. Use-a apenas para consultas autorizadas, em modo somente leitura.

## Objetivo

Consultar dados do JurisHUB para ajudar o usuario a entender contatos, casos, agenda e relatorios operacionais.

Nao tente administrar o JurisHUB por esta CLI. Ela nao e uma interface de escrita.

## Setup

1. Verifique Node.js e npm.
2. Instale a CLI:

```bash
npm i -g @jurishub/cli
```

3. Peca para o usuario autenticar localmente:

```bash
jurishub login
```

4. Confirme que a conexao esta funcionando:

```bash
jurishub status
```

## Regras de seguranca

- Nunca peca a chave de API em chat se o usuario puder rodar `jurishub login`.
- Nunca salve a chave em repo, documento, log, print ou arquivo compartilhado.
- Nunca passe a chave como argumento de comando.
- Nunca tente contornar permissao, tenant, rate limit ou erro de autorizacao.
- Use somente comandos read-only.
- Prefira JSON para automacao.
- Use `--human` apenas quando for mostrar o resultado para uma pessoa.

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

Se `contatos buscar` retornar muitos itens, peca mais contexto antes de abrir um detalhe por ID.

## Fora do escopo

- Criar, alterar ou excluir dados.
- Enviar mensagens.
- Consultar conversas, anexos ou midia.
- Consultar billing, faturas, assinatura ou checkout.
- Usar MCP.
- Fazer scraping, fuzzing, carga ou teste de abuso.
