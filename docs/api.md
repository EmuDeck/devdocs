# api.py

Dynamic API that allows calling any function from the command line or external applications.

## Purpose

Enables remote/external calls to any EmuDeck function via CLI, returning JSON responses. Used by:
- Web UI
- External scripts
- Automation tools

## Usage

```bash
python api.py <function_name> [args_json] [kwargs_json] [--no-silent]
```

## Examples

```bash
# Simple function call
python api.py retroarch_install

# With positional arguments (JSON array)
python api.py copy_and_set_settings_file '["common/retroarch/retroarch.cfg", "/tmp"]'

# With keyword arguments (JSON object)
python api.py install_emu '["Dolphin", "http://...", "7z"]' '{"destination": "/home/user/emus"}'

# Verbose output (not silent)
python api.py dolphin_init --no-silent
```

## Response Format

Success:
```json
{"status": "OK", "result": <return_value>}
```

Error:
```json
{"status": "KO", "error": "error description"}
```

## How It Works

```python
def main():
    # 1. Parse arguments
    func_path = sys.argv[1]      # e.g., "dolphin_install"
    args = json.loads(sys.argv[2]) if len(sys.argv) > 2 else []
    kwargs = json.loads(sys.argv[3]) if len(sys.argv) > 3 else {}

    # 2. Import function dynamically
    from core.all import *
    func = globals()[func_path]

    # 3. Execute with call_func (captures output)
    result = call_func(func, *args, silent=True, **kwargs)

    # 4. Return JSON
    print(json.dumps(result))
```

Any function available via `from core.all import *` can be called through this API.
