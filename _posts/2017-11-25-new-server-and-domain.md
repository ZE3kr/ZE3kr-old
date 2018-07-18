---
layout: post
status: publish
published: true
title: 新的服务器，新的域名
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://guozeyu.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://guozeyu.com
wordpress_id: 3321
wordpress_url: https://guozeyu.com/?p=3321
date: '2017-11-25 23:05:58 +0800'
date_gmt: '2017-11-25 15:05:58 +0800'
categories:
- 日志
tags: []
---
<p style="padding-left: 30px;">近日，本站迁移到了国内主机，并对域名进行了更新。</p>
<p><!--more--></p>
<h2>新的主机</h2>
<p>本站 WordPress 博客使用了阿里云香港服务器，由于是 BGP 网络，国内就不再使用 CDN，而是直接回源，正是因为这样，域名开头也无需再有 <code>www.</code> 。</p>
<p>此外，还将会在 2018 年添加中国北京节点，以便更好的为华北用户提供服务。</p>
<p>除了新的香港服务器外，还有新的新加坡、日本、美国西部、美国中部、美国东部和欧洲服务器，网站静态化的内容自动都会推送到上述服务器中。</p>
<p>对于海外访客，所有流量都走 Cloudflare，利用 Worker 功能自动调度到最近的服务器，不缓存任何页面，只缓存图片、视频、CSS 和 JS 静态文件。同时也启用了 <a href="https://guozeyu.com/2017/05/cloudflare-argo/">Railgun</a>。</p>
<h3>自建的 DNS 服务器</h3>
<p>现在我的大多数域名都是用了自建 DNS，支持 DNSSEC、GeoIP 和 IPv6。对于 DNS 服务器，亚太用户分配阿里云香港、阿里云北京服务器，海外用户分配 Google US-Central 和 OVH France 服务器。</p>
<p>此外，本站已经部署 CAA、TLSA 和 HPKP Pin。</p>
<h3>全面支持 IPv6</h3>
<p>现在本站已经全面支持 IPv6，所使用的百度云加速 CDN 也支持了 IPv6（在浏览器上抓包后可以手动利用 API 直接添加 IPv6 记录的）。</p>
<h2>新的域名</h2>
<p>从 2014-02-03 起，本站就在使用 <code>ze3kr.com</code> 这个域名了。三年之后，终于迎来了新的域名，<code>guozeyu.com</code> 。</p>
<p>原本的域名 <code>ze3kr.com</code> 其实毫无意义，现在的新域名更加好记了。原先域名会继续长期保留，并跳转到新的域名。</p>
