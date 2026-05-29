# dotfiles

Dotfiles managed with [chezmoi](https://www.chezmoi.io/).

## Fresh CachyOS Install

### 1. chezmoi installieren

```bash
sudo pacman -S --needed chezmoi
```

### 2. Dotfiles einrichten

chezmoi holt das Repo und fragt interaktiv, welche Komponenten installiert werden sollen:

```bash
chezmoi init --apply https://github.com/martinbartolome/dotfiles
```

Während `init` werden folgende Fragen gestellt (Enter = Standardwert):

| Frage | Standardwert | Beschreibung |
|---|---|---|
| Install general desktop apps | `true` | Brave Browser, etc. |
| Install gaming apps | `true` | Steam, Heroic |
| Install dev tools | `true` | VS Code || Install VS Code extensions & Copilot skills | `true` | Copilot, Copilot Chat, caveman skill || Install DisplayLink driver | `true` | Für DisplayLink-Docks/-Adapter |
| Install NVIDIA drivers | `true` | NVIDIA proprietary drivers |

### 3. Was passiert automatisch

chezmoi führt die Scripts in dieser Reihenfolge aus:

1. **`run_once_before_install-packages`** — installiert `base-devel`, `dkms`, `linux-cachyos-headers` und `yay`
2. **`run_onchange_after_install-desktop-apps-general`** — Brave Browser *(wenn `desktop = true`)*
3. **`run_onchange_after_install-desktop-apps-devtools`** — VS Code *(wenn `development = true`)*
5. **`run_onchange_after_install-copilot-skills`** — VS Code Extensions (Copilot, Copilot Chat) + [caveman](https://github.com/JuliusBrussee/caveman) skill *(wenn `copilot_skills = true`)*
6. **`run_onchange_after_install-desktop-apps-gaming`** — Steam, Heroic *(wenn `gaming = true`)*
7. **`run_onchange_after_install-displaylink`** — DisplayLink Treiber + Service *(wenn `displaylink = true`)*
8. **`run_onchange_after_install-nvidia`** — NVIDIA Treiber + GRUB DRM-Flag *(wenn `nvidia = true`)*

### 4. Nach der Installation

Bei NVIDIA-Treiber oder DisplayLink ist ein **Neustart erforderlich**:

```bash
reboot
```

### Konfiguration nachträglich ändern

Die Konfiguration liegt in `~/.config/chezmoi/chezmoi.toml`. Werte anpassen und dann:

```bash
chezmoi apply
```
