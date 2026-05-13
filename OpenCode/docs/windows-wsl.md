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
- [Setup](#setup)
- [Desktop App + WSL Server](#desktop-app--wsl-server)
- [Web Client + WSL](#web-client--wsl)
- [Accessing Windows Files](#accessing-windows-files)
- [Tips](#tips)

## On this page

- [Overview](#_top)
- [Setup](#setup)
- [Desktop App + WSL Server](#desktop-app--wsl-server)
- [Web Client + WSL](#web-client--wsl)
- [Accessing Windows Files](#accessing-windows-files)
- [Tips](#tips)

# Windows (WSL)

Run OpenCode on Windows using WSL for the best experience.

While OpenCode can run directly on Windows, we recommend using [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install) for the best experience. WSL provides a Linux environment that works seamlessly with OpenCodeâs features.

Why WSL?

WSL offers better file system performance, full terminal support, and compatibility with development tools that OpenCode relies on.



---

## [Setup](#setup)

1. **Install WSL**

   If you havenât already, [install WSL](https://learn.microsoft.com/en-us/windows/wsl/install) using the official Microsoft guide.
2. **Install OpenCode in WSL**

   Once WSL is set up, open your WSL terminal and install OpenCode using one of the [installation methods](../docs.md).

   Terminal window

   ```
   curl -fsSL https://opencode.ai/install | bash
   ```
3. **Use OpenCode from WSL**

   Navigate to your project directory (access Windows files via `/mnt/c/`, `/mnt/d/`, etc.) and run OpenCode.

   Terminal window

   ```
   cd /mnt/c/Users/YourName/project



   opencode
   ```

---

## [Desktop App + WSL Server](#desktop-app--wsl-server)

If you prefer using the OpenCode Desktop app but want to run the server in WSL:

1. **Start the server in WSL** with `--hostname 0.0.0.0` to allow external connections:

   Terminal window

   ```
   opencode serve --hostname 0.0.0.0 --port 4096
   ```
2. **Connect the Desktop app** to `http://localhost:4096`

Note

If `localhost` does not work in your setup, connect using the WSL IP address instead (from WSL: `hostname -I`) and use `http://<wsl-ip>:4096`.



Caution

When using `--hostname 0.0.0.0`, set `OPENCODE_SERVER_PASSWORD` to secure the server.

Terminal window

```
OPENCODE_SERVER_PASSWORD=your-password opencode serve --hostname 0.0.0.0
```

---

## [Web Client + WSL](#web-client--wsl)

For the best web experience on Windows:

1. **Run `opencode web` in the WSL terminal** rather than PowerShell:

   Terminal window

   ```
   opencode web --hostname 0.0.0.0
   ```
2. **Access from your Windows browser** at `http://localhost:<port>` (OpenCode prints the URL)

Running `opencode web` from WSL ensures proper file system access and terminal integration while still being accessible from your Windows browser.

---

## [Accessing Windows Files](#accessing-windows-files)

WSL can access all your Windows files through the `/mnt/` directory:

- `C:` drive â `/mnt/c/`
- `D:` drive â `/mnt/d/`
- And so onâ¦

Example:

Terminal window

```
cd /mnt/c/Users/YourName/Documents/project



opencode
```

Tip

For the smoothest experience, consider cloning/copying your repo into the WSL filesystem (for example under `~/code/`) and running OpenCode there.



---

## [Tips](#tips)

- Keep OpenCode running in WSL for projects stored on Windows drives - file access is seamless
- Use VS Codeâs [WSL extension](https://code.visualstudio.com/docs/remote/wsl) alongside OpenCode for an integrated development workflow
- Your OpenCode config and sessions are stored within the WSL environment at `~/.local/share/opencode/`

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/windows-wsl.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026