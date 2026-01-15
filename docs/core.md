# core/

The core module contains the system foundation: variables, imports, and dynamic module loading.

## Files

| File | Description |
|------|-------------|
| `vars.py` | Global variables and configuration |
| `imports.py` | Dependencies and logging setup |
| `all.py` | Dynamic module aggregator |

## vars.py

Defines all global variables used throughout the project:

```python
# OS detection
system = "linux" | "darwin" | "windows"

# Main paths
home = Path.home()
emudeck_folder = ~/.config/EmuDeck
emulation_path = ~/Emulation
roms_path = ~/Emulation/roms
bios_path = ~/Emulation/bios
saves_path = ~/Emulation/saves
tools_path = ~/Emulation/tools
storage_path = ~/Emulation/storage

# Loads settings.json into SimpleNamespace objects
settings = SimpleNamespace(...)
install_emus = SimpleNamespace(retroarch=..., dolphin=..., ...)
```

## imports.py

Sets up dependencies and dual logging (console + file):

```python
# Main dependencies
import subprocess, requests, vdf, PySide6, pygame

# Logging: INFO to console, DEBUG to file
logging.basicConfig(...)
```

## all.py

The key file that makes all functions available with a single import.

### `_import_all_functions_and_vars()`

This function dynamically loads all modules and exports their functions:

```python
def _import_all_functions_and_vars():
    # 1. Force-load critical modules first
    force_load = [
        "functions.helpers",
        "functions.tools_scripts.emudeck_plugins",
        "functions.vdf",
        "functions.tools_scripts.emudeck_esde"
    ]

    # 2. Walk and import ALL modules in functions/
    for _, mod_name, _ in pkgutil.walk_packages(functions.__path__):
        importlib.import_module(f"functions.{mod_name}")

    # 3. Export all functions and variables to globals()
    for name, obj in module.__dict__.items():
        if callable(obj) or not name.startswith('_'):
            globals()[name] = obj
```

### Usage

```python
# This single import gives access to everything:
from core.all import *

# Now available:
# - All 70+ helper functions
# - All emulator functions (dolphin_install, retroarch_init, etc.)
# - All tool functions (srm_install, esde_init, etc.)
# - All global variables (system, emulation_path, settings, etc.)
```

This pattern allows any script to access any function without knowing which module it belongs to.
