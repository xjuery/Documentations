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
- [Getting Started](#getting-started)
- [Configuration](#configuration) 
  - [Port](#port)
  - [Hostname](#hostname)
  - [mDNS Discovery](#mdns-discovery)
  - [CORS](#cors)
  - [Authentication](#authentication)
- [Using the Web Interface](#using-the-web-interface) 
  - [Sessions](#sessions)
  - [Server Status](#server-status)
- [Attaching a Terminal](#attaching-a-terminal)
- [Config File](#config-file)

## On this page

- [Overview](#_top)
- [Getting Started](#getting-started)
- [Configuration](#configuration) 
  - [Port](#port)
  - [Hostname](#hostname)
  - [mDNS Discovery](#mdns-discovery)
  - [CORS](#cors)
  - [Authentication](#authentication)
- [Using the Web Interface](#using-the-web-interface) 
  - [Sessions](#sessions)
  - [Server Status](#server-status)
- [Attaching a Terminal](#attaching-a-terminal)
- [Config File](#config-file)

# Web

Using OpenCode in your browser.

OpenCode can run as a web application in your browser, providing the same powerful AI coding experience without needing a terminal.

![OpenCode Web - New Session](/docs/_astro/web-homepage-new-session.BB1mEdgo_Z1AT1v3.webp)

## [Getting Started](#getting-started)

Start the web interface by running:

Terminal window

```
opencode web
```

This starts a local server on `127.0.0.1` with a random available port and automatically opens OpenCode in your default browser.

Caution

If `OPENCODE_SERVER_PASSWORD` is not set, the server will be unsecured. This is fine for local use but should be set for network access.



Windows Users

For the best experience, run `opencode web` from [WSL](windows-wsl.md) rather than PowerShell. This ensures proper file system access and terminal integration.



---

## [Configuration](#configuration)

You can configure the web server using command line flags or in your [config file](config.md).

### [Port](#port)

By default, OpenCode picks an available port. You can specify a port:

Terminal window

```
opencode web --port 4096
```

### [Hostname](#hostname)

By default, the server binds to `127.0.0.1` (localhost only). To make OpenCode accessible on your network:

Terminal window

```
opencode web --hostname 0.0.0.0
```

When using `0.0.0.0`, OpenCode will display both local and network addresses:

```
Local access:       http://localhost:4096



Network access:     http://192.168.1.100:4096
```

### [mDNS Discovery](#mdns-discovery)

Enable mDNS to make your server discoverable on the local network:

Terminal window

```
opencode web --mdns
```

This automatically sets the hostname to `0.0.0.0` and advertises the server as `opencode.local`.

You can customize the mDNS domain name to run multiple instances on the same network:

Terminal window

```
opencode web --mdns --mdns-domain myproject.local
```

### [CORS](#cors)

To allow additional domains for CORS (useful for custom frontends):

Terminal window

```
opencode web --cors https://example.com
```

### [Authentication](#authentication)

To protect access, set a password using the `OPENCODE_SERVER_PASSWORD` environment variable:

Terminal window

```
OPENCODE_SERVER_PASSWORD=secret opencode web
```

The username defaults to `opencode` but can be changed with `OPENCODE_SERVER_USERNAME`.

---

## [Using the Web Interface](#using-the-web-interface)

Once started, the web interface provides access to your OpenCode sessions.

### [Sessions](#sessions)

View and manage your sessions from the homepage. You can see active sessions and start new ones.

![OpenCode Web - Active Session](/docs/_astro/web-homepage-active-session.BbK4Ph6e_Z1O7nO1.webp)

### [Server Status](#server-status)

Click âSee Serversâ to view connected servers and their status.

![OpenCode Web - See Servers](/docs/_astro/web-homepage-see-servers.BpCOef2l_ZB0rJd.webp)

---

## [Attaching a Terminal](#attaching-a-terminal)

You can attach a terminal TUI to a running web server:

Terminal window

```
# Start the web server



opencode web --port 4096



# In another terminal, attach the TUI



opencode attach http://localhost:4096
```

This allows you to use both the web interface and terminal simultaneously, sharing the same sessions and state.

---

## [Config File](#config-file)

You can also configure server settings in your `opencode.json` config file:

```
{



"server": {



"port": 4096,



"hostname": "0.0.0.0",



"mdns": true,



"cors": ["https://example.com"]



}



}
```

Command line flags take precedence over config file settings.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/web.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026