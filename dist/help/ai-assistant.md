# AI Assistant

The AI Assistant helps you configure and manage agents by chat instead of clicking through every form. Open it from the **agent editor** (robot icon in the toolbar). It works in the context of the agent you are editing and has access to the same data and actions as the UI — but with one important limit: it can **edit only the current agent** (see below).

## What the assistant can do

- **Edit the current agent** — the one open in the editor. It can change the prompt (instructions), add or remove tools, edit input and output fields, set triggers, resources, LLM model, execution settings, and activate or deactivate the scheduler. You describe what you want; the assistant applies the changes.
- **Run and monitor runs** — run the current agent or **any other agent** by name or id (with optional input parameters). It can wait for completion or run in the background. It has access to **execution history**: list runs, open a specific run’s **result**, **logs** (by phase and level), and **chat** (messages and tool calls). So you can ask “run this”, “show the last run”, “what went wrong in execution X?” and get real data.
- **Browse agents and tools** — list or search agents and tools, get full details of any agent (read-only). Useful to attach a tool to the current agent, run another agent, or compare settings. It can also see tool status, connection logs, and call a tool function (e.g. for testing).

## What the assistant cannot do

- **Edit another agent** — it cannot change an agent that is not currently open. There is no “edit agent X” by name or id. To change another agent, open it in the editor first; then it becomes the “current” one and the assistant can edit it. It *can* read any agent (view prompt, tools, triggers) and run any agent; only **editing** is limited to the current agent.

## Where to open it

- Open or create an agent in **Agents**.
- In the agent editor toolbar, click the **AI Assistant** (robot) button. The assistant panel opens; you can move and resize it.
- The conversation is about this agent. Phrases like “the prompt”, “add a tool”, “run it” refer to the current agent.

## Settings

The model used by the assistant (and its options) is configured in **Settings → AI Assistant**. That is separate from the model chosen for the agent’s execution. So you can use one model for the assistant and another for running the agent.

## Saving and rollback

When you send your **first message** that might change the agent (and there are unsaved changes), the app **saves the agent automatically** before sending. That creates a checkpoint so you can undo later.

- **In the chat** — you can roll back to a previous message. The assistant can restore the agent to the state at that message (or only undo the chat and keep the current agent).
- **In the Changes panel** — open it from the agent editor side panel (the **Changes** button with history icon). The list shows saved versions; versions saved by the assistant are marked with a **robot icon** (tooltip: "Changed by AI Assistant"). You can load any version from there.

So you can safely try changes in chat and revert either from the conversation or from the version list.

## Tips

- Be specific: “Add the Summarizer tool to this agent” works better than “add some tool”.
- After the assistant makes changes, review them in the editor and save when you're happy. The assistant does not save after every change; the one automatic save is for the rollback checkpoint (see above).
- For more on agents and tools, see [Agents](/help/agents) and [Tools](/help/tools).
