# CODEX-LOCAL 0.5.0-local.8

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
- a glibc-based Linux x86-64 remote host;
- a self-hosted provider implementing `POST /v1/responses`.

## Install on the remote Linux host

First connect to the Linux host using VS Code Remote - SSH. Then open an integrated terminal in that remote window and run:

```bash
VERSION=0.5.0-local.8
RELEASE_URL="https://github.com/XAEAZii/codex-local-extension/releases/download/v${VERSION}"

curl -fLO "${RELEASE_URL}/codex-local-${VERSION}-linux-x64.vsix"
curl -fLO "${RELEASE_URL}/SHA256SUMS"

sha256sum -c SHA256SUMS
code --install-extension "codex-local-${VERSION}-linux-x64.vsix" --force
code --list-extensions --show-versions | grep '^xaeazii.codex-local@'
```

In VS Code run `Developer: Reload Window`, open CODEX-LOCAL, and configure the provider once.

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

Automatic OpenAI/ChatGPT discovery, hosted tools, update checks, telemetry, feedback, and remote-control features are disabled. Traffic is sent only to the explicitly configured self-hosted provider and user-configured MCP servers or commands.
