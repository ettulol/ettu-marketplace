# ChatGPT setup

ChatGPT supports plugins, but repository/local-source availability depends on the surface and workspace policy. The default ettu package supplies a direct HTTP MCP configuration for Codex and Claude. For ChatGPT's documented development flow, create a registered MCP connection and build the variant below.

1. In ChatGPT, enable **Settings → Security and login → Developer mode**, if available.
2. In **Plugins**, select **+** and register the running ettu service's reachable HTTPS `/mcp` endpoint. Use OAuth and sign in with your ettu account. A Secure MCP Tunnel can be used for development; public submission requires HTTPS hosting.
3. Test “Show my ettu characters” with that connection enabled. Copy the connection's technical ID from its browser URL; it starts with `plugin_asdk_app`.
4. To include the bundled skill in a local development plugin, use `@plugin-creator` in ChatGPT Work with the checked-out repository and your registered connection ID. Ask it to import `plugins/ettu/skills/ettu` into a personal plugin connected to that ID, preserving its skill and reference files. This is a local setup task; it does not require running any scripts from this repository.
5. Refresh ChatGPT, install from that local source where supported, and start a new conversation. If the publisher supplies a ChatGPT registered-connection package instead, import that package and follow its connection instructions. A ChatGPT-specific package is not a Claude package.

For team use, a workspace administrator can use OpenAI's GitHub marketplace import/sync flow, subject to its access and connection requirements. For general public discovery, submit ettu to the universal plugin directory using the **With MCP** route. Use a publisher-managed connection accessible to the intended audience; do not distribute an individual's development connection ID as though it automatically grants everyone access.

Sources: [package and registered-connection format](https://developers.openai.com/plugins/build/plugins), [connect and test](https://developers.openai.com/plugins/deploy/connect-chatgpt), [workspace plugin management](https://learn.chatgpt.com/docs/enterprise/plugin-management).
