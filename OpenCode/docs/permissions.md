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
* [Actions](#actions)
* [Configuration](#configuration)
* [Granular Rules (Object Syntax)](#granular-rules-object-syntax)
  + [Wildcards](#wildcards)
  + [Home Directory Expansion](#home-directory-expansion)
  + [External Directories](#external-directories)
* [Available Permissions](#available-permissions)
* [Defaults](#defaults)
* [What âAskâ Does](#what-ask-does)
* [Agents](#agents)

## On this page

* [Overview](#_top)
* [Actions](#actions)
* [Configuration](#configuration)
* [Granular Rules (Object Syntax)](#granular-rules-object-syntax)
  + [Wildcards](#wildcards)
  + [Home Directory Expansion](#home-directory-expansion)
  + [External Directories](#external-directories)
* [Available Permissions](#available-permissions)
* [Defaults](#defaults)
* [What âAskâ Does](#what-ask-does)
* [Agents](#agents)

# Permissions

Control which actions require approval to run.

OpenCode uses the `permission` config to decide whether a given action should run automatically, prompt you, or be blocked.

As of `v1.1.1`, the legacy `tools` boolean config is deprecated and has been merged into `permission`. The old `tools` config is still supported for backwards compatibility.

---

## [Actions](#actions)

Each permission rule resolves to one of:

* `"allow"` â run without approval
* `"ask"` â prompt for approval
* `"deny"` â block the action

---

## [Configuration](#configuration)

You can set permissions globally (with `*`), and override specific tools.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"*": "ask",

"bash": "allow",

"edit": "deny"

}

}
```

You can also set all permissions at once:

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": "allow"

}
```

---

## [Granular Rules (Object Syntax)](#granular-rules-object-syntax)

For most permissions, you can use an object to apply different actions based on the tool input.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"bash": {

"*": "ask",

"git *": "allow",

"npm *": "allow",

"rm *": "deny",

"grep *": "allow"

},

"edit": {

"*": "deny",

"packages/web/src/content/docs/*.mdx": "allow"

}

}

}
```

Rules are evaluated by pattern match, with the **last matching rule winning**. A common pattern is to put the catch-all `"*"` rule first, and more specific rules after it.

### [Wildcards](#wildcards)

Permission patterns use simple wildcard matching:

* `*` matches zero or more of any character
* `?` matches exactly one character
* All other characters match literally

### [Home Directory Expansion](#home-directory-expansion)

You can use `~` or `$HOME` at the start of a pattern to reference your home directory. This is particularly useful for [`external_directory`](#external-directories) rules.

* `~/projects/*` -> `/Users/username/projects/*`
* `$HOME/projects/*` -> `/Users/username/projects/*`
* `~` -> `/Users/username`

### [External Directories](#external-directories)

Use `external_directory` to allow tool calls that touch paths outside the working directory where OpenCode was started. This applies to any tool that takes a path as input (for example `read`, `edit`, `glob`, `grep`, and many `bash` commands).

Home expansion (like `~/...`) only affects how a pattern is written. It does not make an external path part of the current workspace, so paths outside the working directory must still be allowed via `external_directory`.

For example, this allows access to everything under `~/projects/personal/`:

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"external_directory": {

"~/projects/personal/**": "allow"

}

}

}
```

Any directory allowed here inherits the same defaults as the current workspace. Since [`read` defaults to `allow`](#defaults), reads are also allowed for entries under `external_directory` unless overridden. Add explicit rules when a tool should be restricted in these paths, such as blocking edits while keeping reads:

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"external_directory": {

"~/projects/personal/**": "allow"

},

"edit": {

"~/projects/personal/**": "deny"

}

}

}
```

Keep the list focused on trusted paths, and layer extra allow or deny rules as needed for other tools (for example `bash`).

---

## [Available Permissions](#available-permissions)

OpenCode permissions are keyed by tool name, plus a couple of safety guards:

* `read` â reading a file (matches the file path)
* `edit` â all file modifications (covers `edit`, `write`, `patch`)
* `glob` â file globbing (matches the glob pattern)
* `grep` â content search (matches the regex pattern)
* `bash` â running shell commands (matches parsed commands like `git status --porcelain`)
* `task` â launching subagents (matches the subagent type)
* `skill` â loading a skill (matches the skill name)
* `lsp` â running LSP queries (currently non-granular)
* `question` â asking the user questions during execution
* `webfetch` â fetching a URL (matches the URL)
* `websearch` â web search (matches the query)
* `external_directory` â triggered when a tool touches paths outside the project working directory
* `doom_loop` â triggered when the same tool call repeats 3 times with identical input

---

## [Defaults](#defaults)

If you donât specify anything, OpenCode starts from permissive defaults:

* Most permissions default to `"allow"`.
* `doom_loop` and `external_directory` default to `"ask"`.
* `read` is `"allow"`, but `.env` files are denied by default:

opencode.json

```
{

"permission": {

"read": {

"*": "allow",

"*.env": "deny",

"*.env.*": "deny",

"*.env.example": "allow"

}

}

}
```

---

## [What âAskâ Does](#what-ask-does)

When OpenCode prompts for approval, the UI offers three outcomes:

* `once` â approve just this request
* `always` â approve future requests matching the suggested patterns (for the rest of the current OpenCode session)
* `reject` â deny the request

The set of patterns that `always` would approve is provided by the tool (for example, bash approvals typically whitelist a safe command prefix like `git status*`).

---

## [Agents](#agents)

You can override permissions per agent. Agent permissions are merged with the global config, and agent rules take precedence. [Learn more](agents.md) about agent permissions.

Note

Refer to the [Granular Rules (Object Syntax)](#granular-rules-object-syntax) section above for more detailed pattern matching examples.

opencode.json

```
{

"$schema": "https://opencode.ai/config.json",

"permission": {

"bash": {

"*": "ask",

"git *": "allow",

"git commit *": "deny",

"git push *": "deny",

"grep *": "allow"

}

},

"agent": {

"build": {

"permission": {

"bash": {

"*": "ask",

"git *": "allow",

"git commit *": "ask",

"git push *": "deny",

"grep *": "allow"

}

}

}

}

}
```

You can also configure agent permissions in Markdown:

~/.config/opencode/agents/review.md

```
---

description: Code review without edits

mode: subagent

permission:

edit: deny

bash: ask

webfetch: deny

---

Only analyze code and suggest changes.
```

Tip

Use pattern matching for commands with arguments. `"grep *"` allows `grep pattern file.txt`, while `"grep"` alone would block it. Commands like `git status` work for default behavior but require explicit permission (like `"git status *"`) when arguments are passed.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/permissions.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026