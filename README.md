# JJ-stash-config

# Stash iOS 配置文件

> 专为 iOS 平台优化的 Stash 代理配置文件，采用 YAML 格式编写，支持远程规则集自动更新与策略组智能分流。
> 本配置文件不是适用于覆写，请填写机场订阅地址后直接使用。
> 如用于覆写，请自行删除-proxy-providers代码段落。

## ✨ 功能特性

- **iOS 原生适配** —— 针对 Stash iOS 客户端进行优化，移除不支持的虚拟节点和格式，确保配置在 iPhone / iPad 上稳定运行
- **远程规则集（Rule-Set）** —— 通过 `rule-providers` 声明并引用外部规则集，支持后台静默更新，无需重载 Stash 即可生效
- **智能策略组（Proxy-Groups）** —— 支持 `url-test` 自动延迟优选、`fallback` 按优先级故障转移、`select` 手动切换等多种策略类型
- **远程代理集（Proxy-Provider）** —— 支持从 URL 自动更新节点列表，策略组可动态引用最新节点
- **覆写（Override）支持** —— 可通过 `.stoverride` 文件对配置进行动态修正，无需编辑原始配置文件
- **低资源占用** —— 使用 `domain` / `ipcidr` 类型规则集替代大量内联规则，有效降低内存占用并提高匹配速度

## 🚀 快速开始

### 前置要求

