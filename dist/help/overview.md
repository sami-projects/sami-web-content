# What is Sami

**Sami** is a desktop app that helps you automate everyday tasks with AI. You describe what you want done and stay in charge of how it runs—no coding background required.

You might start with something familiar: work that repeats on a schedule, a folder you want Sami to notice when something changes, or a task that needs both a clear decision and a real-world next step. The sections below introduce Sami piece by piece; follow the links at the end for step-by-step guides.

## How it works

**Agents** combine **instructions** for the model, optional **tools**, **input and output fields**, and **triggers** that decide when a run starts—everything for one workflow, in one place. You refine each agent in the editor, run it from the same screen, and come back to results and history whenever you need them.

**Tools** are how agents move from answers to actions—files, search, APIs, and whatever else an **MCP** (Model Context Protocol) server exposes as “do this for me” steps. A server may run **locally** on your machine or **remotely** over the network. Attach the tools you trust to the agents that need them. **Tool Gallery** lets you discover and install new tools from registries **without leaving the app** ([Tool Gallery](/help/gallery)).

**AI Assistant** is a chat panel in the **agent editor**—use it to describe what you want in plain language instead of adjusting every option by hand. It helps you shape that agent’s workflow and try a run together so you can see how it behaves. Nothing is sealed away: every suggestion stays visible and editable until you’re happy with it.

**LLM Accounts** are where you add **providers** and **API keys**—for example OpenAI, Anthropic, OpenRouter, and others—so each agent can run with the account and model you choose.

**Settings** rounds up app-wide preferences—the folder Sami uses on disk, limits for agents and MCP connections, backup and logging, proxy when your network needs it, and the model for the **AI Assistant** (**Settings → AI Assistant**). That assistant model is separate from the model each agent uses when it runs.

**Your data** lives in **one folder you choose**: agents, tools, and backups together. **API keys and other sensitive credentials** are stored in your **operating system’s secure credential store**, not as readable text inside your data folder. Sami runs on your machine; LLM requests and remote tools still use the network when needed—that’s how cloud models and integrations work. What you keep is **clarity and control**: what is stored where, what is connected, and how your agents are set up to run.

## Where to go next

- [Getting Started](/help/getting-started) — first agent and basic setup.
- [Agents](/help/agents) — triggers, status, and how runs work.
- [Tools](/help/tools) — transports, connection, troubleshooting.
- [Tool Gallery](/help/gallery) — discover and install tools safely.
- [LLM Accounts](/help/llm-accounts) — providers and models.
- [Settings](/help/settings) — storage, limits, MCP, backup, logging, assistant model.
- [AI Assistant](/help/ai-assistant) — using the assistant in the editor.
- [Automation (CLI & API)](/help/automation) — run agents and query status from scripts or the REST API while the app is running.
- [Contact](/help/contact) — how to reach us and what to include.

**References:** [Model Context Protocol](https://modelcontextprotocol.io) · [MCP on GitHub](https://github.com/modelcontextprotocol) · [Tools schema (advanced)](/help/schemas/sami-tools-full.schema.json) · [Agents schema (advanced)](/help/schemas/sami-agents-full.schema.json)
