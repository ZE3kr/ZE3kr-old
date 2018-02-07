---
layout: post
status: publish
published: true
title: Cloudflare 免费 CNAME/IP 接入，为你的海外访客加速！
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
<p>立即前往面板，地址 <a href="https://cf.tlo.xyz">cf.tlo.xyz</a> 。通过使用该服务，你可以免费获得海外 CDN（通过分区解析可以单独为海外访客启用）。支持 HTTPS 和 IPv6（再也不用担心 App Store 审核被拒）。海外 CDN 服务不仅支持 CNAME 接入，还提供 Anycast IP 接入，意味着根域名也可以正常使用，不影响邮件接收（即不与 MX 记录冲突）。</p>
<h2><a href="https://wiki.tloxygen.com/CloudFlare_接入/教程" target="_blank">使用教程</a></h2>
<p>上方链接的教程以使用 CloudXNS 作为 DNS 的域名为例。</p>
<h2>介绍</h2>
<p>Cloudflare 是国外 CDN 厂商。默认免费版只能进行 NS 记录，这意味着还需要更改域名的 NS，实在是麻烦。然而 CNAME 接入方式只支持 <strong>200 美元/月</strong>以上的 <strong>Business 或 Enterprise plan</strong>，这对于很多人来说都太贵了。而作为 Cloudflare 的 Partner，却一直可以免费的创建 CNAME 接入的域名。我最近利用我的 Cloudflare Partner 账户做了个图形化 CNAME/IP 接入网站。地址 <a href="https://cf.tlo.xyz">cf.tlo.xyz</a> 。<!--more--></p>
<h2><span style="font-size: 1.25rem;">特性</span></h2>
<ul>
<li>创建 CNAME/IP 方式接入的域名</li>
<li>支持已经 NS 接入域名一键更改为 CNAME 接入</li>
<li>使用 BIND 格式轻松添加 A/AAAA/CNAME/TXT/MX 等 DNS 记录</li>
<li>开启/关闭某个子域名的 CDN 功能</li>
<li>SSL 记录验证与配置</li>
<li>提供 IP 地址接入，每个子域名提供 CNAME 记录接入</li>
<li>也可以使用 NS 方式接入，并可以设置 DNSSEC</li>
<li><a href="https://guozeyu.com/2017/05/cloudflare-argo/#Cloudflare_Railgun">支持 Railgun</a>，与原站建立长链接，为动态页面提升约 7 倍速度！（<a href="mailto:ze3kr@icloud.com?subject=%E7%94%B3%E8%AF%B7%20Railgun%20%E5%86%85%E6%B5%8B%E8%B5%84%E6%A0%BC&amp;body=%E6%88%91%E7%9A%84%E5%9F%9F%E5%90%8D%E6%98%AF%EF%BC%9A%E8%AF%B7%E5%A1%AB%E5%86%99%0A%0A%23%23%23%20%E4%B8%8D%E8%A6%81%E6%9B%B4%E6%94%B9%E4%BB%A5%E4%B8%8B%E5%86%85%E5%AE%B9%20%23%23%23%0A%0A%E6%88%91%E7%9F%A5%E9%81%93%E5%8F%91%E9%80%81%E6%AD%A4%E9%82%AE%E4%BB%B6%E5%90%8E%EF%BC%8C%E7%BD%91%E7%AB%99%E9%9A%8F%E6%97%B6%E5%B0%B1%E5%8F%AF%E8%83%BD%E8%A2%AB%E5%90%AF%E7%94%A8%20Railgun%EF%BC%8C%E4%B8%8D%E6%AD%A3%E7%A1%AE%E7%9A%84%E9%85%8D%E7%BD%AE%E5%B0%86%E4%BC%9A%E5%BD%B1%E5%93%8D%E7%BD%91%E7%AB%99%E5%86%85%E5%AE%B9%E3%80%82%0A%0A%E6%88%91%E7%9A%84%E5%9F%9F%E5%90%8D%E5%B7%B2%E7%BB%8F%E5%9C%A8%20TlOxygen%20%E6%8E%A5%E5%85%A5%E3%80%82%E6%88%91%E4%BA%86%E8%A7%A3%E5%88%B0%E5%86%85%E6%B5%8B%E5%8F%AF%E8%83%BD%E6%9C%89%E4%B8%8D%E7%A8%B3%E5%AE%9A%E6%80%A7%EF%BC%8C%E4%B8%94%E6%9C%AA%E5%BF%85%E6%9C%89%E6%8A%80%E6%9C%AF%E6%94%AF%E6%8C%81%E3%80%82%E6%88%91%E6%B2%A1%E6%9C%89%E5%BC%80%E5%90%AF%E9%92%88%E5%AF%B9%20Cloudflare%20%E7%9A%84%E9%98%B2%E7%81%AB%E5%A2%99%E3%80%82%E6%88%91%E4%B9%9F%E7%9F%A5%E9%81%93%E5%86%85%E6%B5%8B%E7%9A%84%E5%85%8D%E8%B4%B9%E4%BD%BF%E7%94%A8%E8%B5%84%E6%A0%BC%E9%9A%8F%E6%97%B6%E5%8F%AF%E8%83%BD%E7%BB%93%E6%9D%9F%EF%BC%8C%E9%9C%80%E8%A6%81%E4%BA%A4%E8%B4%B9%E6%89%8D%E8%83%BD%E7%BB%A7%E7%BB%AD%E4%BD%BF%E7%94%A8%20Railgun%20%E5%8A%9F%E8%83%BD%E3%80%82%0A%0A%E6%AD%A4%E5%A4%96%EF%BC%8C%E6%88%91%E4%B9%9F%E5%B7%B2%E7%BB%8F%E9%98%85%E8%AF%BB%E7%9B%B8%E5%85%B3%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E%20https%3A%2F%2Fwiki.tloxygen.com%2FCloudFlare_%25E6%258E%25A5%25E5%2585%25A5%2FRailgun">申请 Railgun 免费内测资格</a>。正式上线后将支持 NS 接入，上线后对于 Cloudflare 的免费版，前 3 个域名一共 <b>$5/mo</b>，之后每个域名额外 <b>$1/mo</b>。）</li>
</ul>
<p>立即前往 <a href="https://cf.tlo.xyz" target="_blank">cf.tlo.xyz</a></p>
<h2>注意事项</h2>
<ul>
<li>CNAME/IP 接入的域名将无法在 Cloudflare.com 上管理 DNS。你可以在这个网站上管理 DNS，或者使用 API 管理 DNS。你仍需要在 Cloudflare.com 上管理域名其他部分的设置。</li>
<li>NS 接入更改为 CNAME/IP 接入只能保留前 100 项 DNS 记录。</li>
<li>添加 CNAME/IP 接入的域名可能需要验证你的域名所有权，你需要在子域名上添加一个 TXT 记录。</li>
</ul>
<h2><a href="https://wiki.tloxygen.com/CloudFlare_接入/教程" target="_blank">使用教程</a></h2>
<h2>界面截图</h2>
<p><img class="aligncenter size-large wp-image-3261" src="https://cdn.landcement.com/sites/2/2017/11/Screenshot-2017-11-12-07.39.14-1089x1600.png" alt="" width="525" height="771" /></p>
<p>另外，<a href="https://domain.tloxygen.com/web-hosting/index.php?promo=1711" target="_blank">TlOxygen 主机</a>正在六折促销，欢迎<a href="https://domain.tloxygen.com/web-hosting/index.php?promo=1711" target="_blank">抢购</a>，优惠将在购物车中自动生效。</p>
