 [Skip to content](#_top)

[![](/docs/_astro/logo-dark.DOStV66V.svg) ![](/docs/_astro/logo-light.B0yzR0O5.svg)  OpenCode](../docs.md)

[app.header.home](/)[app.header.docs](../docs.md)

Search  `CtrlK`   

Cancel

       

- [Intro](../docs.md)
- [Config](config.md)
- [Providers](providers.md)
- [Network](network.md)
- [Enterprise](enterprise.md)
- [Troubleshooting](troubleshooting.md)
- [Windows](windows-wsl.md)
- Usage

   
  - [Go](go.md)
  - [TUI](tui.md)
  - [CLI](cli.md)
  - [Web](web.md)
  - [IDE](ide.md)
  - [Zen](zen.md)
  - [Share](share.md)
  - [GitHub](github.md)
  - [GitLab](gitlab.md)
- Configure

   
  - [Tools](tools.md)
  - [Rules](rules.md)
  - [Agents](agents.md)
  - [Models](models.md)
  - [Themes](themes.md)
  - [Keybinds](keybinds.md)
  - [Commands](commands.md)
  - [Formatters](formatters.md)
  - [Permissions](permissions.md)
  - [LSP Servers](lsp.md)
  - [MCP servers](mcp-servers.md)
  - [ACP Support](acp.md)
  - [Agent Skills](skills.md)
  - [Custom Tools](custom-tools.md)
- Develop

   
  - [SDK](sdk.md)
  - [Server](server.md)
  - [Plugins](plugins.md)
  - [Ecosystem](ecosystem.md)

[GitHub](https://github.com/anomalyco/opencode)[Discord](https://opencode.ai/discord)

  Select theme   DarkLightAuto      Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

On this page

- [Overview](#_top)
- [Configure](#configure) 
  - [Zed](#zed)
  - [JetBrains IDEs](#jetbrains-ides)
  - [Avante.nvim](#avantenvim)
  - [CodeCompanion.nvim](#codecompanionnvim)
- [Support](#support)

## On this page

- [Overview](#_top)
- [Configure](#configure) 
  - [Zed](#zed)
  - [JetBrains IDEs](#jetbrains-ides)
  - [Avante.nvim](#avantenvim)
  - [CodeCompanion.nvim](#codecompanionnvim)
- [Support](#support)

# ACP Support

Use OpenCode in any ACP-compatible editor.

OpenCode supports the [Agent Client Protocol](https://agentclientprotocol.com) or (ACP), allowing you to use it directly in compatible editors and IDEs.

Tip

For a list of editors and tools that support ACP, check out the [ACP progress report](https://zed.dev/blog/acp-progress-report#available-now).

ACP is an open protocol that standardizes communication between code editors and AI coding agents.

---

## [Configure](#configure)

To use OpenCode via ACP, configure your editor to run the `opencode acp` command.

The command starts OpenCode as an ACP-compatible subprocess that communicates with your editor over JSON-RPC via stdio.

Below are examples for popular editors that support ACP.

---

### [Zed](#zed)

Add to your [Zed](https://zed.dev) configuration (`~/.config/zed/settings.json`):

~/.config/zed/settings.json

```
{



"agent_servers": {



"OpenCode": {



"command": "opencode",



"args": ["acp"]



}



}



}
```

To open it, use the `agent: new thread` action in the **Command Palette**.

You can also bind a keyboard shortcut by editing your `keymap.json`:

keymap.json

```
[



{



"bindings": {



"cmd-alt-o": [



"agent::NewExternalAgentThread",



{



"agent": {



"custom": {



"name": "OpenCode",



"command": {



"command": "opencode",



"args": ["acp"]



}



}



}



}



]



}



}



]
```

---

### [JetBrains IDEs](#jetbrains-ides)

Add to your [JetBrains IDE](https://www.jetbrains.com/) acp.json according to the [documentation](https://www.jetbrains.com/help/ai-assistant/acp.html):

acp.json

```
{



"agent_servers": {



"OpenCode": {



"command": "/absolute/path/bin/opencode",



"args": ["acp"]



}



}



}
```

To open it, use the new âOpenCodeâ agent in the AI Chat agent selector.

---

### [Avante.nvim](#avantenvim)

Add to your [Avante.nvim](https://github.com/yetone/avante.nvim) configuration:

```
{



acp_providers = {



["opencode"] = {



command = "opencode",



args = { "acp" }



}



}



}
```

If you need to pass environment variables:

```
{



acp_providers = {



["opencode"] = {



command = "opencode",



args = { "acp" },



env = {



OPENCODE_API_KEY = os.getenv("OPENCODE_API_KEY")



}



}



}



}
```

---

### [CodeCompanion.nvim](#codecompanionnvim)

To use OpenCode as an ACP agent in [CodeCompanion.nvim](https://github.com/olimorris/codecompanion.nvim), add the following to your Neovim config:

```
require("codecompanion").setup({



interactions = {



chat = {



adapter = {



name = "opencode",



model = "claude-sonnet-4",



},



},



},



})
```

This config sets up CodeCompanion to use OpenCode as the ACP agent for chat.

If you need to pass environment variables (like `OPENCODE_API_KEY`), refer to [Configuring Adapters: Environment Variables](https://codecompanion.olimorris.dev/getting-started#setting-an-api-key) in the CodeCompanion.nvim documentation for full details.

## [Support](#support)

OpenCode works the same via ACP as it does in the terminal. All features are supported:

Note

Some built-in slash commands like `/undo` and `/redo` are currently unsupported.

- Built-in tools (file operations, terminal commands, etc.)
- Custom tools and slash commands
- MCP servers configured in your OpenCode config
- Project-specific rules from `AGENTS.md`
- Custom formatters and linters
- Agents and permissions system

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/acp.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026