# Automation (CLI & API)

You can run agents, list tools and executions, and check status from **scripts** or **other applications** using the **CLI** or the **REST API**. Both talk to the Sami app over HTTP on the same port. The app must be running; there is no separate server process.

## What you need

- **Sami app running** — start the application first. The API is served from inside the app.
- **Port** — default is **20222**. If that port is busy at startup, the app uses the next free port. Set or check the port in **Settings → General** (API port). The actual port in use may be written to `api-port.json` in the app data directory (e.g. in `userData` for the Electron app).
- **Remote access (optional)** — by default only **localhost** can connect. To call the API from another computer, enable **Settings → General → Allow remote API access** and restart. Traffic is unencrypted; use only on a trusted network or behind an HTTPS reverse proxy. See [Troubleshooting](/help/troubleshooting#cli-or-api-connection-refused-or-cannot-connect).

**Finding agent and tool IDs:** In the app you can use either the **exact name** or the **id**. To see the id: in **Agents** or **Tools**, open the table column menu (Columns button) and enable the **ID** column; or open an agent/tool in the editor, expand **Agent Info** or **Server Info**, then click **More** — the ID is listed there. You can also get ids from the API (e.g. `GET /solutions`, `GET /tools` or `sami list solutions`, `sami list tools`). *(REST paths still use the `solution` segment for compatibility.)*

## CLI

The **CLI** is a command-line client: list agents and tools, run an agent, get execution result or logs, connect a tool, and more. Useful for scripts, scheduled tasks, and quick checks from the terminal.

The CLI ships **inside your Sami installation** (the **`cli`** folder next to the application). Run **`sami.cmd`** (Windows) or **`sami`** (macOS/Linux) from that folder by full path, or add that folder to your PATH. It uses **`SAMI_API_URL`** if set; otherwise it reads the port from **`api-port.json`** in the app data directory; otherwise **`http://localhost:20222`**.

See [CLI](/help/automation/cli) for where files are installed, PATH, commands, and examples.

## REST API

The **REST API** uses a path-based URL layout under `http://localhost:<port>/api/v1`: e.g. `GET /solutions`, `POST /solution/{id}/run`, `GET /execution/{id}/result`. Use it from any HTTP client (curl, scripts, other apps). Same port and remote-access rules as above.

See [REST API](/help/automation/rest-api) for base URL, examples, and security notes.

## Next steps

- [CLI](/help/automation/cli) — install, port, command list, examples.
- [REST API](/help/automation/rest-api) — base URL, remote access, example requests.
- [Configuration](/help/getting-started/configuration) — API port and remote access in Settings.
- [Troubleshooting](/help/troubleshooting) — connection refused, port, app not running.
