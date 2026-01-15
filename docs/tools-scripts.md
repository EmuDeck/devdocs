# functions/tools_scripts/

Contains scripts for auxiliary tools (frontends, utilities). Each follows the same pattern as emulator scripts.

## Pattern

Every tool script implements:

| Function | Description |
|----------|-------------|
| `[tool]_install()` | Downloads and installs the tool |
| `[tool]_uninstall()` | Removes the tool |
| `[tool]_is_installed()` | Checks if tool exists |
| `[tool]_init()` | Configures the tool |
| `[tool]_install_init()` | Calls install + init |

## Example: Steam ROM Manager (SRM)

```python
from core.all import *

def srm_install():
    set_msg("Installing Steam Rom Manager")

    if system == "linux":
        type = "AppImage"
        destination = emus_folder
    if system.startswith("win"):
        type = "exe"
        destination = tools_path
    if system == "darwin":
        type = "dmg"
        destination = emus_folder

    repo = get_latest_release_gh("SteamGridDB/steam-rom-manager", type, "portable")
    install_emu("srm", repo, type, destination)

def srm_uninstall():
    if system == "linux":
        uninstall_emu("Steam Rom Manager", "AppImage")
    if system.startswith("win"):
        uninstall_emu("srm", "dir")
    if system == "darwin":
        uninstall_emu("Steam Rom Manager", "app")

def srm_is_installed():
    if system == "linux":
        return (tools_path / "Steam Rom Manager.AppImage").exists()
    if system.startswith("win"):
        return (tools_path / "srm.exe").exists()
    if system == "darwin":
        return (emus_folder / "Steam Rom Manager.app").exists()

def srm_init():
    set_msg("Setting up Steam Rom Manager")

    # Copy configs
    copy_setting_dir("common/srm/", srm_path)
    copy_and_set_settings_file("common/srm/userData/userSettings.json", f"{srm_path}/userData")
    copy_and_set_settings_file("common/srm/userData/userConfigurations.json", f"{srm_path}/userData")

    # Add parsers for each emulator
    srm_add_custom_parsers()

    # Windows needs path conversion
    if system.startswith("win"):
        srm_windows_paths()

def srm_windows_paths():
    # Convert Unix paths to Windows paths in config files
    sed('/', '\\\\', f"{srm_path}/userData/userConfigurations.json")

def srm_install_init():
    srm_install()
    srm_init()

def srm_add_custom_parsers():
    # Finds all functions ending with _add_custom_parser and calls them
    funcs = [name for name in globals() if name.endswith('_add_custom_parser')]
    for name in sorted(funcs):
        globals()[name]()
```

## Available Tools

| Script | Description |
|--------|-------------|
| `emudeck_srm.py` | Steam ROM Manager |
| `emudeck_esde.py` | EmulationStation-DE |
| `emudeck_retro_library.py` | Artwork downloader for Decky |
| `emudeck_compressor.py` | CHD compression tool |
| `emudeck_cloudsync_local.py` | Cloud sync with rclone |
| `emudeck_migration.py` | Migration between installations |
| `emudeck_copy_games.py` | Copy games between devices |
| `emudeck_update_emus.py` | Update emulators |
| `emudeck_plugins.py` | Plugin management |
| `emudeck_bios_checker.py` | BIOS verification |
