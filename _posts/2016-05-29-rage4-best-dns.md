---
layout: post
status: publish
published: true
title: 国内外 DNS 权威解析服务商对比
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://guozeyu.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://guozeyu.com
wordpress_id: 1668
wordpress_url: https://guozeyu.com/?p=1668
date: '2016-05-29 14:43:00 +0800'
date_gmt: '2016-05-29 06:43:00 +0800'
categories:
- 科技
tags:
- 网站
- 网络
- DNS
---
<p>DNS（<a href="https://zh.wikipedia.org/wiki/域名系统" target="_blank">域名系统</a>）是因特网的一项服务。它能够将域名指向一个 IP（服务器），这样你就可以通过域名来访问一个网站。能够通过域名访问的网站，都需要一个 DNS 服务器。这里指的是给站长的域名使用的权威 DNS 而并非缓存 DNS。</p>
<p>本文包括 CloudXNS、Route 53、Cloudflare、Google Cloud DNS 以及 Rage4 的全面对比<!--more--></p>
<h2>CloudXNS</h2>
<p>国内免费 DNS 中最好用的，作为 DNS 服务来说其功能也算齐全。CloudXNS 的服务器国内有不少，但没有使用 Anycast 技术，所以谈任何国外的服务器都是白搭。</p>
<p style="text-align: left; padding-left: 30px;">CloudXNS 通过 GeoDNS 对其 NS 服务器的域名进行分区解析，国内的解析到国内服务器，国外的解析到国外服务器。然而其根域名的 Glue Record 中的四个仍是国内的四个服务器，实际解析中会优先使用 Glue Record，所以并不会用上任何国外的服务器。</p>
<p style="text-align: left; padding-left: 30px;">为什么不将这些国外服务器也添加到 Glue Record 上？因为 Glue Record 并不支持 GeoDNS，所以解析器将会随机选择服务器，所以如果这样的话会导致国内的一部分请求也走到美国服务器，反而减速。</p>
<ul>
<li>国外速度：★☆☆☆☆，Ping 平均 279ms</li>
<li>国内速度：★★★★☆，Ping 平均 33.5ms</li>
<li>最短 TTL：<strong>60s</strong>，越短代表修改了记录后生效的越早</li>
<li>国内分区解析：★★★★☆，精确到绝大多数的运营商和省</li>
<li>国外分区解析：★★☆☆☆，精确到了大洲和一些国家，而没有城市</li>
<li>DNSSEC：<strong>不支持</strong>，此功能可以让客户端得知 DNS 是否是可信的</li>
<li>IPv6：<strong>不支持</strong>，客户端在纯 IPv6 网络环境下且不使用缓存 DNS 服务器时将无法使用</li>
<li>记录类型：<strong>基本</strong>齐全，只支持 A、AAAA、CNAME、NS、MX、TXT、SRV。</li>
<li>根域名 CNAME 优化：<b>不支持</b>，这个一般叫做：ANAME 或 CNAME Flattening</li>
<li>优先级：<strong>支持</strong>，可以配置解析到不同的服务器的优先级</li>
<li>自定义 NS（Vanity NS/Traffic Flow/Custom Nameservers）：<strong>不支持</strong>，由于它不支持修改根域名下的 SOA 和 NS，所以这是做不到的</li>
<li>价格：<strong>免费</strong></li>
<li>统计功能：<strong>支持</strong>，能精确到国家和省份、运营商</li>
</ul>
<h2>Route 53</h2>
<p>国外相当流行的 DNS 服务，必要的那些功能也算齐全。服务器都遍布全球，使用了 Anycast 保证最低的延迟。</p>
<ul>
<li>国外速度：★★★★☆，Ping 平均 90.4ms</li>
<li>国内速度：★☆☆☆☆，Ping 平均 277.9ms</li>
<li>最短 TTL：<strong>0s</strong></li>
<li>国内分区解析：★★☆☆☆，只能为中国这一个地区作单独设置，不支持省和运营商</li>
<li>国外分区解析：★★★★★，精确到了各个国家，众多的国家还精确到了市</li>
<li>DNSSEC：<strong>不支持</strong></li>
<li>IPv6：<strong>支持</strong></li>
<li>记录类型：<b>更加</b>齐全，支持 A、AAAA、CNAME、NS、MX、TXT、SRV、PTR、SPF、NAPTR。</li>
<li>根域名 CNAME 优化：<strong>不支持</strong></li>
<li>优先级：<strong>支持</strong></li>
<li>自定义 NS：<strong>支持</strong>，同时也可以修改根域名下的 SOA 和 NS</li>
<li>价格：每个域名 <strong>$0.5/月</strong>，<strong>$0.4/100万</strong>个请求，分区解析$0.7/100万个请求</li>
<li>统计功能：基本<strong>不支持</strong>，只有在每月最后结算的账单中看到</li>
</ul>
<h2>Cloudflare</h2>
<p>国外占有量相当大的免费 DNS，服务器都遍布全球，使用了 Anycast 保证最低的延迟。</p>
<ul>
<li>国外速度：★★★★★，Ping 平均 8.4ms</li>
<li>国内速度：★☆☆☆☆，Ping 平均 217.1ms</li>
<li>最短 TTL：<strong>120s</strong></li>
<li>国内分区解析：☆☆☆☆☆，完全不支持国内的分区解析，国内的请求一般会被认作美国西岸。</li>
<li>国外分区解析：★★★☆☆，如果购买了 Load Balancing 服务后，可以根据不同的区域配置分区解析。虽然没有按国家和城市区分，但是有时却比国家还精细（比如它支持为北美洲东西中部不同地区作分区解析）</li>
<li>DNSSEC：<strong>支持</strong>，但却不支持设置那些 DNSSEC 特有的记录，如不支持 IPSECKEY、SSHFP、TLSA、DNSKEY、DS 记录</li>
<li>IPv6：<strong>支持</strong></li>
<li>记录类型：<strong>更加</strong>齐全，支持 A、AAAA、CNAME、NS、MX、TXT、SRV、SPF、LOC。</li>
<li>根域名 CNAME 优化：<strong>支持</strong></li>
<li>优先级：支持，需要购买了 Load Balancing 服务</li>
<li>自定义 NS：<strong>不支持</strong>，购买 $200/月的 Business 版本后才能支持</li>
<li>价格：<strong>免费</strong></li>
<li>统计功能：部分<strong>支持</strong>，免费用户可以看到的统计有限</li>
</ul>
<h2>Google Cloud DNS</h2>
<p>价格低廉，提供 100% 的 SLA，使用了 Anycast 保证最低的延迟。</p>
<ul>
<li>国外速度：★★★★☆，Ping 平均 43.5ms</li>
<li>国内速度：★★★☆☆，Ping 平均 81.7ms</li>
<li>最短 TTL：<strong>0s</strong></li>
<li>分区解析：<strong>不支持</strong></li>
<li>DNSSEC：<strong>支持</strong>，同样支持 DNSSEC 特有的记录，包括 IPSECKEY、SSHFP、TLSA、DNSKEY、DS</li>
<li>IPv6：<strong>支持</strong></li>
<li>记录类型：<strong>几乎完全齐全</strong>，支持 A、AAAA、CNAME、NS、MX、TXT、SRV、SPF、LOC、NAPTR、PTR、CAA 以及上方列出的 DNSSEC 相关记录。</li>
<li>根域名 CNAME 优化：<strong>不支持</strong></li>
<li>优先级：支持，需要购买了 Load Balancing 服务</li>
<li>自定义 NS：<strong>不支持</strong>，购买 $200/月的 Business 版本后才能支持</li>
<li>价格：<strong>免费</strong></li>
<li>统计功能：基本<strong>不支持</strong>，只有在每月最后结算的账单中看到</li>
</ul>
<h2>Rage4</h2>
<p>同时支持 DNSSEC 和分区解析，使用了 Anycast 保证最低的延迟。</p>
<ul>
<li>国外速度：★★★★☆，Ping 平均 30.53ms</li>
<li>国内速度：★★☆☆☆，Ping 平均 152.6ms</li>
<li>最短 TTL：<b>根据套餐情况而定</b></li>
<li>国内分区解析：★★☆☆☆，只能为亚洲东部为中国配置解析</li>
<li>国外分区解析：★★★★☆，可以根据不同的区域配置分区解析</li>
<li>DNSSEC：<strong>支持</strong></li>
<li>IPv6：<strong>支持</strong></li>
<li>记录类型：<b>更加</b>齐全，支持 SOA、NS、A、AAAA、CNAME、TXT、MX、SRV、PTR、SPF、SSHFP、TLSA、LOC、NAPTR</li>
<li>根域名 CNAME 优化：<strong>支持</strong></li>
<li>优先级：<strong>支持</strong></li>
<li>自定义 NS：<strong>支持</strong>，同时也可以修改根域名下的 SOA 和 NS</li>
<li>价格：每个域名 <strong>$0.5/月</strong>，<strong>$0.4/100万</strong>个请求，分区解析$0.7/100万个请求</li>
<li>统计功能：<strong>支持</strong>，能精确到国家</li>
</ul>
<p>[modified github="ZE3kr/ZE3kr"][/modified]</p>
