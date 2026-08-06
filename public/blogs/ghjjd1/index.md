## 1 序言
在个人博客、静态站点、API 服务基于 CloudFlare 全球边缘网络部署后，多数开发者都会遇到共性问题：境外节点默认公共 IP 在国内访问场景下，存在加载慢、资源超时、访问抖动等问题。原生 CloudFlare 公共节点未针对国内跨境网络链路做适配，导致博客页面、静态图床、接口请求体验极差。

本文参考二叉树树优选 IP 教程方案，从业务痛点出发，完整拆解 CloudFlare 优选 IP 的概念、价值、主流方案、实操步骤、测试对比及工程化优化方案，形成可直接落地的优选 IP 部署闭环，适配博客站长、边缘云开发、前端运维等开发者场景。

## 2 什么是 CloudFlare 优选 IP（核心概念）
2.1 优选 IP 基础定义
CloudFlare 优选 IP 是区别于官方公开默认节点 IP 的定制化边缘节点 IP 集合，是通过链路测速、丢包检测、延迟筛选、稳定性校验后，筛选出的国内跨境访问最优 CloudFlare 节点 IP。

该类 IP 仍归属 CloudFlare 官方节点网段，保留 CDN 加速、边缘缓存、防护、SSL 证书等全部原生能力，仅针对国内访问链路做了性能择优，不改变 CloudFlare 核心服务架构。

## 2.2 优选 IP 工作原理简述
CloudFlare 全球拥有数百个边缘节点，普通访问场景下，DNS 会根据全局路由策略随机分配公共节点 IP，该策略优先保障全球通用访问，牺牲了国内跨境访问的专项性能。

优选 IP 的核心原理：

遍历 CloudFlare 合法节点 IP 网段，批量探测国内各运营商（移动、联通、电信）链路延迟、丢包、稳定性；

过滤掉拥堵、高延迟、易封禁、解析异常的劣质节点；

留存长期稳定、低延迟、高可用的优质节点 IP，通过本地/服务商 DNS 绑定，替代默认公共 IP 完成访问解析；

保留 CloudFlare 边缘缓存、防护、加速核心能力，仅优化底层链路入口。

普通小黄云解析分为规则层、解析层两层：

开启代理后，CF 自动配置 DNS 指向 CF、生成路由规则

若手动修改 DNS 指向优选节点，一旦关闭小黄云，配套路由规则同步删除，解析失效，访问失败

SaaS 路由 和 Worker 路由打破该限制：

路由规则由我们自行创建，规则层独立，不再依赖小黄云解析自动生成

DNS 解析可自由配置 CNAME 指向优选节点，解析层自主控制

两层相互解耦，因此依托 SaaS/Worker 路由能够实现节点优选

## 2.3 社区优选域名
常用的社区优选域名：

cf.090227.xyz

秋名山优选域名：cf.877774.xyz
```
bestcf.030101.xyz #Mingyu维护
cdn.2020111.xyz
cdns.doon.eu.org
cf.0sm.com
cf.877771.xyz
cf.877774.xyz #秋名山维护
cf.900501.xyz
cfip.1323123.xyz
cfip.cfcdn.vip
cfip.xxxxxxxx.tk #OTC维护
cloudflare.182682.xyz #WeTest.Vip维护
cloudflare-dl.byoip.top
cloudflare-ip.mofashi.ltd
fn.130519.xyz
freeyx.cloudflare88.eu.org
nrt.xxxxxxxx.nyc.mn
nrtcfdns.zone.id
saas.sin.fan
tencentapp.cn #ktff维护
xn--b6gac.eu.org
777.ai7777777.**xyz**
```
这些优选域名通常是通过扫描Cloudflare官方IP段，找出国内延迟最低的IP整理而成。

## 3 为什么要做 IP 优选
## 3.1 原生 CloudFlare 公共 IP 存在的问题
访问延迟高、网络抖动大：默认公共节点跨境链路绕路严重，国内访问延迟居高不下，且不同时段网络波动剧烈，页面打开忽快忽慢。

国内解析漂移、节点适配差：DNS 智能解析随机分配海外节点，部分偏远节点与国内链路兼容性极差，无固定最优路由。

静态资源加载异常：博客图片、CSS/JS 静态资源、图床文件频繁出现加载超时、空白、加载不全问题，CDN 加速核心功能失效。

接口服务可用性低：依托 CloudFlare 部署的 API 服务，易因节点不稳定出现请求超时、响应失败，影响业务可用性。

## 3.2 优选 IP 带来的核心收益
大幅降低跨境访问延迟：优选节点针对性优化国内链路，延迟直接降低 60%+，页面首屏加载速度显著提升。

修复 CDN 失效问题：稳定的优质节点可保障边缘缓存正常生效，静态资源、图片加载成功率接近 100%。

解决边缘业务卡顿问题：博客、图床、后端 API、小程序接口等全部边缘业务的访问卡顿、超时问题彻底优化。

规避节点拥堵与封禁风险：避开高并发公共节点，减少节点过载拥堵、IP 封禁、限流拦截的概率，提升服务稳定性。

