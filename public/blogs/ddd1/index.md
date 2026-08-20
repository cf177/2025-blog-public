# DNS 服务产品介绍
域名系统(DNS) 是互联网的电话簿，将人类可读的域名转换为机器可读的IP地址。我们的 DNS 服务提供高性能、安全的解析解决方案。
# 核心优势

⚡ 超低延迟解析

🔒 全面安全防护

🌐 全球分布式节点

📊 实时监控与分析

# 什么是 DNS ？ 
域名系统(DNS) 是互联网的基础设施，负责将域名（如 example.com）转换为IP地址（如 192.0.2.1）。
# DNS 工作原理

用户在浏览器输入网址

本地 DNS 缓存检查

递归 DNS 服务器查询

权威 DNS 服务器响应

IP地址返回浏览器

# 什么是 DoT 和 DoH

DoT 和 DoH 都是加密DNS的一种方式，区别在于它们采用不同的协议和端口，两个都是域名解析安全扩展协议的一种。

DoT 全称 DNS over TLS，它使用 TLS 来传输 DNS 协议。 DoH 全称 DNS over HTTPS，它使用 HTTPS 来传输 DNS 协议。

## 国外公共DNS
## 1. Google Public DNS
提供商：Google IP地址：
```
# IPv4
8.8.8.8
8.8.4.4

# IPv6
2001:4860:4860::8888
2001:4860:4860::8844

# DoH
https://dns.google/dns-query
https://8.8.8.8/dns-query
https://8.8.4.4/dns-query

#DoT
dns.google
```
特点​： 

✅ ​全球覆盖​：依托Google服务器实现低延迟解析 

✅ ​高可用性​：全天候无中断服务 

✅ ​安全防护​：自动屏蔽钓鱼和恶意网站 

🚫 ​局限性​：未提供内容过滤和家长控制功能

## 2. Cloudflare DNS
提供商​：Cloudflare ​IP地址​：
```
# IPV4
1.1.1.1
1.0.0.1

# IPV6
2606:4700:4700::1111
2606:4700:4700::1001

# DoH
https://1.1.1.1/dns-query
https://1.0.0.1/dns-query
https://cloudflare-dns.com/dns-query

# DoT
1dot1dot1dot1.cloudflare-dns.com
cloudflare-dns.com
one.one.one.one
```
```
# 安全版（病毒和钓鱼防御）
# IPv4
1.1.1.2
1.0.0.2

# IPv6
2606:4700:4700::1112
2606:4700:4700::1002

# DoH
https://security.cloudflare-dns.com/dns-query
security.cloudflare-dns.com
```
```
# 家庭版（拦截成人内容）
# IPv4
1.1.1.3
1.0.0.3

# IPv6
2606:4700:4700::1113
2606:4700:4700::1003

# DoH
https://family.cloudflare-dns.com/dns-query
family.cloudflare-dns.com
```
特点​： 

⚡ ​极速响应​：全球平均响应速度<10ms 

🔐 ​隐私优先​：承诺永不记录用户查询日志（已通过第三方审计） 

🛡️ ​安全强化​：与APNIC合作拦截恶意域名 

✨ ​增值服务​：1.1.1.2/1.0.0.2提供恶意软件拦截，1.1.1.3/1.0.0.3增加成人内容过滤

## 3. OpenDNS
提供商​：Cisco 思科 ​IP地址​：
```
# 基础服务
# IPv4
208.67.222.222
208.67.222.220
208.67.220.222
208.67.220.220

# IPV6
2620:0:ccc::2
2620:0:ccd::2

# DoH
https://doh.opendns.com/dns-query
https://dns.opendns.com/dns-query
https://doh.umbrella.com/dns-query
https://dns.umbrella.com/dns-query
https://dns.sse.cisco.com/dns-query

# DoT
dns.opendns.com
dns.umbrella.com
dns.sse.cisco.com
```
```
# 家庭防护，阻止成人内容
# IPV4 Family
208.67.222.123
208.67.220.123

# IPV6
2620:119:35::35
2620:119:53::53

# DoH Family
https://familyshield.opendns.com/dns-query
https://doh.familyshield.opendns.com/dns-query
https://familyshield.sse.cisco.com/dns-query

# DoT
familyshield.opendns.com
familyshield.sse.cisco.com
```
特点​： 

🏠 ​家庭防护​：自动过滤成人/暴力内容（FamilyShield服务） 

📊 ​企业级方案​：提供定制化域名策略（Cisco Umbrella）
 
🔄 ​智能缓存​：预加载热门站点加速访问 

⚠️ ​注意​：基础服务无内容过滤，需付费升级高级功能

