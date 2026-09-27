# colmeia-apt

Repositório APT oficial da **Colmeia Linux**, a distribuição do grupo de extensão
[Colmeia](https://colmeiaudesc.github.io/) da UDESC.

Daqui vêm as atualizações dos pacotes próprios da Colmeia. Quem instalou a Colmeia
já usa este repositório e recebe as novidades com `sudo apt update && sudo apt upgrade`
ou pelo Discover. **Não é preciso fazer nada.**

Endereço: `https://colmeiaudesc.github.io/colmeia-apt/`

## Pacotes

| Pacote | O que é |
| --- | --- |
| `colmeia-base` | identidade do sistema (nome, versão, repositórios) |
| `colmeia-artwork` | logos, papéis de parede, cores, telas de boot e login |
| `colmeia-desktop` | painel e menu no estilo do Windows 11, Boas-vindas e configurações padrão |
| `libplasma6`, `libplasmaquick6`, `plasma-desktoptheme` | libplasma do Debian recompilada com os ajustes da Colmeia |

Todos são para Debian 13 (trixie), `amd64`.

## Assinatura

Os índices são assinados com a chave da Colmeia. Confira a impressão digital:

```
Colmeia Linux (repositório APT) <colmeiacct@gmail.com>
90E8 6E1B ECCC 1581 7242  F5F6 4769 07E4 45CF 5103
```

A chave pública está em [`colmeia-archive-keyring.asc`](colmeia-archive-keyring.asc).

## Usar em outro Debian 13 (opcional)

```sh
curl -fsSL https://colmeiaudesc.github.io/colmeia-apt/colmeia-archive-keyring.asc \
    | sudo gpg --dearmor -o /usr/share/keyrings/colmeia-archive-keyring.gpg
gpg --show-keys /usr/share/keyrings/colmeia-archive-keyring.gpg   # confira a impressão digital acima

sudo tee /etc/apt/sources.list.d/colmeia.sources >/dev/null <<'EOF'
Types: deb
URIs: https://colmeiaudesc.github.io/colmeia-apt/
Suites: trixie
Components: main
Signed-By: /usr/share/keyrings/colmeia-archive-keyring.gpg
EOF

sudo apt update
sudo apt install colmeia-desktop
```

Os pacotes mudam a identidade e a área de trabalho do sistema. Instale num
Debian de testes ou numa máquina virtual.

## Para quem mantém

**Não edite os arquivos deste repositório à mão.** Tudo em `dists/` e `pool/` é
gerado e assinado pelo script `scripts/publicar-repo.sh` do projeto
[colmeia-linux](https://github.com/ColmeiaUDESC/colmeia-linux). Qualquer mudança
manual quebra a assinatura e o `apt` recusa o repositório.

Passo a passo em `docs/PACOTES-E-REPOSITORIO.md` do colmeia-linux. Resumo:

1. Aumente a versão em `pacotes/VERSAO` (nunca republique a mesma versão com conteúdo diferente).
2. Na máquina de build: `bash scripts/publicar-repo.sh ~/colmeia-apt` (pede a senha da chave).
3. Faça commit e push de `dists/`, `pool/` e `.gitattributes`.

O `.gitattributes` impede o Git de mudar o fim de linha dos arquivos, o que invalidaria a assinatura.

Problemas: [issues do colmeia-linux](https://github.com/ColmeiaUDESC/colmeia-linux/issues) ou colmeiacct@gmail.com.
