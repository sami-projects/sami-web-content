# LLM Accounts

**LLM Accounts** are where you add and manage API keys and default models for each LLM provider. Agents and the AI Assistant use these accounts to call the models. You need at least one account (and usually one per provider you use) before an agent can run.

## Why accounts exist

Each **account** ties together a **provider** (e.g. OpenAI, Anthropic), your **API key** (or other auth), and an optional **default model**. When you edit an agent, you choose which account and which model to use for that agent’s runs. The AI Assistant uses its own model, set in **Settings → AI Assistant**, which can be a different account and model. So you can have several accounts (e.g. one for OpenAI, one for Yandex) and pick the right one per agent or for the assistant.

## Adding an account

1. Open **LLM Accounts** from the sidebar (or from Settings).
2. Click **Add** and choose a **provider**.
3. Enter your **API key** (or follow the provider-specific flow).
4. Optional:
   - **Default model** — after saving the key, you can load the list of models and pick a default. The agent can still override and choose another model for that account.
   - **Enabled** — turn off to hide the account from agent and assistant choices without deleting it.

You can **Set as default** (radio in the table) so new agents or dropdowns suggest this account first. Default account is a convenience only; each agent explicitly chooses its account and model in the editor.

## Security

The app writes and reads keys only through this store. Settings and agent files never contain API keys; when you edit an account, the key is loaded from the store for the form and, if you change it, written back to the store. So keys stay off disk in readable form and are protected by the same mechanisms as other system credentials (e.g. login keychain lock, user session).

## Where the agent picks the model

When editing an agent, open the **LLM** section in the side panel. There you choose:

- **Account** — which LLM account to use.
- **Model** — which model from that account (or override the default).

If no account is selected or the chosen account has no valid model, the agent may fail at run time or appear misconfigured in the editor. Add or fix accounts in **LLM Accounts**, then reselect in the agent.

## Related settings

- **Settings → AI Assistant** — which account and model the in-editor AI Assistant uses. Separate from the model used when you run an agent.

For your first agent, see [Your First Agent](/help/getting-started/first-agent). For execution and connection issues, see [Troubleshooting](/help/troubleshooting).
