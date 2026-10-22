# CODEX-LOCAL 0.6.0-local.9

Linux x64 VS Code extension powered by the bundled Codex CLI, using your own Responses API provider. Supports coding, file edits, terminal commands, and custom `web_search` and `web_read_url` tools.

**Built-in OpenAI/ChatGPT communication is disabled and blocked**, including telemetry, hosted tools, and update checks. No OpenAI account is required. Web search uses its own bundled worker and accesses the public web directly.

MCP server connections are available but untested and may not work fully yet.

## Install

Download the Linux or WIN VSIX from this release and run in VS Code's integrated terminal (on the remote Linux host when using Remote - SSH):

```bash
Windows:
code --install-extension .\codex-local-0.6.0-local.11-win32-x64.vsix --force

Linux:
code --install-extension ./codex-local-0.6.0-local.9-linux-x64.vsix --force
```

Restart VS Code, open CODEX-LOCAL, and configure your local provider with compatible /responses API endpoint.
