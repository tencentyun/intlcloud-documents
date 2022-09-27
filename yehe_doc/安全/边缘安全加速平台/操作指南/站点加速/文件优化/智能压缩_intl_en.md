## Overview
Smart Compression can automatically compress the resources to Gzip/Brotli files to reduce the files size and shorten the resource loading time.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Site Acceleration** > **File Optimization** on the left sidebar.
2. On the page that appears, select a site, and toggle on/off Smart Compression.
![](https://qcloudimg.tencent-cloud.cn/raw/ba7b8cd394825462e164d68982918a43.png)

**Parameter description:**
 - **On** (default): Smart compression is enabled.

>! To use smart compression, the client request must include the "Accept-Encoding: gzip (or br)" header. If both compression methods are enabled, Brotli compression takes priority.

 - **Off**: Smart compression is disabled.


## Supports and Limits
- File size: 256 B – 30 MB
- File formats (compress based on Content-Type):
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

