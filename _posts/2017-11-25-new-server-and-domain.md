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
<p>近日，本站迁移到了国内主机，并对域名进行了更新。</p>
<p><!--more--></p>
<h2>新的主机</h2>
<p>本站 WordPress 博客使用了阿里云香港服务器，由于是 GBP 网络，国内就不再使用 CDN，而是直接回源，正是因为这样，域名开头也无需再有 <code>www.</code> 。</p>
<p>此外，还将会在 2018 年添加中国北京节点，以便更好的为华北用户提供服务。</p>
<p>除了新的香港服务器外，还有新的阿里云国际的新加坡服务器，Observium 监控系统以及 Polr 短链接等都迁移到了这里。</p>
<p><img class="aligncenter size-large wp-image-3363" src="https://cdn.landcement.com/sites/2/2017/11/newmap-2018-2-1600x888.png" alt="" width="525" height="291" /></p>
<p>此外，国外的主站点也不再使用 CDN，而是直接回源，海外源站还有 Google US-Central、OVH France、QuadraNet US-West。整个 WordPress 站点生成的静态 HTML 都会被主动推送到这些服务器上。对于没有被缓存的内容，将会选取最优线路回源。比如美国到中国走 FATSTER 光缆。欧洲到北京走中国电信直连，延迟约 180ms；欧洲到香港走 Hurricane Electric，延迟约 180ms；美国西部到香港走 PCCW Global，延迟约 150ms；美国中部到香港走 Google FASTER，延迟约 160ms。</p>
<p>之所以主站点没有使用 CDN，一是 CDN 只兼容支持 SNI 的浏览器，二是清理缓存麻烦，而且 CNAME 接入的方式会带来更多的 DNS 上的延迟。且若 CDN 节点上没有缓存，可能会比回源还要慢。对于多媒体文件，本站使用了 CDN，因为多媒体文件不会阻塞页面加载，且主要瓶颈为带宽。多媒体 CDN 是 Cloudflare 专业版，所以也不需要浏览器支持 SNI。</p>
<h3>自建的 DNS 服务器</h3>
<p>现在我的大多数域名都是用了自建 DNS，支持 DNSSEC、GeoIP 和 IPv6。对于 DNS 服务器，亚太用户分配阿里云香港、阿里云北京和 Google Singapore 服务器，海外用户分配 Google US-West，Google US-Central 和 OVH France 服务器。</p>
<h3>全面支持 IPv6</h3>
<p>现在本站已经全面支持 IPv6，所使用的百度云加速 CDN 也支持了 IPv6（在浏览器上抓包后可以手动利用 API 直接添加 IPv6 记录的）。</p>
<h2>新的域名</h2>
<p>从 2014-02-03 起，本站就在使用 <code>ze3kr.com</code> 这个域名了。三年之后，终于迎来了新的域名，<code>guozeyu.com</code> 。</p>
<p>原本的域名 <code>ze3kr.com</code> 其实毫无意义，现在的新域名更加好记了。原先域名会继续长期保留，并跳转到新的域名。</p>
