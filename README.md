# Nova Launcher

> A fast, feature-rich, offline Minecraft launcher built with Electron.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Electron](https://img.shields.io/badge/Electron-28-47848F?logo=electron)](https://electronjs.org)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs)](https://nodejs.org)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)

---

## Features

### Core Launch

- Offline / cracked mode — no Mojang account required
- All Minecraft versions — releases, snapshots, old alpha and beta
- Loader support — Vanilla, Fabric, Forge, OptiFine
- Fabric and Forge auto-install before first launch
- Java auto-management — downloads the correct Adoptium/Eclipse Temurin JRE (Java 8, 17, or 21)
- Stop game button — kill the running game at any time

### Profiles

- Multiple profiles with fully separate game directories
- Per-profile RAM, version, loader, resolution, fullscreen, and custom Java path
- Recently played quick-launch cards on the home screen
- Play count and last played time tracked per profile

### Mods

- Per-profile mod manager — add, remove, enable and disable `.jar` files
- Drag and drop `.jar` files directly into the launcher
- Mod update checker — compares mods against Modrinth via SHA-512 hashes, one-click Update All
- Mod conflict detector — checks Modrinth for known incompatible mod pairs

### Browse (Modrinth)

- Search and install mods directly from Modrinth, filtered by MC version and loader
- Search and install modpacks from Modrinth
- Modpack import and export as `.zip`

### Worlds

- World manager with binary NBT parsing — shows name, game mode, seed, last played
- One-click world backup to ZIP and world deletion

### Assets

- **Resource Packs** — installed list with enable/disable, plus Modrinth browser
- **Shader Packs** — installed list, plus Modrinth browser (OptiFine / Iris)

### Import from Other Launchers

- Auto-detects installed launchers: Official, TLauncher, Prism, MultiMC, CurseForge, GDLauncher, ATLauncher, Modrinth App
- Browse mods, resource packs, shader packs, and versions from each launcher's instances
- One-click import to any Nova Launcher profile (skips already existing files)

### Offline Mode

- Auto-detects internet connection on startup
- Falls back to cached version list when offline
- Manual toggle in Settings — force offline or online mode
- Internet-requiring features (Browse, Modrinth, update check) are automatically disabled offline
- Installed profiles, mods, worlds, and assets always accessible offline

### Screenshots

- Per-profile screenshot grid
- Full-screen lightbox viewer with keyboard navigation (← → ESC)

### Servers

- Saved server list with live Minecraft SLP ping
- Shows MOTD, player count, and server version

### About & Updates

- Dedicated About tab with version info and repo link
- In-app updater — detects new releases, downloads silently, installs without wizard
- Startup loading screen with progress bar

### Tools

- Crash log analyzer — identifies common causes on abnormal game exit
- RAM auto-suggest — recommends 50% of system RAM, capped at 8 GB
- Real-time console with color-coded log levels

---

## Installation

Download the latest release from the [Releases](https://github.com/Rosilon/Nova-launcher/releases) page.

| Platform | File                             |
| -------- | -------------------------------- |
| Windows  | `Nova-Launcher-Setup-x.x.x.exe`  |

**Windows:** run the `.exe` installer and follow the setup wizard.

> SmartScreen warning: click **More info → Run anyway**

---

## Building from Source

### Prerequisites

- [Node.js](https://nodejs.org) 18 or newer
- [Git](https://git-scm.com)

### Steps

```bash
# Clone the repository
git clone https://github.com/Rosilon/Nova-launcher.git
cd Nova-launcher

# Install dependencies
npm install

# Run in development mode
npm start

# Build Windows installer
npm run build:win
```

---

## Project Structure

```text
Nova-launcher/
├── main.js          ← Electron main process
├── preload.js       ← Context bridge
├── package.json
├── assets/
│   ├── icon.ico
│   ├── icon.png
│   └── icon.icns
└── renderer/
    ├── index.html   ← UI layout (13 tabs)
    ├── app.js       ← Frontend logic
    └── style.css    ← Dark green theme
```

---

## Tabs

| Tab | Description |
| --- | ----------- |
| Home | Profile selector, loader, version, Play/Stop, recently played, console |
| Profiles | Create, edit, delete and launch profiles |
| Versions | Browse all Minecraft versions |
| Java | Adoptium JRE status and download |
| Mods | Mod manager, update checker, conflict detector |
| Browse | Modrinth mod and modpack browser |
| Screenshots | Per-profile screenshot grid with lightbox |
| Servers | Server list with live SLP ping |
| Worlds | World cards with NBT metadata, backup, delete |
| Assets | Resource pack and shader pack manager with Modrinth browser |
| Import | Import from other launchers (Official, TLauncher, Prism, etc.) |
| About | Version info, in-app updater |
| Settings | Username, RAM, resolution, Java path, offline mode |

---

## Data Locations

All data stored under `~/.nova-launcher/`:

| Path                  | Contents                      |
| --------------------- | ----------------------------- |
| `settings.json`       | Global settings               |
| `profiles.json`       | Profile definitions           |
| `servers.json`        | Saved server list             |
| `versions-cache.json` | Offline version list cache    |
| `minecraft/`          | Default game directory        |
| `instances/<id>/`     | Per-profile game directories  |
| `java/`               | Adoptium JRE downloads        |
| `world-backups/`      | World ZIP backups             |

---

## Tech Stack

| Technology | Purpose |
| ---------- | ------- |
| [Electron 28](https://electronjs.org) | Desktop app shell |
| [minecraft-launcher-core](https://github.com/Pierce01/MinecraftLauncher-core) | Game launch engine |
| [Adoptium / Eclipse Temurin](https://adoptium.net) | Auto-managed JRE |
| [Modrinth API v2](https://docs.modrinth.com) | Mods, modpacks, resource packs, shaders |
| Node.js `net` module | Minecraft SLP server ping |
| Node.js `zlib` | Binary NBT level.dat parsing |
| [archiver](https://www.npmjs.com/package/archiver) | World and modpack ZIP exports |

---

## Contributing

Pull requests are welcome. For major changes please open an issue first.

1. Fork the repository
2. Create a branch: `git checkout -b feature/my-feature`
3. Commit: `git commit -m "Add my feature"`
4. Push: `git push origin feature/my-feature`
5. Open a Pull Request

---

## License

MIT — see [LICENSE](LICENSE) for details.

---

## Disclaimer

Nova Launcher is an unofficial third-party launcher and is not affiliated with or endorsed by Mojang Studios or Microsoft. Minecraft is a trademark of Mojang Studios.
