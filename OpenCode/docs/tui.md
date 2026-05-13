Title: TUI

URL Source: https://opencode.ai/docs/tui

Markdown Content:
---
title: TUI
description: Using the OpenCode terminal user interface.
image: https://social-cards.sst.dev/opencode-docs/VFVJ.png?desc=Using%20the%20OpenCode%20terminal%20user%20interface.
---

[Skip to content](#%5Ftop) 

# TUI

Using the OpenCode terminal user interface.

OpenCode provides an interactive terminal interface or TUI for working on your projects with an LLM.

Running OpenCode starts the TUI for the current directory.

Terminal window

```

opencode


```

Or you can start it for a specific working directory.

Terminal window

```

opencode /path/to/project


```

Once you’re in the TUI, you can prompt it with a message.

```

Give me a quick summary of the codebase.


```

---

## [File references](#file-references)

You can reference files in your messages using `@`. This does a fuzzy file search in the current working directory.

Tip

You can also use `@` to reference files in your messages.

```

How is auth handled in @packages/functions/src/api/index.ts?


```

The content of the file is added to the conversation automatically.

Configured references also appear in `@` autocomplete. Type `@alias` to add the reference root as context, or type `@alias/` to autocomplete files inside that reference.

```

Compare our setup with @docs/README.md


```

---

## [Bash commands](#bash-commands)

Start a message with `!` to run a shell command.

```

!ls -la


```

The output of the command is added to the conversation as a tool result.

---

## [Commands](#commands)

When using the OpenCode TUI, you can type `/` followed by a command name to quickly execute actions. For example:

```

/help


```

Most commands also have keyboard shortcuts using `ctrl+x` as the default leader key. [Learn more](keybinds.md).

Here are all available slash commands:

---

### [connect](#connect)

Add a provider to OpenCode. Allows you to select from available providers and add their API keys.

```

/connect


```

---

### [compact](#compact)

Compact the current session. _Alias_: `/summarize`

```

/compact


```

**Keybind:** `ctrl+x c`

---

### [details](#details)

Toggle tool execution details.

```

/details


```

---

### [editor](#editor)

Open external editor for composing messages. Uses the editor set in your `EDITOR` environment variable. [Learn more](#editor-setup).

```

/editor


```

**Keybind:** `ctrl+x e`

---

### [exit](#exit)

Exit OpenCode. _Aliases_: `/quit`, `/q`

```

/exit


```

**Keybind:** `ctrl+x q`

---

### [export](#export)

Export current conversation to Markdown and open in your default editor. Uses the editor set in your `EDITOR` environment variable. [Learn more](#editor-setup).

```

/export


```

**Keybind:** `ctrl+x x`

---

### [help](#help)

Show the help dialog.

```

/help


```

---

### [init](#init)

Guided setup for creating or updating `AGENTS.md`. [Learn more](rules.md).

```

/init


```

---

### [models](#models)

List available models.

```

/models


```

**Keybind:** `ctrl+x m`

---

### [new](#new)

Start a new session. _Alias_: `/clear`

```

/new


```

**Keybind:** `ctrl+x n`

---

### [redo](#redo)

Redo a previously undone message. Only available after using `/undo`.

Tip

Any file changes will also be restored.

Internally, this uses Git to manage the file changes. So your project **needs to be a Git repository**.

```

/redo


```

**Keybind:** `ctrl+x r`

---

### [sessions](#sessions)

List and switch between sessions. _Aliases_: `/resume`, `/continue`

```

/sessions


```

**Keybind:** `ctrl+x l`

---

### [share](#share)

Share current session. [Learn more](share.md).

```

/share


```

---

### [themes](#themes)

List available themes.

```

/themes


```

**Keybind:** `ctrl+x t`

---

### [thinking](#thinking)

Toggle the visibility of thinking/reasoning blocks in the conversation. When enabled, you can see the model’s reasoning process for models that support extended thinking.

Note

This command only controls whether thinking blocks are **displayed** \- it does not enable or disable the model’s reasoning capabilities. To toggle actual reasoning capabilities, use `ctrl+t` to cycle through model variants.

```

/thinking


```

---

### [undo](#undo)

Undo last message in the conversation. Removes the most recent user message, all subsequent responses, and any file changes.

Tip

Any file changes made will also be reverted.

Internally, this uses Git to manage the file changes. So your project **needs to be a Git repository**.

```

/undo


```

**Keybind:** `ctrl+x u`

---

### [unshare](#unshare)

Unshare current session. [Learn more](share.md).

```

/unshare


```

---

## [Editor setup](#editor-setup)

Both the `/editor` and `/export` commands use the editor specified in your `EDITOR` environment variable.

* [ Linux/macOS ](#tab-panel-4)
* [ Windows (CMD) ](#tab-panel-5)
* [ Windows (PowerShell) ](#tab-panel-6)

Terminal window

```

# Example for nano or vim

export EDITOR=nano

export EDITOR=vim


# For GUI editors, VS Code, Cursor, VSCodium, Windsurf, Zed, etc.

# include --wait

export EDITOR="code --wait"


```

To make it permanent, add this to your shell profile;`~/.bashrc`, `~/.zshrc`, etc.

Terminal window

```

set EDITOR=notepad


# For GUI editors, VS Code, Cursor, VSCodium, Windsurf, Zed, etc.

# include --wait

set EDITOR=code --wait


```

To make it permanent, use **System Properties** \> **Environment Variables**.

Terminal window

```

$env:EDITOR = "notepad"


# For GUI editors, VS Code, Cursor, VSCodium, Windsurf, Zed, etc.

# include --wait

$env:EDITOR = "code --wait"


```

To make it permanent, add this to your PowerShell profile.

Popular editor options include:

* `code` \- Visual Studio Code
* `cursor` \- Cursor
* `windsurf` \- Windsurf
* `nvim` \- Neovim editor
* `vim` \- Vim editor
* `nano` \- Nano editor
* `notepad` \- Windows Notepad
* `subl` \- Sublime Text

Note

Some editors like VS Code need to be started with the `--wait` flag.

Some editors need command-line arguments to run in blocking mode. The `--wait` flag makes the editor process block until closed.

---

## [Configure](#configure)

You can customize TUI behavior through `tui.json` (or `tui.jsonc`).

tui.json

```

{

  "$schema": "https://opencode.ai/tui.json",

  "theme": "opencode",

  "leader_timeout": 2000,

  "keybinds": {

    "leader": "ctrl+x",

    "command_list": "ctrl+p"

  },

  "scroll_speed": 3,

  "scroll_acceleration": {

    "enabled": false

  },

  "diff_style": "auto",

  "mouse": true

}


```

This is separate from `opencode.json`, which configures server/runtime behavior.

`keybinds` is merged with built-in defaults, so you only need to configure the shortcuts you want to change.

### [Options](#options)

* `theme` \- Sets your UI theme. [Learn more](themes.md).
* `keybinds` \- Customizes keyboard shortcuts. [Learn more](keybinds.md).
* `leader_timeout` \- Controls how long OpenCode waits after the leader key. Defaults to `2000`.
* `scroll_acceleration.enabled` \- Enable macOS-style scroll acceleration for smooth, natural scrolling. When enabled, scroll speed increases with rapid scrolling gestures and stays precise for slower movements. **This setting takes precedence over `scroll_speed` and overrides it when enabled.**
* `scroll_speed` \- Controls how fast the TUI scrolls when using scroll commands (minimum: `0.001`, supports decimal values). Defaults to `3`. **Note: This is ignored if `scroll_acceleration.enabled` is set to `true`.**
* `diff_style` \- Controls diff rendering. `"auto"` adapts to terminal width, `"stacked"` always shows a single-column layout.
* `mouse` \- Enable or disable mouse capture in the TUI (default: `true`). When disabled, the terminal’s native mouse selection/scrolling behavior is preserved.

Use `OPENCODE_TUI_CONFIG` to load a custom TUI config path.

---

## [Customization](#customization)

You can customize various aspects of the TUI view using the command palette (`ctrl+p`). These settings persist across restarts.

---

#### [Username display](#username-display)

Toggle whether your username appears in chat messages. Access this through:

* Command palette: Search for “username” or “hide username”
* The setting persists automatically and will be remembered across TUI sessions