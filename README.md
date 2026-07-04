# JurisHUB CLI

CLI oficial para consultar dados do JurisHUB pela API publica V1.

## Instalacao

```bash
npm i -g @jurishub/cli
```

Depois configure a chave de acesso:

```bash
jurishub login
jurishub status
```

O comando `login` pede a chave no terminal. Nao envie a chave em argumentos de comando, arquivos, prints ou prompts de agente.

## Comandos principais

```bash
jurishub status
jurishub contatos listar
jurishub contatos buscar "Maria"
jurishub contatos buscar "11999999999"
jurishub contatos ver <id>
jurishub casos listar
jurishub casos parados
jurishub agenda listar
jurishub relatorio
```

## Para enviar a um agente

Envie este repositorio e diga:

> Instale a CLI do JurisHUB com npm, rode `jurishub status` e consulte somente dados read-only. Nunca peça nem imprima a chave de API; se precisar autenticar, peça para o usuario executar `jurishub login` localmente.

Instrucoes detalhadas para agentes ficam em [AGENTS.md](AGENTS.md).

## Escopo do piloto

- Somente leitura.
- Sem comandos de escrita.
- Sem OmniChat.
- Sem billing/financeiro.
- Sem MCP.
- Saida JSON por padrao; use `--human` quando quiser leitura humana.

## Problemas

Se a chave expirar, for revogada ou retornar erro de autorizacao, crie uma nova chave em JurisHUB > Configuracoes > Seguranca > Chaves da API publica.