## 4. Quad9
提供商​：IBM、PCH、全球网络联盟 ​IP地址​：
```
# 基础版（快速可靠）
# IPv4
9.9.9.9
149.112.112.112

# IPv6
2620:fe::fe
2620:fe::fe:9

# DoH
https://dns.quad9.net/dns-query

# DoT
dns.quad9.net
```
```
# 安全版（病毒和钓鱼防御）
# IPv4
9.9.9.10
149.112.112.10

# IPv6
2620:fe::10
2620:fe::fe:10

# DoH
https://dns10.quad9.net/dns-query

# DoT
dns10.quad9.net
```
```
# 家庭版（拦截成人内容）
# IPv4
9.9.9.11
149.112.112.11

# IPv6
2620:fe::11
2620:fe::fe:11

# DoH
https://dns11.quad9.net/dns-query

# DoT
dns11.quad9.net
```
特点​： 

🔍 ​实时威胁库​：整合20+安全机构情报（如CISA、Malwarebytes） 

🌱 ​非盈利运营​：专注公共利益而非商业目的 

🚫 ​严格拦截​：默认阻断恶意软件/钓鱼/勒索软件域名 

📜 ​隐私承诺​：不记录用户IP地址且所有数据匿名化


## 选择建议指南 需求场景推荐服务关键优势

⚡ ​极致速度​Cloudflare DNS全球平均响应最快

👪 ​家庭防护​OpenDNS自动内容过滤解决方案

🛡️ ​高安全防护​Quad9多机构实时威胁情报联动

🌍 ​跨平台通用​Google Public DNS安卓/iOS/PC全平台兼容性最佳

🔏 ​隐私至上​Cloudflare/Quad9严格的零日志政策

## 国内大厂DNS 
## 1. 114 DNS
提供商：114 IP地址：
```
# 基础版，无劫持
# IPv4 DNS
114.114.114.114
114.114.115.115
```
```
# 安全版（病毒和钓鱼防御）
# IPv4 DNS
114.114.114.119
114.114.115.119
```
```
# 家庭版（拦截成人内容）
# IPv4 DNS
114.114.114.110
114.114.115.110
```
## 2. 腾讯 DNSPod DNS
提供商：腾讯 IP地址：
```
# IPv4 DNS
119.29.29.29
182.254.116.116

# IPv6 DNS
2402:4e00::
```
## 3. 百度 DNS
提供商：百度 IP地址：
```
# IPv4 DNS
180.76.76.76

# IPv6 DNS
2400:da00::6666
```
## 4. 阿里 DNS
提供商：阿里 IP地址：
```
# IPv4 DNS
223.5.5.5
223.6.6.6

# IPv6 DNS
2400:3200::1
2400:3200:baba::1
```
## 5. 360 DNS
提供商：360 IP地址：
```
# IPv4 DNS
# 电信
101.226.4.6
218.30.118.6

# 联通
123.125.81.6
140.207.198.6

# 移动 
101.226.4.6
218.30.118.6

# DoH
https://doh.360.cn

# DoT
dot.360.cn
```
##  6. TrafficRoute DNS
提供商：字节跳动
IP地址：
```
180.184.1.1
180.184.2.2
```
## 自用 DNS
```
# 阿里 DoQ (极速)
quic://dns.alidns.com:853
# 腾讯 DoH (保底)
https://doh.pub/dns-query
# 阿里 H3 (备用)
h3://dns.alidns.com/dns-query
```
## 规则收录
## Adgruad Home 黑名单
## 1.不是DD啊-高效的广告过滤规则
```
https://raw.githubusercontent.com/afwfv/DD-AD/main/rule/DD-AD.txt
```
## 2.大萌主-专注于界面广告拦截的实用规则
```
https://raw.githubusercontent.com/damengzhu/banad/main/jiekouAD.txt
```
## 3.下个ID见-基于安卓APP抓取的规则
```
https://raw.githubusercontent.com/2Gardon/SM-Ad-FuckU-hosts/master/SMAdHosts
```
## 4.晴雅-针对多种应用的广告黑名单规则
```
http://rssv.cn/adguard/api.php?type=black
https://raw.githubusercontent.com/790953214/qy-Ads-Rule/main/black.txt
```
## 5. CHN: anti-AD
```
https://adguardteam.github.io/HostlistsRegistry/assets/filter_21.txt
```
## 6.秋风
```
https://raw.githubusercontent.com/TG-Twilight/AWAvenue-Ads-Rule/main/AWAvenue-Ads-Rule.txt
```
## 7.海哥
```
https://raw.githubusercontent.com/2771936993/HG/main/hg1.txt
```
## 8.DD
```
https://raw.githubusercontent.com/afwfv/DD-AD/refs/heads/release/DD-AD.txt
```
## Adgruad Home 分流
## DNS 分流
📦 零部署：无需本地运行环境，直接 Fork 后在线配置。

🔄 自动更新：通过 GitHub Actions 定时拉取最新域名列表并生成规则。

🔧 高度自定义：可灵活指定国内外 DNS 服务器、自定义域名走向。

🛡 智能分流：自动区分国内外域名，实现最佳 DNS 解析路径。

