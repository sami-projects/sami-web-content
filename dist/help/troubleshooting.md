# Troubleshooting

Common issues and what to check. When in doubt, check the logs (see [Where to see logs](#where-to-see-logs) below).

## Tool shows "Not configured" or "Error"

- **Command / path** — for **stdio** transport, the MCP server executable path must be correct and the file must be executable. Use absolute paths if the app starts from a different working directory.
- **Arguments and environment** — required arguments (e.g. config file) and environment variables (e.g. `API_KEY`) must be set in the tool **Settings**. They are used when Sami starts the process.
- **SSE** — for **SSE** transport, the server must already be running. Check the URL, network access, and any required headers or auth. From another machine, ensure **Settings → General → Allow remote API access** is on if you need to reach a remote URL from the app.
- **Logs** — open the tool in the editor and check **Logs** in the side panel for connection and protocol errors. For app-wide errors, use **Tools → More → View App Logs** or **Settings → Logs & Diagnostics**.

See [Tools](/help/tools) for status meanings and connection steps.

## stdio startup issues: PATH mismatch or first-run timeout

For **stdio** tools, Sami runs the **command** you configure (for example `uvx`, `npx`, or another launcher) using your system environment.

### 1) PATH mismatch (wrong executable)

If several copies of the same command exist, Sami may start a different executable than expected.

- In a terminal, run **`where <command>`** (Windows) or **`which <command>`** (macOS/Linux) for the exact command configured in tool settings.
- Compare that result with the **full command** shown in the tool **Logs**.
- On Windows, prefer an **absolute path** in **Command** to avoid ambiguity.
- If logs show spawn errors or very old output, update the launcher/tooling you use (for example [uv](https://docs.astral.sh/uv/) / `uvx`, Node.js / `npx`).

### 2) First-run timeout (initial install/download)

The first launch of some commands (`uvx`, `npx`, and similar tools) may install or download packages and exceed connection timeout.

- Retry the connection (the next attempt is often faster).
- Or run the same command once in a terminal to warm package cache.
- If needed, increase **Connection timeout** in **Settings → MCP Server**.
- Keep **Reset timeout on progress** enabled where available.

## OAuth2 sign-in issues (tools)

If a tool uses **OAuth2 (browser login)** and cannot connect:

- Verify provider redirect URI includes exactly: `http://127.0.0.1:43110/oauth/callback`.
- In tool settings, check required OAuth fields: **Authorization URL**, **Token URL**, **Client ID**.
- If status is **Token expired**, use **Sign in again**.
- If sign-in flow is stuck or keeps failing, use **Clear session** and sign in again.
- Check per-tool **Logs** and app logs for the exact provider/server error.

## Agent fails to run or doesn't start

- **Status "Not configured"** — the agent needs a name, instructions (prompt), and at least one enabled trigger. Open it in the editor and complete those; add or enable a trigger in the **Triggers** section if missing.
- **Scheduled runs don't happen** — if the agent has Schedule, Interval, or File system triggers, you must **Activate** it (from the agents list or the editor). Until then, only manual **Run** works. See [Agents](/help/agents).
- **Tools** — ensure every tool attached to the agent is **Connected**. If a tool is disconnected, the agent may fail or skip it. Start or connect tools from **Tools** first.
- **Inputs** — fill any required input fields when you run. Placeholders in the prompt must match input field names.
- **LLM account** — ensure an LLM account is configured (in **LLM Accounts**) and that the agent has an account and model selected in the editor (**LLM** section in the side panel).

## CLI or API: "Connection refused" or cannot connect

The **CLI** and **REST API** talk to the Sami app over HTTP. If you get connection refused or timeouts:

- **App must be running** — start the Sami application first. The API runs inside the app; there is no separate server process.
- **Port** — default is **20222**. If that port was busy at startup, the app uses the next free port. Check **Settings → General** for the current (or preferred) API port. The actual port in use may also be written to a file (e.g. `api-port.json` in the app data directory) depending on your setup.
- **Remote access** — by default the API listens only on **localhost**. To call it from another computer, enable **Settings → General → Allow remote API access** and restart. Then use `http://<this_computer_ip>:20222/api/v1` (or the actual port). Traffic is unencrypted; use only on a trusted network or behind an HTTPS reverse proxy.

For automation details, see the **Automation (CLI & API)** section in Help when available, or [Configuration](/help/getting-started/configuration) for API port and remote access.

## Slow or stuck execution

- Check **Settings → Agent** (execution limits) for timeouts (maximum execution time, LLM response timeout, tool-call iterations). Increase them if your workflow is legitimately long-running.
- Check **Settings → MCP Server** if tool calls hang (timeouts, retries).
- In the logs, look for which step or tool call is slow or timing out.

## Gallery install succeeded, but tool still fails

- Open the entry details in [Tool Gallery](/help/gallery) and inspect **Raw catalog JSON**.
- Verify runtime requirements from entry/project docs (paths, env vars, local dependencies).
- Open external links (**Repository**, **Homepage**, **View on Registry**) and follow setup notes.
- In tool editor, re-check connection settings and status (**Ready / Connected / Not configured / Error**).

## Where to see logs

- **Application logs** — **Settings → Logs & Diagnostics** or **Tools → More → View App Logs**. You can view recent entries, filter by level, export, or clear. Use these for startup errors, API issues, and general debugging.
- **Per-tool logs** — in the **tool editor** side panel, open **Logs**. These show connection and MCP protocol messages for that tool. Use when a tool fails to connect or behaves oddly.
- **Logging must be enabled** — in **Settings → Logging**, turn on **Enable Logging**. If it’s off, no logs are recorded and the log viewers will be empty.

See [Tools](/help/tools) (section “Where to see logs”) and [Settings](/help/settings) for more.

## API key not saved

API keys are stored in the system secure storage: **Keychain** on macOS, **Credential Manager** on Windows, **Secret Service** on Linux. If saving an account fails or the key is not persisted, use the section below for your platform.

### Linux

On Linux, the error usually means the Secret Service daemon is not available (common in WSL or minimal installs).

**What to do:**

1. Install **gnome-keyring** (e.g. `sudo apt install gnome-keyring`).
2. Before starting the app, start the secrets component:  
   `eval $(gnome-keyring-daemon --components=secrets)`  
   You can add this line to `~/.bashrc` or `~/.profile` so it runs in new shells.
3. Restart the application and try saving the API key again.

Keys are stored in the keyring in an encrypted form. For more on building and running on Linux/WSL, see [Linux build and test (WSL)](/deploy/linux-build-test-wsl).

### Windows

On Windows, keys are stored in **Credential Manager** (user credentials), not in app settings. If saving fails:

1. **Open Credential Manager** — search for “Credential Manager” or “Manage Windows credentials” in the Start menu, or run `control /name Microsoft.CredentialManager`. Check that it opens and that you can view stored credentials.
2. **Corporate or school PCs** — access to Credential Manager may be disabled by policy. If you cannot fix it yourself, ask your IT administrator whether saving credentials is allowed.
3. **Antivirus or security software** — may block access to the credential store. Temporarily adding an exception for the app (if you are allowed) can help confirm this; remove the exception if it does not help.

If the problem persists, use **Settings → Logs & Diagnostics** and check for errors when saving an account.

## More help

- **Tools** — [Tools](/help/tools) (adding, connecting, status).
- **Tool Gallery** — [Tool Gallery](/help/gallery) (safe install checks, links, origin/unlink).
- **Agents** — [Agents](/help/agents) (triggers, activate, run).
- **Configuration** — [Configuration](/help/getting-started/configuration) (storage, API port, defaults).
- **Settings** — [Settings](/help/settings) (all sections and when to use them).
- **Contact support** — [Contact](/help/contact) (email, future channels, and what details to include).
