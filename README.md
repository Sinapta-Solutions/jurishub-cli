# JurisHUB CLI

Consulte contatos, casos, agenda e relatórios do JurisHUB direto pelo terminal.

Este é o repositório oficial de instalação e uso da CLI pública do JurisHUB. Ele foi feito para clientes, equipes operacionais e agentes de IA que precisam consultar informações do JurisHUB com rapidez, segurança e saída fácil de automatizar.

## Copie e cole no seu agente

Na maioria dos casos, basta copiar o bloco abaixo e enviar ao agente que vai usar a CLI:

```text
Você vai preparar este projeto para usar a CLI oficial do JurisHUB.

Use este repositório como fonte:
https://github.com/Sinapta-Solutions/jurishub-cli

1. Instale ou carregue a skill pública, se o seu ambiente suportar skills:
   skills/jurishub-cli/SKILL.md

2. Adicione a seção JurisHUB CLI de AGENTS.md ao AGENTS.md do projeto, ou ao arquivo equivalente de instruções do agente.

3. Instale a CLI:
   npm i -g @jurishub/cli

4. Depois da instalação, peça para eu autenticar este computador:
   jurishub login

5. Quando o prompt local aparecer, eu colo a chave de API no meu terminal.
   A chave não aparece enquanto eu colo ou digito; isso é normal.
   Aguarde eu confirmar que o login terminou. Só depois rode:
   jurishub status

6. Use a CLI para consultar contatos, casos, agenda e relatórios quando eu pedir.

Nunca peça, imprima, registre ou salve minha chave de API.
```

Se o agente não conseguir instalar skills automaticamente, envie também o arquivo [skills/jurishub-cli/SKILL.md](skills/jurishub-cli/SKILL.md). As instruções curtas para colar no projeto ficam em [AGENTS.md](AGENTS.md).

## Instalação manual

```bash
npm i -g @jurishub/cli
```

Conecte este computador à sua organização:

```bash
jurishub login
```

Quando o prompt aparecer, cole a chave de API no terminal e pressione Enter. Por segurança, a chave não aparece enquanto você cola ou digita.

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
