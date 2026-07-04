# JurisHUB CLI

Consulte dados do JurisHUB pelo terminal, com segurança e em modo somente leitura.

Este repositório é o ponto público de orientação para clientes e agentes que precisam instalar e usar a CLI do JurisHUB. Ele não contém o código-fonte do produto, chaves de API ou dados de clientes.

> Status: piloto controlado. A instalação por `npm i -g @jurishub/cli` depende da publicação do pacote no npm e da release binária correspondente.

## O que é

A CLI do JurisHUB permite consultar informações operacionais sem abrir a interface web. Ela foi pensada para agentes de IA, automações e equipes que precisam buscar dados do JurisHUB de forma simples, previsível e segura.

## O que ela consulta

- Contatos.
- Casos e pipeline.
- Agenda.
- Relatórios operacionais.
- Diagnóstico básico da conexão.

## O que ela não faz

- Não cria, altera ou exclui dados.
- Não envia mensagens.
- Não acessa OmniChat.
- Não acessa billing, faturas, assinaturas ou dados financeiros.
- Não usa MCP.
- Não acessa dados de outra organização.

## Instalação

Quando o pacote estiver liberado:

```bash
npm i -g @jurishub/cli
```

Depois, autentique este computador:

```bash
jurishub login
jurishub status
```

O comando `jurishub login` pede a chave no terminal. Não envie a chave em argumentos de comando, arquivos, prints, issues públicas ou prompts de agente.

## Primeiros comandos

```bash
jurishub status
jurishub contatos buscar "Maria"
jurishub contatos buscar "11999999999"
jurishub casos listar
jurishub agenda listar
jurishub relatorio
```

Para ver todos os comandos disponíveis:

```bash
jurishub --help
```

## Como enviar isto a um agente

Copie o texto abaixo para o agente que vai usar a CLI:

> Use a CLI oficial do JurisHUB. Instale com `npm i -g @jurishub/cli`, rode `jurishub status` e consulte apenas dados em modo somente leitura. Nunca peça, imprima ou salve a chave de API. Se precisar autenticar, peça para o usuário executar `jurishub login` localmente.

Instruções específicas para agentes ficam em [AGENTS.md](AGENTS.md). Se o seu agente suporta skills, use também [skills/jurishub-cli/SKILL.md](skills/jurishub-cli/SKILL.md).

## Segurança da chave

A chave de API pertence à organização do cliente. O valor bruto aparece uma única vez no JurisHUB, durante a criação.

Use a chave apenas pelo fluxo:

```bash
jurishub login
```

Se houver suspeita de vazamento, revogue a chave no JurisHUB e gere outra.

## Problemas comuns

Se a chave expirar, for revogada ou retornar erro de autorização, gere uma nova chave em:

`JurisHUB > Configurações > Segurança > Chaves da API pública`
