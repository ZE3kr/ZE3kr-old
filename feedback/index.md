---
layout: page
status: publish
published: true
title: 反馈
author:
  display_name: ZE3kr
  login: ZE3kr
  email: ze3kr@icloud.com
  url: https://ze3kr.com
author_login: ZE3kr
author_email: ze3kr@icloud.com
author_url: https://ze3kr.com
wordpress_id: 2135
wordpress_url: https://ze3kr.com/?page_id=2135
date: '2016-11-05 21:55:33 +0000'
date_gmt: '2016-11-05 13:55:33 +0000'
categories: []
tags: []
---
<p>你可以在这个页面给本站写反馈，你写的反馈<strong>可能</strong>会被公开在这个页面上。</p>
<form action="https://ze3kr.com/wp-content/plugins/add-pingback-manually/add-pingback.php" method="post">
<p class="comment-notes"><span id="email-notes">可以匿名提交</span></p>
<p class="comment-form-url"><label for="pingback-content">内容 <span class="required">*</span></label> <textarea id="pingback-content" cols="45" maxlength="65525" name="pingback-content" rows="3"></textarea></p>
<p><label for="pingback-title">姓名</label> <input id="pingback-title" maxlength="100" name="pingback-title" size="30" type="text" value="" /></p>
<p class="comment-form-email"><label for="pingback-email">电子邮件</label> <input id="pingback-email" maxlength="100" name="pingback-email" size="30" type="email" value="" /></p>
<p class="form-submit"><input id="submit" class="submit" name="submit" type="submit" value="提交" /> <input id="pingback-type" name="pingback-type" type="hidden" value="" /><input id="pingback-id" name="pingback-id" type="hidden" value="https://ze3kr.com/feedback/" /></p>
<p><script><br />
var comment_author_email = jQuery.cookie("comment_author_email_dd9fd5473a8961943ad4decbd45b5159");<br />
var comment_author_url = jQuery.cookie("comment_author_dd9fd5473a8961943ad4decbd45b5159");<br />
if(typeof comment_author !== "undefined") {<br />
	jQuery('#pingback-title').val(comment_author);<br />
}<br />
if(typeof comment_author_email !== "undefined") {<br />
	jQuery('#pingback-email').val(comment_author_email);<br />
}<br />
</script></p>
</form>
