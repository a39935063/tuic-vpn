# TUIC 一键安装（基于 sing-box）

在自己的 VPS 上一键部署 TUIC v5：自动安装 sing-box、生成账号、签证书、开启 BBR，装完直接打印可导入客户端的 `tuic://` 链接。

## 一键命令

无域名（自签证书，最简单）：

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/a39935063/tuic-vpn/main/install-tuic.sh)
```

有域名（先把域名 A 记录解析到 VPS 的 IP，再用这一条，会自动申请 Let's Encrypt 证书）：

```bash
DOMAIN=tuic.example.com bash <(curl -fsSL https://raw.githubusercontent.com/a39935063/tuic-vpn/main/install-tuic.sh)
```

## 要求

- Debian / Ubuntu + systemd 的 VPS，root 登录
- 公网 IPv4；云厂商安全组放行 `443/udp`（有域名时另需 `80/tcp`）
- 系统防火墙由脚本自动放行

## 装完怎么用

脚本结尾会输出一行 `tuic://...` 链接，复制到支持 TUIC 的客户端导入即可：
v2rayN / Nekoray / sing-box / Shadowrocket / FlClash。

自签模式（无域名）下，客户端需开启「跳过证书验证 / allow insecure」，这是正常的。

## 说明

- 端口默认 443/udp，可用 `PORT=8443` 环境变量改
- UUID 和密码在安装时随机生成，只出现在你自己服务器的输出里，仓库里不含任何账号密码
- 查看日志：`journalctl -u sing-box -f`
