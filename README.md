# JurisHUB CLI

Consulte e administre contatos, casos, pipeline, agenda e equipe do JurisHUB direto pelo terminal.

Este é o repositório oficial de instalação e uso da CLI pública do JurisHUB. Ele foi feito para clientes, equipes operacionais e agentes de IA que precisam trabalhar com informações do JurisHUB com rapidez, segurança e saída fácil de automatizar.

Consulte também [instalação e verificação de checksum](INSTALL.md), [licença](LICENSE), [avisos legais](NOTICE) e [reporte privado de segurança](SECURITY.md).

## Copie e cole no seu agente

Na maioria dos casos, basta copiar o bloco abaixo e enviar ao agente que vai usar a CLI:

```text
Você vai preparar este projeto para usar a CLI oficial do JurisHUB.

Use este repositório como fonte:
https://github.com/Sinapta-Solutions/jurishub-cli

1. Instale ou carregue a skill pública, se o seu ambiente suportar skills:
   skills/jurishub-cli/SKILL.md

2. Adicione a seção JurisHUB CLI de AGENTS.md ao AGENTS.md do projeto, ou ao arquivo equivalente de instruções do agente.

3. Instale ou atualize a CLI:
   npm i -g @jurishub/cli

4. Depois da instalação, peça para eu autenticar este computador:
   jurishub login

5. Quando o prompt local aparecer, eu colo a chave de API no meu terminal.
   A chave não aparece enquanto eu colo ou digito; isso é normal.
   Aguarde eu confirmar que o login terminou. Só depois rode `jurishub status`
   e um comando de leitura permitido pela chave para validar o acesso de ponta a ponta.

6. Use a CLI para consultar ou alterar dados somente quando eu pedir.
   Antes de excluir ou mesclar algo, explique o efeito e peça minha confirmação.

7. Respeite as permissões da chave. Nunca tente contornar bloqueios, limites ou erros de autorização.

Nunca peça, imprima, registre ou salve minha chave de API.
```

Se o agente não conseguir instalar skills automaticamente, envie também o arquivo [skills/jurishub-cli/SKILL.md](skills/jurishub-cli/SKILL.md). As instruções curtas para colar no projeto ficam em [AGENTS.md](AGENTS.md).

## Instalação manual

```bash
npm i -g @jurishub/cli
jurishub version
```

A CLI já usa a API oficial do JurisHUB. Você não precisa configurar URL.

Conecte este computador à sua organização:

```bash
jurishub login
```

Quando o prompt aparecer, cole a chave de API no terminal e pressione Enter. Por segurança, a chave não aparece enquanto você cola ou digita.

Confira se está tudo certo:

```bash
jurishub status
```

Esse comando confirma configuração e alcance da API. Para validar a chave de ponta a ponta, execute também um comando de leitura permitido pelos escopos dela, como `jurishub contatos listar` em uma chave padrão de leitura.

O login pede a chave de API no terminal. Não envie a chave por chat, prompt de agente, argumento de comando, print, issue pública ou arquivo compartilhado.

Use `JURISHUB_BASE_URL` apenas se o suporte do JurisHUB orientar você a usar outro endereço.

## Primeiros comandos

```bash
jurishub contatos buscar "Maria"
jurishub casos listar
jurishub casos parados
jurishub pipeline colunas listar
jurishub agenda listar
jurishub equipe listar
jurishub relatorio
```

Para ver a lista completa:

```bash
jurishub --help
```

## O que você consegue fazer

| Área | Capacidades |
| --- | --- |
| Contatos | Listar, buscar, consultar, criar, atualizar e excluir com confirmação. |
| Duplicados | Detectar, conferir e mesclar contatos duplicados. |
| Casos | Listar, criar, atualizar e mover entre colunas. |
| Pipeline | Listar, criar, renomear, reordenar e remover colunas protegidas; criar cliente em uma coluna. |
| Agenda | Listar, criar, atualizar, cancelar e excluir eventos. |
| Equipe | Listar membros e departamentos, convidar, atualizar e excluir com confirmação. |
| Integrações e webhooks | Consultar o estado sem expor credenciais. |
| OmniChat | Consultar conversas e mensagens, abrir ou fechar conversa e marcar como lida. |
| Agentes | Consultar e atualizar somente a configuração segura permitida. |
| Relatórios | Consultar resumos operacionais, funil, receita e fontes. |

