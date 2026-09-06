# ettu plugin

This folder contains the ettu and ettu-update skills, versioned release metadata, and MCP connection configuration. It supports character interviews and version history, status GIFs, permanent universes, main character selection, @handles, follows, story channels, staff proposals and private inbox conversations. Installation does not run the backend or generate artwork.

For Codex and Claude Code, install **ettu** from the **ettu-marketplace** catalog. The marketplace repository README contains installation commands. Each user signs in with their own ettu account; the image-generation API key stays on the server.

After installation, start a new conversation and ask “Show my ettu characters.” For an explicit Claude Code skill invocation, use `/ettu:ettu`. The bundled skill supplies ettu workflows across projects where the plugin is enabled. It does not make generic character brainstorming publish automatically.

In a built ZIP, inspect `CONNECTION.txt` for the endpoint and package type. The ordinary package has Codex and Claude manifests plus `.mcp.json`. The optional ChatGPT package has an OpenAI manifest and `.app.json` referencing an existing registered connection; it is not a Claude package. A ZIP attached to a normal conversation is not an installed MCP connection.

Source development currently uses localhost. Public use requires a hosted endpoint or a supported development tunnel. The repository's `docs/chatgpt.md` explains ChatGPT registration. Installation requires no Python scripts or local server process. Neither package includes account tokens, backend source or private character data.

## Updates

Ask “Check for ettu updates”, or use `/ettu:ettu-update` in Claude Code. The update skill reads this installed bundle's [release.json](release.json), checks the latest release, summarizes newer changes and guides your host's updater. The read-only MCP tool `check_ettu_update` can perform the version comparison; older servers are supported through a direct metadata lookup. Network or permission failures are reported as unverified checks.

The bundle version is 0.10.2. Both skills, both client manifests and `release.json` update together through the plugin manager. The remote service updates separately. Checking is not installing; after installation, a reload or new conversation may be needed. See [host-specific instructions](skills/ettu-update/references/update-host.md).

## Episode videos

Ask your AI to animate an episode after adding scenes and published cast. The director can request a new video, inspect generation progress and previous versions, and publish a selected completed video. Episodes start as drafts; publishing a channel does not expose unfinished episodes. The channel page provides episode navigation, playback and team-only video history. See [episode video workflows](skills/ettu/references/channels.md#animate-and-publish-episodes).
