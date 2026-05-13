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
- [Proxy](#proxy) 
  - [Authenticate](#authenticate)
- [Custom certificates](#custom-certificates)

## On this page

- [Overview](#_top)
- [Proxy](#proxy) 
  - [Authenticate](#authenticate)
- [Custom certificates](#custom-certificates)

# Network

Configure proxies and custom certificates.

OpenCode supports standard proxy environment variables and custom certificates for enterprise network environments.

---

## [Proxy](#proxy)

OpenCode respects standard proxy environment variables.

Terminal window

```
# HTTPS proxy (recommended)



export HTTPS_PROXY=https://proxy.example.com:8080



# HTTP proxy (if HTTPS not available)



export HTTP_PROXY=http://proxy.example.com:8080



# Bypass proxy for local server (required)



export NO_PROXY=localhost,127.0.0.1
```

Caution

The TUI communicates with a local HTTP server. You must bypass the proxy for this connection to prevent routing loops.

You can configure the serverâs port and hostname using [CLI flags](cli.md).

---

### [Authenticate](#authenticate)

If your proxy requires basic authentication, include credentials in the URL.

Terminal window

```
export HTTPS_PROXY=http://username:password@proxy.example.com:8080
```

Caution

Avoid hardcoding passwords. Use environment variables or secure credential storage.

For proxies requiring advanced authentication like NTLM or Kerberos, consider using an LLM Gateway that supports your authentication method.

---

## [Custom certificates](#custom-certificates)

If your enterprise uses custom CAs for HTTPS connections, configure OpenCode to trust them.

Terminal window

```
export NODE_EXTRA_CA_CERTS=/path/to/ca-cert.pem
```

This works for both proxy connections and direct API access.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/network.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026