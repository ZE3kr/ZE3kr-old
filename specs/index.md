---
layout: page
status: publish
published: true
title: 技术参数
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://guozeyu.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://guozeyu.com
wordpress_id: 578
wordpress_url: https://guozeyu.com/?page_id=578
date: '2016-01-03 13:33:56 +0800'
date_gmt: '2016-01-03 05:33:56 +0800'
categories: []
tags: []
---
<p>使用 VPS 搭建，几乎完全静态化。</p>
<blockquote><p>注意⚠️：此页面已经过时，请<a href="https://wiki.tlo.xyz/%E7%94%A8%E6%88%B7:ZE3kr/%E6%8A%80%E6%9C%AF%E5%8F%82%E6%95%B0">查看最新的对应页面</a></p></blockquote>
<p><a href="https://status.tlo.xyz/oVxvPUZ9z" target="_blank">主机状态</a></p>
<h2>CDN 节点调试 URL</h2>
<ul>
<li>Cloudflare Edge：<a href="https://cdn.landcement.com/cdn-cgi/trace" target="_blank" rel="noopener noreferrer">https://cdn.landcement.com/cdn-cgi/trace</a></li>
<li>UPYUN：<a href="https://ze3kr.b0.upaiyun.com/cdn-cgi/trace" target="_blank">https://ze3kr.b0.upaiyun.com/cdn-cgi/trace</a></li>
<li>主站默认节点：<a href="https://guozeyu.com/cdn-cgi/trace" target="_blank">https://guozeyu.com/cdn-cgi/trace</a></li>
</ul>
<h2>本站架构</h2>
<p>本站使用了<a href="https://guozeyu.com/2017/01/wordpress-full-site-cdn/">全站 CDN</a>，其中国内是解析到国内的 UPYUN 节点，国外访问使用 CloudFront，均支持 HTTP/2，仅国外访问支持 IPv6。</p>
<p>其中的多媒体文件（包括但不限于图片、视频）均存放到了 Google Cloud Storage 的 Multi-Regional Asia 地区，多媒体前端使用<a href="https://domain.tloxygen.com/web-hosting/index.php" target="_blank" rel="noopener noreferrer">香港 CN2 虚拟主机</a>自带的 CDN 服务进行加速。其中国外的 CDN 节点与 Google Cloud Storage 之间开启了 Interconnect；国内的 CDN 节点经过了 UPYUN 的缓存。</p>
<h2>视频参数</h2>
<h3>视频格式</h3>
<p>此网站使用自己的 CDN 加速视频，使用 MP4 格式，从 2016 年开始，所有的视频还将有 WEBM 格式，并且我还会逐渐的让以前的视频也支持 WEBM。</p>
<h3>视频质量</h3>
<p>使用 qHD（540p）准高清（腾讯视频将其称作为超清也是醉了）。同时使用 MP4 封装的 H.264 + AAC 和 WEBM 封装的 VP9 + Vorbis，每个视频的每种格式使用近似相等的码率，通常后者画质更高一些。本站对于 30 帧的视频使用 1000kbps 的平均码率，60 帧的视频使用 1500kbps 的平均码率；音频均为单声道 64kbps 码率。通常本站的视频（无论是什么格式）在 720p 或更低分辨率下的屏幕上都显得十分清晰（例如 iPhone 6，这只是主观测试）。更高分辨率下的屏幕下若使用 MP4 格式，能看到明显的画质下降的痕迹，WEBM 有明显优势。</p>
<h4>MP4/H.264 压缩方式</h4>
<ul>
<li>视频：H.264 多通路，平均码率 1000k（对于 60 帧的，使用 1500k），540p 画质，降分辨率使用线性滤镜，多次通过</li>
<li>音频：AAC 单声道，平均码率 64k</li>
</ul>
<h4>WEBM/VP9 压缩方式</h4>
<ul>
<li>视频：libvpx-VP9，平均码率 1000k（对于 60 帧的，使用 1500k），540p 画质，两次通过</li>
<li>音频：Vorbis 单声道，平均码率 64k</li>
</ul>
<h3>压制参数</h3>
<h4>1080p/2160p MP4/HEVC</h4>
<pre class="lang:sh decode:true ">./ffmpeg -y -i &lt;input&gt; -c:v libx265 -tag:v hvc1 -threads 8 output.mp4</pre>
<h4>540p 30帧 MP4/H.264</h4>
<pre class="lang:sh decode:true">ffmpeg -y -i input -c:v libx264 -r 30000/1001 -c:a aac -preset veryslow -s 960x540 -b:v 1000k -threads 8 -pass 1 -b:a 64k -ac 1 -f mp4 /dev/null

ffmpeg -y -i input -c:v libx264 -r 30000/1001 -c:a aac -preset veryslow -s 960x540 -b:v 1000k -threads 8 -pass 2 -b:a 64k -ac 1 output.mp4</pre>
<h4>540p 60帧 MP4/H.264</h4>
<pre class="lang:sh decode:true">ffmpeg -y -i input -c:v libx264 -r 60000/1001 -c:a aac -preset veryslow -s 960x540 -b:v 1500k -threads 8 -pass 1 -b:a 64k -ac 1 -f mp4 /dev/null

ffmpeg -y -i input -c:v libx264 -r 60000/1001 -c:a aac -preset veryslow -s 960x540 -b:v 1500k -threads 8 -pass 2 -b:a 64k -ac 1 output.mp4</pre>
<h4>540p 30帧 WEBM/VP9</h4>
<pre class="lang:sh decode:true">ffmpeg -y -i &lt;source&gt; -c:v libvpx-vp9 -pass 1 -b:v 1000K -threads 8 -speed 4 -tile-columns 6 -frame-parallel 1 -b:a 64k -ac 1 -s 960x540 -g 150 -r 30000/1001 -an -f webm /dev/null

ffmpeg -y -i &lt;source&gt; -c:v libvpx-vp9 -pass 2 -b:v 1000K -threads 8 -speed 1 -tile-columns 6 -frame-parallel 1 -auto-alt-ref 1 -lag-in-frames 25 -ac 1 -s 960x540 -r 30000/1001 -c:a libopus -b:a 64k -f webm out.webm</pre>
<h4>540p 60帧 WEBM/VP9</h4>
<pre class="lang:sh decode:true">ffmpeg -y -i &lt;source&gt; -c:v libvpx-vp9 -pass 1 -b:v 1500K -threads 8 -speed 4 -tile-columns 6 -frame-parallel 1 -b:a 64k -ac 1 -s 960x540 -g 250 -r 60000/1001 -an -f webm /dev/null

ffmpeg -y -i &lt;source&gt; -c:v libvpx-vp9 -pass 2 -b:v 1500K -threads 8 -speed 1 -tile-columns 6 -frame-parallel 1 -auto-alt-ref 1 -lag-in-frames 25 -ac 1 -s 960x540 -r 60000/1001 -c:a libopus -b:a 64k -f webm out.webm
</pre>
