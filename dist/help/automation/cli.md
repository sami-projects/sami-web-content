# CLI

The Sami CLI lets you call the Sami API from the command line: list agents and tools, run an agent, get execution results or logs, and manage tools. Command names still use `solution` (e.g. `sami list solutions`) to match the API. The **Sami app must be running**; the CLI connects to it over HTTP (localhost by default).

## Where the CLI lives

The CLI files are in the **`cli`** folder **inside your Sami installation folder** (next to the main application executable).

**Default locations** (when you accept the installer’s suggested folder):

- **Windows (install for current user):** `%LOCALAPPDATA%\Programs\Sami\cli\` — for example `C:\Users\<YourName>\AppData\Local\Programs\Sami\cli\`
- **macOS:** inside the Sami app bundle (e.g. under **Sami.app** → **Show Package Contents** → look for the **`cli`** folder next to the packaged app files)
- **Linux:** **`cli`** next to the unpacked application files (or inside the layout provided by your package)

If you **chose a custom installation directory** in the installer, open that folder instead — the **`cli`** folder is always **next to the Sami application**, not under your documents or settings.

**All users / Program Files (Windows):** If your organization installed Sami “for all users,” the program (and **`cli`**) may be under **`Program Files`** rather than `%LOCALAPPDATA%\Programs\Sami`. Use the **`cli`** folder beside **`Sami.exe`** in that installation.

## Running the CLI

- **Windows:** run **`sami.cmd`** (double-click works for quick tests; a terminal is better for automation).
- **macOS / Linux:** run the **`sami`** script in the **`cli`** folder.

You can:

1. Run **`sami.cmd`** or **`sami`** by **full path**, or  
2. Add the **`cli`** folder to your system [PATH](https://en.wikipedia.org/wiki/PATH_(variable)), then open a **new** terminal and type **`sami`** as usual.

**Windows — add to PATH (one-time), default install path:**  
In Command Prompt:

`setx PATH "%PATH%;%LOCALAPPDATA%\Programs\Sami\cli"`

Then open a new terminal. If Sami was installed elsewhere, substitute your real **`cli`** folder path instead of `%LOCALAPPDATA%\Programs\Sami\cli`.

**Quick test without changing PATH:**

`"%LOCALAPPDATA%\Programs\Sami\cli\sami.cmd" --help`

(Again, replace the path if your install folder is different.)

Use **`sami --help`** or **`sami -h`** to print the command list.

## How the CLI finds the API

The CLI picks the API base URL in this order:

1. **`SAMI_API_URL`** — if set (for example `http://localhost:20222`), that address is used. Use the host and port only (do not append `/api/v1`).
2. **`api-port.json`** — in the Sami **app data** directory (not the install folder): on Windows **`%APPDATA%\sami`**, on macOS **`~/Library/Application Support/sami`**, on Linux **`~/.config/sami`** or **`$XDG_CONFIG_HOME/sami`**. The file contains something like `{"port": 20222}`. If the default port was busy, the app writes the actual port here.
3. **Default** — `http://localhost:20222`.

If the app uses a non-default port, either set **`SAMI_API_URL`** or run the CLI on the **same machine** as the app so it can read **`api-port.json`**.

## Command overview

Format is **verb noun**; for agent and tool commands, `<id>` can be the agent/tool **id** or **exact name**. To find an id in the app: in **Agents** or **Tools** enable the **ID** column via the Columns button, or open the item in the editor → **Agent Info** / **Server Info** → **More**.

| Command | Description |
|--------|-------------|
| `sami list solutions [--limit n]` | List agents (JSON). |
| `sami list executions [--status ...] [--solution-id id] [--limit n]` | List executions; filter by status or agent. |
| `sami list tools [--limit n]` | List MCP tools (JSON). |
| `sami list solution-categories` | List agent categories. |
| `sami search solutions <query> [--limit n]` | Search agents by query. |
| `sami search tools <query> [--limit n]` | Search tools by query. |
| `sami get solution <id> [schema \| status \| scheduler \| llm \| statistics]` | Get agent, schema, status, scheduler, LLM info, or statistics. |
| `sami run solution <id> [--input k=v ...] [--no-wait]` | Run agent; optional inputs; `--no-wait` returns without waiting for completion. Alias: `sami run <id>`. |
| `sami get execution <id> result \| logs \| chat [--limit n] [--include-thinking]` | Get execution result, logs, or chat. |
| `sami get tool <id> [status \| functions \| logs]` | Get tool, status, functions, or logs. |
| `sami get tool <id> function <name> schema` | Get argument schema for a tool function. |
| `sami run tool <id> function <name> [--arg k=v ...] [--json {...}]` | Call a tool function with arguments. |
| `sami connect tool <id>` | Connect (start) the MCP tool. |

Output is JSON to stdout. Redirect or pipe as needed (e.g. `sami list solutions | jq`).

## Examples

List agents and run one by name:

```bash
sami list solutions
sami run solution "My Daily Report" --no-wait
```

Run with input parameters (key=value):

```bash
sami run solution "Summarizer" --input url="https://example.com/article" --input max_length=500
```

Get execution result after a run (use the execution id returned by run, or list executions):

```bash
sami list executions --solution-id "My Daily Report" --limit 1
sami get execution <EXECUTION_ID> result
```

List tools and connect one:

```bash
sami list tools
sami connect tool "My MCP Server"
```

## Typical scenarios

- **Script or scheduled task** — start the app (or assume it’s already running), then call `sami run solution <id>` or `sami run solution <id> --no-wait` and later poll `sami get execution <id> result`. *(Commands use `solution` in the name; they operate on agents.)*
- **Check status** — `sami get solution <id> status`, `sami get solution <id> scheduler`, `sami get tool <id> status`.
- **Remote machine** — set **`SAMI_API_URL`** to `http://<host>:<port>` (and enable **Allow remote API access** in Settings on the computer where Sami runs). Prefer a trusted network or HTTPS via reverse proxy.

For connection issues, see [Troubleshooting](/help/troubleshooting). For HTTP paths and examples without the CLI, see [REST API](/help/automation/rest-api).
