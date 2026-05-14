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
* [Logs](#logs)
* [Storage](#storage)
* [Desktop app](#desktop-app)
  + [Quick checks](#quick-checks)
  + [Disable plugins](#disable-plugins)
  + [Clear the cache](#clear-the-cache)
  + [Fix server connection issues](#fix-server-connection-issues)
  + [Linux: Wayland / X11 issues](#linux-wayland--x11-issues)
  + [Windows: WebView2 runtime](#windows-webview2-runtime)
  + [Windows: General performance issues](#windows-general-performance-issues)
  + [Notifications not showing](#notifications-not-showing)
  + [Reset desktop app storage (last resort)](#reset-desktop-app-storage-last-resort)
* [Getting help](#getting-help)
* [Common issues](#common-issues)
  + [OpenCode wonât start](#opencode-wont-start)
  + [Authentication issues](#authentication-issues)
  + [Model not available](#model-not-available)
  + [ProviderInitError](#provideriniterror)
  + [AI\_APICallError and provider package issues](#ai_apicallerror-and-provider-package-issues)
  + [Copy/paste not working on Linux](#copypaste-not-working-on-linux)

## On this page

* [Overview](#_top)
* [Logs](#logs)
* [Storage](#storage)
* [Desktop app](#desktop-app)
  + [Quick checks](#quick-checks)
  + [Disable plugins](#disable-plugins)
  + [Clear the cache](#clear-the-cache)
  + [Fix server connection issues](#fix-server-connection-issues)
  + [Linux: Wayland / X11 issues](#linux-wayland--x11-issues)
  + [Windows: WebView2 runtime](#windows-webview2-runtime)
  + [Windows: General performance issues](#windows-general-performance-issues)
  + [Notifications not showing](#notifications-not-showing)
  + [Reset desktop app storage (last resort)](#reset-desktop-app-storage-last-resort)
* [Getting help](#getting-help)
* [Common issues](#common-issues)
  + [OpenCode wonât start](#opencode-wont-start)
  + [Authentication issues](#authentication-issues)
  + [Model not available](#model-not-available)
  + [ProviderInitError](#provideriniterror)
  + [AI\_APICallError and provider package issues](#ai_apicallerror-and-provider-package-issues)
  + [Copy/paste not working on Linux](#copypaste-not-working-on-linux)

# Troubleshooting

Common issues and how to resolve them.

To debug issues with OpenCode, start by checking the logs and local data it stores on disk.

---

## [Logs](#logs)

Log files are written to:

* **macOS/Linux**: `~/.local/share/opencode/log/`
* **Windows**: Press `WIN+R` and paste `%USERPROFILE%\.local\share\opencode\log`

Log files are named with timestamps (e.g., `2025-01-09T123456.log`) and the most recent 10 log files are kept.

You can set the log level with the `--log-level` command-line option to get more detailed debug information. For example, `opencode --log-level DEBUG`.

---

## [Storage](#storage)

opencode stores session data and other application data on disk at:

* **macOS/Linux**: `~/.local/share/opencode/`
* **Windows**: Press `WIN+R` and paste `%USERPROFILE%\.local\share\opencode`

This directory contains:

* `auth.json` - Authentication data like API keys, OAuth tokens
* `log/` - Application logs
* `project/` - Project-specific data like session and message data
  + If the project is within a Git repo, it is stored in `./<project-slug>/storage/`
  + If it is not a Git repo, it is stored in `./global/storage/`

---

## [Desktop app](#desktop-app)

OpenCode Desktop runs a local OpenCode server (the `opencode-cli` sidecar) in the background. Most issues are caused by a misbehaving plugin, a corrupted cache, or a bad server setting.

### [Quick checks](#quick-checks)

* Fully quit and relaunch the app.
* If the app shows an error screen, click **Restart** and copy the error details.
* macOS only: `OpenCode` menu -> **Reload Webview** (helps if the UI is blank/frozen).

---

### [Disable plugins](#disable-plugins)

If the desktop app is crashing on launch, hanging, or behaving strangely, start by disabling plugins.

#### [Check the global config](#check-the-global-config)

Open your global config file and look for a `plugin` key.

* **macOS/Linux**: `~/.config/opencode/opencode.jsonc` (or `~/.config/opencode/opencode.json`)
* **macOS/Linux** (older installs): `~/.local/share/opencode/opencode.jsonc`
* **Windows**: Press `WIN+R` and paste `%USERPROFILE%\.config\opencode\opencode.jsonc`

If you have plugins configured, temporarily disable them by removing the key or setting it to an empty array:

```
{

"$schema": "https://opencode.ai/config.json",

"plugin": [],

}
```

#### [Check plugin directories](#check-plugin-directories)

OpenCode can also load local plugins from disk. Temporarily move these out of the way (or rename the folder) and restart the desktop app:

* **Global plugins**
  + **macOS/Linux**: `~/.config/opencode/plugins/`
  + **Windows**: Press `WIN+R` and paste `%USERPROFILE%\.config\opencode\plugins`
* **Project plugins** (only if you use per-project config)
  + `<your-project>/.opencode/plugins/`

If the app starts working again, re-enable plugins one at a time to find which one is causing the issue.

---

### [Clear the cache](#clear-the-cache)

If disabling plugins doesnât help (or a plugin install is stuck), clear the cache so OpenCode can rebuild it.

1. Quit OpenCode Desktop completely.
2. Delete the cache directory:

* **macOS**: Finder -> `Cmd+Shift+G` -> paste `~/.cache/opencode`
* **Linux**: delete `~/.cache/opencode` (or run `rm -rf ~/.cache/opencode`)
* **Windows**: Press `WIN+R` and paste `%USERPROFILE%\.cache\opencode`

3. Restart OpenCode Desktop.

---

### [Fix server connection issues](#fix-server-connection-issues)

OpenCode Desktop can either start its own local server (default) or connect to a server URL you configured.

If you see a **âConnection Failedâ** dialog (or the app never gets past the splash screen), check for a custom server URL.

#### [Clear the desktop default server URL](#clear-the-desktop-default-server-url)

From the Home screen, click the server name (with the status dot) to open the Server picker. In the **Default server** section, click **Clear**.

#### [Remove `server.port` / `server.hostname` from your config](#remove-serverport--serverhostname-from-your-config)

If your `opencode.json(c)` contains a `server` section, temporarily remove it and restart the desktop app.

#### [Check environment variables](#check-environment-variables)

If you have `OPENCODE_PORT` set in your environment, the desktop app will try to use that port for the local server.

* Unset `OPENCODE_PORT` (or pick a free port) and restart.

---

### [Linux: Wayland / X11 issues](#linux-wayland--x11-issues)

On Linux, some Wayland setups can cause blank windows or compositor errors.

* If youâre on Wayland and the app is blank/crashing, try launching with `OC_ALLOW_WAYLAND=1`.
* If that makes things worse, remove it and try launching under an X11 session instead.

---

### [Windows: WebView2 runtime](#windows-webview2-runtime)

On Windows, OpenCode Desktop requires the Microsoft Edge **WebView2 Runtime**. If the app opens to a blank window or wonât start, install/update WebView2 and try again.

---

### [Windows: General performance issues](#windows-general-performance-issues)

If youâre experiencing slow performance, file access issues, or terminal problems on Windows, try using [WSL (Windows Subsystem for Linux)](windows-wsl.md). WSL provides a Linux environment that works more seamlessly with OpenCodeâs features.

---

### [Notifications not showing](#notifications-not-showing)

OpenCode Desktop only shows system notifications when:

* notifications are enabled for OpenCode in your OS settings, and
* the app window is not focused.

---

### [Reset desktop app storage (last resort)](#reset-desktop-app-storage-last-resort)

If the app wonât start and you canât clear settings from inside the UI, reset the desktop appâs saved state.

1. Quit OpenCode Desktop.
2. Find and delete these files (they live in the OpenCode Desktop app data directory):

* `opencode.settings.dat` (desktop default server URL)
* `opencode.global.dat` and `opencode.workspace.*.dat` (UI state like recent servers/projects)

To find the directory quickly:

* **macOS**: Finder -> `Cmd+Shift+G` -> `~/Library/Application Support` (then search for the filenames above)
* **Linux**: search under `~/.local/share` for the filenames above
* **Windows**: Press `WIN+R` -> `%APPDATA%` (then search for the filenames above)

---

## [Getting help](#getting-help)

If youâre experiencing issues with OpenCode:

1. **Report issues on GitHub**

   The best way to report bugs or request features is through our GitHub repository:

   [**github.com/anomalyco/opencode/issues**](https://github.com/anomalyco/opencode/issues)

   Before creating a new issue, search existing issues to see if your problem has already been reported.
2. **Join our Discord**

   For real-time help and community discussion, join our Discord server:

   [**opencode.ai/discord**](https://opencode.ai/discord)

---

## [Common issues](#common-issues)

Here are some common issues and how to resolve them.

---

### [OpenCode wonât start](#opencode-wont-start)

1. Check the logs for error messages
2. Try running with `--print-logs` to see output in the terminal
3. Ensure you have the latest version with `opencode upgrade`

---

### [Authentication issues](#authentication-issues)

1. Try re-authenticating with the `/connect` command in the TUI
2. Check that your API keys are valid
3. Ensure your network allows connections to the providerâs API

---

### [Model not available](#model-not-available)

1. Check that youâve authenticated with the provider
2. Verify the model name in your config is correct
3. Some models may require specific access or subscriptions

If you encounter `ProviderModelNotFoundError` you are most likely incorrectly
referencing a model somewhere.
Models should be referenced like so: `<providerId>/<modelId>`

Examples:

* `openai/gpt-4.1`
* `openrouter/google/gemini-2.5-flash`
* `opencode/kimi-k2`

To figure out what models you have access to, run `opencode models`

---

### [ProviderInitError](#provideriniterror)

If you encounter a ProviderInitError, you likely have an invalid or corrupted configuration.

To resolve this:

1. First, verify your provider is set up correctly by following the [providers guide](providers.md)
2. If the issue persists, try clearing your stored configuration:

   Terminal window

   ```
   rm -rf ~/.local/share/opencode
   ```

   On Windows, press `WIN+R` and delete: `%USERPROFILE%\.local\share\opencode`
3. Re-authenticate with your provider using the `/connect` command in the TUI.

---

### [AI\_APICallError and provider package issues](#ai_apicallerror-and-provider-package-issues)

If you encounter API call errors, this may be due to outdated provider packages. opencode dynamically installs provider packages (OpenAI, Anthropic, Google, etc.) as needed and caches them locally.

To resolve provider package issues:

1. Clear the provider package cache:

   Terminal window

   ```
   rm -rf ~/.cache/opencode
   ```

   On Windows, press `WIN+R` and delete: `%USERPROFILE%\.cache\opencode`
2. Restart opencode to reinstall the latest provider packages

This will force opencode to download the most recent versions of provider packages, which often resolves compatibility issues with model parameters and API changes.

---

### [Copy/paste not working on Linux](#copypaste-not-working-on-linux)

Linux users need to have one of the following clipboard utilities installed for copy/paste functionality to work:

**For X11 systems:**

Terminal window

```
apt install -y xclip

# or

apt install -y xsel
```

**For Wayland systems:**

Terminal window

```
apt install -y wl-clipboard
```

**For headless environments:**

Terminal window

```
apt install -y xvfb

# and run:

Xvfb :99 -screen 0 1024x768x24 > /dev/null 2>&1 &

export DISPLAY=:99.0
```

opencode will detect if youâre using Wayland and prefer `wl-clipboard`, otherwise it will try to find clipboard tools in order of: `xclip` and `xsel`.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/troubleshooting.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026