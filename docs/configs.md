# configs/

Contains configuration files for emulators and tools, organized by operating system.

## Structure

```
configs/
├── common/      # Shared across all OS
├── linux/       # Linux-specific
├── windows/     # Windows-specific
└── darwin/      # macOS-specific
```

## common/

Configurations shared between all operating systems:

| Folder | Description |
|--------|-------------|
| `retroarch/` | RetroArch configs, cores, shaders, overlays |
| `emulationstation/` | ES-DE themes and settings |
| `srm/` | Steam ROM Manager parsers and settings |
| `roms/` | ROM folder structure (180+ systems) |
| `rclone/` | Cloud sync configuration |
| `[emulator]/` | Per-emulator configs |

## linux/

Linux-specific configurations. Paths use:
- Flatpak paths: `~/.var/app/[flatpak-id]/`
- Native paths: `~/.config/[emulator]/`

## windows/

Windows-specific configurations. Paths use:
- Portable paths: `Emulation/tools/[emulator]/`
- User paths: `%APPDATA%/[emulator]/`

## darwin/

macOS-specific configurations. Paths use:
- App Support: `~/Library/Application Support/[emulator]/`

## Placeholders

When configs are copied, these placeholders are replaced:

| Placeholder | Replaced with |
|-------------|---------------|
| `EMULATIONPATH` | User's Emulation folder path |
| `STEAMPATH` | Steam installation path |
| `.EXT` | `.sh` (Unix) or `.bat` (Windows) |
