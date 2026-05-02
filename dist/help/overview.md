# Overview

**Sami** helps you create and run automated workflows that use LLM models and MCP (Model Context Protocol) tools. You configure tools, build agents (prompt + tools + inputs), and run them from the app or from scripts.

## What you can do

- **Agents** — create and edit workflows: instructions (prompt), attached MCP tools, input/output fields, and triggers (e.g. run on a schedule).
- **Tools** — add and manage MCP servers (stdio or SSE); agents use these tools when they run.
- **AI Assistant** — in the agent editor, open the assistant to configure the current agent by chat: change the prompt, add tools, set triggers, run and inspect results.
- **LLM Accounts** — add API keys and models (OpenAI, Anthropic, Yandex, OpenRouter, etc.); each agent can use a chosen account and model.
- **Settings** — data directory, API port, MCP/execution limits, backup, logging, proxy. The assistant’s model is set under **Settings → AI Assistant**.

All data (tools, agents, backups) lives in one configurable directory.

## Main sections (sidebar)

- **Agents** — list and open agents; create, edit, run.
- **Tools** — list and open MCP tools; add, connect, configure.
- **LLM Accounts** — manage LLM accounts and models.
- **Settings** — application and assistant settings.
- **Help** — this documentation.

You can also run agents and query status from the **command line** and **REST API** when the app is running. See [Automation (CLI & API)](/help/automation).

## Next steps

- [Getting Started](/help/getting-started) — first agent and basic configuration.
- [Agents](/help/agents) — how agents and the scheduler work.
- [Tools](/help/tools) — adding and connecting MCP tools.
- [Tool Gallery](/help/gallery) — discover tools from registries and install safely.
- [LLM Accounts](/help/llm-accounts) — adding API keys and choosing models.
- [AI Assistant](/help/ai-assistant) — using the assistant in the agent editor.
- [Automation (CLI & API)](/help/automation) — running agents and querying status from the command line or REST API.
- [Contact](/help/contact) — support channels and what to include in a request.

## Useful links

- [Model Context Protocol](https://modelcontextprotocol.io)
- [MCP GitHub](https://github.com/modelcontextprotocol)
- [Contact support](/help/contact)
- [Tools full schema (advanced)](/help/schemas/sami-tools-full.schema.json)
- [Agents full schema (advanced)](/help/schemas/sami-agents-full.schema.json)
