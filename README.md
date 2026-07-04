# JurisHUB CLI

Consulte dados do JurisHUB por terminal, com seguranca, em modo somente leitura.

Este repo e o link publico para clientes e agentes entenderem como instalar, autenticar e usar a CLI do JurisHUB sem acessar o repositorio principal do produto.

> Status: piloto controlado. A instalacao por npm depende da publicacao do pacote `@jurishub/cli` e da release binaria correspondente.

## Para que serve

A CLI foi feita para agentes, automacoes e times operacionais que precisam consultar informacoes do JurisHUB sem navegar pela interface web.

Ela permite consultar:

- contatos;
- casos e pipeline;
- agenda;
- relatorios operacionais;
- diagnostico basico da conexao.

Ela nao cria, altera, exclui, envia mensagens nem acessa dados fora da organizacao autorizada pela chave.

## Instalacao

Quando o pacote estiver liberado:

```bash
npm i -g @jurishub/cli
```

Depois autentique neste computador:

```bash
jurishub login
jurishub status
```

O `login` pede a chave no terminal. Nao envie a chave em argumentos de comando, arquivos, prints ou prompts de agente.

## Primeiros comandos

```bash
jurishub status
jurishub contatos buscar "Maria"
jurishub contatos buscar "11999999999"
jurishub casos listar
jurishub agenda listar
jurishub relatorio
```

Para ver todos os comandos disponiveis:

```bash
jurishub --help
```

## Envie isto ao seu agente

Copie o texto abaixo para o agente que vai usar a CLI:

> Use a CLI oficial do JurisHUB. Instale com `npm i -g @jurishub/cli`, rode `jurishub status` e consulte apenas dados em modo read-only. Nunca peca, imprima ou salve a chave de API. Se precisar autenticar, peca para o usuario executar `jurishub login` localmente.

Instrucoes especificas para agentes ficam em [AGENTS.md](AGENTS.md).

## Escopo do piloto

- Somente leitura.
- Sem comandos de escrita.
- Sem OmniChat.
- Sem billing ou financeiro.
- Sem MCP.
- Saida JSON por padrao; use `--human` para leitura humana.

## Problemas comuns

Se a chave expirar, for revogada ou retornar erro de autorizacao, gere uma nova chave em:

`JurisHUB > Configuracoes > Seguranca > Chaves da API publica`
