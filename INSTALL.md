# Instalação da JurisHUB CLI

## Instalação recomendada

Use Node.js 18 ou mais recente:

```bash
npm i -g @jurishub/cli
jurishub version
```

O pacote instala o binário correto para sua plataforma e disponibiliza os comandos `jurishub` e `jurishub-pp-cli`.

## Primeiro acesso

```bash
jurishub login
jurishub status
```

Cole a chave apenas no prompt local do login. Ela não aparece enquanto você digita ou cola. Não envie a chave em chat, argumento de comando, issue, arquivo compartilhado ou print.

A CLI já usa a API oficial. Configure `JURISHUB_BASE_URL` somente quando o suporte do JurisHUB fornecer outro endereço.

## Dados de clientes

Prefira stdin para não gravar nomes, telefones e outros dados no histórico:

```bash
jurishub contatos criar --dados -
```

Cole o JSON e encerre com `Ctrl+D` no macOS/Linux ou `Ctrl+Z` seguido de Enter no Windows.

Também é possível usar `--dados @arquivo.json`. Mantenha o arquivo fora de pastas sincronizadas, restrinja o acesso ao seu usuário e apague-o imediatamente após o uso.

## Instalação manual pela GitHub Release

Use este caminho somente quando npm não estiver disponível. Baixe o arquivo da sua plataforma e `checksums.txt` da mesma versão em [Releases](https://github.com/Sinapta-Solutions/jurishub-cli/releases).

Não extraia nem execute o binário se o nome do arquivo não estiver em `checksums.txt` ou se os hashes forem diferentes.

### Windows PowerShell

```powershell
$archive = "jurishub-pp-cli_<version>_windows_amd64.zip"
$checksumLine = Get-Content .\checksums.txt | Where-Object { $_ -match "\s+$([regex]::Escape($archive))$" }
if (@($checksumLine).Count -ne 1) { throw "Arquivo não encontrado exatamente uma vez em checksums.txt" }
$expected = ($checksumLine -split '\s+')[0].ToLowerInvariant()
$actual = (Get-FileHash -Algorithm SHA256 -Path $archive).Hash.ToLowerInvariant()
if ($actual -ne $expected) { throw "Checksum SHA256 diferente" }
```

Depois da validação:

```powershell
Expand-Archive .\jurishub-pp-cli_<version>_windows_amd64.zip -DestinationPath "$env:LOCALAPPDATA\JurisHUB\CLI" -Force
```

### Linux

```bash
archive="jurishub-pp-cli_<version>_linux_amd64.tar.gz"
grep -F "  $archive" checksums.txt | sha256sum --check --strict -
```

### macOS

```bash
archive="jurishub-pp-cli_<version>_darwin_arm64.tar.gz"
expected="$(awk -v file="$archive" '$2 == file {print $1}' checksums.txt)"
actual="$(shasum -a 256 "$archive" | awk '{print $1}')"
test -n "$expected" && test "$actual" = "$expected"
```

No macOS ou Linux, extraia somente depois da validação:

```bash
mkdir -p ~/.local/bin
tar -xzf jurishub-pp-cli_<version>_<os>_<arch>.tar.gz
install -m 0755 jurishub-pp-cli ~/.local/bin/jurishub-pp-cli
```

## Atualização

```bash
npm update -g @jurishub/cli
jurishub version
jurishub status
```

## Remoção do acesso

```bash
jurishub auth logout
```

Depois, revogue a chave correspondente no JurisHUB.

## Problemas comuns

- `no credentials configured`: execute `jurishub login` novamente.
- `permission denied`: a chave não possui o escopo necessário; consulte a matriz na [skill](skills/jurishub-cli/SKILL.md#permission-matrix).
- `ORGANIZATION_DELINQUENT`: regularize a assinatura; uma chave ainda válida volta a funcionar após a reativação.
- `not found`: confirme se o ID pertence à organização autenticada.
- Bloqueio de rede ou CDN: fale com o suporte enviando somente comando, horário e erro sanitizado.

Para vulnerabilidades ou suspeita de chave exposta, siga [SECURITY.md](SECURITY.md).
