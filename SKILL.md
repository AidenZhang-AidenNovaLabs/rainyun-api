---
name: rainyun-api
description: 调用雨云（Rainyun）API 管理云产品。凡涉及雨云/Rainyun 的云服务器(RCS)、游戏云(RGS)、裸金属(RBM)、对象存储(ROS)、域名解析、SSL 证书的查询、创建、续费、改配、删除等操作，或用户提到"雨云 API"，都使用本技能——即使没明说"API"三个字。
---

# 雨云 API

完整接口定义在 `references/openapi.json`（Swagger 2.0，v2.4，223 路径 / 262 接口，中文摘要）。
不要凭记忆猜接口路径或参数——先查 spec，再发请求。

## 基本约定

- Base URL：`https://api.v2.rainyun.com`
- 鉴权：请求头 `X-Api-Key: <密钥>`。密钥由用户在雨云「用户中心 → API密钥」页面创建；没有时向用户要，不要伪造或用旧测试值。
- 请求体和响应均为 JSON。写/删操作走对应 POST/PATCH/DELETE。

## 查接口

1. 用 python 过滤 `references/openapi.json` 的 `paths`，按 summary（中文）或 path 关键词找目标接口，读出 method、path、parameters、definitions 中的请求/响应结构。
2. 产品分组（tags）：`rcs`=云服务器(57)、`rgs`=游戏云/面板(80)、`rbm`=RBM(24)、`ros`=对象存储(36)、`domain`=域名(38)、`ssl`=SSL证书(21)、`public`=公共(6)。
3. 路径里的 `{id}` 是实例 ID，先调对应的列表接口拿到。

## 示例

```bash
# 列出云服务器
curl -s -H "X-Api-Key: $RAINYUN_KEY" "https://api.v2.rainyun.com/product/rcs/"

# 公共接口无需鉴权，可用于验证网络连通
curl -s "https://api.v2.rainyun.com/app_config"
```

## 注意

- 涉及删除、退订、改配的操作，执行前先向用户确认目标实例 ID 和后果。
- 首次调用建议先发一个只读列表请求验证密钥有效，再执行写操作。
