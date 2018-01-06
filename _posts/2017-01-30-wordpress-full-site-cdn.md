---
layout: post
status: publish
published: true
title: 国内外几家全站 CDN 对比
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://guozeyu.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://guozeyu.com
wordpress_id: 2562
wordpress_url: https://guozeyu.com/?p=2562
date: '2017-01-30 08:00:23 +0800'
date_gmt: '2017-01-30 00:00:23 +0800'
categories:
- 开发
tags:
- 网站
- WordPress
- DNS
- CDN
---
<p style="text-align: left;">配置全站 CDN 可以缓存 HTML 页面和加快页面首次加载所耗时间。本文重点讲述 WordPress 的全站缓存，国内外 CDN 混用的解决方案，以及让页面也在 CDN 上缓存的正确做法。本文主要介绍 CloudFront，同时也对 Cloudflare、又拍云、百度云加速、KeyCDN、Google Cloud CDN 这几家 CDN 进行对比。</p>
<p><!--more--></p>
<h2>全站 CDN 能在哪些地方加速？</h2>
<h3>我已经像你之前一样只缓存了图片、视频、CSS 和 JS 之类的静态资源，全站 CDN 有什么优点？</h3>
<p>就算不缓存任何内容，全站 CDN 也是有他的优点的：</p>
<ol>
<li><strong>SSL 卸载</strong>：源站到 CDN 之前走 HTTP 传输，CDN 到用户走 HTTPS 传输。这样，能减轻源站原本因为 SSL 所造成的硬件负担。然而，由于源站到 CDN 的传输是明文的，仅建议全程内网的情况，或线路可控的情况下使用，否则有很大的安全隐患。然而几乎所有的 CDN 也可以配置源站到 CDN 之间走 HTTPS 加密传输。</li>
<li><strong>安全防护</strong>：所有的 CDN 都自带基于第一、二、三层网络的防护（防止 SYN 攻击），大多数还带了第七层的防护（防止 CC 攻击）。</li>
<li><strong>减少延迟</strong>：建立 HTTP 连接之前需要先进行 TCP 和 HTTP 的 SSL 握手，这样会增加首次加载所需时间。而很多 CDN 都会与服务器进行预连接，而且 CDN 的服务器离用户较近，所以能减少首次加载所需时间，即使没有缓存页面。</li>
<li><strong>缓存动态页面</strong>：所谓动态页面，其实大多数对于没有登录的用户来说内容其实是固定的（如 WordPress 的文章页），所以可以针对未登录的用户缓存。这需要 CDN 能自动根据 Cookie 判断用户有没有登录，这下就只剩 Cloudflare 企业版和 CloudFront 可以做到了。</li>
</ol>
<h2>使用 CloudFront 作为全站 CDN</h2>
<p>CloudFront 有 Amazon 自建的网络，单价较高但是 0 元起步，适合中小客户。本文将重点介绍 CloudFront 和 WordPress 配合实现动静分离，缓存 HTML 页面。之后将对比其他的一些 CDN。</p>
<ul>
<li>国外速度：★★★★☆，节点数量众多，但相比 Cloudflare 要差一些，并且不支持 Anycast。</li>
<li>国内速度：★★★☆☆，国内开始走亚洲节点，速度要比 Cloudflare 快</li>
<li>可定制性：★★★★★，可以根据不同的路径回源使用不同的服务器，甚至回源到不同的服务器，且没有规则数量上限。此外，配合 <a href="http://docs.aws.amazon.com/zh_cn/AmazonCloudFront/latest/DeveloperGuide/what-is-lambda-at-edge.html" target="_blank">Lambda@Edge</a> 甚至可以将原本需要源站响应的动态内容交给缓存服务器做，只需使用 Node.js。</li>
<li>廉价指数：★★★☆☆，从免费起，Pay-as-you-go，单价确实高，但是可以通过<em>价格级别</em>牺牲速度来换取更低廉的价格</li>
<li>方便接入：★★☆☆☆，需要配置各种缓存参数才能使用，NS 接入并不直接，CNAME 接入相比 NS 更有难度。SSL 证书首次也需要手动申请，但自动续签。</li>
<li>缓存命中：★★★★☆，支持 <em>Regional Edge Caches</em>，先缓存到全球的 9 个节点，再向下分发，大大提升缓存命中率</li>
<li>动静分离：★★★★★，自动分离，一个服务下可以根据不同目录设置不同 Behaviors，甚至配置多个源站服务器，支持匹配 Cookie、GET、Header 规则缓存，支持禁用 POST 等提交方式</li>
<li>缓存刷新：★★★★☆，支持单个 URL 刷新以及规则匹配刷新</li>
<li>接入方式：NS/CNAME</li>
<li>证书兼容性：默认仅限支持 SNI 的浏览器，可额外购买服务（$600/月）以兼容所有浏览器。</li>
</ul>
<p>CloudFront 作为全站 CDN 的特性：</p>
<ul>
<li>支持根域名</li>
<li>缓存静态文件</li>
<li>缓存页面</li>
<li>页面更新自动清理缓存</li>
<li>免费 SSL 证书</li>
<li>可配置国内外 CDN 混用</li>
</ul>
<h3>使用方法</h3>
<p>先去 <a href="https://console.aws.amazon.com/cloudfront/home" target="_blank">CloudFront 控制面板</a>，点击 “Create Distribution”，选择 “Web”，然后进行类似如下的配置。<strong>源站配置</strong>注意 Origin Domain Name 必须是完整域名，而且如果用了 HTTPS，那么那个域名下必须有配置有效证书。</p>
<p><a href="https://cdn.landcement.com/sites/2/2017/01/Screenshot-2017-01-28-21.51.24.png"><img class="aligncenter size-medium wp-image-2572" src="https://cdn.landcement.com/sites/2/2017/01/Screenshot-2017-01-28-21.51.24-450x339.png" alt="" width="450" height="339" /></a></p>
<p><strong>缓存配置</strong>，我把 Host 加入了 Header 白名单，Cookie 要添加 <code>wordpress*</code> 和 <code>wp*</code> 到白名单。</p>
<p><a href="https://cdn.landcement.com/sites/2/2017/01/Screenshot-2017-01-28-22.19.54.png"><img class="aligncenter wp-image-2576" src="https://cdn.landcement.com/sites/2/2017/01/Screenshot-2017-01-28-22.19.54-1272x1600.png" alt="" width="600" height="755" /></a></p>
<p>然后<strong>前端配置</strong>，证书点 “Request or Import a Certificate with ACM” 就能申请 Amazon 颁发的证书了。CNAMEs 下填写你的网站的域名。</p>
<p><a href="https://cdn.landcement.com/sites/2/2017/01/Screenshot-2017-01-28-21.52.59.png"><img class="aligncenter wp-image-2575" src="https://cdn.landcement.com/sites/2/2017/01/Screenshot-2017-01-28-21.52.59-921x1600.png" alt="" width="600" height="1042" /></a></p>
<p>注意，创建后可能要等不到一小时才能被访问到。</p>
<p>为了根域名和 CloudFront 配合使用，我还得换 Route 53 这个 DNS 解析。由于这是精度非常高的 GeoDNS，是需要将解析服务器向各大 DNS 缓存服务器去提交，让这些缓存服务器去针对你的 DNS 缓存服务器加入到启用 EDNS Client Subnet 的白名单中。还好 Route 53 是最流行的 GeoDNS 之一，所以如果你用它给的 NS 记录，而不去自定义，就不用操心这个了。在配置根域名时，直接选择 A 记录，然后开启 Alias，填写 CloudFront 域名就行。如果想要支持 IPv6，那就再建一个 AAAA 记录即可。这样的话如果你从外部解析，你会直接解析到 A 记录和 AAAA 记录，而不是 CNAME 了！</p>
<p><img class="aligncenter wp-image-2577 size-medium" src="https://cdn.landcement.com/sites/2/2017/01/FullSizeRender-10-450x327.jpg" alt="" width="450" height="327" /></p>
<p>此时，CloudFront 就配置完了。现在 CloudFront 会自动缓存页面约一周的时间，所以需要配置文章更新时清理缓存。我写了一个插件，可以在有文章更新/主题修改/内核更新时清理所有缓存，新评论时清理文章页面，控制刷新频率为 10 分钟（这是由于 CloudFront 刷新缓存的速度是出奇的慢，而且刷新缓存只有前一千次免费）。欢迎<a href="https://wordpress.org/plugins/full-site-cache-cf/" target="_blank">使用我制作的插件</a>。</p>
<p>不过，CloudFront 在国内的访问速度还不如我之前用的 GCE，这可怎么办？没关系，Route 53 可以 GeoDNS，我把中国和台湾还是解析到了原本的 GCE 上，这样速度其实只提不减。注意，若要这样做，原本的服务器也要有有效证书（同理，你要是域名已经备案，则可以设置为国内的 CDN 的 IP，达到国内外 CDN 混用的效果）。CloudFront 会影响 Let's Encrypt 的签发，所以需要通过设置 Behaviors 和多个源站服务器，来继续实现 80 端口的文件认证。实际测试 Route 53 为中国解析的 IPv4 识别率为 100%，IPv6 的识别率欠佳。</p>
<p><img class="aligncenter wp-image-2580 size-large" src="https://cdn.landcement.com/sites/2/2017/01/FullSizeRender-11-1600x497.jpg" width="525" height="163" /></p>
<h3>实际使用情况</h3>
<h4>GeoDNS 效果测试</h4>
<p>国内解析情况：</p>
<pre class="lang:default decode:true">$ dig @8.8.8.8 +short guozeyu.com a
104.199.138.99
$ dig @8.8.8.8 +short guozeyu.com aaaa
2600:9000:2029:3c00:9:c41:b0c0:93a1
2600:9000:2029:9600:9:c41:b0c0:93a1
2600:9000:2029:2a00:9:c41:b0c0:93a1
2600:9000:2029:1600:9:c41:b0c0:93a1
2600:9000:2029:c00:9:c41:b0c0:93a1
2600:9000:2029:ce00:9:c41:b0c0:93a1
2600:9000:2029:6400:9:c41:b0c0:93a1
2600:9000:2029:ac00:9:c41:b0c0:93a1</pre>
<p>国外解析情况：</p>
<pre class="lang:sh decode:true">$ dig @8.8.8.8 +short guozeyu.com a
52.222.238.236
52.222.238.227
52.222.238.207
52.222.238.107
52.222.238.208
52.222.238.71
52.222.238.68
52.222.238.67
$ dig @8.8.8.8 +short guozeyu.com aaaa
2600:9000:202d:5c00:9:c41:b0c0:93a1
2600:9000:202d:ec00:9:c41:b0c0:93a1
2600:9000:202d:7c00:9:c41:b0c0:93a1
2600:9000:202d:2a00:9:c41:b0c0:93a1
2600:9000:202d:9400:9:c41:b0c0:93a1
2600:9000:202d:c600:9:c41:b0c0:93a1
2600:9000:202d:f600:9:c41:b0c0:93a1
2600:9000:202d:6200:9:c41:b0c0:93a1</pre>
<p>没错，CloudFront 分配给的 IP 数量就是多，让别人看了会感觉很厉害。</p>
<h4>Ping 启动前后对比</h4>
<p>这里只对比国外的速度</p>
<p>[img id="2593" size="large"]源站速度[/img]</p>
<p>[img id="2592" size="large"]CDN 速度[/img]</p>
<h4>HTTPs Get 启动前后对比</h4>
<p>这里也是只对比国外的速度</p>
<p>[img id="2596" size="large"]源站速度[/img]</p>
<p>[img id="2595" size="large"]CDN 速度[/img]</p>
<p>启动 CDN 后的 TTFB 几乎全面绿色，建立 TCP 和 TLS 的时间显著降低。</p>
<h4>Amazon 的 SSL 证书</h4>
<p>CloudFront 免费签发的 SSL 证书是<strong>多域名通配符证书</strong>（Wildcard SAN），并且主要名称是自定的，要比 Cloudflare 的共享证书高级。此类证书在 Cloudflare 上需要花费每月 10 美元。此类证书在市面上很难买到，而且价格取决于域名数量，在一年几千到几万不等。</p>
<p>然而，这个证书只能在 AWS 的 CloudFront 和负载均衡器上使用。</p>
<p><img class="aligncenter size-medium wp-image-2597" src="https://cdn.landcement.com/sites/2/2017/01/az-ssl-450x411.png" alt="" width="450" height="411" /></p>
<p>CloudFront 的证书链较长，会影响 TLS 时间，不过由于它同时也是 CDN，这样 TLS 时间几乎减少到了可以忽略不计的程度。主要还是因为 macOS 上还没有直接信任 Amazon Root CA，如果直接信任了，就用不着这样了。</p>
<h2>其他 CDN 厂商对比</h2>
<p>以下列出的所有提供商（或某一提供商的某些版本），均符合以下条件，如果不符合则单独列出：</p>
<ol>
<li>是个 CDN 厂家</li>
<li>支持 HTTPS、HTTP/2</li>
<li>免费签发 SSL 证书，且自动续费</li>
<li>我现在正在使用，或曾经长期使用过，或深入了解过</li>
<li>可以给 WordPress 全站 CDN 加速</li>
</ol>
<h3>Cloudflare 免费版/专业版</h3>
<p>有自建的网络，最快的速度、最低廉的价格，主要提供网站安全防护，当然还附带了 CDN。其提供的 NS 服务也是（国外）业界第一的速度。本站国外使用了 Cloudflare，欢迎直接测试本站国外的速度。</p>
<ul>
<li>国外速度：★★★★★，由于拥有众多的海外节点并支持 Anycast，给满分。速度指标指全球各地的 Ping 值，下同</li>
<li>国内速度：★★☆☆☆，国内走美国西岸的节点，速度欠佳</li>
<li>可定制性：★★☆☆☆，需要使用 Page Rules 进行定制，定制的功能有限，免费版 Page Rules 数量也有限。</li>
<li>廉价指数：★★★★★，从免费起步，给满分</li>
<li>方便接入：★★★★★，改完 NS 直接接入，自动签发 SSL 证书，无需服务器配置，还有比这更简单的吗？</li>
<li>缓存命中：★★★★★，由于节点数量实在众多，于是在每一个地方都需要单独缓存，所以缓存命中率很低；但是如果开启了 <a href="https://blog.cloudflare.com/argo/" target="_blank">Argo</a>，那么就能够实现更高的缓存命中率，此外还能自动调配最优线路。Argo 需要每月额外的消费（$5/mo + $0.10/GB）。</li>
<li>动静分离：★★★☆☆，自动分离，它遵守 Cache-Control 规则，也可以设置 <em>Page Rules</em> 修改默认缓存规则。但是，默认不缓存 HTML 页面、<em>Page Rules</em> 只有 3 个的限制、以及没有开放匹配 Cookie 规则的缓存。</li>
<li>缓存刷新：★★☆☆☆，仅支持刷新某个页面的 URL 和刷新全部内容，不支持规则刷新</li>
<li>接入方式：NS（如果是 Partner 则可以有免费的 CNAME 接入）</li>
<li>证书兼容性：仅限支持 SNI 的浏览器</li>
</ul>
<p>Cloudflare 作为全站 CDN 的特性：</p>
<ul>
<li>支持根域名</li>
<li>缓存静态文件</li>
<li><strong>不支持</strong>缓存页面</li>
<li>免费 SSL 证书</li>
</ul>
<p>有一点不同的是，Cloudflare 签发的是共享证书，证书样式如下：</p>
<p><img class="aligncenter size-medium wp-image-2615" src="https://cdn.landcement.com/sites/2/2017/01/Screenshot-2017-01-29-19.13.26-450x287.png" alt="" width="450" height="287" /></p>
<p>我觉得 Cloudflare 签发共享证书有两个原因，一是历史遗留问题：Cloudflare 专业版的 SSL 证书服务是支持无 SNI 的客户端的，而为了支持无 SNI 的客户端，一个 IP 就只能配置一个证书，所以就使用了共享证书节约 IP 资源。而现在免费版也有了 SSL，虽然免费版使用了 SNI 技术，但是证书总不能比付费版本还要高级吧，于是还是使用了共享 SSL 证书；二是为了增加更多的增值服务，现在 Cloudflare 上可以购买 Dedicated SSL Certificates，实现独立的证书（如果是付费版本启用，不支持 SNI 的客户端仍然 Fall back 到共享证书，所以仍然兼容不支持 SNI 的设备）。</p>
<h3>Cloudflare 企业版</h3>
<p>简介同上，此版本适合大客户，流量越大越适合用。百度云加速是和 Cloudflare 深度整合的，其实基础设施完全一样，但百度云加速没有提供 API 接口。</p>
<ul>
<li>国外速度：★★★★★，同上</li>
<li>国内速度：★★★★★，有众多的国内节点</li>
<li>可定制性：★★★☆☆，同上，Page Rules 数量有所提升</li>
<li>廉价指数：★★☆☆☆，每月固定的花销，不是按需付费，量越大越实惠</li>
<li>方便接入：★★★★★，同上</li>
<li>缓存命中：★★★★★，同上</li>
<li>动静分离：★★★★☆，对于 WordPress 来说安装了官方插件就可以自动分离，相比免费版，他有更多的 <em>Page Rules</em>、支持匹配 Cookie 规则缓存，相比 CloudFront 差一些</li>
<li>缓存刷新：★★★★☆，相比免费版，支持了 Cache-Tag 刷新规则，然而需要服务端的配置</li>
<li>接入方式：NS/CNAME</li>
<li>证书兼容性：<strong>所有</strong>浏览器</li>
</ul>
<p>Cloudflare 企业版作为全站 CDN 的特性：</p>
<ul>
<li>支持根域名</li>
<li>缓存静态文件</li>
<li>支持缓存页面</li>
<li>页面更新自动清理缓存（完美清理缓存）（由于百度云加速没有提供 API，所以云加速没有这个功能）</li>
<li>强大的 DDOS 防御以及 WAF 功能</li>
<li>免费 SSL 证书</li>
</ul>
<h3>UPYUN</h3>
<p>使用自己管理的机房，网络有些受限于中国的环境，单价业界最低。</p>
<ul>
<li>国外速度：★★☆☆☆，北美洲、欧洲、亚洲都有一定数量的节点，但速度欠佳。且 CNAME 接入所用的 NS 在国外没有节点，在解析速度上就牺牲很多。</li>
<li>国内速度：★★★★★，国内节点很多，但是由于只能 CNAME 接入，需要多一次解析请求，花费时间</li>
<li>可定制性：★★★★☆，可以设置很多个缓存规则，并且有<a href="http://docs.upyun.com/cdn/rewrite/" target="_blank">自定义 Rewrite</a>，可以实现比 Rewrite 更丰富的功能，但是函数功能受限。</li>
<li>廉价指数：★★★★½，从免费起，Pay-as-you-go，价格也是一降再降，业界较低的标准</li>
<li>方便接入：★★★☆☆，不需要配置多少参数，CNAME 接入相比 NS 更有难度。SSL 证书首次需要手动添加，自动续签。</li>
<li>缓存命中：★★★★½，有源站资源迁移功能，首次访问后直接永久缓存。但是如果要删除文件，还需要用 API 手动删除，扣半分</li>
<li>动静分离：★★★★☆，自动分离，可以配置不同目录的缓存规则，但是不支持Cookie 规则缓存</li>
<li>缓存刷新：★★★★☆，支持单个 URL 刷新以及规则匹配刷新</li>
<li>接入方式：CNAME，所以不能根域名使用</li>
<li>证书兼容性：仅限支持 SNI 的浏览器</li>
</ul>
<p>UPYUN 作为全站 CDN 的特性：</p>
<ul>
<li><strong>不支持</strong>根域名</li>
<li>缓存静态文件</li>
<li><strong>不支持</strong>缓存页面</li>
<li>有 WAF 功能</li>
<li>免费 SSL 证书</li>
<li>可配置国内外 CDN 混用</li>
</ul>
<p>UPYUN 和下面的 KeyCDN 签发的都是 Let's Encrypt 的独立证书，但都是单域名证书，甚至有 www 和无 www 的都要单独申请。</p>
<h3>Google Cloud CDN</h3>
<p>有全球最密集的网络集群，最快的速度、较低的单价，主要提供负载均衡，SSL 卸载，当然还附带了 CDN。由于缓存命中率低，需要超大型访问量的网站才有效。正是因为这一点，Google 自己只是将用户量极大的搜索服务用上了这个 CDN 系统，其余的很多 CDN 用的是 Cloudflare 和 Fastly 的。Google 的网络和 Cloudflare 和 Fastly 的网络有内网链接。<a href="https://guozeyu.com/2016/10/build-a-anycast-network-gce/">详细介绍看本站的这篇文章</a></p>
<ul>
<li>国外速度：★★★★★，由于拥有众多的海外节点并支持 Anycast，给满分。</li>
<li>国内速度：★★★☆☆，国内直连香港节点，几乎是速度最快的香港网络的，与国内几大运营商都有接入，但毕竟没有国内节点，比不过一些国内的速度。（但是目前所分配到的一些 IP，联通会绕道至美西了）</li>
<li>可定制性：★★☆☆☆，可以根据不同路径配置不同的服务器，然后，好想也没什么别的可定制的了。</li>
<li>廉价指数：★★☆☆☆，由于占用了 IP 资源，每月需要花费 18 美元的固定价格，并还需要再为流量付费。流量的单价较低。</li>
<li>方便接入：★☆☆☆☆，需要各种复杂的配置，但是一旦完成了配置，就同时有了负载均衡，弹性伸缩等等特性。</li>
<li>缓存命中：★½☆☆☆，节点太多，小流量网站都很难遇到命中的情况。但可以利用跨区域负载均衡提高缓存命中率。</li>
<li>动静分离：★★☆☆☆，自动分离，但不能配置任何规则。</li>
<li>缓存刷新：★★★★☆，支持单个 URL 刷新以及规则匹配刷新</li>
<li>接入方式：IP 绑定，它直接给你分配一个独立的 Anycast IP，只需要 A 记录解析即可。</li>
<li>证书兼容性：<strong>所有</strong>浏览器</li>
<li>不包含免费 SSL，需要自己购买</li>
</ul>
<p>Google Cloud CDN 作为全站 CDN 的特性：</p>
<ul>
<li>支持根域名</li>
<li>缓存静态文件</li>
<li><strong>不支持</strong>缓存页面</li>
<li><strong>无</strong>免费 SSL 证书</li>
<li>可配置国内外 CDN 混用</li>
</ul>
<h3>KeyCDN</h3>
<p>他们是租用别人的独立服务器，提供一体化 CDN 服务，单价业界最低。</p>
<ul>
<li>国外速度：★★★★☆，和 CloudFront 有一拼，但是由于只能 CNAME 接入，需要多一次解析请求，花费时间</li>
<li>国内速度：★☆☆☆☆，国内的话香港节点，但是狂绕道，反而比美国还慢</li>
<li>廉价指数：★★★☆☆，有最低年费（相当于起步价）</li>
<li>方便接入：★★★½☆，不需要配置多少参数，CNAME 接入相比 NS 更有难度。SSL 可以一键添加。</li>
<li>缓存命中：★★★★☆，有类似 CloudFront <em>Regional Edge Caches</em> 的功能</li>
<li>动静分离：★★☆☆☆，自动分离，但不能配置规则。支持针对 Cookie 的缓存配置，但不能匹配 Cookie 内容</li>
<li>缓存刷新：★★★★☆，支持单个 URL 刷新、全部刷新、Cache-Tag 刷新</li>
<li>接入方式：CNAME，所以不能根域名使用</li>
<li>证书兼容性：仅限支持 SNI 的浏览器</li>
</ul>
<p>KeyCDN 作为全站 CDN 的特性：</p>
<ul>
<li><strong>不支持</strong>根域名</li>
<li>缓存静态文件</li>
<li>缓存页面</li>
<li>页面更新自动清理缓存（完美清理缓存）</li>
<li>免费 SSL 证书</li>
<li>可配置国内外 CDN 混用</li>
</ul>
<p>我为他写了一个插件可以实现完美清理缓存，<a href="https://guozeyu.com/2016/02/this-site-uses-keycdn-as-a-front-end-to-speed-up-instead-of-cloudflare/">详情见此</a></p>
<h2>关于 WordPress 动静分离的新方法</h2>
<p>WordPress 可以分别设置 Site URL 和 Home URL，对于 https://example.com 这个网站，这两栏就可以这样设置：</p>
<ul>
<li><strong>Home URL</strong>：https://example.com</li>
<li><strong>Site URL</strong>：https://wp.example.com</li>
</ul>
<p>然后，直接给 Home URL 上 CDN，在 CDN 或者源站上配置忽略 Cookie 信息。Site URL 回源，用作 WordPress 后台管理即可。</p>
<p>[modified github="ZE3kr/ZE3kr"]增加 “可定制性” 介绍[/modified]</p>