📝 两种分流模式：支持黑名单模式与白名单模式灵活切换。

[AdGuard DNS Divert 项目地址](https://github.com/qq5460168/AdGuard-DNS-Divert)

## PaoPao DNS docker

泡泡DNS是一个能一键部署递归DNS的docker镜像，它使用了unbound作为递归服务器程序，使用Redis作为底层缓存，此外针对China大陆，还有智能根据CN分流加密查询的功能，也可以自定义分流列表，可以自动更新IP库，分流使用了mosdns程序，加密查询使用dnscrypt程序，针对IPv4/IPv6双栈用户也有优化处理。
泡泡DNS适合的使用场景：

场景一：仅作为一个纯粹准确的递归DNS服务器，作为你其他DNS服务程序的上游，替代114.114.114.114,8.8.8.8.8等公共DNS上游
场景二：作为一个局域网内具备CN智能分流、解决污染问题和IPv6双栈优化的DNS服务器，或者你的局域网已经从IP层面解决了“科学”的问题，需要一个能智能分流的DNS服务器。

Docker Compose 配置用于部署 ‌PaoPaoDNS‌，这是一个基于 SmartDNS 内核优化的 DNS 服务器，主要特点是针对中国大陆网络环境进行了优化（如分流、去广告、加速等）
```
version: '3.8'
services:
  paopaodns:
    image: sliamb/paopaodns:latest
    container_name: paopaodns
    volumes:
      - ./mydata:/data
    environment:
      CNAUTO: "yes"
      DNSPORT: "53"
      DNS_SERVERNAME: "ShellDns.ning.moe"
      TZ: "Asia/Shanghai"
      UPDATE: "weekly"
      IPV6: "raw"
      CNFALL: "yes"
      EXPIRED_FLUSH: "yes"
      CUSTOM_FORWARD_TTL: "0"
      ADDINFO: "no"
      USE_MARK_DATA: "yes"
    restart: always
    ports:
      - "5533:53/tcp"
      - "5533:53/udp"
    ulimits:
      nofile:
        soft: 65535
        hard: 65535
    mem_limit: 2.0G

```
```
services:
  paopaodns:
    image: sliamb/paopaodns:latest
    container_name: paopaodns
    volumes:
      - /opt/paopaodns/data:/data
    environment:
      CNAUTO: "yes"
      DNSPORT: "53"
      DNS_SERVERNAME: "ShellDns.ning.moe"
      TZ: "Asia/Shanghai"
      UPDATE: "weekly"
      IPV6: "raw"
      CNFALL: "yes"
      EXPIRED_FLUSH: "yes"
      CUSTOM_FORWARD_TTL: "0"
      ADDINFO: "yes"
      USE_MARK_DATA: "yes"
    restart: always
    ports:
      - "5533:53/tcp"
      - "5533:53/udp"
    mem_limit: 1.5g
```
```
version: '3'
services:
  paopaodns:
    image: sliamb/paopaodns:latest
    container_name: paopaodns
    volumes:
      - <宿主机地址>/mydata:/data    # 将数据挂载到容器内部的 /data 目录
    environment:
      CNAUTO: "yes"           # 是否CN规则分流（可选值: yes, no）
      DNSPORT: "53"           # DNS 服务端口号
      DNS_SERVERNAME: "ShellDns.ning.moe"  # DNS 服务器名称（不含空格的英文字符串）
      TZ: "Asia/Shanghai"     # 时区设置
      UPDATE: "weekly"        # 更新IP、域名库的频率（可选值: no, daily, weekly, monthly）
      IPV6: "raw"              # 是否启用 IPv6（可选值: no, yes, only6, yes_only6, raw）
      CNFALL: "yes"           # 是否包含中国大陆列表（可选值: no, yes）
      EXPIRED_FLUSH: "yes"    # 是否自动清理过期缓存（可选值: no, yes）
      CUSTOM_FORWARD_TTL: "0" # 自定义转发 TTL
      ADDINFO: "yes"          # 在DNS查询结果中增加ADDITIONAL SECTION的调试信息，如结果来源、查询延迟、失败原因等，使用dig命令就可以实时追踪域名结果来源
      USE_MARK_DATA: "yes"    # 全球百万域名库，在判断大陆分流的时候优先使用该数据.
    restart: always
    ports:
      - "5533:53/tcp"           # 对外开放 TCP 53 端口
      - "5533:53/udp"           # 对外开放 UDP 53 端口
    deploy:
      resources:
        limits:
          memory: 1.5G			#限制容器内存
``
PaopaodNS 服务已成功部署，要测试它是否正常工作，可从本地和网络两个层面验证。

首先，在运行该容器的宿主机上，使用 dig 或 nslookup 命令向本地 5533 端口发起查询，确认服务监听并响应：
```
dig @127.0.0.1 -p 5533 www.baidu.com
```