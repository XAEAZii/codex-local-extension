# CODEX-LOCAL 0.5.0-local.9

Prebuilt Linux x86-64 VS Code workspace extension for a self-hosted Responses API provider. It is intended to run in a remote Linux extension host and does not require an OpenAI or ChatGPT account.

This repository intentionally contains release documentation only. The installable VSIX is published as a GitHub Release asset because it is larger than GitHub's normal Git file limit.

## Supported setup

```text
Windows
└── VS Code + Microsoft Remote - SSH
    └── Remote Linux x86-64 host / VS Code Server
        └── CODEX-LOCAL Linux VSIX
```

The Windows CODEX-LOCAL package is not required for this setup. CODEX-LOCAL runs on the remote Linux host; the Windows VS Code client displays its user interface.

Requirements:

- VS Code 1.96.2 or newer on Windows;
- Microsoft Remote - SSH extension;
- a Linux x86-64 remote host capable of starting the bundled runtime (the current build requires glibc 2.39);
- a self-hosted provider implementing `POST /v1/responses`.

## Install on the remote Linux host

While signed in to GitHub, download the `.vsix` and `SHA256SUMS` assets from the private `v0.5.0-local.9` release. Copy both files to the remote Linux host, connect using VS Code Remote - SSH, and run in its integrated terminal:

```bash
VERSION=0.5.0-local.9
sha256sum -c SHA256SUMS
code --install-extension "codex-local-${VERSION}-linux-x64.vsix" --force
code --list-extensions --show-versions | grep '^xaeazii.codex-local@'
```

In VS Code run `Developer: Reload Window`, open CODEX-LOCAL, and configure the provider once.

The bundled runtime is checked before the Codex engine starts. An incompatible architecture, glibc, dynamic loader, or missing shared library produces a blocking error instead of a broken session.

The provider configuration is stored on the remote Linux host at:

```text
~/.codex-local-extension-home/provider.json
```

It is independent of the Windows VS Code profile, Settings Sync, and the currently opened workspace. The generated Codex configuration is stored in the same directory as `config.toml`.

## Update

Download the newer Linux x64 VSIX from Releases and run the same `code --install-extension ... --force` command from the connected remote terminal.

## Uninstall

Run on the remote Linux host:

```bash
code --uninstall-extension xaeazii.codex-local
```

## Local-only behavior

Automatic OpenAI/ChatGPT discovery, hosted tools, update checks, telemetry, feedback, and remote-control features are disabled. Traffic is sent only to the explicitly configured self-hosted provider and user-configured MCP servers or commands. The provider may be addressed by a loopback, LAN, routed-network, or remote hostname/IP and is reached through an authenticated loopback relay on the extension host.
