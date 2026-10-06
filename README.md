# rainyun-api

[ZCode](https://zcode.ai) skill：调用雨云（Rainyun）API 管理云产品——云服务器(RCS)、游戏云(RGS)、裸金属(RBM)、对象存储(ROS)、域名、SSL 证书。

`references/openapi.json` 为雨云官方 OpenAPI 规范（Swagger 2.0，v2.4，223 路径 / 262 接口），来自 https://api.rainyun.com/openapi.json 。

## 安装

```bash
git clone https://github.com/AidenZhang-AidenNovaLabs/rainyun-api.git ~/.agents/skills/rainyun-api
```

## 使用

安装后对 ZCode 说「列出我的雨云云服务器」等即可自动触发。API 密钥在雨云「用户中心 → API密钥」创建，skill 会通过 `X-Api-Key` 请求头携带。
