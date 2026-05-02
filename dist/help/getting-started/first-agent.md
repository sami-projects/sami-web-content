# Your First Agent

An agent is a workflow: a prompt (instructions for the LLM), optional MCP tools, and input/output fields. You create it in the editor, then run it from the app or from the CLI/API when the app is running.

## Steps

1. **Optional: add an MCP tool**  
   If the agent should use tools, go to **Tools**, add a tool (e.g. from an MCP server), and make sure it shows as **Ready**. You can also create an agent with no tools and add them later.

2. **Create a new agent**  
   In **Agents**, click the **Add** button (➕) in the toolbar. The agent editor opens with a new, unsaved agent. Give it a **name** and, if you like, a **category** (location). New agents use the **Default Agent Location** from Settings unless you choose another.

3. **Set the prompt**  
   In the editor, write the **Instructions** (prompt) that describe what the agent should do. You can add **input fields** and reference them in the prompt with placeholders: type **/** for autocomplete or double‑click a field in the **Input/Output** panel. See [Prompt and placeholders](/help/prompt-placeholders) for the full format.

4. **Attach tools (optional)**  
   In the side panel, open **Tools** and add the MCP tools this agent is allowed to use. Without tools, the agent only calls the LLM.

5. **Choose the model**  
   In the editor, set the **LLM** account and model for this agent. You need at least one **LLM account** configured in **LLM Accounts** or **Settings**.

6. **Run**  
   Use the **Run** (play) action. Fill any required inputs and check the result in the test panel or execution history.

**Tip:** You can use the **AI Assistant** (robot icon in the editor toolbar) to configure the agent by chat: e.g. "Add the Summarizer tool" or "Set the prompt to …". See [AI Assistant](/help/ai-assistant).

For more, see [Agents](/help/agents), [Prompt and placeholders](/help/prompt-placeholders), and [Tools](/help/tools).
