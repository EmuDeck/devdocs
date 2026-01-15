# tools/

Auxiliary tools and scripts used by EmuDeck.

## Structure

```
tools/
├── launcher.py      # Universal emulator launcher
├── launchers/       # Launch scripts per OS
├── wrappers/        # Emulator wrappers
├── compressor/      # CHD compression tool
├── retro-library/   # Retro Library
├── gamemode/        # GameMode integration (Windows)
└── server/          # Local HTTP server
```

## launcher.py

Universal launcher that maps emulator names to executables based on OS.

```python
# Maps emulator to correct executable per platform
# Example: "Dolphin" ->
#   Linux:   flatpak run org.DolphinEmu.dolphin-emu
#   Windows: C:/Emulation/tools/Dolphin-x64/Dolphin.exe
#   macOS:   /Applications/Dolphin.app
```

## launchers/

Shell/batch scripts that ES-DE and SRM use to launch emulators.

```
launchers/
├── unix/           # .sh scripts for Linux/macOS
│   └── es-de/      # ES-DE specific launchers
└── windows/        # .bat scripts for Windows
```

## wrappers/

Scripts that wrap some api call so they can be easily called from outside apps like the EmuDecky plugin.

## compressor/

CHD compression tool for converting ISOs to CHD format.

| File         | Description             |
| ------------ | ----------------------- |
| `chddeck.sh` | Main compression script |

## retro-library/

Decky plugin for Steam Deck. Game Launcher

| File                        | Description                   |
| --------------------------- | ----------------------------- |
| `vars.py`                   | Variables and paths           |
| `utils.py`                  | Utility functions             |
| `retro_achievements.py`     | RetroAchievements integration |
| `download_art_platforms.py` | Art download per platform     |
| `_generate_game_lists.py`   | Game list generation          |

## gamemode/

GameMode for Windows, replaces Windows Desktop for Steam Big Picture for a SteamOS like experience.

## server/

Local HTTP server for uploading roms to the user's device using Wifi.

| File        | Description                |
| ----------- | -------------------------- |
| `server.py` | HTTP server implementation |
