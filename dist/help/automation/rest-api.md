# REST API

The Sami app exposes a **REST API** so you can list agents and tools, run agents, and get execution results from any HTTP client (curl, scripts, other applications). URL paths still use the `solution` segment (e.g. `/solutions`, `/solution/{id}/run`) for backward compatibility. The API runs on the **same port** as the app; the **app must be running**. There is no separate API server process.

## Base URL and port

- **Base URL:** `http://localhost:<port>/api/v1`
- **Port:** default **20222**. If that port is busy at startup, the app uses the next free port. Check **Settings → General** (API port) or the `api-port.json` file in the app data directory.
- **Example:** `http://localhost:20222/api/v1`

So all paths below are relative to that base (e.g. `GET /solutions` → `GET http://localhost:20222/api/v1/solutions`).

## Remote access

By default the API listens only on **localhost**. To call it from another computer:

1. Open **Settings → General**.
2. Enable **Allow remote API access**.
3. Restart the app.

Then use `http://<this_computer_ip>:20222/api/v1` (or the actual port). **Traffic is not encrypted.** Use only on a trusted network or put a reverse proxy with HTTPS (e.g. Caddy, nginx) in front. See [Troubleshooting](/help/troubleshooting#cli-or-api-connection-refused-or-cannot-connect).

## Example requests

Replace `AGENT_ID` with the agent id or exact name; use the port your app is actually using. To find an id in the app: in **Agents** or **Tools** enable the **ID** column (Columns button), or open the item in the editor → **Agent Info** / **Server Info** → **More**.

**List agents** *(HTTP: `GET /solutions`)*

```bash
curl -s "http://localhost:20222/api/v1/solutions" | jq
```

**Get agent status** — readiness and execution state (in the app UI: **Ready**, **Not configured**, **Error**, **Running**; some automation or query parameters may still use the slug `not_ready` for the not-configured state)

```bash
curl -s "http://localhost:20222/api/v1/solution/AGENT_ID/status" | jq
```

**Run agent** (without waiting for completion)

```bash
curl -s -X POST "http://localhost:20222/api/v1/solution/AGENT_ID/run" \
  -H "Content-Type: application/json" \
  -d '{"waitForCompletion": false}' | jq
```

**Run agent** (wait for completion; can be slow)

```bash
curl -s -X POST "http://localhost:20222/api/v1/solution/AGENT_ID/run" \
  -H "Content-Type: application/json" \
  -d '{"waitForCompletion": true, "inputParameters": {"key": "value"}}' | jq
```

**Get execution result** (use the execution id returned by the run, or from listing executions)

```bash
curl -s "http://localhost:20222/api/v1/execution/EXECUTION_ID/result" | jq
```

**List tools**

```bash
curl -s "http://localhost:20222/api/v1/tools" | jq
```

**List executions** (optional: `solutionId`, `status`, `limit`, `offset`)

```bash
curl -s "http://localhost:20222/api/v1/executions?solutionId=AGENT_ID&limit=10" | jq
```

On Windows (PowerShell) you can set a variable and use `Invoke-RestMethod`:

```powershell
$base = "http://localhost:20222/api/v1"
Invoke-RestMethod -Uri "$base/solutions" -Method Get
Invoke-RestMethod -Uri "$base/solution/MY_AGENT_ID/status" -Method Get
Invoke-RestMethod -Uri "$base/solution/MY_AGENT_ID/run" -Method Post -Body '{"waitForCompletion":false}' -ContentType "application/json"
```

## Main endpoints (overview)

| Area | Examples |
|------|----------|
| **Agents** *(paths use `solution` in the URL)* | `GET /solutions`, `GET /solutions/search?q=...`, `GET /solutions/categories`, `GET /solution/{id}`, `GET /solution/{id}/schema`, `GET /solution/{id}/status`, `GET /solution/{id}/scheduler`, `GET /solution/{id}/llm`, `GET /solution/{id}/statistics`, `POST /solution/{id}/run` |
| **Executions** | `GET /executions`, `GET /execution/{id}/result`, `GET /execution/{id}/logs`, `GET /execution/{id}/chat` |
| **Tools** | `GET /tools`, `GET /tools/search`, `GET /tool/{id}`, `GET /tool/{id}/status`, `POST /tool/{id}/connect`, `GET /tool/{id}/functions`, `GET /tool/{id}/logs` |

Path parameters: `{id}` can be the object’s id or, where supported (e.g. agent, tool), its exact name. To see the id in the app: enable the **ID** column in the Agents or Tools table (Columns button), or in the editor open **Agent Info** / **Server Info** and click **More**. Query parameters vary by endpoint (e.g. `limit`, `category`, `status`, `q` for search).

**Using names in the URL:** When you use a **name** (e.g. an agent name with spaces like `Weather Check`) in the path or in query parameters, it must be **URL-encoded**. Otherwise the path is cut at the first space and the server receives only part of the name. Encode spaces as `%20`, parentheses as `%28` and `%29`. Example: `Weather Check` → `Weather%20Check`. In query params (e.g. `?solutionId=...`) encode the value the same way. *(The query parameter name `solutionId` is unchanged in the API.)*

For a full list of endpoints, request/response shapes, and query parameters, see **docs/rest-api-design.md** in the repository.

## Security

- The API uses **HTTP only** (no TLS). Do not expose it directly to the internet or untrusted networks.
- With **Allow remote API access** on, anyone on the same network can call the API. Use a firewall, VPN, or reverse proxy with HTTPS if you need safer remote access.

For automation overview and CLI, see [Automation (CLI & API)](/help/automation) and [CLI](/help/automation/cli). For port and connection issues, see [Troubleshooting](/help/troubleshooting).
