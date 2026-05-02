# Settings

**Settings** control where Sami stores data, how it connects to MCP and LLM services, and how agents and tools behave. Open **Settings** from the sidebar; the left panel lists sections, the right panel shows the selected section. Changes are applied when you save (button at the top). Many options have sensible defaults — adjust them when you need different behavior or run into limits.

## Sections overview

**General** — Storage base path (where tools, agents, and backups are stored; restart required to move data). Default locations for new tools and agents. API port and whether to allow remote API access. Tools startup mode when the app launches (none, manual for auto-start tools, or all enabled tools). See [Configuration](/help/getting-started/configuration) for a short guide to the most common options.

**Agent** — Global limits for all agents: maximum execution time, LLM response timeout, tool-call iterations, and related safety or performance options. These apply to every agent unless overridden in the agent’s own settings (editor → Settings).

**MCP Server** — Timeouts, retries, max message size, and similar options for communication with MCP servers. Useful when you have slow or unreliable servers or large payloads.

**LLM** — Global LLM profiles and retry behavior (e.g. per-provider limits, retry rules). This is separate from **LLM Accounts** in the main sidebar, where you add API keys and choose models; here you tune how the app uses those accounts.

**AI Assistant** — Model and parameters for the in-editor AI Assistant chat. This is the model that powers the assistant; each agent can use a different model for execution. See [AI Assistant](/help/ai-assistant).

**Geo Restriction** — Optionally block LLM requests by country for selected providers (e.g. to comply with regional policies). You choose which providers to restrict and which country codes to block.

**Proxy** — HTTP/HTTPS proxy for outbound requests (to LLM APIs, SSE tool endpoints, etc.). Use when your network requires a proxy to reach the internet.

**Logging** — Enable or disable application logging, set log level, and how long to keep logs. When logging is disabled, the **Logs** section and per-tool logs will be empty. See [Tools](/help/tools) for where to view logs.

**Backup** — How many backup versions to keep: common backups (tools and agents, created at app start) and result backups. Higher values use more disk space but give more history to restore from.

**Logs & Diagnostics** — View application logs, see error/warning counts, export or clear logs. Use this when debugging or when sending logs to support. The same logs are available from **Tools → More → View App Logs**.

**Backups** — List of existing backups, create a new backup now, or restore a backup. Restoring replaces current tools and agents with the backup contents; the app may reload data after restore.

## When to open which section

- **First-time or moving data** → General (storage path, default locations, API port).
- **Agents time out or hit limits** → Agent (execution time, timeouts).
- **Tools disconnect or hang** → MCP Server (timeouts, retries).
- **LLM rate limits or retries** → LLM (profiles, retry settings).
- **Assistant model or behavior** → AI Assistant.
- **Restrict by region** → Geo Restriction.
- **Behind corporate proxy** → Proxy.
- **Nothing in logs or too much noise** → Logging.
- **How much history to keep** → Backup.
- **Inspect or export logs** → Logs & Diagnostics.
- **Restore or create a backup** → Backups.

For connection and run issues, see [Troubleshooting](/help/troubleshooting).
