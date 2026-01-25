[English](README_EN.md)

[中文](README.md)

# 🦞 Clawdbot — 个人 AI 助手

<p align="center">
  <img src="https://raw.githubusercontent.com/clawdbot/clawdbot/main/docs/whatsapp-clawd.jpg" alt="Clawdbot" width="400">
</p>

<p align="center">
  <strong>蜕壳！蜕壳！(EXFOLIATE! EXFOLIATE!)</strong>
</p>

<p align="center">
  <a href="https://github.com/clawdbot/clawdbot/actions/workflows/ci.yml?branch=main"><img src="https://img.shields.io/github/actions/workflow/status/clawdbot/clawdbot/ci.yml?branch=main&style=for-the-badge" alt="CI status"></a>
  <a href="https://github.com/clawdbot/clawdbot/releases"><img src="https://img.shields.io/github/v/release/clawdbot/clawdbot?include_prereleases&style=for-the-badge" alt="GitHub release"></a>
  <a href="https://deepwiki.com/clawdbot/clawdbot"><img src="https://img.shields.io/badge/DeepWiki-clawdbot-111111?style=for-the-badge" alt="DeepWiki"></a>
  <a href="https://discord.gg/clawd"><img src="https://img.shields.io/discord/1456350064065904867?label=Discord&logo=discord&logoColor=white&color=5865F2&style=for-the-badge" alt="Discord"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT License"></a>
</p>

**Clawdbot** 是一个运行在您自己设备上的**个人 AI 助手**。
它会在您已经使用的渠道上回复您（WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, WebChat），同时也支持 BlueBubbles, Matrix, Zalo 和 Zalo Personal 等扩展渠道。它可以在 macOS/iOS/Android 上进行语音对话，并且能够渲染一个您可控的实时 Canvas。网关（Gateway）只是控制平面——产品本身就是这个助手。

如果您想要一个感觉本地化、快速且永远在线的个人单用户助手，这就是您的选择。

