---
layout: post
status: publish
published: true
title: 全面迁移到 Google Cloud Platform
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://ze3kr.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://ze3kr.com
wordpress_id: 2254
wordpress_url: https://ze3kr.com/?p=2254
date: '2016-12-10 19:24:36 +0000'
date_gmt: '2016-12-10 11:24:36 +0000'
categories:
- 开发
tags:
- 网站
- WordPress
- DNS
- CDN
- Google Cloud Platform
---
<p>这一周，终于将这个网站<strong>全面迁移到 Google Cloud Platform</strong> 上了。WordPress 原站服务器从 OVH 迁移到了 Google Compute Engine（简称 GCE），对象存储从 Amazon S3 换到了 Google Cloud Storage。同时，原先自建的 DNS 也换到了 Google Cloud DNS。</p>
<p><!--more--></p>
<p>所使用的 <strong>Google Compute Engine</strong> 是 <del>1.7GB 版本</del>（经过几周的使用，发现 0.6GB 加上合理的 SWAP 就足够了，已经降级）的，主要是因为有比较占用内存的 Piwik 统计软件，目前实际占用长期在三分之一以下。原先 WordPress 是安装在 OVH 的服务器上的，然后 GCE 亚洲东区缓存加速。现在重新迁移到了 GCE 亚洲东区上，由于减少了网络延迟，动态内容的速度快了很多。看来现在 GCE 的确是 VPS 的首选。其实，0.6GB 的版本应该也是够用的。10GB 硬盘价格：0.6GB @ $5.00/月；1.7GB @ $15.73/月。若要换用 SSD，需要再加 $1.3/月。详细的 <a href="https://ze3kr.com/2016/10/asia-google-compute-engine/">GCE</a> 介绍</p>
<p>对象存储换成了 <strong>Google Cloud Storage</strong>，与 GCE 同区，配合 <a href="https://github.com/GoogleCloudPlatform/gcsfuse" target="_blank">gcsfuse</a> 几乎可以当作本地硬盘使用。但是，要注意目录和文件数量不要太多，否则会严重影响性能。我使用的是 Regional Storage，价格 $0.02/GB/月。价格比 S3 稍稍低一些。经测试，Google Cloud Storage 的静态文件存储服务在中国似乎可以正常访问，这相比几乎无法访问的 S3 要好不少。前端我使用了 UPYUN 和 Cloudflare 直接进行分发。<a href="https://cloud.google.com/storage/pricing" target="_blank">价格表</a></p>
<p><strong>Google Cloud DNS</strong> 是具备 Anycast、IPv6 和 DNSSEC (需要申请) 的，而且中国连接也不怎么绕道。但是需要注意的是，Google Cloud DNS 所给的四个 NS 中第一个在中国是被屏蔽了的，所以配置时将其删除即可。价格十分低廉：每个域名 @ $0.2/月，$0.40/百万个请求。<a href="https://cloud.google.com/dns/pricing" target="_blank">价格表</a></p>
<p>至此，原本分布式的两个 VPS 改为了一个，管理起来终于方便多了，而且亚洲的访问速度反而是变快了。全部上云后灵活性以及稳定性有明显改善！</p>
<p>注：WordPress 主题已经换成 2017 版新版主题。</p>
<p>2017 年 4 月更新：本站已经正式用上了 <a href="https://ze3kr.com/2016/10/build-a-anycast-network-gce/">Google Cloud CDN</a>，并同时使用了美国东部和亚洲的服务器，保证全球快速访问！</p>
<p>[modified][/modified]</p>
