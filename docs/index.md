# EmuDeck Developer Documentation

EmuDeck is a cross-platform (Linux, Windows, macOS) emulator management tool that automates installation, configuration and organization of emulators.

## Project Structure

```
EmuDeck/
├── setup.py           # Main entry point
├── api.py             # Dynamic API for remote calls
├── versions.json      # Emulator version tracking
├── core/              # Core system (vars, imports, loader)
├── functions/         # Main logic
│   ├── helpers.py     # Utility functions
│   ├── emus_scripts/  # Emulator scripts (33+)
│   └── tools_scripts/ # Tool scripts (14+)
├── configs/           # Configuration files by OS
└── tools/             # Auxiliary tools
```

## Quick Links

- [configs/](configs.md) - Configuration files organized by OS
- [core/](core.md) - Core system and module loader
- [tools/](tools.md) - Auxiliary tools (launchers, compressor, etc.)
- [helpers.py](helpers.md) - All utility functions
- [emus_scripts/](emus-scripts.md) - How emulator scripts work
- [tools_scripts/](tools-scripts.md) - How tool scripts work
- [api.py](api.md) - Dynamic API
- [setup.py](setup.md) - Installation entry point
- [versions.json](versions.md) - Version tracking system
