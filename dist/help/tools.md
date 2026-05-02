# Tools

Tools in Sami are **MCP (Model Context Protocol)** servers. Each tool exposes capabilities (e.g. read files, search the web) that agents can use when calling the LLM. You add a tool by connecting to an MCP server; the app discovers its tools, resources, and prompts. Then you attach the tool to agents in the agent editor.

## Adding and connecting

- **Add** — in **Tools**, use the **Add** (➕) button in the toolbar. A new tool opens in the editor.
- **Transport** — choose how the app talks to the server:
  - **stdio** — local process: you set the **command** (path to the executable) and optional **arguments** and **environment variables**. The app starts the process when you connect. The app does **not** bundle `uv`, `node`, or `npx`; it uses whatever is installed on your machine. If `uvx` / `npx` (or similar launchers) misbehave, check versions and **PATH** (see [Troubleshooting](/help/troubleshooting) → **stdio startup issues: PATH mismatch or first-run timeout**).
  - **SSE** — remote server: you set the **URL** and optional **headers**. The app connects to an already running server.
- **Settings** — in the tool editor side panel, open **Settings** (connection icon) to set command/URL, args, env, and other options. Save the tool before connecting.
- **Connect** — in the editor, use **Save & Start Server** (stdio) or **Save & Connect to Server** (SSE) to apply changes and connect. If the config is already saved, use **Start Server** or **Connect to Server**. Once connected, the **Server Info** section shows server name, version, and number of tools/resources/prompts.

From the **Tools** list you can start several tools at once: **Start Available** starts all tools that are **Ready** (configured but not yet connected). **Stop All** stops all connected tools. The **More** menu offers **Start All**, **Restart Connected**, **Export Tools**, **Import Tools**, and **View App Logs**.

You can also discover servers in **Tool Gallery** (browse registries, inspect entry details, and install). See [Tool Gallery](/help/gallery).

## Delete and Trash

Deleting a tool moves it to **Trash** (use **Trash** in the sidebar under **Tools**). Open **Trash** to **Restore** a tool or delete it permanently.

Built-in tools you remove stay out of the bundled set until you restore or reinstall them from the gallery. See [Tool Gallery](/help/gallery) (section **Built-in tools: delete and restore**).

## Sidebar: category order

With **Tools** expanded in the main sidebar, **drag** tool categories to reorder them, or switch to **alphabetical** order via the icon that appears when you **hover the chevron** next to **Tools**. The setting is saved locally on this machine. The **Category** field in the tool editor, export/import pickers, and similar lists follow the **same** order as the sidebar. Alphabetical mode does not remove your saved manual order.

## Status: Ready, Connected, Not configured, Error

In the list and in the editor, each tool has a status:

- **Ready** — configured (e.g. command or URL set) but not connected. You can start or connect from the list or the editor.
- **Connected** — the app is connected to the MCP server; agents can use this tool.
- **Starting** — connection or process start in progress.
- **Not configured** — configuration is missing or invalid (e.g. empty command for stdio, invalid URL for SSE, or required settings not filled). Open the tool and complete **Settings**.
- **Error** — connection or start failed (wrong path, server not running, network issue). Check **Settings** and **Logs** (see below).

**Not configured** is a configuration signal, not a hard blocker. You can still try to start/connect the tool, and in many real-world cases it may work (for example, when a registry marks a field as required but the server accepts an empty value). In the Tools table, **Not configured** rows also show a short hint under the status with the first missing setting.

If a field is incorrectly marked as required, you can disable that requirement in **Server Settings** (for supported fields such as custom headers and environment variables).

## Where to see logs

- **Per-tool logs** — in the tool editor side panel, open **Logs**. These are connection and protocol logs for that MCP server. Useful when a tool fails to connect or behaves oddly.
- **App logs** — in **Tools**, open the **More** (⋮) menu and choose **View App Logs**. Use this for app-wide events, API, and general debugging.

Logging can be enabled or disabled in **Settings → Logging**. If **Logs** in the tool editor is empty, ensure logging is enabled and try connecting again.

## Authentication for HTTP/SSE tools

For remote tools, open **Settings** in the tool editor and choose **Authentication Type**:

- **Auto** — let the app handle auth automatically when possible.
- **Bearer Token (manual API key)** — enter token/key manually.
- **OAuth2 (browser login)** — sign in through a browser flow.
- **Basic Authentication** — username + password.

### OAuth2 (browser login)

Use this when the MCP server requires OAuth sign-in.

1. In tool **Settings**, set **Authentication Type** to **OAuth2 (browser login)**.
2. Fill required fields: **Authorization URL**, **Token URL**, **Client ID**.
3. Optional fields: **Scopes**, **Client Secret (optional)**, **Provider name (optional)**.
4. Register redirect URI in your OAuth provider:
   - `http://127.0.0.1:43110/oauth/callback`
5. Use **Sign in** (or **Sign in again** if token expired).

Status appears in the settings panel as **Signed in**, **Token expired**, or **Not signed in**.  
Use **Clear session** if you need to reset OAuth state and sign in again.

## Export and import

Use **More → Export Tools** to save selected tools to a JSON file (backup or sharing). In the export dialog you can enable **Anonymize sensitive data**: only environment variables that you marked as secret (lock icon next to the variable in **Settings**) are replaced with `[ANONYMIZED]` in the file. Nothing is masked by name alone — you decide which values to hide.

**More → Import Tools** loads tools from a JSON file (e.g. after export or from another machine).

### Advanced: full Sami JSON schema

For programmatic generation and validation of the full Sami tools file format (advanced use), see:

- [/help/schemas/sami-tools-full.schema.json](/help/schemas/sami-tools-full.schema.json)

## Using tools in agents

When editing an agent, open the **Tools** section in the side panel. Attach the MCP tools that this agent is allowed to use. The LLM will be able to call only those tools during execution. Tools must be **Connected** for the agent to use them; if a tool is disconnected, the agent may fail or skip that tool.

**Tip:** Use **Testing** in the tool editor side panel (when the tool is connected) to call tools and see responses without running a full agent.

For connection issues and common errors, see [Troubleshooting](/help/troubleshooting). For gallery-specific advice and safety checks, see [Tool Gallery](/help/gallery). For agent workflows, see [Agents](/help/agents). Global options for tool startup (e.g. start all tools on app launch) are in **Settings → General** (Tools Startup Mode).
