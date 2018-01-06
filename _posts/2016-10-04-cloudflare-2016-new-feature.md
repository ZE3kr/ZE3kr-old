---
layout: post
status: publish
published: true
title: Cloudflare 的全新功能体验——Load Balancing、Rate Limiting
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://guozeyu.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://guozeyu.com
wordpress_id: 2031
wordpress_url: https://guozeyu.com/?p=2031
date: '2016-10-04 09:26:00 +0800'
date_gmt: '2016-10-04 01:26:00 +0800'
categories:
- 开发
tags:
- CDN
---
<p>Cloudflare 在 2016 年末终于增加了两个重磅的功能，分别是：</p>
<ul>
<li>Load Balancing（原名：Traffic Manager）</li>
<li>Rate Limiting（原名：Traffic Control）</li>
</ul>
<p>Load Balancing 支持更加高级的负载均衡功能，并终于支持了大家很需要的跨区域负载均衡功能；Rate Limiting 支持了高级的访问次数限制功能。越来越多的原本需要在服务器上配置的功能，现在在 Cloudflare 上也能进行配置了。（目前这两个功能还属于 Beta 阶段，需要认证用户才能使用）</p>
<p><!--more--></p>
<h2>Load Balancing</h2>
<p>此功能可以把 Cloudflare 当作负载均衡器使用，而不需要再在主机提供商上配置负载均衡，<a href="https://www.cloudflare.com/load-balancing/">官网介绍</a>。目前此功能仅向 Enterprise 账户和部分有资格的用户开放。该功能有两种实现方式，分别如下：</p>
<h3>通过 Cloudflare 的 CDN 实现（Anycast）</h3>
<p>负载均衡的功能是在 Cloudflare 的边缘服务器上实现，是通过第 7 层反代的方式实现，其实很类似于原本的 CDN 功能，不过回源可以高度定制。源站可以配置多个地区（需手动设置服务器的位置），每个地区也可以配置多个服务器，可以将这些众多服务器设置为一个 Group。将域名指向这个 Group，然后 Cloudflare 的边缘服务器的回源可以根据服务器的地区来<strong>自动</strong>选择最近的源站服务器。这样可以非常有效的降低首字节的延迟，对动态资源速度的提升会有很大的帮助。</p>
<p>[img id="2030" size="medium"]可配置服务器的地区（两种方式一样）[/img]</p>
<p>此外，Cloudflare 还自带了 Health Check 功能，可以当服务器宕机后能够自动更改回源。虽然通过 DNS 的方式也可以实现宕机后切换，但是 DNS 方式毕竟会收到缓存时长影响，若使用 CDN 切换，则可以实现秒级切换。</p>
<p>我的一个 WordPress 站点 tlo.xyz 就使用了这个功能，默认是美国东部和亚洲东部跨区域负载均衡，两者有一者宕机自动切换。如果全部宕机，则 fallback 到 Google Cloud Storage 上的静态页面。你可以观察 https://tlo.xyz 上的 TLO-Hostname 的 Header 来判断是哪一个服务器做的响应。</p>
<p><img class="aligncenter size-medium wp-image-2849" src="https://cdn.landcement.com/sites/2/2016/10/Screenshot-2017-03-18-下午7.05.53-450x247.png" alt="" width="450" height="247" /></p>
<h3>通过 DNS 实现（GeoDNS + 权重）</h3>
<p>使用此功能不需要开启它的 CDN 功能，故访客是直接连接源站的。同上一种方式也是配置一个 Group，只是不开启 CDN 功能，然后 Cloudflare 会只作为 DNS 服务器的功能。它会自动进行 GeoDNS，给访客返回最近的服务器的 IP 地址，同样也支持 Health Check 功能，当服务器宕机后会自动切换解析。</p>
<p>不同于其他的 DNS 解析商，Cloudflare 真正做到了智能，只需要配置一个 Group 即可，剩下的 Cloudflare 会自动搞定，而不是去手动地选择哪一个地区解析到哪一个服务器。</p>
<p>此功能已经被我测试，目前的测试期间，GeoDNS 的定位功能是根据请求最终抵达的 CloudFlare 的服务器来决定的，也就是说是依靠 Anycast 系统来决定的。然而中国用户绝大多数会被运营商定向到 CloudFlare 的美国西部服务器，于是就会被 GeoDNS 系统解析道美国西部位置所对应的结果。所以此功能还是十分有限，不适合国内使用。</p>
<h2>Rate Limiting</h2>
<p>Cloudflare 终于可以限制 IP 的请求速率，此功能能够相当有效的过滤 CC 攻击，而且对于普通访客几乎没有影响（以前只能通过 I'm under attack 功能实现，然而这个功能会让所有用户等 5 秒才能载入）。它可以根据不同的路径配置不同的请求速率，能够实现防止暴力破解密码、防止 API 接口滥用等功能。</p>
<p>&nbsp;</p>
<p>[modified github="ZE3kr/ZE3kr"]更新功能的名称，添加图形界面的截图[/modified]</p>
