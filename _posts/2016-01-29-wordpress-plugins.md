---
layout: post
status: publish
published: true
title: WordPress 上的几个推荐安装的插件
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://ze3kr.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://ze3kr.com
wordpress_id: 96
wordpress_url: https://xn--oor13x.tlo.xyz/?p=96
date: '2016-01-29 10:19:00 +0000'
date_gmt: '2016-01-29 02:19:00 +0000'
categories:
- 开发
tags:
- WordPress
---
<h2>EWWW Image Optimizer</h2>
<p>无损及有损压缩 JPEG 和 PNG 图像，支持压缩已有的图像，可以加快访问者加载图片的速度。同时支持 JPEG 的渐进式加载。正常情况下，网速低时，图片是一点点从上往下加载，<b>而使用渐进式加载，则是先加载这个图片的低分辨率版本，然后逐渐变得清晰。</b>我已经成为这个插件的付费用户，能够进一步有损压缩 PNG 和 JPEG 格式图片、降低服务器 CPU 占用（否则每上传一张图片，CPU 都消耗很多）。</p>
<h2>Autoptimize</h2>
<p><img class="aligncenter size-medium wp-image-1029" src="https://cdn.tloxygen.com/sites/2/20160201140304/2016-01-29-09.35.09-450x355.png" alt="" width="450" height="355" /></p>
<p>这个插件能够自动的合并 CSS 和 JS，并对其压缩，非常<!--more-->的方便。而且一些主题会有大量的 inline CSS，当开启了合并 CSS 后，这些 inline CSS 会自动添加到文件中。</p>
<p>我在这个插件中的一些配置，分享出来：</p>
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
<h2>Crayon Syntax Highlighter</h2>
<p><img class="aligncenter size-medium wp-image-1030" src="https://cdn.tloxygen.com/sites/2/20160201140310/2016-01-29-09.55.25-450x259.png" alt="" width="450" height="259" /></p>
<p>这个插件能够让 WordPress 上展示自动高亮的源代码，有多种主题可以选择，支持多种编程语言。</p>
<h2>Slimpack</h2>
<p><img class="aligncenter size-medium wp-image-1031" src="https://cdn.tloxygen.com/sites/2/20160201140314/2016-01-29-09.59.11-450x333.png" alt="" width="450" height="333" /></p>
<p>这是 Jetpack 的简化版，没有 Jetpack 那一堆没用的特性，不需要登录到 wordpress.com，功能齐全，使用起来也非常简便。</p>
<h2>XML Sitemap &amp; Google News feeds</h2>
<p>这个插件能够自动生成网站的 <code>sitemap.xml</code> 和 <code>robots.txt</code>，你可以直接将 <code>sitemap.xml</code> 提交到百度和 Google，这样搜索引擎就不会漏掉你的网站上的每一篇文章了。</p>
<p>这个插件支持 WordPress 的多站点，不需要任何配置，推荐在整个网络上启用。</p>
<h2>WP-Piwik</h2>
<p>这个插件能够让你的整个网站拥有统计功能，支持 WordPress 的多站点，推荐在整个网络上启用。关于 Piwik 配合 WordPress，请参见这篇文章：<a href="https://ze3kr.com/2016/01/piwik-wordpress/">Piwik 与 WordPress 配合使用，建立强大统计系统</a>。</p>
<h2>Blubrry PowerPress</h2>
<p><img class="aligncenter size-medium wp-image-1032" src="https://cdn.tloxygen.com/sites/2/20160201140316/IMG_1301-253x450.png" alt="" width="253" height="450" /></p>
<p>这个插件能够让你的 WordPress 生成一个 Podcast Feed，让你有一个播客平台，你也可以把这个 Feed 直接提交到 iTunes 等地方。</p>
<h2>Add From Server</h2>
<p>这个插件能够让你通过 FTP 方式上传媒体到主机，并通过它将这个媒体添加到媒体库。</p>
<h2>Exif Caption</h2>
<p>这个插件可以让你将图片的 Exif 信息插入到图片的说明中，缺点是需要上传图片后手动添加，但是它可以批量添加，还算方便。将 Exif 信息插入到图片的说明后，再将这个图片插入到文章中，Exif 信息就能够显示在文章中。</p>
<h2>xili-language</h2>
<p>这个插件能够让网站支持多语言，还支持自动适配语言。主站 [a href="https://tlo.xyz/"]TLO.XYZ[/a] 就支持多语言。</p>
