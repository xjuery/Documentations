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
* [Creating a tool](#creating-a-tool)
  + [Location](#location)
  + [Structure](#structure)
  + [Arguments](#arguments)
  + [Context](#context)
* [Examples](#examples)
  + [Write a tool in Python](#write-a-tool-in-python)

## On this page

* [Overview](#_top)
* [Creating a tool](#creating-a-tool)
  + [Location](#location)
  + [Structure](#structure)
  + [Arguments](#arguments)
  + [Context](#context)
* [Examples](#examples)
  + [Write a tool in Python](#write-a-tool-in-python)

# Custom Tools

Create tools the LLM can call in opencode.

Custom tools are functions you create that the LLM can call during conversations. They work alongside opencodeâs [built-in tools](tools.md) like `read`, `write`, and `bash`.

---

## [Creating a tool](#creating-a-tool)

Tools are defined as **TypeScript** or **JavaScript** files. However, the tool definition can invoke scripts written in **any language** â TypeScript or JavaScript is only used for the tool definition itself.

---

### [Location](#location)

They can be defined:

* Locally by placing them in the `.opencode/tools/` directory of your project.
* Or globally, by placing them in `~/.config/opencode/tools/`.

---

### [Structure](#structure)

The easiest way to create tools is using the `tool()` helper which provides type-safety and validation.

.opencode/tools/database.ts

```
import { tool } from "@opencode-ai/plugin"

export default tool({

description: "Query the project database",

args: {

query: tool.schema.string().describe("SQL query to execute"),

},

async execute(args) {

// Your database logic here

return `Executed query: ${args.query}`

},

})
```

The **filename** becomes the **tool name**. The above creates a `database` tool.

---

#### [Multiple tools per file](#multiple-tools-per-file)

You can also export multiple tools from a single file. Each export becomes **a separate tool** with the name **`<filename>_<exportname>`**:

.opencode/tools/math.ts

```
import { tool } from "@opencode-ai/plugin"

export const add = tool({

description: "Add two numbers",

args: {

a: tool.schema.number().describe("First number"),

b: tool.schema.number().describe("Second number"),

},

async execute(args) {

return args.a + args.b

},

})

export const multiply = tool({

description: "Multiply two numbers",

args: {

a: tool.schema.number().describe("First number"),

b: tool.schema.number().describe("Second number"),

},

async execute(args) {

return args.a * args.b

},

})
```

This creates two tools: `math_add` and `math_multiply`.

---

#### [Name collisions with built-in tools](#name-collisions-with-built-in-tools)

Custom tools are keyed by tool name. If a custom tool uses the same name as a built-in tool, the custom tool takes precedence.

For example, this file replaces the built-in `bash` tool:

.opencode/tools/bash.ts

```
import { tool } from "@opencode-ai/plugin"

export default tool({

description: "Restricted bash wrapper",

args: {

command: tool.schema.string(),

},

async execute(args) {

return `blocked: ${args.command}`

},

})
```

Note

Prefer unique names unless you intentionally want to replace a built-in tool. If you want to disable a built in tool but not override it, use [permissions](permissions.md).

---

### [Arguments](#arguments)

You can use `tool.schema`, which is just [Zod](https://zod.dev), to define argument types.

```
args: {

query: tool.schema.string().describe("SQL query to execute")

}
```

You can also import [Zod](https://zod.dev) directly and return a plain object:

```
import { z } from "zod"

export default {

description: "Tool description",

args: {

param: z.string().describe("Parameter description"),

},

async execute(args, context) {

// Tool implementation

return "result"

},

}
```

---

### [Context](#context)

Tools receive context about the current session:

.opencode/tools/project.ts

```
import { tool } from "@opencode-ai/plugin"

export default tool({

description: "Get project information",

args: {},

async execute(args, context) {

// Access context information

const { agent, sessionID, messageID, directory, worktree } = context

return `Agent: ${agent}, Session: ${sessionID}, Message: ${messageID}, Directory: ${directory}, Worktree: ${worktree}`

},

})
```

Use `context.directory` for the session working directory.
Use `context.worktree` for the git worktree root.

---

## [Examples](#examples)

### [Write a tool in Python](#write-a-tool-in-python)

You can write your tools in any language you want. Hereâs an example that adds two numbers using Python.

First, create the tool as a Python script:

.opencode/tools/add.py

```
import sys

a = int(sys.argv[1])

b = int(sys.argv[2])

print(a + b)
```

Then create the tool definition that invokes it:

.opencode/tools/python-add.ts

```
import { tool } from "@opencode-ai/plugin"

import path from "path"

export default tool({

description: "Add two numbers using Python",

args: {

a: tool.schema.number().describe("First number"),

b: tool.schema.number().describe("Second number"),

},

async execute(args, context) {

const script = path.join(context.worktree, ".opencode/tools/add.py")

const result = await Bun.$`python3 ${script} ${args.a} ${args.b}`.text()

return result.trim()

},

})
```

Here we are using the [`Bun.$`](https://bun.com/docs/runtime/shell) utility to run the Python script.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/custom-tools.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026