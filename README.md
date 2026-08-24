# JJ-stash-config

# Stash iOS 配置文件

> 专为 iOS 平台优化的 Stash 代理配置文件，采用 YAML 格式编写，支持远程规则集自动更新与策略组智能分流。
> ⚠️如用于覆写，请自行删除 `-proxy-providers` 代码段落。

## 🚀 快速开始

### 前置要求

- iOS 设备（系统版本 ≥ iOS 14.0）
- 已安装 [Stash - Rule Based Proxy](https://apps.apple.com/app/stash-rule-based-proxy/id1596063349)（需非国区 Apple ID）

### 导入配置

1. **下载配置文件**：将本仓库中的 `JJ-stash-config.yaml` 下载到你的 iOS 设备（可通过 iCloud Drive、AirDrop 等方式）
2. **导入 Stash**：打开 Stash → 进入「配置列表」标签页 → 选择「从文件导入」或「从 URL 下载」（配置下载地址见下方）
3. **填写机场订阅地址**：填写方法见下方
4. **启动代理**：返回主页，点击顶部「启动」按钮

## 🔧 填写机场订阅地址

本配置文件使用 `proxy-providers` 从远程订阅地址自动获取代理节点。你需要将自己的订阅链接填入配置文件中。

#### 方法一：「从文件导入」

1. **下载`JJ-stash-config.yaml`，用记事本或其他编辑器打开，填写机场订阅地址并保存。**
2. **在Stash中选择「从文件导入」将`JJ-stash-config.yaml`导入Stash。**

具体:找到 `JJ-stash-config.yaml` 中的 `proxy-providers` 部分，将 `url` 字段的值替换为你的机场订阅链接：

```yaml
proxy-providers:
  Airport1:
    url: "https://"          # 替换为你的机场订阅地址
    path: ./providers/Airport1.yaml
    interval: 43200          #订阅定期更新时间（秒），不更新填写0
```

#### 方法二：「从 URL 下载」

1. **在Stash中选择「从 URL 下载」，复制粘贴下面的🔗 配置下载地址，完成配置导入。**
2. **在Stash中点击已导入的配置文件`JJ-stash-config`，选择「可视化编辑器」（创建副本防止配置更新覆盖机场订阅）**

在`可视化编辑器`→`代理`→`远程代理集`→`Airport1`中填写你自己的机场订阅地址。

## 🔗 配置下载地址

### 直接在 Safar 浏览器中打开以下链接快速导入：

**原始链接：**
```text
stash://install-config?url=https://raw.githubusercontent.com/sydneygao/JJ-stash-config/main/JJ-stash-config.yaml
```

**国内加速🚀：**
```text
stash://install-config?url=https://cdn.jsdelivr.net/gh/sydneygao/JJ-stash-config@main/JJ-stash-config.yaml
```

### 在Stash app中选择「从URL下载」填写以下链接：

 **原始链接：**
```text
https://raw.githubusercontent.com/sydneygao/JJ-stash-config/main/JJ-stash-config.yaml
```

 **国内加速🚀：** 
 ```text
https://cdn.jsdelivr.net/gh/sydneygao/JJ-stash-config@main/JJ-stash-config.yaml
```

## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源协议。你可以自由使用、修改、分发本配置，但需保留原作者的版权声明。

## 🤝 贡献

欢迎提交 Issue 或 Pull Request 来改进本配置！
