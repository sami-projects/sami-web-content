# Agents

An agent is a workflow: **instructions** (prompt) for the LLM, optional **MCP tools**, **input and output fields**, and **triggers** (when to run). You edit it in the agent editor, then run it manually or on a schedule.

## Editor and side panel

The editor has a main area (name, **Instructions** prompt, and optional panels) and a **side panel** with sections. The prompt can contain **placeholders** (inputs, outputs, tools, resources); they are shown as chips in the editor and replaced with values or markers when the agent runs. See [Prompt and placeholders](/help/prompt-placeholders) for format and how to insert them.

The **side panel** includes: **Agent Info** (status, last run), **Triggers**, **Input/Output**, **Tools**, **Subagents** (nested), **Resources**, **LLM** (model choice). Use **Settings** for agent-specific limits and pre/post actions; **Changes** for version history; **Results** for execution history (runs and logs).

## Status: Ready, Not configured, Error

In the list and in the editor, each agent has a status:

- **Ready** — has a name, instructions (prompt), and at least one trigger. You can run it.
- **Not configured** — missing name, prompt, or triggers (or every trigger is disabled). Add or enable them in the editor.
- **Error** — the agent is activated (see below) but the last run failed; the error is stored and shown until the next successful run or you deactivate.
- **Executing** — a run is in progress.

So if you see **Not configured**, open the agent and complete the required fields and at least one enabled trigger.

## Triggers

Triggers define when the agent runs:

- **On demand** — run manually only (Run button or CLI/API). Every agent has at least one trigger; new agents get an On Demand trigger by default.
- **Schedule** — at fixed times: hourly, daily, weekly, monthly, or a custom cron expression.
- **Interval** — every N minutes, hours, or days (with optional start time and mode).
- **File system** — when files or folders change (e.g. create, update).

Add or edit triggers in the editor → **Triggers** section. You can enable or disable individual triggers.

## Activate and scheduled runs

If the agent has **Schedule**, **Interval**, or **File system** triggers, they run automatically only when the agent is **Activated**. In the agents list (or in the editor), use **Activate** to turn the scheduler on for this agent; use **Deactivate** to stop automatic runs. The side panel shows **Activated** or **Not Activated** and **Last Executed**.

If the agent has **only On demand** triggers, you don’t need to activate; just use **Run** when you want to execute.

**Tip:** Before activating, configure triggers and save. If you add triggers later, activate again if needed (the app may prompt you to activate when you add a scheduled trigger).

## Running and results

- **Run** — from the agents list or from the editor. Fill any required input fields; the app calls the LLM and, if configured, the MCP tools, and shows the result.
- **Results** — in the editor side panel, open **Results** to see execution history: runs, logs, and chat for each execution. You can open a past run to see output and details.

## Pre- and post-execution

You can run **one action before** the agent (pre-execution) and **a chain of actions after** it (post-execution). Configure them in the agent editor: open **Settings** (gear in the side panel) and use the **Pre-execution** and **Post-execution** blocks.

- **Pre-execution** — a single step: run an external command or script (e.g. prepare data, check env) before the main agent runs. You can pass execution id, input parameters, and other context via environment variables. If the step fails and is set to abort, the agent is not run.
- **Post-execution** — a list of steps that run after the agent finishes. Each step can be:
  - **Script** — run a command (e.g. notify, cleanup).
  - **Agent** — run **another agent** (nested subagent), passing the current result or inputs into it (input mapping). So you can chain agents: e.g. “Summarize” runs, then a post-step runs “Save to file” with the summary as input.
  - **Tool** — call an MCP tool with arguments (e.g. send result somewhere).

For each post-step you choose when it runs: always, only on success, or only on error; and what to do on failure (abort the chain, continue, or warn). Inputs to a post-step agent or tool can use placeholders such as `$AGENT_RESULT`, `$AGENT_STATUS`, `$AGENT_INPUT_PARAMS`, and similar, so the next step sees the outcome of the main run. This is how you build **pipelines** of several agents or mix agents with scripts and tools.

## Organizing

Use **categories** (locations) to group agents in the sidebar. You can export/import agents for backup or sharing. When exporting, you can enable **Anonymize sensitive data** so that values in env-like fields and in properties with names like token, password, or apiKey are replaced with `[ANONYMIZED]` in the JSON. The **Changes** panel in the editor lists saved versions of the agent (including versions saved by the [AI Assistant](/help/ai-assistant)); you can load any version from there.

### Sidebar: category order

With **Agents** expanded in the main sidebar, you can **drag** categories to set a custom order. For a long list, switch to **alphabetical** order: **hover the chevron** next to **Agents** (a small icon appears briefly; you can move the pointer to it). The choice is stored in your browser profile on this machine. The **Category** field in the agent editor, copy/move dialogs, and agent pickers use the **same** order. Alphabetical mode does **not** discard your custom order; switch back to manual to see it again.

### Advanced: full Sami JSON schema

For programmatic generation and validation of the full Sami agents file format (advanced use), see:

- [/help/schemas/sami-agents-full.schema.json](/help/schemas/sami-agents-full.schema.json)

For a first-time setup, see [Your First Agent](/help/getting-started/first-agent). For placeholder syntax and the prompt editor, see [Prompt and placeholders](/help/prompt-placeholders). For MCP tools, see [Tools](/help/tools).
