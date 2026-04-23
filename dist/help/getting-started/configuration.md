# Configuration

Main configuration is under **Settings**. Here are the most relevant parts for getting started.

## Storage Base Path

Sami keeps tools, agents, and backups in one base directory. In **Settings → General**, set **Storage Base Path** to the folder you want. A **restart** is required for the change to take effect. Default is `./storage` (relative to the app).

## Default locations for new items

In **Settings → General**:

- **Default Tool Location** — category/location used when you create a new tool (e.g. "Development").
- **Default Agent Location** — category used when you create a new agent (e.g. "My Agents").

So new tools and agents appear in the right place in the sidebar without you picking every time.

## API port and remote access

The app runs an **API** (for CLI and REST) on a fixed port. In **Settings → General**:

- **API port** — default **20222**. If that port is busy at startup, the app uses the next free port. You can set a **Preferred API port**; if it’s in use, the app still picks another and shows the actual port (restart to try your preferred one again).
- **Allow remote API access** — when **off**, only this computer can call the API (localhost). Turn it **on** to allow other devices on the network (e.g. to run agents from another machine). **Restart required.** Traffic is **unencrypted** — use only on a trusted network or put a reverse proxy with HTTPS in front.

For scripts and automation, see [Automation (CLI & API)](/help/automation).

## Tools at startup

**Tools Startup Mode** (Settings → General) controls whether MCP tools are started when the app launches:

- **None** — don’t start any tools.
- **Manual** — start only tools that have **autoStart** enabled.
- **All** — start all enabled tools.

Useful if you want the app to connect to MCP servers automatically or to keep them off until you open an agent.

## LLM and limits

- **LLM accounts** — add and manage API keys and models in **LLM Accounts** (sidebar) or in Settings. Each agent picks an account and model in the editor.
- **MCP / Agent execution** — timeouts, retries, message size, and similar limits are in **Settings** (MCP, Agent execution) for tuning when needed.

For an overview of all settings sections, see [Settings](/help/settings).
