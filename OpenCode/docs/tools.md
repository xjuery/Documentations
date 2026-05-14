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
* [Configure](#configure)
* [Built-in](#built-in)
  + [bash](#bash)
  + [edit](#edit)
  + [write](#write)
  + [read](#read)
  + [grep](#grep)
  + [glob](#glob)
  + [lsp (experimental)](#lsp-experimental)
  + [apply\_patch](#apply_patch)
  + [skill](#skill)
  + [todowrite](#todowrite)
  + [webfetch](#webfetch)
  + [websearch](#websearch)
  + [question](#question)
* [Custom tools](#custom-tools)
* [MCP servers](#mcp-servers)
* [Internals](#internals)
  + [Ignore patterns](#ignore-patterns)

## On this page

* [Overview](#_top)
* [Configure](#configure)
* [Built-in](#built-in)
  + [bash](#bash)
  + [edit](#edit)
  + [write](#write)
  + [read](#read)
  + [grep](#grep)
  + [glob](#glob)
  + [lsp (experimental)](#lsp-experimental)
  + [apply\_patch](#apply_patch)
  + [skill](#skill)
  + [todowrite](#todowrite)
  + [webfetch](#webfetch)
  + [websearch](#websearch)
  + [question](#question)
* [Custom tools](#custom-tools)
* [MCP servers](#mcp-servers)
* [Internals](#internals)
  + [Ignore patterns](#ignore-patterns)

# Tools

Manage the tools an LLM can use.

Tools allow the LLM to perform actions in your codebase. OpenCode comes with a set of built-in tools, but you can extend it with [custom tools](custom-tools.md) or [MCP servers](mcp-servers.md).

By default, all tools are **enabled** and donât need permission to run. You can control tool behavior through [permissions](permissions.md).

---

## [Configure](#configure)

Use the `permission` field to control tool behavior. You can allow, deny, or require approval for each tool.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"edit": "deny",

"bash": "ask",

"webfetch": "allow"

}

}
```

You can also use wildcards to control multiple tools at once. For example, to require approval for all tools from an MCP server:

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"mymcp_*": "ask"

}

}
```

[Learn more](permissions.md) about configuring permissions.

---

## [Built-in](#built-in)

Here are all the built-in tools available in OpenCode.

---

### [bash](#bash)

Execute shell commands in your project environment.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"bash": "allow"

}

}
```

This tool allows the LLM to run terminal commands like `npm install`, `git status`, or any other shell command.

---

### [edit](#edit)

Modify existing files using exact string replacements.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"edit": "allow"

}

}
```

This tool performs precise edits to files by replacing exact text matches. Itâs the primary way the LLM modifies code.

---

### [write](#write)

Create new files or overwrite existing ones.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"edit": "allow"

}

}
```

Use this to allow the LLM to create new files. It will overwrite existing files if they already exist.

Note

The `write` tool is controlled by the `edit` permission, which covers all file modifications (`edit`, `write`, `apply_patch`).

---

### [read](#read)

Read file contents from your codebase.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"read": "allow"

}

}
```

This tool reads files and returns their contents. It supports reading specific line ranges for large files.

---

### [grep](#grep)

Search file contents using regular expressions.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"grep": "allow"

}

}
```

Fast content search across your codebase. Supports full regex syntax and file pattern filtering.

---

### [glob](#glob)

Find files by pattern matching.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"glob": "allow"

}

}
```

Search for files using glob patterns like `**/*.js` or `src/**/*.ts`. Returns matching file paths sorted by modification time.

---

### [lsp (experimental)](#lsp-experimental)

Interact with your configured LSP servers to get code intelligence features like definitions, references, hover info, and call hierarchy.

Note

This tool is only available when `OPENCODE_EXPERIMENTAL_LSP_TOOL=true` (or `OPENCODE_EXPERIMENTAL=true`).

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"lsp": "allow"

}

}
```

Supported operations include `goToDefinition`, `findReferences`, `hover`, `documentSymbol`, `workspaceSymbol`, `goToImplementation`, `prepareCallHierarchy`, `incomingCalls`, and `outgoingCalls`.

To configure which LSP servers are available for your project, see [LSP Servers](lsp.md).

---

### [apply\_patch](#apply_patch)

Apply patches to files.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"edit": "allow"

}

}
```

This tool applies patch files to your codebase. Useful for applying diffs and patches from various sources.

When handling `tool.execute.before` or `tool.execute.after` hooks, check `input.tool === "apply_patch"` (not `"patch"`).

`apply_patch` uses `output.args.patchText` instead of `output.args.filePath`. Paths are embedded in marker lines within `patchText` and are relative to the project root (for example: `*** Add File: src/new-file.ts`, `*** Update File: src/existing.ts`, `*** Move to: src/renamed.ts`, `*** Delete File: src/obsolete.ts`).

Note

The `apply_patch` tool is controlled by the `edit` permission, which covers all file modifications (`edit`, `write`, `apply_patch`).

---

### [skill](#skill)

Load a [skill](skills.md) (a `SKILL.md` file) and return its content in the conversation.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"skill": "allow"

}

}
```

---

### [todowrite](#todowrite)

Manage todo lists during coding sessions.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"todowrite": "allow"

}

}
```

Creates and updates task lists to track progress during complex operations. The LLM uses this to organize multi-step tasks.

Note

This tool is disabled for subagents by default, but you can enable it manually. [Learn more](agents.md)

---

### [webfetch](#webfetch)

Fetch web content.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"webfetch": "allow"

}

}
```

Allows the LLM to fetch and read web pages. Useful for looking up documentation or researching online resources.

---

### [websearch](#websearch)

Search the web for information.

Note

This tool is only available when using the OpenCode provider or when the `OPENCODE_ENABLE_EXA` environment variable is set to any truthy value (e.g., `true` or `1`).

To enable when launching OpenCode:

Terminal window

```
OPENCODE_ENABLE_EXA=1 opencode
```

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"websearch": "allow"

}

}
```

Performs web searches using Exa AI to find relevant information online. Useful for researching topics, finding current events, or gathering information beyond the training data cutoff.

No API key is required â the tool connects directly to Exa AIâs hosted MCP service without authentication.

Tip

Use `websearch` when you need to find information (discovery), and `webfetch` when you need to retrieve content from a specific URL (retrieval).

---

### [question](#question)

Ask the user questions during execution.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"question": "allow"

}

}
```

This tool allows the LLM to ask the user questions during a task. Itâs useful for:

* Gathering user preferences or requirements
* Clarifying ambiguous instructions
* Getting decisions on implementation choices
* Offering choices about what direction to take

Each question includes a header, the question text, and a list of options. Users can select from the provided options or type a custom answer. When there are multiple questions, users can navigate between them before submitting all answers.

---

## [Custom tools](#custom-tools)

Custom tools let you define your own functions that the LLM can call. These are defined in your config file and can execute arbitrary code.

[Learn more](custom-tools.md) about creating custom tools.

---

## [MCP servers](#mcp-servers)

MCP (Model Context Protocol) servers allow you to integrate external tools and services. This includes database access, API integrations, and third-party services.

[Learn more](mcp-servers.md) about configuring MCP servers.

---

## [Internals](#internals)

Internally, tools like `grep` and `glob` use [ripgrep](https://github.com/BurntSushi/ripgrep) under the hood. By default, ripgrep respects `.gitignore` patterns, which means files and directories listed in your `.gitignore` will be excluded from searches and listings.

---

### [Ignore patterns](#ignore-patterns)

To include files that would normally be ignored, create a `.ignore` file in your project root. This file can explicitly allow certain paths.

.ignore

```
!node_modules/

!dist/

!build/
```

For example, this `.ignore` file allows ripgrep to search within `node_modules/`, `dist/`, and `build/` directories even if theyâre listed in `.gitignore`.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/tools.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026