- iOS 设备（系统版本 ≥ iOS 14.0）
- 已安装 [Stash - Rule Based Proxy](https://apps.apple.com/app/stash-rule-based-proxy/id1596063349)（需非国区 Apple ID）

### 导入配置

1. **下载配置文件**：将本仓库中的 `config.yaml` 下载到你的 iOS 设备（可通过 iCloud Drive、AirDrop 等方式）
2. **导入 Stash**：打开 Stash → 进入「配置」标签页 → 点击右上角「+」→ 选择「从文件导入」或「从 URL 下载」
3. **启动代理**：返回主页，点击顶部「启动」按钮

### 通过 URL 一键导入

你也可以直接在 Safari 中打开以下链接快速导入：

<stash://install-config?url=https://raw.githubusercontent.com/sydneygao/JJ-stash-config/main/jj-config.yaml>

## 📁 配置文件说明

本配置文件遵循 Stash / Clash 标准 YAML 语法，主要包含以下核心字段：

| 字段 | 说明 |
|------|------|
| `mode` | 运行模式：`rule`（规则模式）/ `global`（全局代理）/ `direct`（全局直连） |
| `proxies` | 代理节点定义（如 Shadowsocks、VMess 等） |
| `proxy-providers` | 远程代理集，从 URL 自动更新节点列表 |
| `proxy-groups` | 策略组，定义分流策略和节点选择逻辑 |
| `rule-providers` | 远程规则集声明，引用外部规则文件 |
| `rules` | 分流规则，按优先级从上至下匹配 |

## 📦 引用的外部规则集（Rule-Sets）

本项目通过 `rule-providers` 引用了以下外部规则集：

## 📦 引用的外部规则集（Rule-Sets）

本项目通过 `rule-providers` 引用了以下外部规则集：

### 域名规则集（Domain Rule-Sets）

| 规则集名称 | 类型 | 用途 |
|-----------|------|------|
| `private_domain` | `domain` | 私有域名（内网、本地等） |
| `ai` | `domain` | AI 服务（如 ChatGPT、Claude 等） |
| `youtube_domain` | `domain` | YouTube 视频平台 |
| `google_domain` | `domain` | Google 旗下服务（搜索、Gmail、Drive 等） |
| `github_domain` | `domain` | GitHub 代码托管平台 |
| `spotify_domain` | `domain` | Spotify 音乐流媒体 |
| `telegram_domain` | `domain` | Telegram 即时通讯 |
| `netflix_domain` | `domain` | Netflix 视频流媒体 |
| `paypal_domain` | `domain` | PayPal 支付服务 |
| `whatsapp_domain` | `domain` | WhatsApp 即时通讯 |
| `facebook_domain` | `domain` | Facebook 社交平台 |
| `instagram_domain` | `domain` | Instagram 社交平台 |
| `snapchat_domain` | `domain` | Snapchat 社交平台 |
| `twitter_domain` | `domain` | Twitter（X）社交平台 |
| `discord_domain` | `domain` | Discord 游戏聊天平台 |
| `microsoft_domain` | `domain` | Microsoft 服务（Office 365、Azure 等） |
| `apple_domain` | `domain` | Apple 服务（iCloud、App Store 等） |
| `porn_domain` | `domain` | 成人内容（用于拦截或代理） |
| `games_domain` | `domain` | 海外游戏服务（Nintendo、Steam、Epic、PlayStation 等） |
| `geolocation-!cn` | `domain` | 非中国大陆地区网站聚合 |
| `cn_domain` | `domain` | 中国大陆常用网站域名 |

### IP 规则集（IPCIDR Rule-Sets）

| 规则集名称 | 类型 | 用途 |
|-----------|------|------|
| `private_ip` | `ipcidr` | 私有 IP 地址段（内网） |
| `cn_ip` | `ipcidr` | 中国大陆 IP 地址段 |
| `google_ip` | `ipcidr` | Google 服务 IP 地址段 |
| `telegram_ip` | `ipcidr` | Telegram 服务器 IP 地址段 |
| `netflix_ip` | `ipcidr` | Netflix 服务器 IP 地址段 |
| `apple_ip` | `ipcidr` | Apple 服务 IP 地址段 |

> 所有规则集均来自 [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat) 仓库。

**使用规则集的优势**：
- 低资源占用，适合 iOS 移动设备
- 支持后台静默更新，无需重载 Stash
- `domain` 和 `ipcidr` 类型匹配性能优秀，内存占用低

## 🔧 自定义机场版使用

本配置文件使用 `proxy-providers` 从远程订阅地址自动获取代理节点。你需要将真实的订阅链接填入配置文件中。

找到 `JJ-config.yaml` 中的 `proxy-providers` 部分，将 `url` 字段的值替换为你的机场订阅链接：

```yaml
proxy-providers:
  Airport1:
    url: "机场订阅地址"       # 请替换为您的机场订阅地址
    type: http
    interval: 0              #订阅定期更新时间（秒），不更新填写0
    health-check:
      enable: true
      url: https://www.gstatic.com/generate_204
      interval: 300
```
## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源协议。你可以自由使用、修改、分发本配置，但需保留原作者的版权声明。

## 🤝 贡献

欢迎提交 Issue 或 Pull Request 来改进本配置！

---

# JJ-stash-config

# Stash iOS Configuration Files

> A Stash proxy configuration file optimized for the iOS platform, written in YAML format, with support for automatic remote rule-set updates and intelligent proxy-group routing.
>
> **This configuration is NOT intended for use as an override.** Please fill in your subscription URL and use it directly.
>
> If you intend to use it as an override, please delete the `proxy-providers` section manually.

## ✨ Features

- **iOS Native Optimization** —— Tailored for the Stash iOS client, removing unsupported virtual nodes and formats to ensure stable performance on iPhone / iPad
- **Remote Rule-Sets** —— Declare and reference external rule sets via `rule-providers`, with silent background updates that take effect without reloading Stash
- **Smart Proxy-Groups** —— Supports multiple policy types including `url-test` for automatic latency-based selection, `fallback` for priority-based failover, and `select` for manual switching
- **Remote Proxy-Providers** —— Automatically update proxy lists from URLs, with policy groups dynamically referencing the latest nodes
- **Override Support** —— Use `.stoverride` files to apply dynamic modifications without editing the original configuration
- **Low Resource Usage** —— Use `domain` / `ipcidr` rule sets instead of numerous inline rules, effectively reducing memory usage and improving matching speed

## 🚀 Quick Start

### Prerequisites

- iOS device (system version ≥ iOS 14.0)
- [Stash - Rule Based Proxy](https://apps.apple.com/app/stash-rule-based-proxy/id1596063349) installed (requires a non-China App Store account)

### Import Configuration

1. **Download the config file**: Download `jj-config.yaml` from this repository to your iOS device (via iCloud Drive, AirDrop, etc.)
2. **Import to Stash**: Open Stash → Go to the "Configurations" tab → Tap the 「+」 in the upper right → Select "Import from File" or "Download from URL"
3. **Start Proxy**: Return to the home screen and tap the "Start" button

### One-Click Import via URL

You can also quickly import by opening the following link in Safari:

- 「Download from URL」: `stash://install-config?url=https://raw.githubusercontent.com/sydneygao/JJ-stash-config/main/jj-config.yaml`

## 📁 Configuration Structure

This configuration follows standard Stash / Clash YAML syntax and includes the following core sections:

| Field | Description |
|-------|-------------|
| `mode` | Running mode: `rule` / `global` / `direct` |
| `proxies` | Proxy node definitions (e.g., Shadowsocks, VMess) |
| `proxy-providers` | Remote proxy sets that auto-update node lists from URLs |
| `proxy-groups` | Policy groups that define routing strategies and node selection logic |
| `rule-providers` | Remote rule-set declarations referencing external rule files |
| `rules` | Routing rules, matched from top to bottom by priority |

## 📦 External Rule-Sets Referenced

This project references the following external rule-sets via `rule-providers`:

### Domain Rule-Sets

| Rule-Set Name | Type | Purpose |
|---------------|------|---------|
| `private_domain` | `domain` | Private domains (LAN, local, etc.) |
| `ai` | `domain` | AI services (ChatGPT, Claude, etc.) |
| `youtube_domain` | `domain` | YouTube video platform |
| `google_domain` | `domain` | Google services (Search, Gmail, Drive, etc.) |
| `github_domain` | `domain` | GitHub code hosting |
| `spotify_domain` | `domain` | Spotify music streaming |
| `telegram_domain` | `domain` | Telegram instant messaging |
| `netflix_domain` | `domain` | Netflix video streaming |
| `paypal_domain` | `domain` | PayPal payment service |
| `whatsapp_domain` | `domain` | WhatsApp instant messaging |
| `facebook_domain` | `domain` | Facebook social platform |
| `instagram_domain` | `domain` | Instagram social platform |
| `snapchat_domain` | `domain` | Snapchat social platform |
| `twitter_domain` | `domain` | Twitter (X) social platform |
| `discord_domain` | `domain` | Discord gaming chat platform |
| `microsoft_domain` | `domain` | Microsoft services (Office 365, Azure, etc.) |
| `apple_domain` | `domain` | Apple services (iCloud, App Store, etc.) |
| `porn_domain` | `domain` | Adult content (for blocking or proxying) |
| `games_domain` | `domain` | Overseas gaming services (Nintendo, Steam, Epic, PlayStation, etc.) |
| `geolocation-!cn` | `domain` | Aggregated domains outside mainland China |
| `cn_domain` | `domain` | Common domains from mainland China |

### IPCIDR Rule-Sets

| Rule-Set Name | Type | Purpose |
|---------------|------|---------|
| `private_ip` | `ipcidr` | Private IP address ranges (LAN) |
| `cn_ip` | `ipcidr` | Mainland China IP address ranges |
| `google_ip` | `ipcidr` | Google service IP address ranges |
| `telegram_ip` | `ipcidr` | Telegram server IP address ranges |
| `netflix_ip` | `ipcidr` | Netflix server IP address ranges |
| `apple_ip` | `ipcidr` | Apple service IP address ranges |

> All rule-sets are sourced from the [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat) repository.

**Advantages of using rule-sets**:
- Low resource consumption, ideal for iOS mobile devices
- Silent background updates without reloading Stash
- `domain` and `ipcidr` types offer excellent matching performance with low memory usage

## 🔧 Customizing with Your Subscription

This configuration uses `proxy-providers` to automatically fetch proxy nodes from a remote subscription URL. You need to fill in your actual subscription link in the configuration file.

Locate the `proxy-providers` section in `jj-config.yaml` and replace the `url` field value with your subscription address:

```yaml
proxy-providers:
  Airport1:
    url: "YOUR_SUBSCRIPTION_URL"       # Replace with your subscription URL
    type: http
    interval: 0                        # Update interval in seconds (set to 0 to disable auto-update)
    health-check:
      enable: true
      url: https://www.gstatic.com/generate_204
      interval: 300
```
Important: Do not commit configuration files containing real subscription links to public repositories. Use placeholders (e.g., YOUR_SUBSCRIPTION_URL) and replace them manually before use.

📄 License
This project is licensed under the MIT License. You are free to use, modify, and distribute this configuration, provided that the original copyright notice is retained.

🤝 Contributing
Issues and Pull Requests are welcome!
