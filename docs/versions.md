# versions.json

Tracks configuration versions for each emulator.

## Purpose

The AppImage/installer checks this file to determine if there's a **new configuration** available for any emulator. When the version number increases, it signals that the emulator's configuration should be updated.

## Format

```json
{
  "ra": { "id": "ra", "code": "RetroArch", "version": 2 },
  "dolphin": { "id": "dolphin", "code": "Dolphin", "version": 4 },
  "ryujinx": { "id": "ryujinx", "code": "Ryujinx", "version": 4 },
  "srm": { "id": "srm", "code": "SRM", "version": 8 },
  "esde": { "id": "esde", "code": "ESDE", "version": 4 },
  "pcsx2": { "id": "pcsx2", "code": "PCSX2", "version": 3 },
  "rpcs3": { "id": "rpcs3", "code": "RPCS3", "version": 2 },
  ...
}
```

## Fields

| Field | Description |
|-------|-------------|
| `id` | Short identifier |
| `code` | Display name |
| `version` | Configuration version number |

## How It Works

1. AppImage downloads `versions.json` from repository
2. Compares with local stored versions
3. If remote version > local version for any emulator:
   - Prompts user to update configuration
   - Runs `[emu]_init()` to apply new config
4. Stores new version numbers locally

## When to Increment

Increment an emulator's version when:
- Default settings change
- New configuration options are added
- Paths or folder structure changes
- Bug fixes require config update

Do NOT increment for:
- Emulator binary updates (handled separately)
- User-facing features that don't affect config files
