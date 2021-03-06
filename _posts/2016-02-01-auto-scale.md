---
layout: post
status: publish
published: true
title: 建立自动负载均衡与服务器集群并存的博客系统
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://guozeyu.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://guozeyu.com
wordpress_id: 989
wordpress_url: https://guozeyu.com/?p=989
date: '2016-02-01 10:40:00 +0800'
date_gmt: '2016-02-01 02:40:00 +0800'
categories:
- 开发
tags:
- 网站
- 网络
- WordPress
---
<p>注：2016 年五月中旬，服务器已经不再是这样了。</p>
<p>2016-01-30 这一天，TLO XYZ 的博客系统（包括 guozeyu.com）整个迁移到了 “一个” 新的服务器，准确的说，服务器已经不止一个，而是许多个服务器负载均衡。</p>
<p>我们的服务器选用的是 Amazon 提供的的服务器，使用多个 EC2 （环境：PHP+Apache）服务器和一个 RDS（环境：MySQL）。EC2 上的程序代码可以直接使用 Git 部署，方便至极。我们使用的博客系统软件是 WordPress，这个软件分别放到了多个 EC2 上，配置都完全相同（每次 Git Push 时都会同步）。每一个 EC2 都使用同一个 RDS 作为数据库，这样可以保证发布文章等操作都是实时的。</p>
<p><!--more--></p>
<p>[img id="992" size="large"]图解服务器布局[/img]</p>
<p>多个 EC2 上使用一个 HAProxy 作为第四层负载均衡，公网 IP 只有一个。HAProxy 性能极高，每秒钟可以轻松应对数十万个请求。当你首次访问后，你的浏览器中会保存一个 Cookie 标记给你提供服务的 EC2，下次发送请求时仍使用同一台服务器。</p>
<p>在 HAProxy 之上，还有 CloudFlare 作为第七层负载均衡，支持 IPv6，DNS 负载均衡。同时 CloudFlare 的节点（Edge Network）遍布全球，它会缓存 CSS 和 JS 文件，加快浏览速度，优化 HTML。</p>
<p>除了这些服务器之外，我们还有一个 S3 存储服务器，它是专门用来存放多媒体文件用的，它和 EC2 在一个地区。当在网站上上传文件时，EC2 将会自动将文件 “转发” 到 S3。S3 的数据可靠性极高，不容易丢失文件。</p>
<p>在 S3 存储服务器之上，我们还有一个多 CDN 网络，同时使用 KeyCDN 和 UPYUN 两家的 CDN。UPYUN 专门给中国准备的，它在中国各省份和各运营商都有节点。为了提高可靠性和速度，所有存储在 S3 上的文件都还会被存到 UPYUN 的中央服务器中（这个过程走的是专线），而不是每一个节点上，这样当其中的一个节点缓存过期或没有缓存时，将会直接从中国的中央服务器获取，速度和可靠性都大大提升。</p>
<p>除此之外，我们的 HAProxy 到 CloudFlare、CloudFlare 到浏览器和 CDN 节点到浏览器均使用了 SSL 加密连接，不怕中间人攻击。</p>
<p>我们启动的 EC2 服务器的数量是根据负载而决定的，当负载变大时，最高可以启动 16 个 EC2 服务器，基本上能够应对超大的浏览量。</p>
