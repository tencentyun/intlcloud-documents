## Overview
Smart Compression can automatically compress the resources to Gzip/Brotli files to reduce the files size and shorten the resource loading time.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Site Acceleration** > **File Optimization** on the left sidebar.
2. On the page that appears, select a site, and toggle on/off Smart Compression.
![](https://qcloudimg.tencent-cloud.cn/raw/ba7b8cd394825462e164d68982918a43.png)
**Parameter description:**
 - **On** (default): Smart compression is enabled.
 - **Off**: Smart compression is disabled.

## Notes
1. Smart compression supports files of 256 B to 30 MB.
2. By default, smart compression compresses resources by `Content-Type` and supports the following types:
```js.
text/html
text/xml
text/plain
text/css
text/javascript
application/json
application/javascript
application/x-javascript
application/rss+xml
application/xmltext
image/svg+xml
image/tiff
text/richtext
text/x-script
text/x-component
text/x-java-source
text/x-markdown
text/js
image/x-icon
image/vnd.microsoft.icon
application/x-perl
application/x-httpd-cgi
application/xml
application/xml+rss
application/vnd.api+json 
application/x-protobuf 
multipart/bag
multipart/mixed
application/xhtml+xml
font/ttf
font/otf
font/x-woff
application/vnd.ms-fontobject
application/ttf
application/x-ttf
application/otf
application/x-otf
application/truetype
application/opentype
application/x-opentype
application/font-woff
application/eot
application/font
application/font-sfnt
application/wasm
application/javascript-binast 
application/manifest+json 
application/ld+json
```
3. If both Gzip compression and Brotli compression are enabled, and the client request header `Accept-Encoding` carries both `br` and `gzip`:
 - If the node has cached resources compressed in Brotli and Gzip, Brotli compressed resources are returned first.
 - If the node has cached resources compressed only in Brotli, Brotli compressed resources are returned first.
 - If the node has cached resources compressed only in Gzip, Gzip compressed resources are returned first.
4. If only Brotli compression or Gzip compression is enabled and the request header carries `gzip` or `br`, the compression will not take effect, and the original resource will be returned.
5. If the origin server has the compression feature enabled, and the server carries the response header `Content-Encoding`, the smart compression feature will no longer take effect.
