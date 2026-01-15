# Universal Installer Tool (UIT)

O **UIT** é um script shell wrapper que oferece uma interface visual (TUI - Text User Interface) para a instalação e extração dos formatos de pacotes mais comuns no ecossistema Linux.

Inspirado nos instaladores clássicos da NVIDIA e Debian, ele elimina a necessidade de decorar comandos de terminal para descompactar arquivos `.tar.gz`, `.xz`, `.zip`, converter `.rpm`s e instalar `.deb`s.

Desenvolvido após identificar a dificuldade de novos usuários do ecossistema Linux em gerenciar e instalar aplicações que fogem do padrão `apt` ou das lojas de apps nativas.

## Funcionalidades

- **Interface Visual Interativa:** Menus de seleção e caixas de diálogo baseadas em whiptail.

- **Detecção Automática:** Reconhece arquivos no diretório atual de acordo com a extensão selecionada.

- **Instalação Inteligente de RPM:** Detecta sua distribuição (Ubuntu, Fedora, OpenSUSE, etc.) e aplica a melhor estratégia: instalação nativa (`dnf`/`zypper`) ou conversão automática (`alien`) para sistemas Debian-based.

- **Suporte Multi-Formato:**

  - `.deb` (Instalação nativa via APT)
 
  - `.rpm` (Suporte nativo ou via conversão Alien)

  - `.tar.gz` e `.tar.xz` (Extração automática)

  - `.zip` (Descompactação)

  - `.AppImage` (Permissão de execução + Instalação)

- **Modo Híbrido:** Funciona tanto via menu gráfico quanto via linha de comando direta (ex: uit app.zip).

- **Pós-Instalação:** Opção para abrir o gerenciador de arquivos na pasta de destino automaticamente.

## Pré-requisitos

O script foi desenhado para Ubuntu/Debian e derivados. Ele verifica e tenta instalar automaticamente as dependências, mas requer:

- `bash`

- `sudo`

- `whiptail` (para a interface gráfica)

- `unzip`, `tar` (utilitários de arquivo)

- `alien` (opcional: instalado automaticamente em distros Debian/Ubuntu ao tentar usar `.rpm`)

## Instalação

Para usar o `uit` como um comando nativo do sistema (acessível de qualquer pasta):

1. Baixe o script e dê permissão de execução:
```bash
chmod +x universal_installer.sh.sh
```

2. Instale no sistema (renomeando para uit):

```bash
sudo cp universal_installer.sh /usr/local/bin/uit
```

3. Execute o comando `uit` em qualquer terminal.

## Como Usar

O UIT possui três modos principais de operação:

1. **Modo Interativo (Interface Gráfica)**

Basta digitar o comando sozinho. O script abrirá o menu azul para você navegar.
```bash
uit
# ou
uit -gui
```

2. **Modo Direto (Linha de Comando)**

Passe o arquivo que deseja instalar como argumento. O script pulará a seleção de arquivos e irá direto para a confirmação e escolha do destino.
```bash
# Instalar um pacote Debian
sudo uit discord.deb

# Instalar um pacote RPM (Conversão automática se estiver no Ubuntu)
sudo uit zoom.rpm

# Instalar um arquivo compactado
sudo uit site-backup.tar.gz
```

3. **Ajuda Rápida**

Exibe as instruções de uso no terminal sem abrir a interface gráfica.
```bash
uit -help
```

## Como Desinstalar Aplicativos

Como o UIT gerencia diferentes tipos de arquivos, a remoção varia:

- Arquivos `.deb`: Instalados via APT. Use o comando padrão do sistema: `sudo apt remove nome_do_pacote`

- Arquivos `.rpm`:

  - Se instalados nativamente (Fedora/OpenSUSE): `sudo dnf remove pacote` ou `sudo zypper remove pacote`.

  - Se convertidos via Alien (Ubuntu/Debian): O pacote foi instalado no sistema, então use `sudo apt remove nome_do_pacote`.

- Arquivos `.tar.gz`, `.zip`, `.xz`, `.AppImage`: Estes são instalados "manualmente" na pasta de destino que você escolheu (Padrão: `/opt`). Para desinstalar, basta remover a pasta.

*Exemplo:*
```bash
sudo rm -rf /opt/NomeDoApp
```

## Futuras Atualizações

Em um futuro próximo pretendo adicionar:

- Opções de desinstalação automatizada.

- Busca por pacotes instalados via UIT.

- Histórico de instalações.

- Um gerenciador de versões do próprio UIT, embutido na instalação.

## Contribuição

Sugestões e Pull Requests são bem-vindos! Sinta-se à vontade para adicionar suporte a novos formatos (como `.rpm` ou `.flatpakref`) ou melhorar a interface.
