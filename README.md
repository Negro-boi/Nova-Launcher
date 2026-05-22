# Nova Launcher

Nova Launcher is a feature-rich offline Minecraft launcher built with Electron. It is designed for fast local profile management, flexible modded gameplay, and a polished desktop experience without requiring an online Microsoft/Mojang login flow.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Electron](https://img.shields.io/badge/Electron-28-47848F?logo=electron)](https://www.electronjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs)](https://nodejs.org/)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)](#platform-support)

## Highlights

- Launch Vanilla, Fabric, Forge, and OptiFine profiles.
- Manage separate Minecraft instances with per-profile settings.
- Install and manage mods, resource packs, shader packs, and Modrinth content.
- Import assets and versions from other launchers.
- Browse worlds, screenshots, saved servers, logs, and launcher updates from one app.
- Auto-manage Java runtimes for modern and legacy Minecraft versions.
- Run in offline mode with cached version metadata and local profiles.
- Preview player skins with an integrated 3D skin viewer.

## Screenshots

Screenshots can be added here as the project evolves.

| Home | Profiles | Mods |
| --- | --- | --- |
| `docs/screenshots/home.png` | `docs/screenshots/profiles.png` | `docs/screenshots/mods.png` |

| Worlds | Assets | Settings |
| --- | --- | --- |
| `docs/screenshots/worlds.png` | `docs/screenshots/assets.png` | `docs/screenshots/settings.png` |

## Feature Overview

### Launching

- Offline username-based launch flow.
- Minecraft release, snapshot, old beta, and old alpha version browsing.
- Fabric and Forge loader version selection.
- OptiFine support through manual mod-folder installation.
- Real-time launch console with progress and debug messages.
- Stop button for canceling or terminating a running game process.

### Profiles

- Multiple local profiles.
- Per-profile Minecraft version, loader, RAM, resolution, fullscreen mode, Java path, and game directory.
- Recently played profile shortcuts.
- Profile play count and last-played tracking.

### Mods and Modrinth

- Add, remove, enable, disable, and drag-drop `.jar` mods.
- Search and install Modrinth mods directly from the launcher.
- Search and install Modrinth modpacks.
- Check installed mods for updates using Modrinth SHA-512 matching.
- Detect known Modrinth incompatibilities between installed mods.
- Import and export Nova modpack ZIP archives.

### Worlds, Assets, and Media

- World manager with `level.dat` metadata parsing.
- World backup, deletion, folder opening, and generated region overview maps.
- Screenshot gallery with lightbox navigation.
- Resource pack manager with enable/disable support.
- Shader pack manager.
- Modrinth resource pack and shader pack search/install flows.

### Java and System Tools

- Detect bundled and system Java installations.
- Download Adoptium/Eclipse Temurin JREs.
- Choose Java 8, 17, or 21 based on Minecraft version needs.
- Suggest RAM based on local system memory.
- Analyze crash reports after abnormal game exits.

### Import and Updates

- Detect installations from Official Launcher, TLauncher, Prism Launcher, MultiMC, CurseForge, GDLauncher, ATLauncher, and Modrinth App.
- Import mods, resource packs, shader packs, and local versions.
- Check GitHub releases for Nova Launcher updates.
- Download and start installer updates from inside the app.

## Platform Support

Nova Launcher is an Electron application and is intended to run on:

- Windows 10/11
- Linux desktop distributions supported by Electron
- macOS versions supported by Electron

The current packaged build script targets Windows. Linux and macOS packaging can be added through `electron-builder` configuration.

## Installation

### Windows Release

1. Open the project releases page.
2. Download the latest `Nova Launcher Setup x.x.x.exe`.
3. Run the installer.
4. Start Nova Launcher from the Start menu or desktop shortcut.

If Windows SmartScreen appears, choose **More info** and then **Run anyway** only if you trust the downloaded build source.

### From Source

```bash
git clone https://github.com/Rosilon/Nova-launcher.git
cd Nova-launcher
npm install
npm start
```

## Development Setup

### Requirements

- Node.js 18 or newer
- npm
- Git

### Install Dependencies

```bash
npm install
```

### Run the App

```bash
npm start
```

### Build the Windows Installer

```bash
npm run build:win
```

Build output is written to `dist/`.

## Project Structure

```text
nova-launcher/
├── assets/
│   ├── icon.icns
│   ├── icon.ico
│   └── icon.png
├── renderer/
│   ├── app.js          # Renderer process UI behavior
│   ├── index.html      # Launcher layout and tabs
│   └── style.css       # Nova visual styling
├── main.js             # Electron main process and launcher services
├── preload.js          # Safe context bridge API
├── package.json        # Scripts, dependencies, and build config
├── package-lock.json
├── start.bat
└── start.sh
```

## Technology Stack

- Electron 28 for the desktop shell.
- Node.js for local filesystem, process, networking, and archive operations.
- `minecraft-launcher-core` for Minecraft launch orchestration.
- `fs-extra` for reliable filesystem operations.
- `extract-zip` and `archiver` for import, export, and backup workflows.
- Modrinth API v2 for content search, install, update checks, and conflict metadata.
- Mojang and Minecraft metadata APIs for versions and player skin lookup.
- WebGL canvas rendering for the 3D skin viewer.

## Data Locations

Nova stores launcher data in:

```text
~/.nova-launcher/
```

Important files and folders:

```text
settings.json          Global launcher settings
profiles.json          Profile definitions
servers.json           Saved server list
versions-cache.json    Offline Minecraft version cache
minecraft/             Default game directory
instances/             Per-profile game directories
java/                  Managed Java runtimes
world-backups/         World backup archives
```

## Troubleshooting

### The Launcher Does Not Start

- Run `npm install` again if dependencies are missing.
- Make sure Node.js 18 or newer is installed.
- Start from a terminal with `npm start` and inspect the error output.

### Minecraft Fails to Launch

- Check the real-time console in the Home tab.
- Confirm that the selected Minecraft version has a compatible Java runtime.
- Use the Java tab to download a managed runtime.
- Try a clean Vanilla profile to separate launcher issues from mod issues.

### Mods Do Not Load

- Confirm the profile uses Fabric or Forge when required.
- Check that mods are installed in the selected profile's `mods/` folder.
- Verify Minecraft version and loader compatibility.
- Use the mod conflict checker for known Modrinth incompatibilities.

### Skin Preview Does Not Load

- Confirm the username is a valid Minecraft username.
- Check internet connectivity; skin lookup uses Mojang session services.
- If WebGL is unavailable, Nova falls back to a 2D preview.

### Online Features Are Disabled

- Open Settings and check Offline Mode.
- Nova may automatically enter offline mode if connectivity checks fail.
- Modrinth search, update checks, and skin lookup require internet access.

## Contributing

Contributions are welcome. Please keep changes focused, incremental, and compatible with existing launcher behavior.

1. Fork the repository.
2. Create a feature branch.
3. Make your changes.
4. Run syntax checks and start the launcher locally.
5. Open a pull request with a clear summary and test notes.

Useful checks:

```bash
node --check main.js
node --check preload.js
node --check renderer/app.js
npm run build:win
```

## Security Notes

Nova uses Electron context isolation and exposes renderer functionality through `preload.js`. Main-process IPC handlers should validate paths, filenames, URLs, and external inputs before performing filesystem or network operations.

When adding features, prefer narrow IPC methods over exposing generic filesystem or shell access.

## License

Nova Launcher is released under the MIT License. See [LICENSE](LICENSE) for details.

## Disclaimer

Nova Launcher is an unofficial third-party Minecraft launcher. It is not affiliated with, endorsed by, or sponsored by Mojang Studios or Microsoft. Minecraft is a trademark of Mojang Studios. Use this project responsibly and comply with Minecraft's applicable terms and licenses.
