---
layout: post
status: publish
published: true
title: WordPress 上的几个推荐安装的插件
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://guozeyu.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://guozeyu.com
wordpress_id: 96
wordpress_url: https://xn--oor13x.tlo.xyz/?p=96
date: '2016-01-29 10:19:00 +0800'
date_gmt: '2016-01-29 02:19:00 +0800'
categories:
- 开发
tags:
- WordPress
---
<h2>EWWW Image Optimizer</h2>
<p>无损及有损压缩 JPEG 和 PNG 图像，支持压缩已有的图像，可以加快访问者加载图片的速度。同时支持 JPEG 的渐进式加载。正常情况下，网速低时，图片是一点点从上往下加载，<b>而使用渐进式加载，则是先加载这个图片的低分辨率版本，然后逐渐变得清晰。</b>我已经成为这个插件的付费用户，能够进一步有损压缩 PNG 和 JPEG 格式图片、降低服务器 CPU 占用（否则每上传一张图片，CPU 都消耗很多）。不过最近使用了 Cloudflare 的 Polish 功能，就没有再在服务器上安装同类软件了。</p>
<h2>Autoptimize</h2>
<p>[img id="1029" size="medium"][/img]</p>
<p>这个插件能够自动的合并 CSS 和 JS，并对其压缩，非常<!--more-->的方便。而且一些主题会有大量的 inline CSS，当开启了合并 CSS 后，这些 inline CSS 会自动添加到文件中。</p>
<p>我在这个插件中的<strong>一些配置</strong>，分享出来：</p>
<h3>Exclude scripts from Autoptimize</h3>
<pre class="lang:default decode:true ">functions.js,player,mediaelement,sparkline,toolbar,admin,akismet,themes</pre>
<ul>
<li>functions.js,themes：排除所有主体主题相关的脚本，全面解决合并后会导致菜单的交互出现问题</li>
<li>player,mediaelement：排除 WordPress 播放器的合并，因为这部分文件有的页面有，有的页面没有</li>
<li>sparkline,toolbar,admin：这些文件只有用户登录后才会加载</li>
<li>akismet：安装了 akismet 插件后推荐添加</li>
</ul>
<h3>Exclude CSS from Autoptimize</h3>
<pre class="lang:default decode:true">admin,mediaelement,wordfence,piwik,toolbar,dashicons,crayon-syntax-highlighter/themes,crayon-syntax-highlighter/fonts</pre>
<ul>
<li>admin,mediaelement,toolbar,dashicons：同上，只有管理员才会加载，或者是只有部分页面才会加载的东西</li>
<li>crayon-syntax-highlighter/themes,crayon-syntax-highlighter/fonts：排除 Crayon Syntax Highlighter 插件仅在部分页面才会加载的 CSS</li>
<li>wordfence,piwik：排除一些插件</li>
</ul>
<h3>建议开启</h3>
<ul>
<li><strong>Optimize HTML Code</strong>：优化 HTML 代码，能减少页面大小</li>
<li><strong>Optimize JavaScript Code</strong>：优化 JS 代码，能减少 JS 大小并合并 JS</li>
<li><strong>Force JavaScript in &lt;head&gt;</strong>：能提前加载 JS</li>
<li><strong>Optimize CSS Code</strong>：优化 CSS 代码，能减少 CSS 大小并合并 CSS</li>
<li><strong>Generate data: URIs for images</strong>：将文件直接嵌入 CSS 中，减少请求数</li>
<li><strong>Remove Google Fonts</strong>：移除 Google 字体，这种字体文件都是只对西文有效的，对于中文没有意义。</li>
<li><strong>Also aggregate inline CSS</strong>：将 Inline 的 CSS 放到 CSS 文件里，能减少页面大小</li>
<li><strong>Save aggregated script/css as static files</strong>：能提高处理性能</li>
</ul>
<h3>建议关闭</h3>
<ul>
<li><strong>Keep HTML comments</strong>：有些时候 HTML comments 是有作用的</li>
<li><strong>Also aggregate inline JS</strong>：每个页面的 JS 都不同，不要开启</li>
<li><strong>Add try-catch wrapping</strong>：没有什么意义的东西</li>
<li><strong>Inline and Defer CSS</strong>：将 CSS 全面嵌入到页面里，会极大增加页面大小，但能减少请求数，但是真的大多数情况下只会让网站更慢。</li>
<li><strong>Inline all CSS</strong>：同上</li>
</ul>
<h2>AMP</h2>
<p>插件作者是：Automattic ，为 Google 优化，搜索结果中展示超快的 AMP 页面。详情：<a class=" wrap external" href="https://guozeyu.com/2016/10/amp-html/" target="_blank" rel="nofollow noreferrer">使用 AMP 构建超快的移动页面</a></p>
<h2>Google Authenticator</h2>
<p>二部认证器（需要配合同名手机客户端，或者 1Password 专业版）。你可曾听说过 Heart Bleed 漏洞？有了二部认证，就算再有 Heart Bleed 漏洞，都无需害怕。</p>
<p>原理：手机生成器上扫描二维码保存密钥，然后生成器根据时间变量生成6位数字。这6位数字有有效期，并且只能用一次。安全性甚至大于短信验证码</p>
<h2>IP Dependent Cookies</h2>
<p>更换 IP 后需要重新登录，就算使用 HTTP 也可以一定程度上避免 Cookie 泄漏的风险</p>
<h2>Wordfence</h2>
<p>WordPress #1 的<b>安全防御</b>插件，可限制密码尝试次数防止暴力破解，可为你的 WordPress 增加 WAF 功能，查看实时访问。通过查看它的日志我才发现，原来我的 WordPress 一直在被恶意的暴力破解，有时一天几千次，<b>几乎天天都有</b>。不过还好只要尝试 3 次错误密码，IP 会直接被屏蔽掉，这也是 Failed Logins 数量不多的原因。</p>
<p>像这种是基于应用层面的防御，并不是 Cloudflare 等云加速，抗 DDOS 服务所能防御的。</p>
<h2>Crayon Syntax Highlighter</h2>
<p>[img id="1030" size="medium"][/img]</p>
<p>这个插件能够让 WordPress 上展示自动高亮的源代码，有多种主题可以选择，支持多种编程语言。</p>
<h2>Slimpack</h2>
<p>[img id="1031" size="medium"][/img]</p>
<p>这是 Jetpack 的简化版，没有 Jetpack 那一堆没用的特性，不需要登录到 wordpress.com，功能齐全，使用起来也非常简便。</p>
<h2>XML Sitemap &amp; Google News feeds</h2>
<p>这个插件能够自动生成网站的 <code>sitemap.xml</code> 和 <code>robots.txt</code>，你可以直接将 <code>sitemap.xml</code> 提交到百度和 Google，这样搜索引擎就不会漏掉你的网站上的每一篇文章了。</p>
<p>这个插件支持 WordPress 的多站点，不需要任何配置，推荐在整个网络上启用。</p>
<h2>WP-Piwik</h2>
<p>这个插件能够让你的整个网站拥有统计功能，支持 WordPress 的多站点，推荐在整个网络上启用。关于 Piwik 配合 WordPress，请参见这篇文章：<a href="https://guozeyu.com/2016/01/piwik-wordpress/">Piwik 与 WordPress 配合使用，建立强大统计系统</a>。</p>
<h2>Blubrry PowerPress</h2>
<p>[img id="1032" size="medium"][/img]</p>
<p>这个插件能够让你的 WordPress 生成一个 Podcast Feed，让你有一个播客平台，你也可以把这个 Feed 直接提交到 iTunes 等地方。</p>
<p>&nbsp;</p>
<h2>Exif Caption</h2>
<p>这个插件可以让你将图片的 Exif 信息插入到图片的说明中，缺点是需要上传图片后手动添加，但是它可以批量添加，还算方便。将 Exif 信息插入到图片的说明后，再将这个图片插入到文章中，Exif 信息就能够显示在文章中。</p>
