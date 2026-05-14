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
* [Create command files](#create-command-files)
* [Configure](#configure)
  + [JSON](#json)
  + [Markdown](#markdown)
* [Prompt config](#prompt-config)
  + [Arguments](#arguments)
  + [Shell output](#shell-output)
  + [File references](#file-references)
* [Options](#options)
  + [Template](#template)
  + [Description](#description)
  + [Agent](#agent)
  + [Subtask](#subtask)
  + [Model](#model)
* [Built-in](#built-in)

## On this page

* [Overview](#_top)
* [Create command files](#create-command-files)
* [Configure](#configure)
  + [JSON](#json)
  + [Markdown](#markdown)
* [Prompt config](#prompt-config)
  + [Arguments](#arguments)
  + [Shell output](#shell-output)
  + [File references](#file-references)
* [Options](#options)
  + [Template](#template)
  + [Description](#description)
  + [Agent](#agent)
  + [Subtask](#subtask)
  + [Model](#model)
* [Built-in](#built-in)

# Commands

Create custom commands for repetitive tasks.

Custom commands let you specify a prompt you want to run when that command is executed in the TUI.

```
/my-command
```

Custom commands are in addition to the built-in commands like `/init`, `/undo`, `/redo`, `/share`, `/help`. [Learn more](tui.md).

---

## [Create command files](#create-command-files)

Create markdown files in the `commands/` directory to define custom commands.

Create `.opencode/commands/test.md`:

.opencode/commands/test.md

```
---

description: Run tests with coverage

agent: build

model: anthropic/claude-3-5-sonnet-20241022

---

Run the full test suite with coverage report and show any failures.

Focus on the failing tests and suggest fixes.
```

The frontmatter defines command properties. The content becomes the template.

Use the command by typing `/` followed by the command name.

```
"/test"
```

---

## [Configure](#configure)

You can add custom commands through the OpenCode config or by creating markdown files in the `commands/` directory.

---

### [JSON](#json)

Use the `command` option in your OpenCode [config](config.md):

opencode.jsonc

```
{

"$schema": "https://opencode.ai/config.json",

"command": {

// This becomes the name of the command

"test": {

// This is the prompt that will be sent to the LLM

"template": "Run the full test suite with coverage report and show any failures.\nFocus on the failing tests and suggest fixes.",

// This is shown as the description in the TUI

"description": "Run tests with coverage",

"agent": "build",

"model": "anthropic/claude-3-5-sonnet-20241022"

}

}

}
```

Now you can run this command in the TUI:

```
/test
```

---

### [Markdown](#markdown)

You can also define commands using markdown files. Place them in:

* Global: `~/.config/opencode/commands/`
* Per-project: `.opencode/commands/`

~/.config/opencode/commands/test.md

```
---

description: Run tests with coverage

agent: build

model: anthropic/claude-3-5-sonnet-20241022

---

Run the full test suite with coverage report and show any failures.

Focus on the failing tests and suggest fixes.
```

The markdown file name becomes the command name. For example, `test.md` lets
you run:

```
/test
```

---

## [Prompt config](#prompt-config)

The prompts for the custom commands support several special placeholders and syntax.

---

### [Arguments](#arguments)

Pass arguments to commands using the `$ARGUMENTS` placeholder.

.opencode/commands/component.md

```
---

description: Create a new component

---

Create a new React component named $ARGUMENTS with TypeScript support.

Include proper typing and basic structure.
```

Run the command with arguments:

```
/component Button
```

And `$ARGUMENTS` will be replaced with `Button`.

You can also access individual arguments using positional parameters:

* `$1` - First argument
* `$2` - Second argument
* `$3` - Third argument
* And so onâ¦

For example:

.opencode/commands/create-file.md

```
---

description: Create a new file with content

---

Create a file named $1 in the directory $2

with the following content: $3
```

Run the command:

```
/create-file config.json src "{ \"key\": \"value\" }"
```

This replaces:

* `$1` with `config.json`
* `$2` with `src`
* `$3` with `{ "key": "value" }`

---

### [Shell output](#shell-output)

Use *!`command`* to inject [bash command](tui.md) output into your prompt.

For example, to create a custom command that analyzes test coverage:

.opencode/commands/analyze-coverage.md

```
---

description: Analyze test coverage

---

Here are the current test results:

!`npm test`

Based on these results, suggest improvements to increase coverage.
```

Or to review recent changes:

.opencode/commands/review-changes.md

```
---

description: Review recent changes

---

Recent git commits:

!`git log --oneline -10`

Review these changes and suggest any improvements.
```

Commands run in your projectâs root directory and their output becomes part of the prompt.

---

### [File references](#file-references)

Include files in your command using `@` followed by the filename.

.opencode/commands/review-component.md

```
---

description: Review component

---

Review the component in @src/components/Button.tsx.

Check for performance issues and suggest improvements.
```

The file content gets included in the prompt automatically.

---

## [Options](#options)

Letâs look at the configuration options in detail.

---

### [Template](#template)

The `template` option defines the prompt that will be sent to the LLM when the command is executed.

opencode.json

```
{

"command": {

"test": {

"template": "Run the full test suite with coverage report and show any failures.\nFocus on the failing tests and suggest fixes."

}

}

}
```

This is a **required** config option.

---

### [Description](#description)

Use the `description` option to provide a brief description of what the command does.

opencode.json

```
{

"command": {

"test": {

"description": "Run tests with coverage"

}

}

}
```

This is shown as the description in the TUI when you type in the command.

---

### [Agent](#agent)

Use the `agent` config to optionally specify which [agent](agents.md) should execute this command.
If this is a [subagent](agents.md) the command will trigger a subagent invocation by default.
To disable this behavior, set `subtask` to `false`.

opencode.json

```
{

"command": {

"review": {

"agent": "plan"

}

}

}
```

This is an **optional** config option. If not specified, defaults to your current agent.

---

### [Subtask](#subtask)

Use the `subtask` boolean to force the command to trigger a [subagent](agents.md) invocation.
This is useful if you want the command to not pollute your primary context and will **force** the agent to act as a subagent,
even if `mode` is set to `primary` on the [agent](agents.md) configuration.

opencode.json

```
{

"command": {

"analyze": {

"subtask": true

}

}

}
```

This is an **optional** config option.

---

### [Model](#model)

Use the `model` config to override the default model for this command.

opencode.json

```
{

"command": {

"analyze": {

"model": "anthropic/claude-3-5-sonnet-20241022"

}

}

}
```

This is an **optional** config option.

---

## [Built-in](#built-in)

opencode includes several built-in commands like `/init`, `/undo`, `/redo`, `/share`, `/help`; [learn more](tui.md).

Note

Custom commands can override built-in commands.

If you define a custom command with the same name, it will override the built-in command.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/commands.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026