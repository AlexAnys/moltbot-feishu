# openclaw-feishu

[![npm version](https://img.shields.io/npm/v/openclaw-feishu.svg)](https://www.npmjs.com/package/openclaw-feishu)

> **🆕 2025.1.31 更新**：v0.2.0 多版本兼容，修复 Zod schema 问题，支持 Clawdbot / OpenClaw

让 AI 助手接入飞书，无需服务器。  
Connect your AI assistant to Feishu (Lark) — no server required.

---

## 🚀 三种安装方式 / Three Install Methods

| 方式 | 命令 | 适合 | 链接 |
|------|------|------|------|
| **① Clawdbot 一键** | 告诉 Clawdbot：`帮我安装飞书插件` | 新手首选 | — |
| **② npm 插件** ⬅️ | `clawdbot plugins install openclaw-feishu` | 开发者 | [npm](https://www.npmjs.com/package/openclaw-feishu) |
| **③ 独立桥接** | `git clone` + 手动启动 | 生产/隔离 | [GitHub](https://github.com/AlexAnys/feishu-openclaw) |

### 方式对比 / Comparison

| | 插件 (①②) | 桥接 (③) |
|---|---|---|
| 进程数 | 1 个（内置 Gateway） | 2 个（独立进程） |
| 崩溃影响 | 影响 Gateway | 互不影响 |
| 配置方式 | `clawdbot config` | 环境变量 |
| 适合场景 | 日常使用 | 生产/隔离部署 |

---

## 📋 你必须做的事 / What You Must Do

### 1. 创建飞书机器人 / Create Feishu Bot

1. [飞书开放平台](https://open.feishu.cn/app) → 创建企业自建应用
2. 添加「机器人」能力
3. **权限配置** — 开启：
   - `im:message`
   - `im:message.group_at_msg`
   - `im:message.p2p_msg`
4. **事件订阅** → `im.message.receive_v1` → ⚠️ **选「长连接」不是 webhook**
5. 版本管理 → 创建版本 → 发布上线
6. 记下 **App ID** (`cli_xxx`) 和 **App Secret**

### 2. 配置 / Configure

```bash
clawdbot config set channels.feishu.enabled true --json
clawdbot config set channels.feishu.appId "cli_你的AppID"
clawdbot config set channels.feishu.appSecret "你的AppSecret"
clawdbot gateway restart
```

### 3. 测试 / Test

去飞书私聊或群里 @机器人 🎉

---

## ⚠️ 常见问题 / Troubleshooting

### 收不到消息？ / Not receiving messages?

| 检查项 | Check |
|--------|-------|
| 应用已发布（不是草稿） | App is published (not draft) |
| 事件订阅用「长连接」 | Event uses "long connection" |
| 权限都已开启 | All permissions enabled |

### 报错 `not configured`？

**必须用 `appSecret`，不是 `appSecretPath`**：

```bash
# ✅ 正确
clawdbot config set channels.feishu.appSecret "你的secret"

# ❌ 错误 — 插件不支持
clawdbot config set channels.feishu.appSecretPath "/path/to/file"
```

### 群聊不回复？ / No response in groups?

@机器人，或消息末尾加问号。

---

## 特点 / Features

- **无需服务器** — WebSocket 长连接
- **私聊+群聊** — 都支持
- **图片文件** — 收发都行
- **多账号** — 可同时接多个机器人

---

## 链接 / Links

- 📦 [npm: openclaw-feishu](https://www.npmjs.com/package/openclaw-feishu)
- 🔌 [GitHub: openclaw-feishu](https://github.com/AlexAnys/openclaw-feishu) (插件)
- 🌉 [GitHub: feishu-openclaw](https://github.com/AlexAnys/feishu-openclaw) (桥接)
- 📖 [Clawdbot 文档](https://docs.clawd.bot)
- 🐛 [问题反馈](https://github.com/AlexAnys/openclaw-feishu/issues)

## License

MIT
