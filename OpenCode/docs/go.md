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
- [Background](#background)
- [How it works](#how-it-works)
- [Usage limits](#usage-limits) 
  - [Usage beyond limits](#usage-beyond-limits)
- [Endpoints](#endpoints) 
  - [Models](#models)
- [Privacy](#privacy)
- [Goals](#goals)

## On this page

- [Overview](#_top)
- [Background](#background)
- [How it works](#how-it-works)
- [Usage limits](#usage-limits) 
  - [Usage beyond limits](#usage-beyond-limits)
- [Endpoints](#endpoints) 
  - [Models](#models)
- [Privacy](#privacy)
- [Goals](#goals)

# Go

Low cost subscription for open coding models.

OpenCode Go is a low cost subscription â **$5 for your first month**, then **$10/month** â that gives you reliable access to popular open coding models.

Note

OpenCode Go is currently in beta.

Go works like any other provider in OpenCode. You subscribe to OpenCode Go and
get your API key. Itâs **completely optional** and you donât need to use it to
use OpenCode.

It is designed primarily for international users, with models hosted in the US, EU, and Singapore for stable global access.

---

## [Background](#background)

Open models have gotten really good. They now reach performance close to
proprietary models for coding tasks. And because many providers can serve them
competitively, they are usually far cheaper.

However, getting reliable, low latency access to them can be difficult. Providers
vary in quality and availability.

Tip

We tested a select group of models and providers that work well with OpenCode.

To fix this, we did a couple of things:

1. We tested a select group of open models and talked to their teams about how to
   best run them.
2. We then worked with a few providers to make sure these were being served
   correctly.
3. Finally, we benchmarked the combination of the model/provider and came up
   with a list that we feel good recommending.

OpenCode Go gives you access to these models for **$5 for your first month**, then **$10/month**.

---

## [How it works](#how-it-works)

OpenCode Go works like any other provider in OpenCode.

1. You sign in to **[OpenCode Zen](https://opencode.ai/auth)**, subscribe to Go, and
   copy your API key.
2. You run the `/connect` command in the TUI, select `OpenCode Go`, and paste
   your API key.
3. Run `/models` in the TUI to see the list of models available through Go.

Note

Only one member per workspace can subscribe to OpenCode Go.

The current list of models includes:

- **GLM-5**
- **GLM-5.1**
- **Kimi K2.5**
- **Kimi K2.6**
- **MiMo-V2.5**
- **MiMo-V2.5-Pro**
- **MiniMax M2.5**
- **MiniMax M2.7**
- **Qwen3.5 Plus**
- **Qwen3.6 Plus**
- **DeepSeek V4 Pro**
- **DeepSeek V4 Flash**

The list of models may change as we test and add new ones.

---

## [Usage limits](#usage-limits)

OpenCode Go includes the following limits:

- **5 hour limit** â $12 of usage
- **Weekly limit** â $30 of usage
- **Monthly limit** â $60 of usage

Limits are defined in dollar value. This means your actual request count depends on the model you use. Cheaper models like Qwen3.5 Plus allow for more requests, while higher-cost models like GLM-5.1 allow for fewer.

The table below provides an estimated request count based on typical Go usage patterns:

| Model | requests per 5 hour | requests per week | requests per month |
| --- | --- | --- | --- |
| GLM-5.1 | 880 | 2,150 | 4,300 |
| GLM-5 | 1,150 | 2,880 | 5,750 |
| Kimi K2.5 | 1,850 | 4,630 | 9,250 |
| Kimi K2.6 | 1,150 | 2,880 | 5,750 |
| MiMo-V2.5 (â¤ 256K) | 2,150 | 5,450 | 10,900 |
| MiMo-V2.5-Pro | 1,290 | 3,225 | 6,450 |
| MiniMax M2.7 | 3,400 | 8,500 | 17,000 |
| MiniMax M2.5 | 6,300 | 15,900 | 31,800 |
| Qwen3.6 Plus | 3,300 | 8,200 | 16,300 |
| Qwen3.5 Plus | 10,200 | 25,200 | 50,500 |
| DeepSeek V4 Pro | 3,450 | 8,550 | 17,150 |
| DeepSeek V4 Flash | 31,650 | 79,050 | 158,150 |

Estimates are based on observed average request patterns:

- GLM-5/5.1 â 700 input, 52,000 cached, 150 output tokens per request
- Kimi K2.5/K2.6 â 870 input, 55,000 cached, 200 output tokens per request
- DeepSeek V4 Pro â 750 input, 82,000 cached, 290 output tokens per request
- DeepSeek V4 Flash â 790 input, 68,000 cached, 280 output tokens per request
- MiniMax M2.7/M2.5 â 300 input, 55,000 cached, 125 output tokens per request
- MiMo-V2.5 â 1000 input, 60,000 cached, 140 output tokens per request
- MiMo-V2.5-Pro â 350 input, 41,000 cached, 250 output tokens per request
- Qwen3.5 Plus â 410 input, 47,000 cached, 140 output tokens per request
- Qwen3.6 Plus â 500 input, 57,000 cached, 190 output tokens per request

You can track your current usage in the **[console](https://opencode.ai/auth)**.

Tip

If you reach the usage limit, you can continue using the free models.

Usage limits may change as we learn from early usage and feedback.

---

### [Usage beyond limits](#usage-beyond-limits)

If you also have credits on your Zen balance, you can enable the **Use balance**
option in the console. When enabled, Go will fall back to your Zen balance
after youâve reached your usage limits instead of blocking requests.

---

## [Endpoints](#endpoints)

You can also access Go models through the following API endpoints.

| Model | Model ID | Endpoint | AI SDK Package |
| --- | --- | --- | --- |
| GLM-5.1 | glm-5.1 | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| GLM-5 | glm-5 | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| Kimi K2.5 | kimi-k2.5 | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| Kimi K2.6 | kimi-k2.6 | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| DeepSeek V4 Pro | deepseek-v4-pro | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| DeepSeek V4 Flash | deepseek-v4-flash | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| MiMo-V2.5 | mimo-v2.5 | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| MiMo-V2.5-Pro | mimo-v2.5-pro | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| MiniMax M2.7 | minimax-m2.7 | `https://opencode.ai/zen/go/v1/messages` | `@ai-sdk/anthropic` |
| MiniMax M2.5 | minimax-m2.5 | `https://opencode.ai/zen/go/v1/messages` | `@ai-sdk/anthropic` |
| Qwen3.6 Plus | qwen3.6-plus | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/alibaba` |
| Qwen3.5 Plus | qwen3.5-plus | `https://opencode.ai/zen/go/v1/chat/completions` | `@ai-sdk/alibaba` |

The [model id](config.md) in your OpenCode config
uses the format `opencode-go/<model-id>`. For example, for Kimi K2.6, you would
use `opencode-go/kimi-k2.6` in your config.

---

### [Models](#models)

You can fetch the full list of available models and their metadata from:

```
https://opencode.ai/zen/go/v1/models
```

---

## [Privacy](#privacy)

The plan is designed primarily for international users, with models hosted in the US, EU, and Singapore for stable global access. Our providers follow a zero-retention policy and do not use your data for model training.

---

## [Goals](#goals)

We created OpenCode Go to:

1. Make AI coding **accessible** to more people with a low cost subscription.
2. Provide **reliable** access to the best open coding models.
3. Curate models that are **tested and benchmarked** for coding agent use.
4. Have **no lock-in** by allowing you to use any other provider with OpenCode as well.

[Edit page](https://github.com/anomalyco/opencode/edit/dev/packages/web/src/content/docs/go.mdx)[Found a bug? Open an issue](https://github.com/anomalyco/opencode/issues/new)[Join our Discord community](https://opencode.ai/discord) Select language   EnglishØ§ÙØ¹Ø±Ø¨ÙØ©BosanskiDanskDeutschEspaÃ±olFranÃ§aisItalianoæ¥æ¬èªíêµ­ì´Norsk BokmÃ¥lPolskiPortuguÃªs (Brasil)Ð ÑÑÑÐºÐ¸Ð¹à¹à¸à¸¢TÃ¼rkÃ§eç®ä½ä¸­æç¹é«ä¸­æ

© [Anomaly](https://anoma.ly)

Last updated: May 13, 2026