# XrayR Node Deployment Script

> Currently only supports a single use case. If you need to connect to other panels or systems, feel free to contribute.

## Prerequisites 
- Currently only supports `CentOS 7/8` 
- Requires registration of a `cloudflare` account and application for a [token](https://dash.cloudflare.com/profile/api-tokens) . Users obtain an `SSL` certificate. 
- Uses `SSPanel` as the default panel. To make other changes, please refer to the `XrayR` manual configuration. 
- By default, the client link uses `443` and the server listens on `8443`. If you need to make changes, please configure it manually. 
- `cloudflare` has port restrictions when CDN is enabled. If you need to customize the port, please pay attention to the [guide](https://developers.cloudflare.com/fundamentals/get-started/reference/network-ports/#network-ports-compatible-with-cloudflares-proxy) . 
- Only supports the `Trojan-GO ws` protocol. 
- If you use protocols such as `TCP/UDP`, use `nginx-mod-stream` to process them.

## SSPanel Custom Config
The automatic script defaults to using the `ws` protocol, with `Trojan` service listening on port `8443`, and `nginx` listening on ports `443` and `80`.
Port `80` is used for a fallback website to disguise, while port `443` is used to handle `SSL` proxy forwarding to the `8443` service.

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

## One-Click Installation
First configure the `Custom Config`, and then use the script below for one-click deployment success.

```sh
bash <(curl -fsSL raw.githubusercontent.com/fupengl/xrayr-node.sh/master/trojan-node.sh)
```

## Features 
- Uses `SSPanel-Uim` panel 
- `Trojan-go` ws protocol 
- Automatically applies for a `cloudflare` certificate 
- Uses `nginx` to process `ssl websocket` 
- Automatically wraps `IPV4/IPV6` network cards using `cloudflare wrap` to solve website blocking of `VPS` addresses 
- Supports `cloudflare CDN` configuration

## Related Links 
- [SSPanel-Uim](https://github.com/Anankke/SSPanel-Uim) 
- [XrayR](https://github.com/XrayR-project/XrayR) 
- [XrayR-release](https://github.com/XrayR-project/XrayR-release/) 
- [warp.sh](https://github.com/P3TERX/warp.sh) 
- [acme.sh](https://github.com/acmesh-official/get.acme.sh)

## License
[MIT](https://github.com/fupengl/xrayr-node.sh/blob/master/LICENSE) © **[fupengl](https://github.com/fupengl)**