As ações disponíveis dependem das permissões escolhidas ao criar a chave. Uma chave de leitura não pode alterar dados.

## Exemplos de escrita

```bash
jurishub contatos criar --dados -
jurishub casos criar --dados @caso.json
jurishub casos mover <case-id> --dados @movimentacao.json
jurishub pipeline clientes criar --dados @cliente.json
jurishub agenda criar --dados @evento.json
jurishub agentes config-atualizar --dados @configuracao.json
```

Prefira `--dados -` para dados de clientes. Cole o JSON e encerre a entrada com `Ctrl+D` no macOS/Linux ou `Ctrl+Z` seguido de Enter no Windows. Assim, nomes, telefones e detalhes de casos não ficam no histórico do terminal.

Se usar `--dados @arquivo.json`, mantenha o arquivo fora de pastas sincronizadas, restrinja o acesso ao seu usuário e apague-o depois. Operações destrutivas exigem `--yes` e devem ser executadas somente após confirmação consciente do usuário.

## Permissões da chave

- Chaves somente de leitura podem durar até 180 dias.
- Chaves com escrita comum podem durar até 30 dias e só podem ser criadas pelo proprietário da organização.
- Exclusão de contato, mesclagem, exclusão de coluna, exclusão de evento e exclusão de membro exigem uma chave exclusiva para um único escopo, válida por no máximo 24 horas.
- Cada organização pode manter no máximo duas chaves ativas.

A tabela completa de comandos e escopos está em [skills/jurishub-cli/SKILL.md](skills/jurishub-cli/SKILL.md#permission-matrix).

## O que a CLI não faz

- Não envia mensagens pelo OmniChat.
- Não conecta ou desconecta integrações e instâncias WhatsApp.
- Não reconcilia webhooks.
- Não reenvia convites de equipe.
- Não pausa, retoma ou escala sessões de agentes.
- Não acessa billing, faturas, assinaturas ou checkout.
- Não acessa dados de outra organização.

## Segurança da chave

A chave de API pertence à organização do cliente. O valor completo aparece uma única vez no JurisHUB, durante a criação.

Use a chave pelo fluxo seguro:

```bash
jurishub login
```

Para automações, use `JURISHUB_API_KEY` nas configurações protegidas de segredo da plataforma. Nunca coloque a chave em argumentos, arquivos versionados ou prompts.

Se houver suspeita de vazamento, revogue a chave no JurisHUB e gere outra.

## Disponibilidade da versão 0.2.0

As consultas V1 continuam disponíveis durante o rollout. Os comandos de escrita dependem da API Pública V2 e podem ficar temporariamente indisponíveis enquanto a atualização chega a todos os ambientes. Não repita uma escrita em loop; preserve a `Idempotency-Key` informada pela CLI e aguarde a orientação do suporte.

## Problemas comuns

- Chave expirada ou revogada: gere uma nova chave em `JurisHUB > Configurações > Segurança > Chaves da API pública`.
- Organização inadimplente: regularize a assinatura; a mesma chave válida volta a funcionar após a reativação.
- Permissão insuficiente: crie uma chave com o escopo exato necessário. Não tente contornar o bloqueio.
- Escrita temporariamente indisponível: aguarde a conclusão do rollout da API V2 ou fale com o suporte do JurisHUB.

## Instalação por arquivo

Se npm não estiver disponível, baixe o arquivo da sua plataforma e `checksums.txt` na mesma GitHub Release. Siga a verificação SHA256 detalhada em [INSTALL.md](INSTALL.md) antes de extrair ou executar o binário.

## Segurança e licença

Não publique chaves, payloads ou dados de clientes em issues. Para vulnerabilidades ou suspeita de vazamento, siga [SECURITY.md](SECURITY.md).

Este projeto é distribuído sob a [Apache License 2.0](LICENSE). Consulte também [NOTICE](NOTICE).
