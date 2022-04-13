## Overview
A node can perform Brotli compression on resources to reduce the size of transferred files for quicker resource loading.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.
>

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **File optimization** on the left sidebar.
2. On the file optimization page, select the target site and toggle the Brotli feature on or off.
![](https://qcloudimg.tencent-cloud.cn/raw/ba7b8cd394825462e164d68982918a43.png)
**Parameter description:**
 - Enabled status (default): Brotli compression is enabled.
>!Brotli compression takes effect only if the client request carry the request header `Accept-Encoding: br`.
 - Disabled status: Brotli compression is disabled.


## Notes
- The platform supports gzip compression by default but responds to Brotli compression first.
- Files that are 256 B–30 MB in size can be compressed with Brotli.
- Brotli compression supports the following file types:
```
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

