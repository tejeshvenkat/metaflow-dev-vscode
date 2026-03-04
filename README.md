# Metaflow Shortcuts for VSCode

This lightweight VS Code extension supercharges your Metaflow dev workflow:

1. Develop a flow
2. Run the flow with **Ctrl + Opt + R**
3. Point at a step, edit it, and _spin_ it with **Ctrl + Opt + S** for quick results ⚡
4. Rinse and repeat 2-3

## Commands

| Command | Purpose | Keyboard Shortcut | Runs |
|---------|---------|-------------------|------|
| **Run a flow** | Execute the entire Metaflow flow | `Ctrl+Alt+R` | `python <file> run` |
| **Spin the current step** | Run only the step under the cursor for fast iteration | `Ctrl+Alt+S` | `python <file> spin <step_name>` |

Both commands are available when editing a Python file (`editorLangId == python`).

**Python interpreter resolution:** The extension uses the interpreter selected in VS Code. If the [Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python) is installed and an interpreter is chosen (venv, conda, pyenv, etc.), that interpreter is used. Otherwise, it falls back to `python` from the system PATH.

## How the Extension Works

1. **Detects the current Python function** — Finds the nearest `def` or `async def` above the cursor to determine which step to run or spin.
2. **Saves the file before execution** — Ensures your latest changes are used.
3. **Reuses a shared terminal** — Uses a single "Metaflow Runner" terminal to avoid cluttering the terminal panel.
4. **Uses the selected VS Code Python interpreter** — Respects `python.defaultInterpreterPath` from the Python extension when available.

## Installation

1. **Clone or copy** this repository to a local folder

2. **Install the VSCE packager** (if not already):

   ```bash
   npm install -g @vscode/vsce
   ```

3. **Build the `.vsix` package:**

   ```bash
   vsce package
   ```

   This creates a file like:

   ```
   metaflow-dev-0.0.7.vsix
   ```

4. **Install it in VS Code:**

   * Open **Command Palette → Extensions: Install from VSIX...**
   * Choose the generated `.vsix` file
     or run in terminal:

     ```bash
     code --install-extension metaflow-dev-0.0.7.vsix
     ```

5. Reload VS Code window. You’re good to go.

## Optional Customization

You can modify the script names or keybindings in `package.json`:

```json
"keybindings": [
  { "command": "extension.runPythonFunction", "key": "ctrl+alt+r" },
  { "command": "extension.spinPythonFunction", "key": "ctrl+alt+s" }
]
```

