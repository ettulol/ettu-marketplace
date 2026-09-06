# ettu marketplace

Install ettu's MCP connection and skills together. Create characters, switch live status, claim @handles, follow users and characters, and manage story channels and private inbox conversations through your AI.

**Current status:** the source connects to `http://localhost:3001/mcp` for development. The distribution repository is [ettulol/ettu-marketplace](https://github.com/ettulol/ettu-marketplace). Before inviting other users, the maintainer must set the actual hosted HTTPS endpoint and publish the release files. Installation downloads configuration and instructions; the ettu backend must run separately.

## Install in Codex

Run:

```sh
codex plugin marketplace add https://github.com/ettulol/ettu-marketplace
codex plugin add ettu@ettu-marketplace
```

If Codex asks for a marketplace repository URL, provide the same **repository URL**, then install **ettu** from **ettu-marketplace**. Do not provide a raw JSON URL, a link to `plugins/ettu`, or the MCP service URL in that repository field.

For this local checkout:

```sh
codex plugin marketplace add ~/git/ettu-marketplace
codex plugin add ettu@ettu-marketplace
```

Start a new Codex conversation after installing. Complete ettu OAuth sign-in when prompted. Ask “Show my ettu characters” as a read-only check. The skill is bundled and available across projects on the host where the plugin is installed; no per-project skill copy is needed. Enable it on other hosts separately. Generic character brainstorming does not request publication on ettu.

The installed Codex CLI provides these `plugin marketplace add` and `plugin add` commands. For the plugin browser, open `/plugins`. See [OpenAI plugin usage](https://learn.chatgpt.com/docs/plugins).

## Install in Claude Code

Run inside Claude Code:

```text
/plugin marketplace add https://github.com/ettulol/ettu-marketplace
/plugin install ettu@ettu-marketplace
```

Choose **user** scope to use it across your projects. Follow the install summary if it asks you to reload plugins, or start a new session. Open `/mcp` and authenticate the ettu connection. Ask “Show my ettu characters”; `/ettu:ettu` explicitly invokes the bundled skill.

For local testing, replace the repository URL with the absolute path to this checkout, or load only this session:

```sh
claude --plugin-dir "$HOME/git/ettu-marketplace/plugins/ettu"
```

The two catalogs point to the same `plugins/ettu` directory. Claude reads `.claude-plugin/marketplace.json`; Codex reads `.agents/plugins/marketplace.json`. See [Claude marketplace documentation](https://code.claude.com/docs/en/plugin-marketplaces).

## Claude desktop and ChatGPT

In Claude, open **Customize → Plugins → Personal plugins + → Add marketplace → Add from a repository**, paste the GitHub repository URL, then install ettu. You can also upload the **plugin ZIP** from a release; GitHub's archive of the whole marketplace is not the same package. Complete the connector sign-in. Cloud connections need the hosted HTTPS endpoint. See [Claude installation and marketplace setup](https://support.claude.com/en/articles/13837440-use-plugins-in-claude).

ChatGPT's documented MCP plugin development flow first registers the running service, then connects the skill to that registered connection. A Git URL or ZIP attached to an ordinary chat does not install a connection. Follow [ChatGPT setup](docs/chatgpt.md). OpenAI workspace GitHub marketplace import and public directory submission are separate distribution paths; a GitHub push alone does not publish a universal-directory listing.

## Check for updates

Ask **“Check for ettu updates”**. The bundled `ettu-update` skill reports your installed version, the latest available version, relevant changes, and how to update in your AI app. In Claude Code, `/ettu:ettu-update` invokes it explicitly. Version **0.9.0** introduces this skill; users of older bundles need one ordinary plugin update to receive it.

The remote MCP service updates on the server. Local skills and connection configuration update when your host installs a new plugin bundle, including its `release.json`. Refreshing the marketplace catalog alone is not the same as updating the installed plugin. Checking is read-only; it does not automatically install anything. An unreachable release source is reported as an unverified check.

For an existing Codex Git marketplace installation:

```sh
codex plugin marketplace upgrade ettu-marketplace
codex plugin add ettu@ettu-marketplace
```

For Claude Code:

```text
/plugin marketplace update ettu-marketplace
/plugin update ettu@ettu-marketplace
/reload-plugins
```

Start a new Codex conversation, or follow your host's reload instructions. Keep your existing installation source and scope. For local development, update that local source first; for managed workspaces or uploaded ZIPs, use the installation surface's update process. See the [host update guide](plugins/ettu/skills/ettu-update/references/update-host.md).

The installed `release.json` records the version on disk. Its `latest_manifest_url` checks this repository's default branch for the latest release, using the GitHub contents API with `Accept: application/vnd.github.raw+json`. Release notes travel with each bundle so older installations can explain what changed. No installer scripts or GitHub tokens are needed.

## Repository layout

```text
.agents/plugins/marketplace.json     Codex catalog
.claude-plugin/marketplace.json      Claude catalog
plugins/ettu/
  .codex-plugin/plugin.json          Codex manifest
  .claude-plugin/plugin.json         Claude manifest
  .mcp.json                         Shared endpoint configuration
  release.json                      Bundle version and release notes
  skills/ettu-update/SKILL.md        Update check and guidance
  skills/ettu-update/references/update-host.md
  skills/ettu/SKILL.md               Character and channel skill
  skills/ettu/references/channels.md Channel/inbox guidance
```

There are no backend sources, credentials, user records, generated character assets or account-specific tokens in this repository. Users authenticate with their own ettu account. The OpenAI key stays on the ettu server.

## What installation includes

This repository contains marketplace catalogs, plugin manifests, the HTTP MCP connection configuration, the ettu and ettu-update skills and their references, release metadata, and installation documentation. There are no install scripts, hooks, local server commands, Python dependencies or bundled credentials. Users authenticate through ettu OAuth; the service runs separately.

Maintainer-only ZIP packaging, validation and release tooling lives in the separate `ettu` application repository. Users do not need that repository or its scripts to install this plugin.
