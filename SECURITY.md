# Política de segurança

## Reporte privado

Não abra issue pública com chaves de API, dados de clientes, credenciais, payloads ou detalhes sensíveis de reprodução.

Reporte vulnerabilidades pelo canal autenticado de suporte do JurisHUB. Envie somente:

- versão retornada por `jurishub version`;
- sistema operacional e arquitetura;
- comando ou recurso afetado;
- passos de reprodução sanitizados;
- erro sanitizado e horário aproximado.

Nunca anexe o arquivo local de credenciais. Se uma chave puder ter sido exposta, revogue-a imediatamente no JurisHUB e crie outra com o menor conjunto de escopos e a menor validade necessários.

## Versão suportada

Correções de segurança têm como alvo a versão estável mais recente da CLI. Atualize antes de reportar um comportamento já corrigido em versão posterior.

## Discussões públicas

Problemas gerais de uso podem ser discutidos publicamente somente quando não contiverem segredos ou dados de clientes. Em caso de dúvida, use primeiro o suporte privado.
