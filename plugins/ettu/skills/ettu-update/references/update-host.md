# Update using the installed host

First identify how THIS plugin was installed: marketplace, explicit local directory, ZIP, or managed workspace. Follow that source. Commands below use this distribution's marketplace name, `ettu-marketplace`; confirm the installed source before using them.

## Codex CLI or Codex app with a local CLI

For a configured Git marketplace, the supported CLI flow is:

```sh
codex plugin marketplace upgrade ettu-marketplace
codex plugin add ettu@ettu-marketplace
```

The first command refreshes the marketplace snapshot; the second installs its plugin. Check `codex plugin --help` if the installed CLI uses a different command surface. Inspect installed details through the plugin manager or `codex plugin list`; do not confuse an available catalog version with the installed copy. Start a new conversation after updating so it loads the new skills/tools.

For an explicitly local marketplace, the owner must first update that source directory, then install ettu from it. Refreshing a remote catalog cannot update a different local source. Preserve local changes; do not reset a checkout. Do not use uninstall/remove as the normal upgrade flow.

For app-managed or workspace-managed plugins without local CLI access, use the plugin manager's available update flow or ask the workspace administrator to sync/update its source. Do not invent a universal Codex auto-update setting.

## Claude Code

For an installed marketplace plugin, run inside Claude Code:

```text
/plugin marketplace update ettu-marketplace
/plugin update ettu@ettu-marketplace
/reload-plugins
```

Use the same install scope as the existing plugin. Follow the host's reload/restart message if `/reload-plugins` is unavailable. For future automatic updates, users can open `/plugin`, select Marketplaces → ettu-marketplace → Enable auto-update. Third-party marketplaces default to auto-update off. Installing updates on disk and reloading the active session are separate steps.

A session started with `claude --plugin-dir ...` uses that local directory, not a marketplace installation. Update the actual source with its owner and reload/restart; do not install a duplicate marketplace copy.

## Claude desktop or ChatGPT

Use the plugin's installation surface. A workspace marketplace installation is updated/synced through that marketplace and may require an administrator. For a manually uploaded plugin ZIP, obtain the publisher's matching new ZIP and replace/update the installed plugin through the supported UI, then follow its reload instructions. An attachment in an ordinary conversation is not an installed plugin update.

ChatGPT registered-connection packages must keep the existing registered connection: don't replace them with the direct-MCP Codex/Claude package or invent a new app ID. If the current UI cannot update that installation, explain who must do it and which release they need rather than claiming completion.

## Remote MCP only

Users who added only the HTTP MCP URL have no ettu skill bundle to update. Server behavior changes arrive on the server. If tools are missing or stale, refresh/reconnect using the host's MCP controls or start a new session. Installing the optional plugin is a separate action, not required for every server release.

References: [OpenAI plugins](https://learn.chatgpt.com/docs/plugins), [Claude update/reload and auto-updates](https://code.claude.com/docs/en/discover-plugins), [Claude version detection](https://code.claude.com/docs/en/plugin-marketplaces#version-resolution-and-release-channels), [MCP tool discovery](https://modelcontextprotocol.io/specification/2025-11-25/server/tools).
