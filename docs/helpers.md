# functions/helpers.py

Contains 70+ utility functions used across all emulator and tool scripts.

## Function Reference

| Function | Description | OS-specific |
|----------|-------------|-------------|
| `install()` | Creates Emulation folder structure (roms, bios, saves, tools) | No |
| `get_sd_path()` | Detects SD card mount point | Linux only |
| `test_location_valid()` | Tests if path is writable and supports symlinks | No |
| `get_product_name()` | Gets hardware product name (e.g., "Jupiter" for Steam Deck) | Linux only |
| `get_screen_ar()` | Returns screen aspect ratio (169, 1610, or 0) | No |
| `get_environment_details()` | Prints environment info as JSON | No |
| `get_primary_monitor_size()` | Returns monitor resolution (width, height) | No |
| `bool_from(val)` | Converts various values to boolean | No |
| `set_msg(message)` | Updates progress message (writes to msg.log) | No |
| `update_or_append_config_line()` | Updates or appends line in config file | No |
| `ar_169_screen()` | Applies RetroArch bezel fixes for 16:9 screens | No |
| `get_xdg_user_dir(name)` | Gets XDG directory (DESKTOP, DOCUMENTS, etc.) | Linux only |
| `command_exists(cmd)` | Checks if command exists in PATH | No |
| `remove_if_exists(path)` | Removes file/directory if exists | No |
| `create_desktop_shortcut()` | Creates .desktop (Linux), .lnk (Windows), or symlink (macOS) | Yes |
| `create_desktop_icon()` | Creates EmuDeck desktop icon | Yes |
| `controller_layout_ABXY()` | Sets ABXY controller layout for all emulators | No |
| `controller_layout_BAYX()` | Sets BAYX controller layout for all emulators | No |
| `download_file(url, dest)` | Downloads file using curl | No |
| `md5_of(path)` | Calculates MD5 hash of file | No |
| `changeLine(keyword, replace, file)` | Replaces line containing keyword | No |
| `escapeSedKeyword(input)` | Escapes special chars for sed pattern | No |
| `escapeSedValue(input)` | Escapes special chars for sed replacement | No |
| `deleteConfigs()` | Deletes RetroArch core configs | No |
| `customLocation()` | Opens folder selection dialog (Zenity) | Linux only |
| `get_latest_release_gh()` | Gets download URL from GitHub latest release | No |
| `get_latest_prerelease_gh()` | Gets download URL from GitHub prerelease | No |
| `linkToSaveFolder()` | Creates symlink to centralized saves folder | No |
| `linkToTexturesFolder()` | Creates symlink to textures folder | No |
| `linkToStorageFolder()` | Creates symlink to storage folder | No |
| `moveSaveFolder()` | Moves save folder and creates symlink | No |
| `iniFieldUpdate()` | Updates field in INI file (with section support) | No |
| `iniSectionUpdate()` | Replaces entire INI section | No |
| `calculate_checksum_sha256()` | Calculates SHA256 of file | No |
| `safeDownload()` | Downloads with checksum verification | No |
| `addSteamInputCustomIcons()` | Copies Steam Input icons | No |
| `is_flatpak_installed(id)` | Checks if Flatpak is installed | Linux only |
| `check_internet_connection()` | Pings 8.8.8.8 to check connectivity | No |
| `zip_logs()` | Creates ZIP of logs for support | No |
| `setResolutions()` | Applies resolution settings to all emulators | No |
| `addParser(parser)` | Adds parser to Steam ROM Manager | No |
| `removeParser(parser)` | Removes parser from Steam ROM Manager | No |
| `scriptConfigFileGetVar()` | Reads variable from shell-style config file | No |
| `getEmuRepo(name)` | Maps emulator name to GitHub repo | No |
| `getLatestVersionGH(repo)` | Gets latest release ID from GitHub | No |
| `addProtonLaunch()` | Copies proton-launch.sh script | Linux only |
| `store_patreon_token(token)` | Saves Patreon token to settings | No |
| `server_install()` | Installs local HTTP server script | No |
| `startCompressor()` | Launches CHD compressor tool | No |
| `call_func(func, *args)` | Executes function with output capture | No |
| `create_symlink_crossplatform()` | Creates symlink (ln on Unix, mklink /J on Windows) | Yes |
| `install_emu(name, url, type, dest)` | Downloads and installs emulator | Yes |
| `uninstall_emu(name, type)` | Removes emulator | Yes |
| `create_app_shortcut(name)` | Creates app launcher shortcut | Yes |
| `create_mac_app()` | Creates macOS .app bundle from script | macOS only |
| `extract(zip, dest)` | Extracts ZIP preserving structure | No |
| `extract_flat(zip, dest)` | Extracts ZIP ignoring top-level folder | No |
| `extract7z_flat(archive, dest)` | Extracts 7z (py7zr or CLI fallback) | Yes |
| `install_dmg(name, path)` | Installs app from DMG | macOS only |
| `extract_tar_gz(archive, dest)` | Extracts tar.gz | No |
| `copy_setting_dir(src, dst)` | Copies config directory from configs/ | No |
| `copy_and_set_settings_file()` | Copies file replacing placeholders | No |
| `sed(old, new, file)` | Find and replace in file | No |
| `move_contents_and_link()` | Moves contents and creates symlink | Yes |
| `set_config(key, value, file)` | Updates key=value in config file | No |
| `extract_tar_xz(archive, dest)` | Extracts tar.xz | No |
| `darwin_trust_app(path)` | Removes quarantine attribute | macOS only |
| `get_linux_version_id()` | Gets Linux distro version | Linux only |
| `update_json_key(key, value, file)` | Updates key in JSON file | No |
| `md5_of_file(path)` | Calculates MD5 (alternative) | No |
| `set_setting(key, value)` | Updates settings.json (supports dot notation) | No |
| `popup_ask_conflict()` | Shows Yes/No/Cancel dialog | No |
| `popup_show_info()` | Shows info dialog with OK button | No |
| `popup_ask_string()` | Shows text input dialog | No |
| `popup_ask_password()` | Shows password input dialog | No |
| `get_locations()` | Gets available drives | Windows only |
| `load_remote_module()` | Loads Python module from URL | No |
| `netplay_set_ip()` | Detects and sets netplay IP | No |
| `calculate_md5(file)` | Calculates MD5 | No |
| `calculate_md5_without_header()` | Calculates MD5 skipping header bytes | No |

## OS-Specific Behavior

Functions marked "Yes" in OS-specific column have different implementations:

**install_emu()**:
- Linux: Flatpak or AppImage
- Windows: exe or 7z extraction
- macOS: DMG mount and copy

**create_symlink_crossplatform()**:
- Linux/macOS: `ln -sf`
- Windows: `mklink /J` (junction point)

**move_contents_and_link()**:
- Linux/macOS: Standard symlink
- Windows: Junction point (no admin required)

**extract7z_flat()**:
- Windows: Uses native `tar.exe`
- Linux/macOS: Uses py7zr library or 7z CLI
