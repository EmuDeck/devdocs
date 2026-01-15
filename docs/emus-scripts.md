# functions/emus_scripts/

Contains one Python file per emulator (33+ emulators). Each follows the same pattern.

## Pattern

Every emulator script implements these functions:

| Function | Description |
|----------|-------------|
| `[emu]_get_url()` | Returns download URL for current OS |
| `[emu]_install()` | Downloads and installs the emulator |
| `[emu]_uninstall()` | Removes the emulator |
| `[emu]_is_installed()` | Checks if emulator exists |
| `[emu]_init()` | Configures the emulator |
| `[emu]_install_init()` | Calls install + init |

## Example: Dolphin

```python
from core.all import *

def dolphin_get_download_url() -> Optional[str]:
    # Returns URL based on OS
    if system == "linux":
        return "org.DolphinEmu.dolphin-emu"  # Flatpak ID
    if system.startswith("win"):
        # Parse download page for Windows 7z
        return "https://dl.dolphin-emu.org/.../dolphin-x64.7z"
    if system == "darwin":
        # Parse download page for macOS DMG
        return "https://dl.dolphin-emu.org/.../dolphin-universal.dmg"

def dolphin_install():
    set_msg("Installing dolphin")

    if system == "linux":
        type = "flatpak"
        destination = emus_folder
    if system.startswith("win"):
        type = "7z"
        destination = f"{emus_folder}/Dolphin-x64"
    if system == "darwin":
        type = "dmg"
        destination = emus_folder

    install_emu("Dolphin", dolphin_get_download_url(), type, destination)

def dolphin_uninstall():
    if system == "linux":
        uninstall_emu("org.DolphinEmu.dolphin-emu", "flatpak")
    if system.startswith("win"):
        uninstall_emu("Dolphin-x64", "dir")
    if system == "darwin":
        uninstall_emu("Dolphin", "app")

def dolphin_is_installed():
    if system == "linux":
        return is_flatpak_installed("org.DolphinEmu.dolphin-emu")
    if system.startswith("win"):
        return (emus_folder / "Dolphin-x64" / "dolphin.exe").exists()
    if system == "darwin":
        return (emus_folder / "Dolphin.app").exists()

def dolphin_init():
    set_msg("Setting up dolphin")

    # Determine config path per OS
    if system == "linux":
        destination = f"{home}/.var/app/org.DolphinEmu.dolphin-emu/config/dolphin-emu/"
    if system.startswith("win"):
        destination = f"{emus_folder}/Dolphin-x64/"
    if system == "darwin":
        destination = f"{home}/Library/Application Support/Dolphin/Config"

    # Copy config files
    copy_setting_dir(f"{system}/dolphin-emu/", destination)
    copy_and_set_settings_file(f"{system}/dolphin-emu/Dolphin.ini", destination)

    # Setup saves, resolution, controls
    dolphin_setup_saves()
    dolphin_set_resolution()
    dolphin_set_controller_style()
    dolphin_widescreen()

def dolphin_install_init():
    dolphin_install()
    dolphin_init()
```

## Key Points

1. **OS Detection**: Every function checks `system` variable
2. **install_emu()**: Handles download and extraction
3. **copy_setting_dir()**: Copies configs from `configs/[system]/`
4. **move_contents_and_link()**: Centralizes saves to `Emulation/saves/`
5. **set_msg()**: Updates progress UI

## Available Emulators

RetroArch, Dolphin, Primehack, PPSSPP, DuckStation, melonDS, Azahar, PCSX2, RPCS3, Yuzu, Citron, Ryujinx, ShadPS4, Xemu, Cemu, RMG, ScummVM, Vita3K, Xenia, mGBA, Flycast, BigPEmu, Model2, Supermodel, MAME, and more.
