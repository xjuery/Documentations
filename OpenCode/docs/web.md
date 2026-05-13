Title: Web

URL Source: https://opencode.ai/docs/web

Markdown Content:
---
title: Web
description: Using OpenCode in your browser.
image: https://social-cards.sst.dev/opencode-docs/V2Vi.png?desc=Using%20OpenCode%20in%20your%20browser.
---

[Skip to content](#%5Ftop) 

# Web

Using OpenCode in your browser.

OpenCode can run as a web application in your browser, providing the same powerful AI coding experience without needing a terminal.



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



### [Server Status](#server-status)

Click “See Servers” to view connected servers and their status.



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