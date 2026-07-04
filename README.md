# JurisHUB CLI

Consulte contatos, casos, agenda e relatórios do JurisHUB direto pelo terminal.

Este é o repositório oficial de instalação e uso da CLI pública do JurisHUB. Ele foi feito para clientes, equipes operacionais e agentes de IA que precisam consultar informações do JurisHUB com rapidez, segurança e saída fácil de automatizar.

## Instalação

```bash
npm i -g @jurishub/cli
```

Conecte este computador à sua organização:

```bash
jurishub login
```

Confira se está tudo certo:

```bash
jurishub status
```

O login pede a chave de API no terminal. Não envie a chave por chat, prompt de agente, argumento de comando, print, issue pública ou arquivo compartilhado.

## Primeiros comandos

```bash
jurishub contatos buscar "Maria"
jurishub contatos buscar "11999999999"
jurishub casos listar
jurishub casos parados
jurishub agenda listar
jurishub relatorio
```

Para ver a lista completa:

```bash
jurishub --help
```

## O que você consegue consultar

- Contatos.
- Casos e pipeline.
- Agenda.
- Relatórios operacionais.
- Diagnóstico da conexão.

## O que a CLI não faz

- Não cria, altera ou exclui dados.
- Não envia mensagens.
- Não acessa conversas, anexos ou mídia do OmniChat.
- Não acessa billing, faturas, assinaturas ou checkout.
- Não acessa dados de outra organização.

## Para usar com um agente

Envie este repositório ao agente e use a instrução abaixo:

> Use a CLI oficial do JurisHUB. Instale com `npm i -g @jurishub/cli`, rode `jurishub status` e consulte apenas dados em modo somente leitura. Nunca peça, imprima ou salve a chave de API. Se precisar autenticar, peça para o usuário executar `jurishub login` localmente.

Instruções específicas para agentes ficam em [AGENTS.md](AGENTS.md). Se o seu agente suporta skills, use também [skills/jurishub-cli/SKILL.md](skills/jurishub-cli/SKILL.md).

## Segurança da chave

A chave de API pertence à organização do cliente. O valor completo aparece uma única vez no JurisHUB, durante a criação.

Use a chave pelo fluxo seguro:

```bash
jurishub login
```

Se houver suspeita de vazamento, revogue a chave no JurisHUB e gere outra.

## Problemas comuns

Se a chave expirar, for revogada ou retornar erro de autorização, gere uma nova chave em:

`JurisHUB > Configurações > Segurança > Chaves da API pública`
