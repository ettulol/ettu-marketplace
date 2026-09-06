# ettu marketplace

Install ettu's MCP connection and skill together. Create characters, switch live status, claim @handles, follow users and characters, and manage story channels and private inbox conversations through your AI.

**Current status:** the source connects to `http://localhost:3001/mcp` for development. A public Git repository has not been configured yet. Before inviting other users, the maintainer must set the actual hosted HTTPS endpoint and publish this repository. Installation downloads configuration and instructions; the ettu backend must run separately.

## Install in Codex

After this repository is published, replace `YOUR_OWNER` with its GitHub owner:

```sh
codex plugin marketplace add https://github.com/YOUR_OWNER/ettu-marketplace
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

After publication, run inside Claude Code:

```text
/plugin marketplace add https://github.com/YOUR_OWNER/ettu-marketplace
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

## Repository layout

```text
.agents/plugins/marketplace.json     Codex catalog
.claude-plugin/marketplace.json      Claude catalog
plugins/ettu/
  .codex-plugin/plugin.json          Codex manifest
  .claude-plugin/plugin.json         Claude manifest
  .mcp.json                         Shared endpoint configuration
  skills/ettu/SKILL.md               Shared skill
  skills/ettu/references/channels.md Channel/inbox guidance
```

There are no backend sources, credentials, user records, generated character assets or account-specific tokens in this repository. Users authenticate with their own ettu account. The OpenAI key stays on the ettu server.

## What installation includes

This repository contains marketplace catalogs, plugin manifests, the HTTP MCP connection configuration, the ettu skill and its reference, and installation documentation. There are no install scripts, hooks, local server commands, Python dependencies or bundled credentials. Users authenticate through ettu OAuth; the service runs separately.

Maintainer-only ZIP packaging, validation and release tooling lives in the separate `ettu` application repository. Users do not need that repository or its scripts to install this plugin.
