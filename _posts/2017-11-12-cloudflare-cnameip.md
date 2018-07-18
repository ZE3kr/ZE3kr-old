---
layout: post
status: publish
published: true
title: Cloudflare 免费 CNAME/IP 接入，添加 IPv6 支持并为你的海外访客加速！
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://guozeyu.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://guozeyu.com
wordpress_id: 3260
wordpress_url: https://guozeyu.com/?p=3260
date: '2017-11-12 08:23:31 +0800'
date_gmt: '2017-11-12 00:23:31 +0800'
categories:
- 未归类
tags: []
---
<blockquote>原标题：推出 Cloudflare CNAME/IP 接入模式以及 Railgun 免费内测！</p></blockquote>
<p>立即前往面板，地址 <a href="https://cf.tlo.xyz" target="_blank">cf.tlo.xyz</a> 。通过使用该服务，你可以免费获得海外 CDN（通过分区解析可以单独为海外访客启用）。支持 HTTPS 和 IPv6（再也不用担心 App Store 审核被拒）。海外 CDN 服务不仅支持 CNAME 接入，还提供 Anycast IP 接入，意味着根域名也可以正常使用，不影响邮件接收（即不与 MX 记录冲突）。</p>
<p><!--more--></p>
<p>本站目前就使用了 CNAME/IP 接入，海外访问走 Cloudflare 加速！</p>
<h2><a href="https://wiki.tloxygen.com/CloudFlare_接入/教程" target="_blank">使用教程</a></h2>
<p>上方链接的教程以使用 CloudXNS 作为 DNS 的域名为例。</p>
<h2>介绍</h2>
<p>Cloudflare 是国外 CDN 厂商。默认免费版只能进行 NS 记录，这意味着还需要更改域名的 NS，实在是麻烦。然而 CNAME 接入方式只支持 <strong>200 美元/月</strong>以上的 <strong>Business 或 Enterprise plan</strong>，这对于很多人来说都太贵了。而作为 Cloudflare 的 Partner，却一直可以免费的创建 CNAME 接入的域名。我最近利用我的 Cloudflare Partner 账户做了个图形化 CNAME/IP 接入网站。地址 <a href="https://cf.tlo.xyz" target="_blank">cf.tlo.xyz</a> 。</p>
<h2><span style="font-size: 1.25rem;">特性</span></h2>
<ul>
<li>支持所有 Cloudflare 原本就有的功能</li>
<li>创建 CNAME/IP 方式接入的域名</li>
<li>查看最近一年的统计记录</li>
<li>支持已经 NS 接入域名一键更改为 CNAME 接入</li>
<li>使用 BIND 格式轻松添加 A/AAAA/CNAME/TXT/MX 等 DNS 记录</li>
<li>开启/关闭某个子域名的 CDN 功能</li>
<li>SSL 记录验证与配置 (自动签发证书，同时也支持文件验证）</li>
<li>提供 IP 地址接入，每个子域名提供 CNAME 记录接入</li>
<li>也可以使用 NS 方式接入，并可以设置 DNSSEC</li>
<li><a href="https://guozeyu.com/2017/05/cloudflare-argo/#Cloudflare_Railgun">支持</a><a href="https://guozeyu.com/2017/05/cloudflare-argo/#Cloudflare_Railgun"> Railgun</a>，与原站建立长链接，为动态页面提升约 7 倍速度！</li>
</ul>
<p>立即前往 <a href="https://cf.tlo.xyz" target="_blank">cf.tlo.xyz</a></p>
<h2>注意事项</h2>
<ul>
<li>CNAME/IP 接入的域名将无法在 Cloudflare.com 上管理 DNS。你可以在这个网站上管理 DNS，或者使用 API 管理 DNS。你仍需要在 Cloudflare.com 上管理域名其他部分的设置。</li>
<li>NS 接入更改为 CNAME/IP 接入只能保留前 100 项 DNS 记录。</li>
<li>添加 CNAME/IP 接入的域名可能需要验证你的域名所有权，你需要在子域名上添加一个 TXT 记录。</li>
</ul>
<h2><a href="https://wiki.tloxygen.com/CloudFlare_接入/教程" target="_blank">使用教程</a></h2>
<h2><a href="https://cf.tlo.xyz/analytics.php" target="_blank">统计界面截图</a></h2>
<h2>界面截图</h2>
<p><img class="aligncenter size-large wp-image-3468" src="https://cdn.landcement.com/sites/2/2017/11/Cloudflare_Partner_管理页面-1-586x1600.png" alt="" width="525" height="1433" /></p>
<p>另外，<a href="https://domain.tloxygen.com/web-hosting/index.php?promo=1711" target="_blank">TlOxygen </a><a href="https://domain.tloxygen.com/web-hosting/index.php?promo=1711" target="_blank">主机</a>正在六折促销，欢迎<a href="https://domain.tloxygen.com/web-hosting/index.php?promo=1711" target="_blank">抢购</a>，优惠将在购物车中自动生效。</p>
