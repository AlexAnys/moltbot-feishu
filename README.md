# feishu-openclaw

[![npm version](https://img.shields.io/npm/v/feishu-openclaw.svg)](https://www.npmjs.com/package/feishu-openclaw)

> **🆕 2025.1.31**：v0.3.0 多版本兼容，支持 Clawdbot / OpenClaw

飞书 × AI 助手插件 — 无需服务器  
Feishu × AI Assistant plugin — no server required

---

## 🤖 一键安装 / One-Click Install

**复制以下内容发给你的 Clawdbot：**

```
帮我安装飞书插件，参考这个页面：https://github.com/AlexAnys/openclaw-feishu
```

Clawdbot 会自动：
1. 安装插件
2. 引导你配置 App ID / App Secret
3. 重启 Gateway

---

## ⚠️ 安装前必做 / Before Installing

### 创建飞书机器人（约 5 分钟）

1. [飞书开放平台](https://open.feishu.cn/app) → **创建企业自建应用**
2. 添加「**机器人**」能力
3. **权限配置** → 开启：
   - `im:message`
   - `im:message.group_at_msg`
   - `im:message.p2p_msg`
4. **事件订阅** → 添加 `im.message.receive_v1` → ⚠️ **必须选「长连接」**（不是 webhook）
5. **版本管理** → 创建版本 → 发布上线
6. 记下 **App ID** (`cli_xxx`) 和 **App Secret**

---

## 📦 安装方式 / Install Methods

| 方式 | 说明 | 链接 |
|------|------|------|
| **① 一键安装** | 复制上方内容给 Clawdbot | 本页 ⬆️ |
| **② npm 命令** | `clawdbot plugins install feishu-openclaw` | [npm](https://www.npmjs.com/package/feishu-openclaw) |
| **③ 独立桥接** | 独立进程，生产/隔离部署 | [feishu-openclaw](https://github.com/AlexAnys/feishu-openclaw) |

### 插件 vs 桥接

| | 插件 (①②) | 桥接 (③) |
|---|---|---|
| 进程 | 1 个（内置 Gateway） | 2 个（独立） |
| 崩溃 | 影响 Gateway | 互不影响 |
| 适合 | 日常使用 | 生产环境 |

---

## 🔧 手动配置 / Manual Config

如果没用一键安装，手动配置：

```bash
clawdbot config set channels.feishu.enabled true --json
clawdbot config set channels.feishu.appId "cli_你的AppID"
clawdbot config set channels.feishu.appSecret "你的AppSecret"
clawdbot gateway restart
```

---

## ❗ 常见问题 / Troubleshooting

### 收不到消息？

| 检查项 | 说明 |
|--------|------|
| 应用已发布 | 不是草稿状态 |
| 用「长连接」 | **不是 webhook** |
| 权限已开启 | 三个 im 权限 |

### 报错 `not configured`？

**必须用 `appSecret`，不支持 `appSecretPath`**：

```bash
# ✅ 正确
clawdbot config set channels.feishu.appSecret "你的secret"

# ❌ 错误
clawdbot config set channels.feishu.appSecretPath "/path/to/file"
```

### 群聊不回复？

@机器人，或消息末尾加问号。

---

## 特点 / Features

- ✅ 无需服务器 — WebSocket 长连接
- ✅ 私聊 + 群聊
- ✅ 图片文件收发
- ✅ 多账号支持

---

## 链接 / Links

- 📦 [npm: feishu-openclaw](https://www.npmjs.com/package/feishu-openclaw)
- 🔌 [GitHub: openclaw-feishu](https://github.com/AlexAnys/openclaw-feishu) (本项目)
- 🌉 [GitHub: feishu-openclaw](https://github.com/AlexAnys/feishu-openclaw) (桥接)
- 📖 [Clawdbot 文档](https://docs.clawd.bot)

## License

MIT
