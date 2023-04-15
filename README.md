# XrayR 节点部署脚本

> 目前支持比较单一,如需要对接其他面板或者系统,欢迎 MR 一起共建

## 前置条件
- 目前仅支持 `CentOS 7/8`
- 需要 VPS 有 `IPV6` 地址
- 需要注册 `cloudflare` 账号,申请 [token](https://dash.cloudflare.com/profile/api-tokens), 用户获取 `SSL` 证书
- 默认使用 `SSPanel` 作为面板, 其余要改动可以参照 `XrayR` 手动配置
- 默认客户端链接使用 `443` 服务端监听地址为 `8443`,如果需要改动,手动配置
- `cloudflare` 开启 CDN 有端口限制,如需要自定义端口请注意 [传送门](https://developers.cloudflare.com/fundamentals/get-started/reference/network-ports/#network-ports-compatible-with-cloudflares-proxy)
- 不支持 `Trojan` 协议,仅支持 `Trojan-GO ws` 协议
- 如果走 `TCP/UDP` 等协议使用 `nginx-mod-stream` 处理

## SSPanel Custom Config
自动脚本默认写死使用 `ws` 协议, `Trojan` 服务监听 `8443` 端口, `nginx` 监听 `443`、`80` 端口, 
`80` 用于 `fallback` 网站用于伪装, `443` 用于处理 `SSL` 代理转发到 `8443` 服务
```json
{
  "allow_insecure": false,
  "offset_port_user": "443",
  "offset_port_node": "8443",
  "server_sub": "domain",
  "host": "domain",
  "network": "ws",
  "path": "/ws",
  "ws-opts": {
    "path": "/ws"
  }
}
```

### 一键安装
先配置好 `Custom Config`, 使用下面脚本一键部署成功
```sh
bash <(curl -fsSL raw.githubusercontent.com/fupengl/xrayr-node.sh/master/trojan-node.sh)
```

## 特点
- 使用 `SSPanel-Uim` 面板
- `Trojan-go` ws 协议
- 自动申请 `cloudflare` 证书
- 使用 `nginx` 处理 `ssl/websocket`
- 自动使用 `cloudflare wrap` 包装 `IPV6` 网卡, 解决网站屏蔽 `VPS` 地址问题
- 支持配置 `cloudflare CDN`

## 相关链接
- [SSPanel-Uim](https://github.com/Anankke/SSPanel-Uim)
- [XrayR](https://github.com/XrayR-project/XrayR)
- [XrayR-release](https://github.com/XrayR-project/XrayR-release/)
- [warp.sh](https://github.com/P3TERX/warp.sh)
- [acme.sh](https://github.com/acmesh-official/get.acme.sh)
