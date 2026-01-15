# setup.py

Main entry point for EmuDeck installation. You need to have a settings.json file in APPDATA/EmuDeck/

## Purpose

Orchestrates the complete installation process:

1. Environment setup
2. Folder structure creation
3. Parallel emulator installation
4. Parallel configuration
5. Desktop icon creation

## Flow

```python
# 1. Create Python virtual environment
from functions.env import generate_python_env
generate_python_env()

# 2. Import everything
from core.all import *

# 3. Create folder structure
emulation_path.mkdir()
roms_path.mkdir()
tools_path.mkdir()
bios_path.mkdir()
saves_path.mkdir()
storage_path.mkdir()
ESDEscrapData.mkdir()

# 4. Copy ROM folder structure
shutil.copytree("configs/common/roms", roms_path)

# 5. Install emulators in parallel (5 concurrent jobs)
with ThreadPoolExecutor(max_workers=5) as executor:
    executor.submit(esde_install)
    executor.submit(srm_install)
    executor.submit(retroarch_install)
    executor.submit(dolphin_install)
    # ... 27 emulators total

# 6. Initialize/configure emulators in parallel
with ThreadPoolExecutor(max_workers=5) as executor:
    executor.submit(esde_init)
    executor.submit(srm_init)
    executor.submit(retroarch_init)
    executor.submit(dolphin_init)
    # ... 26 init functions

# 7. Post-installation
get_screen_ar()         # Detect aspect ratio
create_desktop_icon()   # Create desktop shortcut

# 8. Mark complete
set_msg("100")          # Signal UI that installation finished
```

## Parallelization

Uses `ThreadPoolExecutor` with 5 concurrent workers to speed up installation. Each emulator install/init runs independently.

## Progress Tracking

The `set_msg()` function writes progress to `~/.config/EmuDeck/logs/msg.log` which the UI reads to display progress percentage.