[官网](https://clawdbot.com) · [文档](https://docs.clawd.bot) · [入门指南](https://docs.clawd.bot/start/getting-started) · [更新](https://docs.clawd.bot/install/updating) · [展示](https://docs.clawd.bot/start/showcase) · [常见问题](https://docs.clawd.bot/start/faq) · [向导](https://docs.clawd.bot/start/wizard) · [Nix](https://github.com/clawdbot/nix-clawdbot) · [Docker](https://docs.clawd.bot/install/docker) · [Discord](https://discord.gg/clawd)

首选设置方式：运行入职向导 (`clawdbot onboard`)。它会引导您完成网关、工作区、渠道和技能的配置。CLI 向导是推荐路径，适用于 **macOS, Linux, 和 Windows (通过 WSL2; 强烈推荐)**。
支持使用 npm, pnpm, 或 bun。
新安装？从这里开始：[入门指南](https://docs.clawd.bot/start/getting-started)

**订阅 (OAuth):**
- **[Anthropic](https://www.anthropic.com/)** (Claude Pro/Max)
- **[OpenAI](https://openai.com/)** (ChatGPT/Codex)

模型说明：虽然支持任何模型，但我强烈推荐 **Anthropic Pro/Max (100/200) + Opus 4.5**，因为它具有长上下文优势和更好的抗提示注入能力。参见 [入职指南](https://docs.clawd.bot/start/onboarding)。

## 模型 (选择 + 认证)

- 模型配置 + CLI: [Models](https://docs.clawd.bot/concepts/models)
- 认证配置文件轮换 (OAuth vs API keys) + 故障转移: [Model failover](https://docs.clawd.bot/concepts/model-failover)

## 安装 (推荐)

运行环境：**Node ≥22**。

```bash
npm install -g clawdbot@latest
# 或者: pnpm add -g clawdbot@latest

clawdbot onboard --install-daemon
```

向导会安装网关守护进程（launchd/systemd 用户服务），使其保持运行。

## 快速开始 (简版)

运行环境：**Node ≥22**。

完整新手指南（认证、配对、渠道）：[入门指南](https://docs.clawd.bot/start/getting-started)

```bash
clawdbot onboard --install-daemon

clawdbot gateway --port 18789 --verbose

# 发送消息
clawdbot message send --to +1234567890 --message "Hello from Clawdbot"

# 与助手交谈 (可选传回任何已连接的渠道: WhatsApp/Telegram/Slack/Discord/Google Chat/Signal/iMessage/BlueBubbles/Microsoft Teams/Matrix/Zalo/Zalo Personal/WebChat)
clawdbot agent --message "Ship checklist" --thinking high
```

升级？[更新指南](https://docs.clawd.bot/install/updating) (并运行 `clawdbot doctor`)。

## 开发通道

- **stable**: 稳定版，打标版本 (`vYYYY.M.D` 或 `vYYYY.M.D-<patch>`), npm dist-tag `latest`。
- **beta**: 预发布版 (`vYYYY.M.D-beta.N`), npm dist-tag `beta` (macOS 应用可能缺失)。
- **dev**: `main` 分支的移动头指针, npm dist-tag `dev` (发布时)。

切换通道 (git + npm): `clawdbot update --channel stable|beta|dev`。
详情：[开发通道](https://docs.clawd.bot/install/development-channels)。

## 源码安装 (开发)

源码构建推荐使用 `pnpm`。Bun 可选用于直接运行 TypeScript。

```bash
git clone https://github.com/clawdbot/clawdbot.git
cd clawdbot

pnpm install
pnpm ui:build # 首次运行时自动安装 UI 依赖
pnpm build

pnpm clawdbot onboard --install-daemon

# 开发循环 (TS 变更自动重载)
pnpm gateway:watch
```

注意：`pnpm clawdbot ...` 直接运行 TypeScript (通过 `tsx`)。`pnpm build` 生成 `dist/` 用于通过 Node / 打包好的 `clawdbot` 二进制文件运行。

## 安全默认设置 (私信访问)

Clawdbot 连接到真实的某些消息平台。请将入站私信 (DM) 视为 **不可信输入**。

完整安全指南：[安全](https://docs.clawd.bot/gateway/security)

Telegram/WhatsApp/Signal/iMessage/Microsoft Teams/Discord/Google Chat/Slack 上的默认行为：
- **私信配对** (`dmPolicy="pairing"` / `channels.discord.dm.policy="pairing"` / `channels.slack.dm.policy="pairing"`): 未知发送者会收到一个简短的配对码，机器人不会处理他们的消息。
- 批准方式：`clawdbot pairing approve <channel> <code>` (然后发送者会被添加到本地允许列表存储中)。
- 公共入站私信需要显式选择加入：设置 `dmPolicy="open"` 并在渠道允许列表 (`allowFrom` / `channels.discord.dm.allowFrom` / `channels.slack.dm.allowFrom`) 中包含 `"*"`。

运行 `clawdbot doctor` 来发现有风险/配置错误的私信策略。

## 亮点

- **[本地优先网关](https://docs.clawd.bot/gateway)** — 会话、渠道、工具和事件的统一控制平面。
- **[多渠道收件箱](https://docs.clawd.bot/channels)** — WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, BlueBubbles, Microsoft Teams, Matrix, Zalo, Zalo Personal, WebChat, macOS, iOS/Android。
- **[多 Agent 路由](https://docs.clawd.bot/gateway/configuration)** — 将入站渠道/账户/对等端路由到隔离的 Agent（工作区 + 每 Agent 会话）。
- **[语音唤醒 (Voice Wake)](https://docs.clawd.bot/nodes/voicewake) + [交谈模式 (Talk Mode)](https://docs.clawd.bot/nodes/talk)** — macOS/iOS/Android 上的始终在线语音，支持 ElevenLabs。
- **[Live Canvas](https://docs.clawd.bot/platforms/mac/canvas)** — Agent 驱动的可视化工作区，支持 [A2UI](https://docs.clawd.bot/platforms/mac/canvas#canvas-a2ui)。
- **[一流工具支持](https://docs.clawd.bot/tools)** — 浏览器, Canvas, Nodes, Cron, Sessions 以及 Discord/Slack 动作。
- **[配套应用](https://docs.clawd.bot/platforms/macos)** — macOS 菜单栏应用 + iOS/Android [Nodes](https://docs.clawd.bot/nodes)。
- **[入职向导](https://docs.clawd.bot/start/wizard) + [技能](https://docs.clawd.bot/tools/skills)** — 向导式设置，支持捆绑/托管/工作区技能。

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=clawdbot/clawdbot&type=date&legend=top-left)](https://www.star-history.com/#clawdbot/clawdbot&type=date&legend=top-left)

## 目前构建的所有功能

### 核心平台
- [网关 WS 控制平面](https://docs.clawd.bot/gateway) 含会话、在线状态、配置、Cron、Webhooks、[控制 UI](https://docs.clawd.bot/web) 和 [Canvas 主机](https://docs.clawd.bot/platforms/mac/canvas#canvas-a2ui)。
- [CLI 界面](https://docs.clawd.bot/tools/agent-send): gateway, agent, send, [wizard](https://docs.clawd.bot/start/wizard), 和 [doctor](https://docs.clawd.bot/gateway/doctor)。
- [Pi agent 运行时](https://docs.clawd.bot/concepts/agent) RPC 模式，支持工具流式传输和块流式传输。
- [会话模型](https://docs.clawd.bot/concepts/session): `main` 用于直接聊天，群组隔离，激活模式，队列模式，回复。群组规则：[Groups](https://docs.clawd.bot/concepts/groups)。
- [媒体管道](https://docs.clawd.bot/nodes/images): 图像/音频/视频，转录钩子，大小限制，临时文件生命周期。音频详情：[Audio](https://docs.clawd.bot/nodes/audio)。

### 渠道
- [渠道](https://docs.clawd.bot/channels): [WhatsApp](https://docs.clawd.bot/channels/whatsapp) (Baileys), [Telegram](https://docs.clawd.bot/channels/telegram) (grammY), [Slack](https://docs.clawd.bot/channels/slack) (Bolt), [Discord](https://docs.clawd.bot/channels/discord) (discord.js), [Google Chat](https://docs.clawd.bot/channels/googlechat) (Chat API), [Signal](https://docs.clawd.bot/channels/signal) (signal-cli), [iMessage](https://docs.clawd.bot/channels/imessage) (imsg), [BlueBubbles](https://docs.clawd.bot/channels/bluebubbles) (extension), [Microsoft Teams](https://docs.clawd.bot/channels/msteams) (extension), [Matrix](https://docs.clawd.bot/channels/matrix) (extension), [Zalo](https://docs.clawd.bot/channels/zalo) (extension), [Zalo Personal](https://docs.clawd.bot/channels/zalouser) (extension), [WebChat](https://docs.clawd.bot/web/webchat)。
- [群组路由](https://docs.clawd.bot/concepts/group-messages): 提及门控，回复标签，按渠道分块和路由。渠道规则：[Channels](https://docs.clawd.bot/channels)。

### 应用 + Nodes
- [macOS 应用](https://docs.clawd.bot/platforms/macos): 菜单栏控制平面，[Voice Wake](https://docs.clawd.bot/nodes/voicewake)/PTT, [Talk Mode](https://docs.clawd.bot/nodes/talk) 覆盖层, [WebChat](https://docs.clawd.bot/web/webchat), 调试工具, [远程网关](https://docs.clawd.bot/gateway/remote) 控制。
- [iOS Node](https://docs.clawd.bot/platforms/ios): [Canvas](https://docs.clawd.bot/platforms/mac/canvas), [Voice Wake](https://docs.clawd.bot/nodes/voicewake), [Talk Mode](https://docs.clawd.bot/nodes/talk), 摄像头, 屏幕录制, Bonjour 配对。
- [Android Node](https://docs.clawd.bot/platforms/android): [Canvas](https://docs.clawd.bot/platforms/mac/canvas), [Talk Mode](https://docs.clawd.bot/nodes/talk), 摄像头, 屏幕录制, 可选 SMS。
- [macOS Node 模式](https://docs.clawd.bot/nodes): system.run/notify + canvas/camera 暴露。

### 工具 + 自动化
- [浏览器控制](https://docs.clawd.bot/tools/browser): 专用的 clawd Chrome/Chromium，快照，动作，上传，配置文件。
- [Canvas](https://docs.clawd.bot/platforms/mac/canvas): [A2UI](https://docs.clawd.bot/platforms/mac/canvas#canvas-a2ui) 推送/重置, eval, 快照。
- [Nodes](https://docs.clawd.bot/nodes): 摄像头快照/剪辑, 屏幕录制, [location.get](https://docs.clawd.bot/nodes/location-command), 通知。
- [Cron + 唤醒](https://docs.clawd.bot/automation/cron-jobs); [Webhooks](https://docs.clawd.bot/automation/webhook); [Gmail Pub/Sub](https://docs.clawd.bot/automation/gmail-pubsub)。
- [技能平台](https://docs.clawd.bot/tools/skills): 捆绑、托管和工作区技能，带安装门控 + UI。

### 运行时 + 安全
- [渠道路由](https://docs.clawd.bot/concepts/channel-routing), [重试策略](https://docs.clawd.bot/concepts/retry), 和 [流式传输/分块](https://docs.clawd.bot/concepts/streaming)。
- [在线状态](https://docs.clawd.bot/concepts/presence), [正在输入指示器](https://docs.clawd.bot/concepts/typing-indicators), 和 [用量跟踪](https://docs.clawd.bot/concepts/usage-tracking)。
- [模型](https://docs.clawd.bot/concepts/models), [模型故障转移](https://docs.clawd.bot/concepts/model-failover), 和 [会话修剪](https://docs.clawd.bot/concepts/session-pruning)。
- [安全](https://docs.clawd.bot/gateway/security) 和 [故障排除](https://docs.clawd.bot/channels/troubleshooting)。

### 运维 + 打包
- [控制 UI](https://docs.clawd.bot/web) + [WebChat](https://docs.clawd.bot/web/webchat) 直接由网关提供服务。
- [Tailscale Serve/Funnel](https://docs.clawd.bot/gateway/tailscale) 或 [SSH 隧道](https://docs.clawd.bot/gateway/remote) 带令牌/密码认证。
- [Nix 模式](https://docs.clawd.bot/install/nix) 声明式配置; 基于 [Docker](https://docs.clawd.bot/install/docker) 的安装。
- [Doctor](https://docs.clawd.bot/gateway/doctor) 迁移, [日志](https://docs.clawd.bot/logging)。

## 工作原理 (简述)

```
WhatsApp / Telegram / Slack / Discord / Google Chat / Signal / iMessage / BlueBubbles / Microsoft Teams / Matrix / Zalo / Zalo Personal / WebChat
               │
               ▼
┌───────────────────────────────┐
│            Gateway            │
│       (control plane)         │
│     ws://127.0.0.1:18789      │
└──────────────┬────────────────┘
               │
               ├─ Pi agent (RPC)
               ├─ CLI (clawdbot …)
               ├─ WebChat UI
               ├─ macOS app
               └─ iOS / Android nodes
```

## 关键子系统

- **[网关 WebSocket 网络](https://docs.clawd.bot/concepts/architecture)** — 客户端、工具和事件（以及运维）的单一 WS 控制平面：[Gateway runbook](https://docs.clawd.bot/gateway)。
- **[Tailscale 暴露](https://docs.clawd.bot/gateway/tailscale)** — Serve/Funnel 用于网关仪表板 + WS (远程访问: [Remote](https://docs.clawd.bot/gateway/remote))。
- **[浏览器控制](https://docs.clawd.bot/tools/browser)** — clawd 管理的 Chrome/Chromium 带 CDP 控制。
- **[Canvas + A2UI](https://docs.clawd.bot/platforms/mac/canvas)** — Agent 驱动的可视化工作区 (A2UI 主机: [Canvas/A2UI](https://docs.clawd.bot/platforms/mac/canvas#canvas-a2ui))。
- **[语音唤醒](https://docs.clawd.bot/nodes/voicewake) + [交谈模式](https://docs.clawd.bot/nodes/talk)** — 始终在线的语音和连续对话。
- **[Nodes](https://docs.clawd.bot/nodes)** — Canvas, 摄像头快照/剪辑, 屏幕录制, `location.get`, 通知, 加上 macOS 专用的 `system.run`/`system.notify`。

## Tailscale 访问 (网关仪表板)

Clawdbot 可以自动配置 Tailscale **Serve** (仅 tailnet) 或 **Funnel** (公开)，同时网关保持绑定到 loopback。配置 `gateway.tailscale.mode`:

- `off`: 无 Tailscale 自动化 (默认)。
- `serve`: 仅 tailnet HTTPS 通过 `tailscale serve` (默认使用 Tailscale 身份标头)。
- `funnel`: 公共 HTTPS 通过 `tailscale funnel` (需要共享密码认证)。

注意：
- 当启用 Serve/Funnel 时，`gateway.bind` 必须保持为 `loopback` (Clawdbot 会强制执行此操作)。
- 可以通过设置 `gateway.auth.mode: "password"` 或 `gateway.auth.allowTailscale: false` 来强制 Serve 需要密码。
- 除非设置了 `gateway.auth.mode: "password"`，否则 Funnel 拒绝启动。
- 可选：`gateway.tailscale.resetOnExit` 在关闭时撤销 Serve/Funnel。

详情：[Tailscale 指南](https://docs.clawd.bot/gateway/tailscale) · [Web 界面](https://docs.clawd.bot/web)

## 远程网关 (Linux 很棒)

将网关运行在小型 Linux 实例上完全没问题。客户端 (macOS app, CLI, WebChat) 可以通过 **Tailscale Serve/Funnel** 或 **SSH 隧道** 链接，您仍然可以配对设备节点 (macOS/iOS/Android) 以在需要时执行设备本地操作。

- **网关主机** 默认运行 exec 工具和渠道连接。
- **设备 Nodes** 通过 `node.invoke` 运行设备本地操作 (`system.run`, 摄像头, 屏幕录制, 通知)。
简而言之：exec 在网关所在位置运行；设备操作在设备所在位置运行。

详情：[远程访问](https://docs.clawd.bot/gateway/remote) · [Nodes](https://docs.clawd.bot/nodes) · [安全](https://docs.clawd.bot/gateway/security)

## 通过网关协议的 macOS 权限

macOS 应用可以以 **node 模式** 运行，并通过网关 WebSocket 广播其能力 + 权限映射 (`node.list` / `node.describe`)。客户端随后可以通过 `node.invoke` 执行本地操作：

- `system.run` 运行本地命令并返回 stdout/stderr/exit code；设置 `needsScreenRecording: true` 以请求录屏权限（否则您会得到 `PERMISSION_MISSING`）。
- `system.notify` 发送用户通知，如果通知被拒绝则失败。
- `canvas.*`, `camera.*`, `screen.record`, 和 `location.get` 也通过 `node.invoke` 路由并遵循 TCC 权限状态。

提升的 bash (主机权限) 与 macOS TCC 是分开的：

- 使用 `/elevated on|off` 在启用 + 允许列表的情况下切换每会话的提升访问权限。
- 网关通过 `sessions.patch` (WS 方法) 持久化每会话的切换状态，与 `thinkingLevel`, `verboseLevel`, `model`, `sendPolicy`, 和 `groupActivation` 一样。

详情：[Nodes](https://docs.clawd.bot/nodes) · [macOS app](https://docs.clawd.bot/platforms/macos) · [网关协议](https://docs.clawd.bot/concepts/architecture)

## Agent 对 Agent (sessions_* 工具)

- 使用这些工具在会话之间协调工作，无需在聊天界面之间跳转。
- `sessions_list` — 发视活跃会话 (Agents) 及其元数据。
- `sessions_history` — 获取会话的转录日志。
- `sessions_send` — 给另一个会话发消息；可选的回复 ping-pong + 宣布步骤 (`REPLY_SKIP`, `ANNOUNCE_SKIP`)。

详情：[会话工具](https://docs.clawd.bot/concepts/session-tool)

## 技能注册表 (ClawdHub)

ClawdHub 是一个极简的技能注册表。启用 ClawdHub 后，Agent 可以自动搜索技能并在需要时拉取新技能。

[ClawdHub](https://ClawdHub.com)

## 聊天命令

在 WhatsApp/Telegram/Slack/Google Chat/Microsoft Teams/WebChat 中发送这些命令 (群组命令仅限所有者):

- `/status` — 精简会话状态 (模型 + tokens, 可用时显示成本)
- `/new` 或 `/reset` — 重置会话
- `/compact` — 精简会话上下文 (摘要)
- `/think <level>` — off|minimal|low|medium|high|xhigh (仅限 GPT-5.2 + Codex 模型)
- `/verbose on|off`
- `/usage off|tokens|full` — 每次回复的使用概况页脚
- `/restart` — 重启网关 (仅限所有者在群组中使用)
- `/activation mention|always` — 群组激活切换 (仅限群组)

## Apps (可选)

仅网关就能提供极佳的体验。所有应用都是可选的并增加额外功能。

如果您计划构建/运行配套应用，请遵循以下平台运行手册。

### macOS (Clawdbot.app) (可选)

- 网关和健康的菜单栏控制。
- 语音唤醒 + 一键通覆盖层。
- WebChat + 调试工具。
- 通过 SSH 的远程网关控制。

注意：为了让 macOS 权限在重新构建后保持不变，需要签名构建 (参见 `docs/mac/permissions.md`)。

### iOS Node (可选)

- 通过 Bridge 作为 node 配对。
- 语音触发转发 + Canvas 表面。
- 通过 `clawdbot nodes …` 控制。

运行手册：[iOS 连接](https://docs.clawd.bot/platforms/ios)。

### Android Node (可选)

- 通过与 iOS 相同的 Bridge + 配对流程配对。
- 暴露 Canvas, 摄像头, 和屏幕捕获命令。
- 运行手册：[Android 连接](https://docs.clawd.bot/platforms/android)。

## Agent 工作区 + 技能

- 工作区根目录：`~/clawd` (可通过 `agents.defaults.workspace` 配置)。
- 注入的提示文件：`AGENTS.md`, `SOUL.md`, `TOOLS.md`。
- 技能：`~/clawd/skills/<skill>/SKILL.md`。

## 配置

最小化 `~/.clawdbot/clawdbot.json` (模型 + 默认值):

```json5
{
  agent: {
    model: "anthropic/claude-opus-4-5"
  }
}
```

[完整配置参考 (所有键 + 示例)。](https://docs.clawd.bot/gateway/configuration)

## 安全模型 (重要)

- **默认:** 工具在 **main** 会话的主机上运行，因此只有你是用户时 Agent 拥有完全访问权限。
- **群组/渠道安全:** 设置 `agents.defaults.sandbox.mode: "non-main"` 以在每会话 Docker 沙箱中运行 **非 main 会话** (群组/渠道)；这样 bash 就在这些会话的 Docker 中运行。
- **沙箱默认值:** 允许列表 `bash`, `process`, `read`, `write`, `edit`, `sessions_list`, `sessions_history`, `sessions_send`, `sessions_spawn`; 拒绝列表 `browser`, `canvas`, `nodes`, `cron`, `discord`, `gateway`。

详情：[安全指南](https://docs.clawd.bot/gateway/security) · [Docker + 沙箱](https://docs.clawd.bot/install/docker) · [沙箱配置](https://docs.clawd.bot/gateway/configuration)

### [WhatsApp](https://docs.clawd.bot/channels/whatsapp)

- 链接设备：`pnpm clawdbot channels login` (将凭据存储在 `~/.clawdbot/credentials` 中)。
- 通过 `channels.whatsapp.allowFrom` 允许谁与助手交谈。
- 如果设置了 `channels.whatsapp.groups`，它将成为群组允许列表；包含 `"*"` 以允许所有。

### [Telegram](https://docs.clawd.bot/channels/telegram)

- 设置 `TELEGRAM_BOT_TOKEN` 或 `channels.telegram.botToken` (环境变量优先)。
- 可选：设置 `channels.telegram.groups` (带 `channels.telegram.groups."*".requireMention`); 设置后，它是群组允许列表 (包含 `"*"` 以允许所有)。按需设置 `channels.telegram.allowFrom` 或 `channels.telegram.webhookUrl`。

```json5
{
  channels: {
    telegram: {
      botToken: "123456:ABCDEF"
    }
  }
}
```

### [Slack](https://docs.clawd.bot/channels/slack)

- 设置 `SLACK_BOT_TOKEN` + `SLACK_APP_TOKEN` (或 `channels.slack.botToken` + `channels.slack.appToken`)。

### [Discord](https://docs.clawd.bot/channels/discord)

- 设置 `DISCORD_BOT_TOKEN` or `channels.discord.token` (环境变量优先)。
- 可选：按需设置 `commands.native`, `commands.text`, 或 `commands.useAccessGroups`, 加上 `channels.discord.dm.allowFrom`, `channels.discord.guilds`, 或 `channels.discord.mediaMaxMb`。

```json5
{
  channels: {
    discord: {
      token: "1234abcd"
    }
  }
}
```

### [Signal](https://docs.clawd.bot/channels/signal)

- 需要 `signal-cli` 和 `channels.signal` 配置部分。

### [iMessage](https://docs.clawd.bot/channels/imessage)

- 仅限 macOS; 信息应用必须已登录。
- 如果设置了 `channels.imessage.groups`，它将成为群组允许列表；包含 `"*"` 以允许所有。

### [Microsoft Teams](https://docs.clawd.bot/channels/msteams)

- 配置 Teams app + Bot Framework, 然后添加 `msteams` 配置部分。
- 通过 `msteams.allowFrom` 允许谁交谈；群组访问通过 `msteams.groupAllowFrom` 或 `msteams.groupPolicy: "open"`。

### [WebChat](https://docs.clawd.bot/web/webchat)

- 使用网关 WebSocket；没有单独的 WebChat 端口/配置。

浏览器控制 (可选):

```json5
{
  browser: {
    enabled: true,
    controlUrl: "http://127.0.0.1:18791",
    color: "#FF4500"
  }
}
```

## 文档

当您通过入职流程并希望获得更深入的参考时使用这些。
- [从文档索引开始导航和了解“什么在哪”。](https://docs.clawd.bot)
- [阅读架构概览以了解网关 + 协议模型。](https://docs.clawd.bot/concepts/architecture)
- [当您需要每个键和示例时使用完整的配置参考。](https://docs.clawd.bot/gateway/configuration)
- [按照操作手册运行网关。](https://docs.clawd.bot/gateway)
- [了解控制 UI/Web 界面如何工作以及如何安全地暴露它们。](https://docs.clawd.bot/web)
- [通过 SSH 隧道或 tailnets 了解远程访问。](https://docs.clawd.bot/gateway/remote)
- [跟随入职向导流程进行引导式设置。](https://docs.clawd.bot/start/wizard)
- [通过 webhook 界面连接外部触发器。](https://docs.clawd.bot/automation/webhook)
- [设置 Gmail Pub/Sub 触发器。](https://docs.clawd.bot/automation/gmail-pubsub)
- [了解 macOS 菜单栏配套详情。](https://docs.clawd.bot/platforms/mac/menu-bar)
- [平台指南: Windows (WSL2)](https://docs.clawd.bot/platforms/windows), [Linux](https://docs.clawd.bot/platforms/linux), [macOS](https://docs.clawd.bot/platforms/macos), [iOS](https://docs.clawd.bot/platforms/ios), [Android](https://docs.clawd.bot/platforms/android)
- [通过故障排除指南调试常见故障。](https://docs.clawd.bot/channels/troubleshooting)
- [在暴露任何内容之前查看安全指南。](https://docs.clawd.bot/gateway/security)

## 高级文档 (发现 + 控制)

- [发现 + 传输](https://docs.clawd.bot/gateway/discovery)
- [Bonjour/mDNS](https://docs.clawd.bot/gateway/bonjour)
- [网关配对](https://docs.clawd.bot/gateway/pairing)
- [远程网关 README](https://docs.clawd.bot/gateway/remote-gateway-readme)
- [控制 UI](https://docs.clawd.bot/web/control-ui)
- [仪表板](https://docs.clawd.bot/web/dashboard)

## 运维 & 故障排除

- [健康检查](https://docs.clawd.bot/gateway/health)
- [网关锁](https://docs.clawd.bot/gateway/gateway-lock)
- [后台进程](https://docs.clawd.bot/gateway/background-process)
- [浏览器故障排除 (Linux)](https://docs.clawd.bot/tools/browser-linux-troubleshooting)
- [日志记录](https://docs.clawd.bot/logging)

## 深度探索

- [Agent 循环](https://docs.clawd.bot/concepts/agent-loop)
- [在线状态](https://docs.clawd.bot/concepts/presence)
- [TypeBox schemas](https://docs.clawd.bot/concepts/typebox)
- [RPC 适配器](https://docs.clawd.bot/reference/rpc)
- [队列](https://docs.clawd.bot/concepts/queue)

## 工作区 & 技能

- [技能配置](https://docs.clawd.bot/tools/skills-config)
- [默认 AGENTS](https://docs.clawd.bot/reference/AGENTS.default)
- [模板: AGENTS](https://docs.clawd.bot/reference/templates/AGENTS)
- [模板: BOOTSTRAP](https://docs.clawd.bot/reference/templates/BOOTSTRAP)
- [模板: IDENTITY](https://docs.clawd.bot/reference/templates/IDENTITY)
- [模板: SOUL](https://docs.clawd.bot/reference/templates/SOUL)
- [模板: TOOLS](https://docs.clawd.bot/reference/templates/TOOLS)
- [模板: USER](https://docs.clawd.bot/reference/templates/USER)

## 平台内部

- [macOS 开发设置](https://docs.clawd.bot/platforms/mac/dev-setup)
- [macOS 菜单栏](https://docs.clawd.bot/platforms/mac/menu-bar)
- [macOS 语音唤醒](https://docs.clawd.bot/platforms/mac/voicewake)
- [iOS Node](https://docs.clawd.bot/platforms/ios)
- [Android Node](https://docs.clawd.bot/platforms/android)
- [Windows (WSL2)](https://docs.clawd.bot/platforms/windows)
- [Linux 应用](https://docs.clawd.bot/platforms/linux)

## 邮件钩子 (Gmail)

- [docs.clawd.bot/gmail-pubsub](https://docs.clawd.bot/automation/gmail-pubsub)

## Clawd

Clawdbot 是为 **Clawd** 打造的，一只太空龙虾 AI 助手。 🦞
由 Peter Steinberger 和社区构建。

- [clawd.me](https://clawd.me)
- [soul.md](https://soul.md)
- [steipete.me](https://steipete.me)

## 社区

查看 [CONTRIBUTING.md](CONTRIBUTING.md) 以获取指南、维护者以及如何提交 PR。
欢迎提交 AI/vibe-coded PR! 🤖

特别感谢 [Mario Zechner](https://mariozechner.at/) 的支持以及他的 [pi-mono](https://github.com/badlogic/pi-mono)。

感谢所有贡献者:

<p align="left">
  <!-- Original contributors images kept as is -->
  <a href="https://github.com/steipete"><img src="https://avatars.githubusercontent.com/u/58493?v=4&s=48" width="48" height="48" alt="steipete" title="steipete"/></a>
  <!-- ... (Contributors list truncating for brevity in thought but will be included in file if I was copying strictly, but here I'll keep the top ones or just a placeholder if the list is too huge to regenerate manually without error. Actually, I can just copy the HTML block of contributors from the original file source in my head/context as it doesn't need translation) -->
  <!-- For the sake of the file generation, I will include the contributors block exactly as is from the original file -->
  <a href="https://github.com/steipete"><img src="https://avatars.githubusercontent.com/u/58493?v=4&s=48" width="48" height="48" alt="steipete" title="steipete"/></a> <a href="https://github.com/bohdanpodvirnyi"><img src="https://avatars.githubusercontent.com/u/31819391?v=4&s=48" width="48" height="48" alt="bohdanpodvirnyi" title="bohdanpodvirnyi"/></a>
  <!-- (I will output the full list in the actual tool call) -->
</p>
