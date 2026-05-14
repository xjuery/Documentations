[Skip to content](#_top)

[![](/docs/_astro/logo-dark.DOStV66V.svg) ![](/docs/_astro/logo-light.B0yzR0O5.svg)  OpenCode](../docs.md)

[app.header.home](/)[app.header.docs](../docs.md)

Search  `CtrlK`

Cancel

* [Intro](../docs.md)
* [Config](config.md)
* [Providers](providers.md)
* [Network](network.md)
* [Enterprise](enterprise.md)
* [Troubleshooting](troubleshooting.md)
* [Windows](windows-wsl.md)
* Usage

  + [Go](go.md)
  + [TUI](tui.md)
  + [CLI](cli.md)
  + [Web](web.md)
  + [IDE](ide.md)
  + [Zen](zen.md)
  + [Share](share.md)
  + [GitHub](github.md)
  + [GitLab](gitlab.md)
* Configure

  + [Tools](tools.md)
  + [Rules](rules.md)
  + [Agents](agents.md)
  + [Models](models.md)
  + [Themes](themes.md)
  + [Keybinds](keybinds.md)
  + [Commands](commands.md)
  + [Formatters](formatters.md)
  + [Permissions](permissions.md)
  + [LSP Servers](lsp.md)
  + [MCP servers](mcp-servers.md)
  + [ACP Support](acp.md)
  + [Agent Skills](skills.md)
  + [Custom Tools](custom-tools.md)
* Develop

  + [SDK](sdk.md)
  + [Server](server.md)
  + [Plugins](plugins.md)
  + [Ecosystem](ecosystem.md)

[GitHub](https://github.com/anomalyco/opencode)[Discord](https://opencode.ai/discord)

  Select theme   DarkLightAuto      Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

On this page

* [Overview](#_top)
* [Built-in](#built-in)
* [How It Works](#how-it-works)
* [Configure](#configure)
  + [Environment variables](#environment-variables)
  + [Initialization options](#initialization-options)
  + [Disabling LSP servers](#disabling-lsp-servers)
  + [Custom LSP servers](#custom-lsp-servers)
* [Additional Information](#additional-information)
  + [PHP Intelephense](#php-intelephense)

## On this page

* [Overview](#_top)
* [Built-in](#built-in)
* [How It Works](#how-it-works)
* [Configure](#configure)
  + [Environment variables](#environment-variables)
  + [Initialization options](#initialization-options)
  + [Disabling LSP servers](#disabling-lsp-servers)
  + [Custom LSP servers](#custom-lsp-servers)
* [Additional Information](#additional-information)
  + [PHP Intelephense](#php-intelephense)

# LSP Servers

OpenCode integrates with your LSP servers.

OpenCode can integrate with your Language Server Protocol (LSP) to help the LLM interact with your codebase. It uses diagnostics to provide feedback to the LLM.

---

## [Built-in](#built-in)

OpenCode comes with several built-in LSP servers for popular languages:

| LSP Server | Extensions | Requirements |
| --- | --- | --- |
| astro | .astro | Auto-installs for Astro projects |
| bash | .sh, .bash, .zsh, .ksh | Auto-installs bash-language-server |
| clangd | .c, .cpp, .cc, .cxx, .c++, .h, .hpp, .hh, .hxx, .h++ | Auto-installs for C/C++ projects |
| csharp | .cs, .csx | `.NET SDK` installed |
| clojure-lsp | .clj, .cljs, .cljc, .edn | `clojure-lsp` command available |
| dart | .dart | `dart` command available |
| deno | .ts, .tsx, .js, .jsx, .mjs | `deno` command available (auto-detects deno.json/deno.jsonc) |
| elixir-ls | .ex, .exs | `elixir` command available |
| eslint | .ts, .tsx, .js, .jsx, .mjs, .cjs, .mts, .cts, .vue | `eslint` dependency in project |
| fsharp | .fs, .fsi, .fsx, .fsscript | `.NET SDK` installed |
| gleam | .gleam | `gleam` command available |
| gopls | .go | `go` command available |
| hls | .hs, .lhs | `haskell-language-server-wrapper` command available |
| jdtls | .java | `Java SDK (version 21+)` installed |
| julials | .jl | `julia` and `LanguageServer.jl` installed |
| kotlin-ls | .kt, .kts | Auto-installs for Kotlin projects |
| lua-ls | .lua | Auto-installs for Lua projects |
| nixd | .nix | `nixd` command available |
| ocaml-lsp | .ml, .mli | `ocamllsp` command available |
| oxlint | .ts, .tsx, .js, .jsx, .mjs, .cjs, .mts, .cts, .vue, .astro, .svelte | `oxlint` dependency in project |
| php intelephense | .php | Auto-installs for PHP projects |
| prisma | .prisma | `prisma` command available |
| pyright | .py, .pyi | `pyright` dependency installed |
| razor | .razor, .cshtml | `.NET SDK` and VS Code C# extension installed |
| ruby-lsp (rubocop) | .rb, .rake, .gemspec, .ru | `ruby` and `gem` commands available |
| rust | .rs | `rust-analyzer` command available |
| sourcekit-lsp | .swift, .objc, .objcpp | `swift` installed (`xcode` on macOS) |
| svelte | .svelte | Auto-installs for Svelte projects |
| terraform | .tf, .tfvars | Auto-installs from GitHub releases |
| tinymist | .typ, .typc | Auto-installs from GitHub releases |
| typescript | .ts, .tsx, .js, .jsx, .mjs, .cjs, .mts, .cts | `typescript` dependency in project |
| vue | .vue | Auto-installs for Vue projects |
| yaml-ls | .yaml, .yml | Auto-installs Red Hat yaml-language-server |
| zls | .zig, .zon | `zig` command available |

When LSP is enabled, servers start when one of the above file extensions is detected and the requirements are met.

Note

You can disable automatic LSP server downloads by setting the `OPENCODE_DISABLE_LSP_DOWNLOAD` environment variable to `true`.

---

## [How It Works](#how-it-works)

When LSP is enabled and opencode opens a file, it:

1. Checks the file extension against all enabled LSP servers.
2. Starts the appropriate LSP server if not already running.

---

## [Configure](#configure)

You can enable and customize LSP servers through the `lsp` section in your opencode config.

To enable all built-in LSP servers, set `lsp` to `true`.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"lsp": true

}
```

Use an object to keep built-ins enabled while configuring overrides or custom servers.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"lsp": {}

}
```

Each configured LSP server entry supports the following:

Server entries need `command` unless they only disable a server.

| Property | Type | Description |
| --- | --- | --- |
| `disabled` | boolean | Set this to `true` to disable the LSP server |
| `command` | string[] | The command to start the LSP server |
| `extensions` | string[] | File extensions this LSP server should handle |
| `env` | object | Environment variables to set when starting server |
| `initialization` | object | Initialization options to send to the LSP server |

Letâs look at some examples.

---

### [Environment variables](#environment-variables)

Use the `env` property to set environment variables when starting the LSP server:

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"lsp": {

"rust": {

"command": ["rust-analyzer"],

"env": {

"RUST_LOG": "debug"

}

}

}

}
```

---

### [Initialization options](#initialization-options)

Use the `initialization` property to pass initialization options to the LSP server. These are server-specific settings sent during the LSP `initialize` request:

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"lsp": {

"custom-lsp": {

"command": ["custom-lsp-server", "--stdio"],

"extensions": [".custom"],

"initialization": {

"preferences": {

"importModuleSpecifierPreference": "relative"

}

}

}

}

}
```

Note

Initialization options vary by LSP server. Check your LSP serverâs documentation for available options.

---

### [Disabling LSP servers](#disabling-lsp-servers)

If `lsp` is omitted, all LSP servers are disabled. To disable all LSP servers after another config enabled them, set `lsp` to `false`:

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"lsp": false

}
```

To disable a **specific** LSP server, set `disabled` to `true`:

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"lsp": {

"typescript": {

"disabled": true

}

}

}
```

---

### [Custom LSP servers](#custom-lsp-servers)

You can add custom LSP servers by specifying the command and file extensions:

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"lsp": {

"custom-lsp": {

"command": ["custom-lsp-server", "--stdio"],

"extensions": [".custom"]

}

}

}
```

---

## [Additional Information](#additional-information)

### [PHP Intelephense](#php-intelephense)

PHP Intelephense offers premium features through a license key. You can provide a license key by placing (only) the key in a text file at:

* On macOS/Linux: `$HOME/intelephense/license.txt`
* On Windows: `%USERPROFILE%/intelephense/license.txt`

The file should contain only the license key with no additional content.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/lsp.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026