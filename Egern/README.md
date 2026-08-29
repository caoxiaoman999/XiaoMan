# Egern 配置（小满的松鼠🐿️ 2.1）

小满的 Egern 2.1 配置，带详细中文注释，适合新手参考。

## 配置文件

[XiaoManEgern2.1.yaml](XiaoManEgern2.1.yaml) — 完整注释版配置

## 配置链接

```
https://raw.githubusercontent.com/CaoXiaoMann/XiaoMan/main/Egern/XiaoManEgern2.1.yaml
```

## 🚀 新手使用教程

### 第 1 步：导入配置

1. 打开 **Egern** → 配置（Configuration）
2. 从 URL 导入 → 粘贴上面的链接

### 第 2 步：安装 CA 证书（必做）

配置里证书已删除，需要自己生成：

1. Egern → 设置 → 生成 CA 证书
2. 安装证书到 iPhone（设置 → 已下载描述文件 → 安装）
3. 设置 → 通用 → 关于本机 → 证书信任设置 → 开启信任

### 第 3 步：添加机场订阅（必做！）

> ⚠️ 不添加订阅 = 策略组为空 = 无法上网！

1. Egern → 订阅（Subscription）→ 添加你的机场订阅链接
2. 更新订阅
3. PROXY 策略组里就能看到 港/台/日/韩/美/泰 各分组

---

## 📝 配置结构说明（在哪里添加什么）

打开 `XiaoManEgern2.1.yaml`，按需修改：

| 位置 | 配置项 | 你要做什么 |
|------|--------|-----------|
| **基础设置** | `ipv6`、`http_port` 等 | 一般不用改 |
| **DNS** | `bootstrap`、`upstreams` | 改 DNS 服务器 |
| **策略组** | `policy_groups` | 添加/修改节点分组（smart 类型自动从订阅筛选） |
| **分流规则** | `rules` | 添加/修改分流规则（广告拦截、国内外分流等） |
| **URL 重写** | `url_rewrites` | 添加网页跳转规则 |
| **脚本** | `scriptings` | 添加脚本链接（小组件用的） |
| **MITM** | `mitm` | 添加需要解密的域名（`hostnames.includes`） |
| **HTTP 抓包** | `http_captures` | 添加需要抓包的域名 |
| **小组件** | `widgets` | 添加桌面小组件（`script_name` 对应上面 `scriptings` 的 `name`） |
| **模块** | `modules` | 添加功能模块（去广告、会员解锁等） |

### 常见操作示例

**添加一个去广告模块：**
```yaml
modules:
- url: https://example.com/ad-block.lpx   # 模块链接
  enabled: true                            # 启用
```

**添加一个桌面小组件：**
```yaml
scriptings:                                # 先在这里添加脚本
- generic:
    name: 我的脚本
    script_url: https://example.com/script.js

widgets:                                   # 再在这里添加小组件
- name: 小组件名称
  script_name: 我的脚本                    # 对应上面 scriptings 的 name
```

**添加一个分流规则：**
```yaml
rules:
- rule_set:
    name: 规则名
    match: https://example.com/rules.list  # 规则集链接
    policy: PROXY                          # 走哪个策略组
    disabled: false
```

## 配置包含

- **基础设置**：IPv4 代理端口、DNS 劫持、隧道模式
- **DNS**：国内外 DNS 分流（国内阿里+腾讯双备份 / 海外 Google DoH 防污染）
- **策略组**：PROXY、Telegram、ChatGPT、港台日韩美泰各地区节点组
- **分流规则**：广告拦截、国内直连、Telegram/TikTok/ChatGPT/Twitter/YouTube/Spotify/Google/GitHub/Apple 分流
- **URL 重写**：google.cn → google.com 跳转
- **脚本**：网络诊断雷达（基础版 + 增强版）
- **小组件**：网络诊断雷达 Pro
- **模块**：Spotify 去广告、广告拦截、Telegram 增强、微信增强、Google 增强、Script Hub、HTTPDNS 拦截、Sub-Store、BoxJs 等

## 注意事项

- **MITM 证书已删除**，导入后需自己生成并信任
- **必须添加机场订阅**，否则策略组为空
- 每天定时自动更新各规则集
- 修改配置后需重新导入或同步

## 来源

- TG频道: https://t.me/XiaoManWangMingTianYa
- 最后更新时间: 2026-08-29 20:23