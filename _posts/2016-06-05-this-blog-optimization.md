---
layout: post
status: publish
published: true
title: 本网站底层的具体配置和优化
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://guozeyu.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://guozeyu.com
wordpress_id: 1691
wordpress_url: https://guozeyu.com/?p=1691
date: '2016-06-05 14:49:00 +0800'
date_gmt: '2016-06-05 06:49:00 +0800'
categories:
- 开发
tags:
- 网站
- 网络
- WordPress
- 安全
- VPS
---
<p>2017 年 6 月更新：时隔一年，最新的底层优化请见<a href="https://guozeyu.com/2017/06/beian/">本站备案后的各种优化及底层具体配置</a>。</p>
<p>维护这个网站已经有一段时间了，是时候谈一谈这个网站的具体细节了。</p>
<p>我有多个网站，好几个不同的域名，不过这篇文章就只从 guozeyu.com 这一个网站做具体的介绍。跳过域名注册和 DNS 解析，直接从网站 Web 服务用的主机开始。<!--more--></p>
<h2>Web 服务器</h2>
<p>本网站使用了一个台湾的 VPS 作为主要服务器，使用 Ubuntu 16.04 LTS，并开启了自动更新，使用 LEMP （Linux + Nginx + MySQL + PHP）配置。写这篇文章时，Nginx 版本是 1.10.1，支持 HTTP/2 协议；MySQL 版本是 5.7，<a href="https://www.mysql.com/why-mysql/benchmarks/" target="_blank">比上一代快了 3 倍</a>；PHP 版本是 7.0，<a href="https://www.zend.com/en/resources/php7_infographic" target="_blank">也比上一代快了 3 倍</a>。</p>
<p>台湾服务器由 Google 提供，海外连接稳定性很高，亚洲的连接几乎不绕道，国内连接直接从香港走，速度很快。</p>
<h2>攻击防御</h2>
<p>我在 Nginx 上同时使用了 <code>set_real_ip_from</code> 和 <code>limit_req</code>，这样可以一定程度上避免 CC 攻击。具体细节就不透露，不同的页面有着不同的限制。</p>
<p>Google Cloud 有能力防御 DDOS，所以 DDOS 方面就不用我操心了。</p>
<h2>页面静态化与动静分离</h2>
<p>我的网站使用了 WordPress，这是一个动态博客引擎，所以静态化对缓存和防攻击都有很大的帮助。我选择了使用 “WP Super Cache” 作为静态化工具，当页面被访问后，该页面的 HTML 会以静态文件的形式存储下来，下次访问时直接由 Nginx 提供缓存文件，不经过 PHP，速度大大提高了。除此之外，这个插件还有 Preload 功能，它会定期在后台缓存网站上的所有页面。</p>
<h2>图片、视频存储</h2>
<p>这个网站的图片和视频等静态文件存储在 Google Cloud 上，以为我的主机提供更多的空间。我的网站上的图片有很多，所以存在 Google Cloud 上，是最经济且安全的选择。</p>
<h2>CDN 网络</h2>
<p>本网站将文件使用 Google 对象存储，但为了防止恶意刷流量，数据必须要经过 CDN 后才能被访问。本站同时使用了 CloudFlare 和 UPYUN，分别是国外和国内速度最快的 CDN。CloudFlare 使用 IP 段验证，UPYUN 使用了 Host 验证。CloudFlare 是免费的，所以不怕被盗链。对于 UPYUN，我使用了域名防盗链技术。所以，如果想拿我网站上的图片进行外链，请将 URL 中的域名替换为 cdn.landcement.com，并删除链接后面 <code>?</code> 及其之后的东西。</p>
<h2>统计功能优化</h2>
<p>本网站使用自己的 Piwik 进行统计，所有报表都能存到自己的数据库里，而不是别人的。为了提高统计速度，本网站对发往统计脚本的请求做了特殊的处理：先立即返回 204，然后再后台异步的发送请求给后端服务器，达到速度最优化。</p>
<h2>网站备份及灾难恢复</h2>
<p>本网站自动将数据库备份到 Google Cloud，并自动的做 Snapshot。</p>
<p>备份有多么重要？假如你的服务商把你的服务停掉了，或者是服务商硬盘损坏，那么你的所有数据可就没了啊。而且备份还有助于那天不小心进 root 给 <code>rm -rf /*</code> 了之后还能恢复……而且这个还有助于方便你更换主机服务商，说换就换，直接从备份中恢复。</p>