## 3.3 不做优选的业务风险
个人博客、展示站点用户流失严重，访问体验极差，无法满足正常展示需求；

图床服务频繁失效，图片加载失败，导致网站内容残缺；

线上 API 接口不稳定，出现随机报错、超时，影响业务正常运行；

长期使用劣质公共节点，可能触发 CloudFlare 风控策略，导致域名临时封禁、节点拉黑。

## 4 最终方案选型理由
综合成本、落地难度、通用性、稳定性四大核心维度，本文最终选择 Workers 优选 或 SaaS 优选

组合方案：

零成本落地，无需企业资质、无需付费、无备案要求，适配绝大多数个人开发者；

覆盖静态站点、图床、API 接口全场景，弥补 R2 优选场景单一的缺陷；

配置轻量化，工程化落地步骤简单，可快速复现部署；

相比 Byoip 方案，大幅降低部署门槛，兼顾性能与实用性。

## 5 怎么优选 IP
## 5.1 CloudFlare 域名优选
首先我们需要在 CloudFlare 解析一个域名，你得有一个域名在 CloudFlare 解析，比如你的域名.com，这里我在 CloudFlare 解析的是 9600000.xyz

其次我们需要创建一个指向优选域名，也就是yx.你的域名.com cname 指向 cf.090227.xyz，这里我设置的是yx.99600000.xyz，记得千万不要开启小黄云代理

设置为 cf.090227.xyz 和设置 yx.cf.090227.xyz 效果是一样的

最后我们打开 itdog.cn，找到 DNS 解析，输入刚刚我们解析的 yx.99600000.xyz，可以看到结果已经 cname 到 yx.cf.090227.xyz，而且基本是绿色的。

## 5.2 Works 优选
核心原理：依托 CloudFlare Works 边缘函数路由能力，将域名解析流量引流至优选优质节点，通过边缘转发规避公共节点链路缺陷，实现无感知 IP 优选。

实操步骤

登录 CloudFlare 控制台，进入 Workers & Pages 模块，打开你的 workers 项目

找到域，添加路由，一定是添加路由

然后输入blog.你的域名.com/*，记住 /* 不能忽略，代表通配符

这里我输入我的域名blog.jxx6.com/*

最后我们只需要把 blog.你的域名.com cname 到 yx.你的域名.com ，记得关闭小黄云

优选基础测试

这样我们就可以对于优选前的域名和优选后的域名在 itdog.cn 上看 DNS 解析中的 cname 记录，以及观看 A 记录的 IP多少，IP 越多说明选择越多，打开也就更快。

## 6 Pages 优选邪修
众所周知，pages 优选要改 DNS，那些很麻烦，又不能直接使用 workers，SaaS 是需要真实 IP。

那么，有没有一种方法不需要把 pages 转换成 workers，又能使用优选呢？

有的，我们可以创建一个 workers 透明代理 pages 的源站域名流量，那么直接用 workers 的路由不是就可以优选了？

所以我们需要先创建一个 workers 的 hello word 项目，名称就叫做 pages-proxy，最后点部署

最后我们点击编辑代码，输入以下代码，修改成你的 pages 域名，部署
```
export default {
  async fetch(request, env, ctx) {
    const url = new URL(request.url);
    // 将目标地址强行指定为你的 Pages 原始域名
    const targetDomain = "Pages 原始域名";
    url.hostname = targetDomain;
    const newHeaders = new Headers(request.headers);
    newHeaders.set("Host", targetDomain);
    const method = request.method;
    const hasBody = !["GET", "HEAD"].includes(method);
    const fetchOptions = {
      method: method,
      headers: newHeaders,
      redirect: request.redirect,
    };
    if (hasBody) {
      fetchOptions.body = request.body;
      fetchOptions.duplex = 'half';
    }
    const newRequest = new Request(url, fetchOptions);
    try {
      return await fetch(newRequest);
    } catch (e) {
      return new Response("Proxy Error: " + e.message, { status: 500 });
    }
  },
};
```
那么现在就简单了，又回到刚刚的 workers 优选配置了。

## 7 优选前和优选后测试
## 7.1 核心测试指标
统一测试环境：国内三网（移动、联通、电信）、本地网络、无代理、无缓存，测试指标包含平均延迟、丢包率、页面首屏时间、资源加载成功率。

## 7.2 测试数据对比
打开 itdog.cn ，点击网站测试，输入源站域名，可以看到基本黄的，可能还有红的；但是打开优选线路，基本都是看的绿色线路，IP 也变多了，但是也有可能有的地方没解析红的。

## 7.3 测试结论
部署优选 IP 方案后，国内跨境访问 延迟降低 70%+，丢包问题基本解决，静态资源加载、页面访问、接口请求的稳定性大幅提升，完全解决原生公共节点的核心痛点，满足个人站点、轻量边缘业务的生产使用需求。

## 8 总结
优选 IP，并不一定会快，理性看到这个事情
但是优选会优化线路，可以选择的更多
我觉得走腾讯 EdgeOne 海外线路，没备案域名，也很快，毕竟腾讯对国内优化很好
有的人使用 vercel 部署也很快