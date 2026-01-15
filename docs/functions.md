# functions/ - Other Files

Additional files in the functions directory outside of emus_scripts and tools_scripts.

## Files

| File | Description |
|------|-------------|
| `helpers.py` | Main utility functions (see [helpers.md](helpers.md)) |
| `env.py` | Python virtual environment manager |
| `app_init.py` | Application initialization |
| `vdf.py` | Valve Data Format file handling |
| `mocks.py` | Mock objects for testing |
| `all.sh` | Legacy bash compatibility |
| `allCloud.ps1` | Legacy PowerShell compatibility |
| `__init__.py` | Package initialization |

## env.py

Manages Python virtual environment creation and activation:

```python
def generate_python_env():
    # Creates venv at ~/.config/EmuDeck/backend/venv
    # Installs dependencies from requirements.txt
```

## app_init.py

Application startup and initialization routines.

## vdf.py

Handles reading and writing Valve Data Format files (used by Steam).

```python
# Read Steam shortcuts
data = vdf.load(open(shortcuts_path))

# Write shortcuts
vdf.dump(data, open(shortcuts_path, 'w'))
```

## mocks.py

Mock objects used during testing to simulate emulators and configurations without actual installation.

## all.sh and allCloud.ps1

These files exist for **backward compatibility with legacy launchers**.

The previous version of EmuDeck used bash scripts (all.sh) and PowerShell scripts (allCloud.ps1) for automation. These files are kept so that existing launchers and integrations that call them continue to work.

They essentially source/import the Python functionality to maintain compatibility with the older shell-based architecture.
