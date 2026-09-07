# ChatGPT setup

ChatGPT supports plugins, but repository/local-source availability depends on the surface and workspace policy. The default ettu package supplies a direct HTTP MCP configuration for Codex and Claude. For ChatGPT, connect to ettu and add the bundled skills using the steps below.

1. In ChatGPT, enable **Settings → Security and login → Developer mode**, if available.
2. In **Plugins**, select **+** and register **ettu** with the MCP server URL **`https://ettu.lol/mcp`**. Use OAuth and sign in with your approved ettu account. You do not need to run a server, create a tunnel or supply an API key.
3. Test “Show my ettu characters” with that connection enabled. Copy the connection's technical ID from its browser URL; it starts with `plugin_asdk_app`.
4. To include the bundled skills in a personal plugin, use `@plugin-creator` in ChatGPT Work with the checked-out repository and your registered connection ID. Ask it to import both directories under `plugins/ettu/skills/`, `plugins/ettu/assets/`, and the root `plugins/ettu/release.json` into a personal plugin connected to that ID, preserving the relative layout and reference files. The ettu and ettu-update skills share this bundle metadata; keep it beside the skills directory. This is a local setup task; it does not require running any scripts from this repository.
5. Refresh ChatGPT, install from that local source where supported, and start a new conversation. If the publisher supplies a ChatGPT registered-connection package instead, import that package and follow its connection instructions. A ChatGPT-specific package is not a Claude package.

For team use, a workspace administrator can use OpenAI's GitHub marketplace import/sync flow, subject to its access and connection requirements. For general public discovery, submit ettu to the universal plugin directory using the **With MCP** route. Use a publisher-managed connection accessible to the intended audience; do not distribute an individual's development connection ID as though it automatically grants everyone access.

Sources: [package and registered-connection format](https://developers.openai.com/plugins/build/plugins), [connect and test](https://developers.openai.com/plugins/deploy/connect-chatgpt), [workspace plugin management](https://learn.chatgpt.com/docs/enterprise/plugin-management).

For an invitation-only account, request access through [ettu’s waitlist](https://ettu.lol/waitlist). If the site or endpoint is unreachable, connection setup must wait for the hosted service. The [MCP contract](mcp/README.md) documents the tools; the live connection determines which are available to your account.

## Updates

Ask “Check for ettu updates”. The update skill compares the installed `release.json` with the publisher's release, describes newer changes, and guides your installation surface's update flow. A workspace administrator may need to sync the marketplace. A manually imported personal plugin must be refreshed from the new bundle while preserving its registered connection ID. Installing a direct-MCP Codex/Claude package over this variant would lose that connection setup.

Checking does not install files. After an update, inspect the installed version and follow reload instructions. Remote service deployments do not update your locally imported skills, and a new ZIP attached to an ordinary chat does not install it.

## ettu icon

The yellow ettu dot is available as a public 512×512 PNG at [ettu icon](https://ettu.lol/brand/pwa-512.png). Use that URL if ChatGPT's connection setup asks for a hosted image, or upload the same image if it asks for a file. The asset requires no account token.

The bundle supplies `composerIcon` and `logo` in the plugin manifest and `icon_small`/`icon_large` in each skill's `agents/openai.yaml`. The image files are included in the plugin and each skill directory; retain them when importing a personal plugin. The MCP server also advertises this URL in its initialization metadata. These are branding hints; the host controls where they appear.

If the icon does not appear after installation, reload or start a new conversation and refresh your registered connection's metadata. If that connection has its own manually configured image, update it in the connection settings as well. Published directory metadata may require the publisher's review/update flow.

References: [skill UI metadata](https://learn.chatgpt.com/docs/build-skills#optional-metadata), [plugin branding](https://developers.openai.com/plugins/build/plugins#manifest-fields), [MCP icons](https://modelcontextprotocol.io/specification/2025-11-25/basic#icons).
