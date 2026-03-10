---
layout: post
title:  "Ubuntu Server Use Proxy"
date:   2026-03-10 11:51:20 +0800
categories: basic tutorial
usemathjax: true
---


# Ubuntu for Server Use Proxy

## 1. 安装V2Ray Core

```bash
# 安装依赖
sudo apt update && sudo apt install curl unzip -y

# 下载并执行官方安装脚本
bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)

```

## 2. 编写配置文件
输入指令:
`sudo vim /usr/local/etc/v2ray/config.json`  

**日志配置**：记录 warning 级别及以上的日志到 `/var/log/v2ray/`。

**本地监听入口**：
- 端口 `1080`：SOCKS5 代理，支持 UDP 及流量嗅探
- 端口 `1081`：HTTP 代理
- 两个端口均只监听 `127.0.0.1`，不对外暴露

**流量出口**：
- `proxy`：通过 VMess + WebSocket 协议连接远程代理服务器
- `direct`：直连，不走代理

**路由规则**：私有 IP（局域网）走直连，其余流量走代理。

> **注意**：以下 `address`、`port`、`id`、`alterId`、`path`、`Host` 需要替换为自己的节点信息。

```json
{
  "log": {
    "loglevel": "warning",
    "access": "/var/log/v2ray/access.log",
    "error": "/var/log/v2ray/error.log"
  },
  "inbounds": [
    {
      "port": 1080,
      "listen": "127.0.0.1",
      "protocol": "socks",
      "settings": {
        "auth": "noauth",
        "udp": true
      },
      "sniffing": {
        "enabled": true,
        "destOverride": ["http", "tls"]
      }
    },
    {
      "port": 1081,
      "listen": "127.0.0.1",
      "protocol": "http"
    }
  ],
  "outbounds": [
    {
      "protocol": "vmess",
      "settings": {
        "vnext": [
          {
            "address": "your-server-address",
            "port": 12345,
            "users": [
              {
                "id": "your-uuid",
                "alterId": 0,
                "security": "auto"
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "wsSettings": {
          "path": "/your-path",
          "headers": {
            "Host": "your-server-address"
          }
        },
        "security": "none"
      },
      "tag": "proxy"
    },
    {
      "protocol": "freedom",
      "tag": "direct"
    }
  ],
  "routing": {
    "domainStrategy": "IPIfNonMatch",
    "rules": [
      {
        "type": "field",
        "ip": ["geoip:private"],
        "outboundTag": "direct"
      }
    ]
  }
}
```

## 3. 启动和管理V2Ray

```bash
# 重载 systemd 配置
sudo systemctl daemon-reload

# 启动 V2Ray
sudo systemctl start v2ray

# 设置开机自启
sudo systemctl enable v2ray

# 查看运行状态（检查是否正常启动）
sudo systemctl status v2ray
```

- 测试代理是否可用

```bash
# 测试 HTTP 代理
curl --proxy http://127.0.0.1:1081 https://www.google.com

# 测试 SOCKS5 代理
curl --socks5 127.0.0.1:1080 https://www.google.com
```

- 常用命令

```bash
# 停止
sudo systemctl stop v2ray

# 重启（修改配置后必须执行）
sudo systemctl restart v2ray

# 查看日志
sudo journalctl -u v2ray -f
```

- 终端使用代理

```bash
# HTTP/HTTPS 代理
export http_proxy=http://127.0.0.1:1081
export https_proxy=http://127.0.0.1:1081

# 取消代理
unset http_proxy https_proxy
```


## 参考链接

- [v2fly project](https://www.v2fly.org/)
- [v2ray core](https://github.com/v2fly/v2ray-core)
- [fhs-install-v2ray](https://github.com/v2fly/fhs-install-v2ray)







