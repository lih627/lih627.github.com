---
layout: article
title: 华硕梅林系统 wifi 设置
tags: wifi
---

wifi 配置记录, 基于使用梅林系统的 BE-88U, 使用梅林版本为 3.0.0.6.102_33921_koolcenter

<!--more-->

# 路由器开启 ssh

刷新梅林后, 路由器默认ip 为 `192.168.50.1`, 系统管理 -> 系统设置 -> 启用 ssh 可以开启 ssh.
为了安全性, 我设置 LAN only, 端口 24

```
ssh user@192.168.50.1 -p 24
```

测试可以连上.


# 内网 DNS 解析

希望在连接 wifi 的情况下, 访问 www.asusrouter.com 自动跳转到 192.168.50.1 的路由器界面.
同时在连接 wifi 的情况下, 访问我个人域名直接跳转到内网ip.

首先要将自己的设备DNS服务器切换成路由器的, MacOS 系统设置 -> 网络 -> 详细信息 -> DNS, 将设置的`8.8.8.8`这种google DNS 服务都删掉. 下图是配置好的样子.
![pic](/imgs/wifi-config/macos_wifi_dns.png){:height="100%" width="100%"}

华硕路由器通过 dnsmasq 控制域名解析. 下一步ssh到华硕路由器配置 dnsmasq.

```
ssh user@192.168.50.1 -p 24
# 登陆后, 进入 jffs 分区, 注意华硕 /etc 分区是非持久化分区, 每次重启其中的 hosts 都会修改.

cd /jffs/configs/dnsmasq.d
vi dnsmasq.conf.add
# 写入 address=/test.top/192.168.50.11 保存
```
上面将 test.top 直接定向到本地的 192.168.50.11.

配置文件写好后, 重新启动路由器服务:

```
service restart_dnsmasq
```

路由器端配置结束, 在路由器查看配置是否正确

```
lihao@RT-BE88U-66A0:/jffs/configs# nslookup test.top 127.0.0.1
Server:    127.0.0.1
Address 1: 127.0.0.1 localhost.localdomain

Name:      nonote.top
Address 1: 192.168.50.11 xxxxxx.www.asusrouter.com
```

返回笔记本电脑端, 需要处理两个事情:
- 之前的DNS缓存清空
```
sudo dscacheutil -flushcache
sudo killall -HUP mDNSResponder
```
- VPN 等给对应域名设置白名单, Clash 更多设置 -> 忽略主机与域的代理设置
```
# Clash 白名单
192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,127.0.0.1,localhost,*.local,timestamp.apple.com,sequoia.apple.com,seed-sequoia.siri.apple.com,test.top,www.asusrouter.com
```

配置结束后, 本地可以通过 `nslookup test.top` 查看对应 ip 是否正确.