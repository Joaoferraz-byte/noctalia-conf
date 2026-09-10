# Plugins locais do Noctalia

Os plugins ativos do Noctalia são mantidos como fontes locais versionadas neste diretório. O Noctalia recebe somente links store-backed gerados pelo Home Manager; caches, settings e estado de execução permanecem em `$XDG_STATE_HOME/noctalia`. `auto_update = "none"` evita alterações de código no runtime.

| Plugin local | ID | Upstream auditado | API | Dependências principais | Integração |
| --- | --- | --- | ---: | --- | --- |
| `cat` | `dotnetrob/cat` | seleção anterior do projeto | 3 | fonte local existente | barra/painel existentes |
| `timer` | `noctalia/timer` | `noctalia-dev/official-plugins` em `8cb833c3e2502f57e49d34fa64386b4d66794b77` | 3 | nenhuma externa | barra/painel existentes |
| `screen_toolkit` | `alexander/screen-toolkit` | `noctalia-dev/community-plugins` em `f1b74c2b5cbd5d16983bfdf46a3752d0cd84ffb4` | 13 | `grim`, `slurp`, `tesseract`, `zbar`, `ffmpeg`, `satty`/`swappy`, `imagemagick`, `gpu-screen-recorder`, `wl-screenrec`, `wf-recorder` | painel, shortcut e widget da barra; owner único de captura e gravação |
| `gamer_mode` | `nomadcxx/gamer-mode` | `noctalia-dev/community-plugins` em `f1b74c2b5cbd5d16983bfdf46a3752d0cd84ffb4` | 19 | `pgrep`, `pkill`, `systemctl`; `powerprofilesctl` opcional por host | painel via `Mod+G`; sem widget na barra |
| `prismlauncher_instances` | `radimous/prismlauncher-instances` | `noctalia-dev/community-plugins` em `f1b74c2b5cbd5d16983bfdf46a3752d0cd84ffb4` | 3 | `flatpak` | provider `/pl` adaptado para FreeSM Flatpak |
| `bitwarden` | `noctalia/bitwarden` | `noctalia-dev/official-plugins` em `8cb833c3e2502f57e49d34fa64386b4d66794b77` | 8 | `bitwarden-cli` (`bw`) | provider `/bw`; login e unlock continuam interativos |

Os manifestos upstream declaram licença MIT. Os diretórios foram copiados após revisão de código e permanecem legíveis, sem download ou execução de código remoto pelo plugin. A atualização futura deve repetir a auditoria, copiar uma revisão explicitamente escolhida e registrar o novo commit neste arquivo.

## Política de screenshot

O atalho `Mod+Shift+S` usa a ação `annotate` do Screen Toolkit: `slurp` seleciona a região, `grim` captura e `satty`/`swappy` fornece a anotação, salvando em `screenshot-path`. `Mod+Shift+P` permanece como alias para abrir o painel; `Mod+K` é o atalho principal do popup. O widget da barra é `alexander/screen-toolkit:widget`; quando uma gravação está ativa, clicar nele envia `recordStop` ao mesmo serviço. Os utilitários necessários são instalados pelo módulo `nix-conf/modules/features/niri.nix`.

## Política de serviços

Gamer Mode é um painel acionado por atalho, sem ocupar a barra. Usa perfil `light` e preserva a política de energia do host: em `latitude`, TLP continua sendo o owner de energia; em `myMachine`, o power-profiles-daemon já existente pode fornecer `powerprofilesctl`.

Bitwarden usa o servidor local `bw serve` em loopback e não recebe credenciais por TOML ou argumentos. A primeira autenticação deve ser feita pelo painel `/bw` ou pela CLI, e o vault deve ser bloqueado quando não estiver em uso.

## Fontes

- https://docs.noctalia.dev/noctalia/plugins/
- https://noctalia.dev/plugins/community/screen-toolkit
- https://noctalia.dev/plugins/community/gamer-mode
- https://noctalia.dev/plugins/community/prismlauncher-instances
- https://noctalia.dev/plugins/official/bitwarden
- https://docs.noctalia.dev/noctalia/bar/widgets/screenshot/
- https://github.com/noctalia-dev/community-plugins/commit/f1b74c2b5cbd5d16983bfdf46a3752d0cd84ffb4
- https://github.com/noctalia-dev/official-plugins/commit/8cb833c3e2502f57e49d34fa64386b4d66794b77
