# crptochat — cliente

Binários do cliente de terminal do crptochat. **Este repositório não contém o código-fonte do aplicativo.**

O crptochat é um chat de terminal com criptografia ponta a ponta, servidor cego e transferência de arquivos P2P. As chaves nascem e ficam no seu computador (ou num pendrive).

## Baixar

Abra a [página de Releases](https://github.com/diegobnx/crptochat-client/releases/latest) e baixe o arquivo da sua plataforma:

| Arquivo | Plataforma |
|---|---|
| `crptochat-linux-amd64` | Linux 64 bits (Intel/AMD) |
| `crptochat-linux-arm64` | Linux 64 bits (ARM) |
| `crptochat-macos-arm64` | macOS Apple Silicon (M1 e posteriores) |
| `crptochat-macos-amd64` | macOS Intel |
| `crptochat-windows-amd64.exe` | Windows 64 bits |

A primeira publicação pode ter só o Linux amd64; as outras plataformas entram quando o build automático estiver ligado.

Se quiser conferir o arquivo:

```bash
sha256sum -c SHA256SUMS
```

## Instalar

### Linux e macOS

```bash
chmod +x crptochat-linux-amd64
mkdir -p ~/.local/bin
mv crptochat-linux-amd64 ~/.local/bin/crptochat
```

Use o nome do arquivo que você baixou. No macOS, na primeira execução o sistema pode pedir permissão em Ajustes → Privacidade e segurança.

### Windows

Baixe o `.exe` e rode pelo **Windows Terminal**. O SmartScreen pode avisar porque o executável não é assinado; se você baixou deste repositório, pode seguir.

Não é preciso instalar Python.

## Conectar

Quem administra o servidor te passa:

1. o endereço (`host` ou `host:porta`; a porta padrão é `7777`);
2. de preferência, a fingerprint SHA-256 do certificado TLS.

```bash
crptochat host.exemplo:7777
# recomendado, já conferindo o certificado:
crptochat host.exemplo:7777 --pin AABBCCDD...
```

Na primeira vez o cliente pede um nickname e uma senha, e cria uma chave em `~/.config/crptochat/identities/<nick>.json` (no Windows, `C:\Users\<você>\.config\crptochat\identities\`). **Faça backup desse arquivo**: se perder a chave ou a senha, aquele nick não pode ser recuperado.

O servidor usa TLS com certificado autoassinado. Na primeira conexão o cliente fixa a fingerprint (como o SSH). Confira com o operador. Se o certificado mudar de verdade, use `--reset-pin`.

Outras opções: `crptochat --help`. Destaques: `-n nick`, `-j '#canal'`, `--key-dir` para guardar a chave num pendrive, `--reg-token` se o servidor exigir token para registrar nick novo.

## Mensagens de voz (opcional)

Para gravar e ouvir áudio com qualidade melhor, instale o `ffmpeg`. Sem ele, a voz mascarada não é enviada.

## O que este pacote não esconde

O binário é gerado com PyInstaller. O código-fonte `.py` não está neste repositório e não aparece em texto claro no arquivo, mas o bytecode Python ainda vai dentro do pacote e **pode ser extraído e descompilado**. Isso serve para distribuir o cliente sem publicar o repositório da aplicação; não trate o binário como segredo nem como proteção forte contra engenharia reversa.

## Licença

MIT. Veja `LICENSE`.
