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
* [Place files](#place-files)
* [Understand discovery](#understand-discovery)
* [Write frontmatter](#write-frontmatter)
* [Validate names](#validate-names)
* [Follow length rules](#follow-length-rules)
* [Use an example](#use-an-example)
* [Recognize tool description](#recognize-tool-description)
* [Configure permissions](#configure-permissions)
* [Override per agent](#override-per-agent)
* [Disable the skill tool](#disable-the-skill-tool)
* [Troubleshoot loading](#troubleshoot-loading)

## On this page

* [Overview](#_top)
* [Place files](#place-files)
* [Understand discovery](#understand-discovery)
* [Write frontmatter](#write-frontmatter)
* [Validate names](#validate-names)
* [Follow length rules](#follow-length-rules)
* [Use an example](#use-an-example)
* [Recognize tool description](#recognize-tool-description)
* [Configure permissions](#configure-permissions)
* [Override per agent](#override-per-agent)
* [Disable the skill tool](#disable-the-skill-tool)
* [Troubleshoot loading](#troubleshoot-loading)

# Agent Skills

Define reusable behavior via SKILL.md definitions

Agent skills let OpenCode discover reusable instructions from your repo or home directory.
Skills are loaded on-demand via the native `skill` toolâagents see available skills and can load the full content when needed.

---

## [Place files](#place-files)

Create one folder per skill name and put a `SKILL.md` inside it.
OpenCode searches these locations:

* Project config: `.opencode/skills/<name>/SKILL.md`
* Global config: `~/.config/opencode/skills/<name>/SKILL.md`
* Project Claude-compatible: `.claude/skills/<name>/SKILL.md`
* Global Claude-compatible: `~/.claude/skills/<name>/SKILL.md`
* Project agent-compatible: `.agents/skills/<name>/SKILL.md`
* Global agent-compatible: `~/.agents/skills/<name>/SKILL.md`

---

## [Understand discovery](#understand-discovery)

For project-local paths, OpenCode walks up from your current working directory until it reaches the git worktree.
It loads any matching `skills/*/SKILL.md` in `.opencode/` and any matching `.claude/skills/*/SKILL.md` or `.agents/skills/*/SKILL.md` along the way.

Global definitions are also loaded from `~/.config/opencode/skills/*/SKILL.md`, `~/.claude/skills/*/SKILL.md`, and `~/.agents/skills/*/SKILL.md`.

---

## [Write frontmatter](#write-frontmatter)

Each `SKILL.md` must start with YAML frontmatter.
Only these fields are recognized:

* `name` (required)
* `description` (required)
* `license` (optional)
* `compatibility` (optional)
* `metadata` (optional, string-to-string map)

Unknown frontmatter fields are ignored.

---

## [Validate names](#validate-names)

`name` must:

* Be 1â64 characters
* Be lowercase alphanumeric with single hyphen separators
* Not start or end with `-`
* Not contain consecutive `--`
* Match the directory name that contains `SKILL.md`

Equivalent regex:

```
^[a-z0-9]+(-[a-z0-9]+)*$
```

---

## [Follow length rules](#follow-length-rules)

`description` must be 1-1024 characters.
Keep it specific enough for the agent to choose correctly.

---

## [Use an example](#use-an-example)

Create `.opencode/skills/git-release/SKILL.md` like this:

```
---

name: git-release

description: Create consistent releases and changelogs

license: MIT

compatibility: opencode

metadata:

audience: maintainers

workflow: github

---

## What I do

- Draft release notes from merged PRs

- Propose a version bump

- Provide a copy-pasteable `gh release create` command

## When to use me

Use this when you are preparing a tagged release.

Ask clarifying questions if the target versioning scheme is unclear.
```

---

## [Recognize tool description](#recognize-tool-description)

OpenCode lists available skills in the `skill` tool description.
Each entry includes the skill name and description:

```
<available_skills>

<skill>

<name>git-release</name>

<description>Create consistent releases and changelogs</description>

</skill>

</available_skills>
```

The agent loads a skill by calling the tool:

```
skill({ name: "git-release" })
```

---

## [Configure permissions](#configure-permissions)

Control which skills agents can access using pattern-based permissions in `opencode.json`:

```
{

"permission": {

"skill": {

"*": "allow",

"pr-review": "allow",

"internal-*": "deny",

"experimental-*": "ask"

}

}

}
```

| Permission | Behavior |
| --- | --- |
| `allow` | Skill loads immediately |
| `deny` | Skill hidden from agent, access rejected |
| `ask` | User prompted for approval before loading |

Patterns support wildcards: `internal-*` matches `internal-docs`, `internal-tools`, etc.

---

## [Override per agent](#override-per-agent)

Give specific agents different permissions than the global defaults.

**For custom agents** (in agent frontmatter):

```
---

permission:

skill:

"documents-*": "allow"

---
```

**For built-in agents** (in `opencode.json`):

```
{

"agent": {

"plan": {

"permission": {

"skill": {

"internal-*": "allow"

}

}

}

}

}
```

---

## [Disable the skill tool](#disable-the-skill-tool)

Completely disable skills for agents that shouldnât use them:

**For custom agents**:

```
---

tools:

skill: false

---
```

**For built-in agents**:

```
{

"agent": {

"plan": {

"tools": {

"skill": false

}

}

}

}
```

When disabled, the `<available_skills>` section is omitted entirely.

---

## [Troubleshoot loading](#troubleshoot-loading)

If a skill does not show up:

1. Verify `SKILL.md` is spelled in all caps
2. Check that frontmatter includes `name` and `description`
3. Ensure skill names are unique across all locations
4. Check permissionsâskills with `deny` are hidden from agents

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/skills.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026