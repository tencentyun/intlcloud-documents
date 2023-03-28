## Overview

By configuring the cache TTL, you can optimize node cache to improve resource loading and update resources in a timely manner.

>?
>- EdgeOne determines whether a resource cached on a node expires based on the cache TTL you configure.
>- Cache available: The node returns the cached resource directly.
>- Cache not available: The node pulls the latest resource from the origin, caches it and then returns it to the client.
>- After a resource on the origin server is updated, its cache on the node needs to be updated immediately. You can use the [cache purge](https://intl.cloud.tencent.com/document/product/1145/46179) feature to clear historical caches that haven't expired on the node, so that the latest resources can be requested from the origin server.

## Directions

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Site Acceleration** > **Cache Configuration** on the left sidebar.
2. On the cache configuration page, select a target site and click **Set** in the node cache TTL** module.
![](https://qcloudimg.tencent-cloud.cn/raw/9507c0e41ed6723a2aec1556713fd208.png)
Description of configuration items:
 - Follow the origin's Cache-Control
<table>
<thead>
<tr>
<th width="30%">Item</th>
<th>No Cache-Control</th>
<th>Details</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=3 >Follow the origin's Cache-Control (<strong>automatically configured</strong>)</td>
<td>Default cache policy (<strong>automatically configured</strong>)</td>
<td>See <a href="#mr">the table</a> for details.</td>
</tr>
<tr>
<td>Do not cache</td>
<td>-</td>
</tr>
<tr>
<td>Custom TTL</td>
<td>-</td>
</tr>
</tbody></table>
<p><a id="mr"></a>Follow default cache policy:</p>
<table>
<thead>
<tr>
<th width="30%">Category</th>
<th width="70%">Cache</th>
</tr>
</thead>
<tbody><tr>
<td>The origin contains the Last-Modified header</td>
<td>TTL = ( Current time - last_modified ) × 0.1. If the result is within the range of 10 to 3600 seconds. A TTL less than 10 seconds is rounded up to 10 seconds, while a TTL longer than 3600 seconds is set to 3600 seconds.</td>
</tr>
<tr>
<td>The origin doesn’t contain the Last-Modified header</td>
<td>Cache by the file extension<ul><li>Dynamic files are not cached. Format: php, aspx, asp, jsp, do, dwr, cgi, fcgi, action, ashx, axd, json. </li><li>Static files are cached for 2 hours. <ul><li>Image: jpg, png, jpeg, webp, gif, heif, heic, kpg, ico. </li><li>Video: mp4, mp3, m3u8, ts, m4a, avi, m4s, ogg. </li><li>Web page: html, js, css. </li><li>Compressed package: zip, 7z, tar, br, gz, rar, bz2. </li><li>Document: doc, docx, xls, xlsx, pdf, ppt, pptx. </li><li>Application: apk, exe, bin. </li><li>Others: vsv, iso, jar, swf, chunk, atlas. </li></ul></td>
</tr>
</tbody></table>

  - Do not cache: Do not cache the resources on nodes.
  - Custom TTL: Specify a cache validity. 
>?
>- By default, the custom TTL setting here overwrites the origin's cache setting, which means even if the origin’s `Cache-Control` is set to `no-cache/no-store/private`, resources are stilled cached to the node accordingly.
>- To follow the origin’s cache setting, you need to change the node cache TTL rules in **Rule Engine**. See [Rule Engine](https://intl.cloud.tencent.com/document/product/1145/46151). 
>- To increase the cache hit rate, it’s recommended to keep the default setting.

3. To define fine-grained settings targeting specific sub-domain names and request URLs, you can create custom rules with [Rule Engine](https://intl.cloud.tencent.com/document/product/1145/46151).


See below for the node cache workflow:

![](https://qcloudimg.tencent-cloud.cn/raw/ff3e0f7407150bbf0c84c0c24eec02cf.png)
