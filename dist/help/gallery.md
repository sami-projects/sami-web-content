# Tool Gallery

The **Tool Gallery** helps you discover MCP servers from registries (public catalogs and the built-in **Sami registry**) and install them quickly. For third-party catalogs, treat entries as external content: quality and reliability can vary.

## Open the gallery

- In **Tools**, click **Browse Tool Gallery**.
- In the gallery, pick a registry, search, and open a card to see details.

## Sami registry

- **Sami registry** is a separate option in the registry list. It ships with the app and lists MCP servers curated for use with Sami (configuration is local to the install).
- Installing from here sets **Origin = Built-in** in the tool editor (**Info**).
- Some cards show short hints: **External** (may rely on provider-hosted infrastructure) and **Browser login** when sign-in uses a browser flow—check the tooltip on the card if unsure.

## Install safely (recommended flow)

1. Open the card details and check **Raw catalog JSON** (`View JSON`).
2. Review installation/runtime hints (transport type, arguments, required env values).
3. Open external links from the card when available:
   - **Repository**
   - **Homepage**
   - **View on Registry**
4. Install, then open the tool in the editor and verify settings before connecting.

If an entry requires local runtime setup (for example Python-based servers), you may need to clone/build/install dependencies manually and point Sami to valid executable paths in tool settings.

## Risk and quality hints

- Some servers may install but still fail to start on your machine.
- Registry metadata may be incomplete or outdated.
- For Archestra entries, use the Trust score as a hint, not a guarantee.

Always verify the source project and configuration before using a tool in production workflows.

## Origin and unlinking

- **Gallery** — tools installed from external registries usually show **Origin = Gallery**. To treat one as fully local, open **Info** and use **Set as My (unlink from gallery)**. That switches origin to **My** and removes the catalog binding.
- **Built-in** — tools installed from **Sami registry** show **Origin = Built-in**. There is no **Set as My** for built-in tools; you can still edit connection settings like any other tool.

## Built-in tools: delete and restore

If you delete a **built-in** tool, Sami remembers that choice: it will **not** automatically put that server back from the bundled catalog when you update the app.

To restore it:

- Open **Trash** under **Tools** and use **Restore**, or  
- Install the same entry again from **Tool Gallery** → **Sami registry**.

Either action tells Sami you want that tool again, so future app updates can refresh its bundled definition when applicable. For moving tools to Trash and permanent deletion, see [Tools](/help/tools) (section **Delete and Trash**).

## Refresh behavior

- The gallery can show **Updating...** while refreshing in the background.
- If refresh fails, you may see: **Update failed — showing cached results**.
- Some heavy registries (such as Archestra) refresh less frequently and can appear stale longer.

## Related pages

- [Tools](/help/tools) — connection settings and statuses.
- [Troubleshooting](/help/troubleshooting) — what to check when install/connect fails.
