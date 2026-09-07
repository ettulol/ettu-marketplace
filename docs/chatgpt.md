# ChatGPT setup

ChatGPT supports plugins, but repository/local-source availability depends on the surface and workspace policy. The default ettu package supplies a direct HTTP MCP configuration for Codex and Claude. For ChatGPT's documented development flow, create a registered MCP connection and build the variant below.

1. In ChatGPT, enable **Settings → Security and login → Developer mode**, if available.
2. In **Plugins**, select **+** and register **ettu** with the MCP server URL **`https://ettu.lol/mcp`**. Use OAuth and sign in with your approved ettu account. You do not need to run a server, create a tunnel or supply an API key.
3. Test “Show my ettu characters” with that connection enabled. Copy the connection's technical ID from its browser URL; it starts with `plugin_asdk_app`.
4. To include the bundled skill in a local development plugin, use `@plugin-creator` in ChatGPT Work with the checked-out repository and your registered connection ID. Ask it to import both directories under `plugins/ettu/skills/` and the root `plugins/ettu/release.json` into a personal plugin connected to that ID, preserving the relative layout and reference files. The ettu and ettu-update skills share this bundle metadata; keep it beside the skills directory. This is a local setup task; it does not require running any scripts from this repository.
5. Refresh ChatGPT, install from that local source where supported, and start a new conversation. If the publisher supplies a ChatGPT registered-connection package instead, import that package and follow its connection instructions. A ChatGPT-specific package is not a Claude package.

For team use, a workspace administrator can use OpenAI's GitHub marketplace import/sync flow, subject to its access and connection requirements. For general public discovery, submit ettu to the universal plugin directory using the **With MCP** route. Use a publisher-managed connection accessible to the intended audience; do not distribute an individual's development connection ID as though it automatically grants everyone access.

Sources: [package and registered-connection format](https://developers.openai.com/plugins/build/plugins), [connect and test](https://developers.openai.com/plugins/deploy/connect-chatgpt), [workspace plugin management](https://learn.chatgpt.com/docs/enterprise/plugin-management).

For an invitation-only account, request access through [ettu’s waitlist](https://ettu.lol/waitlist). If the site or endpoint is unreachable, connection setup must wait for the hosted service. The [MCP contract](mcp/README.md) documents the tools; the live connection determines which are available to your account.

## Updates

Ask “Check for ettu updates” after installing bundle 0.9.0 or newer. The update skill compares the installed `release.json` with the publisher's release, describes newer changes, and guides your installation surface's update flow. A workspace administrator may need to sync the marketplace. A manually imported personal plugin must be refreshed from the new bundle while preserving its registered connection ID. Installing a direct-MCP Codex/Claude package over this variant would lose that connection setup.

Version 0.12.0 uses `https://ettu.lol/mcp`. If an older registered connection still points to a development server, update its endpoint through ChatGPT’s connection controls and complete production OAuth. Replacing skills alone cannot change a registered server connection; keep its existing technical ID when updating the package. If your installation deliberately targets another server, explain the difference before changing it.

Checking does not install files. After an update, inspect the installed version and follow reload instructions. Remote service deployments do not update your locally imported skills, and a new ZIP attached to an ordinary chat does not install it.
