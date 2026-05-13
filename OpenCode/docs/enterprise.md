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
- [Trial](#trial) 
  - [Data handling](#data-handling)
  - [Code ownership](#code-ownership)
- [Pricing](#pricing)
- [Deployment](#deployment) 
  - [Central Config](#central-config)
  - [SSO integration](#sso-integration)
  - [Internal AI gateway](#internal-ai-gateway)
  - [Self-hosting](#self-hosting)
- [FAQ](#faq)

## On this page

- [Overview](#_top)
- [Trial](#trial) 
  - [Data handling](#data-handling)
  - [Code ownership](#code-ownership)
- [Pricing](#pricing)
- [Deployment](#deployment) 
  - [Central Config](#central-config)
  - [SSO integration](#sso-integration)
  - [Internal AI gateway](#internal-ai-gateway)
  - [Self-hosting](#self-hosting)
- [FAQ](#faq)

# Enterprise

Using OpenCode securely in your organization.

OpenCode Enterprise is for organizations that want to ensure that their code and data never leaves their infrastructure. It can do this by using a centralized config that integrates with your SSO and internal AI gateway.

Note

OpenCode does not store any of your code or context data.

To get started with OpenCode Enterprise:

1. Do a trial internally with your team.
2. **[Contact us](mailto:contact@anoma.ly)** to discuss pricing and implementation options.

---

## [Trial](#trial)

OpenCode is open source and does not store any of your code or context data, so your developers can simply [get started](../docs.md) and carry out a trial.

---

### [Data handling](#data-handling)

**OpenCode does not store your code or context data.** All processing happens locally or through direct API calls to your AI provider.

This means that as long as you are using a provider you trust, or an internal
AI gateway, you can use OpenCode securely.

The only caveat here is the optional `/share` feature.

---

#### [Sharing conversations](#sharing-conversations)

If a user enables the `/share` feature, the conversation and the data associated with it are sent to the service we use to host these share pages at opencode.ai.

The data is currently served through our CDNâs edge network, and is cached on the edge near your users.

We recommend you disable this for your trial.

opencode.json

```
{



"$schema": "https://opencode.ai/config.json",



"share": "disabled"



}
```

[Learn more about sharing](share.md).

---

### [Code ownership](#code-ownership)

**You own all code produced by OpenCode.** There are no licensing restrictions or ownership claims.

---

## [Pricing](#pricing)

We use a per-seat model for OpenCode Enterprise. If you have your own LLM gateway, we do not charge for tokens used. For further details about pricing and implementation options, **[contact us](mailto:contact@anoma.ly)**.

---

## [Deployment](#deployment)

Once you have completed your trial and you are ready to use OpenCode at
your organization, you can **[contact us](mailto:contact@anoma.ly)** to discuss
pricing and implementation options.

---

### [Central Config](#central-config)

We can set up OpenCode to use a single central config for your entire organization.

This centralized config can integrate with your SSO provider and ensures all users access only your internal AI gateway.

---

### [SSO integration](#sso-integration)

Through the central config, OpenCode can integrate with your organizationâs SSO provider for authentication.

This allows OpenCode to obtain credentials for your internal AI gateway through your existing identity management system.

---

### [Internal AI gateway](#internal-ai-gateway)

With the central config, OpenCode can also be configured to use only your internal AI gateway.

You can also disable all other AI providers, ensuring all requests go through your organizationâs approved infrastructure.

---

### [Self-hosting](#self-hosting)

While we recommend disabling the share pages to ensure your data never leaves
your organization, we can also help you self-host them on your infrastructure.

This is currently on our roadmap. If youâre interested, **[let us know](mailto:contact@anoma.ly)**.

---

## [FAQ](#faq)

What is OpenCode Enterprise?

OpenCode Enterprise is for organizations that want to ensure that their code and data never leaves their infrastructure. It can do this by using a centralized config that integrates with your SSO and internal AI gateway.

How do I get started with OpenCode Enterprise?

Simply start with an internal trial with your team. OpenCode by default does not store your code or context data, making it easy to get started.

Then **[contact us](mailto:contact@anoma.ly)** to discuss pricing and implementation options.

How does enterprise pricing work?

We offer per-seat enterprise pricing. If you have your own LLM gateway, we do not charge for tokens used. For further details, **[contact us](mailto:contact@anoma.ly)** for a custom quote based on your organizationâs needs.

Is my data secure with OpenCode Enterprise?

Yes. OpenCode does not store your code or context data. All processing happens locally or through direct API calls to your AI provider. With central config and SSO integration, your data remains secure within your organizationâs infrastructure.

Can we use our own private NPM registry?

OpenCode supports private npm registries through Bunâs native `.npmrc` file support. If your organization uses a private registry, such as JFrog Artifactory, Nexus, or similar, ensure developers are authenticated before running OpenCode.

To set up authentication with your private registry:

Terminal window

```
npm login --registry=https://your-company.jfrog.io/api/npm/npm-virtual/
```

This creates `~/.npmrc` with authentication details. OpenCode will automatically
pick this up.

Caution

You must be logged into the private registry before running OpenCode.

Alternatively, you can manually configure a `.npmrc` file:

~/.npmrc

```
registry=https://your-company.jfrog.io/api/npm/npm-virtual/



//your-company.jfrog.io/api/npm/npm-virtual/:_authToken=${NPM_AUTH_TOKEN}
```

Developers must be logged into the private registry before running OpenCode to ensure packages can be installed from your enterprise registry.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/enterprise.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026