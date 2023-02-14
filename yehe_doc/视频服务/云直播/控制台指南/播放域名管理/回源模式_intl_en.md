If you have a self-built origin server and live streaming source, CSS can pull streams from your origin server and distribute the content for you. This document describes how to configure origin server information for a playback domain in the CSS console.

## Limits
- Origin server configuration takes effect about one hour after configuration is complete.
- After configuring an origin server for a playback domain, you can no longer bind a push domain to the playback domain by specifying a `StreamName`. Nor can you configure watermarking, transcoding, recording, screenshot, or porn detection tasks for the playback domain. 

## Prerequisites
- You have logged in to the [CSS console](https://console.tencentcloud.com/live).
- You have built a live streaming origin server.
- You have added a **playback domain name**.

## Origin-Pull Configuration
You can edit a domain’s origin server information, including the basic information, protocol, and host in the console.
1. In the CSS console, select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of your playback domain or click **Manage** on the right.
2. Toggle on **Origin server mode** next to the domain name.
3. If the origin server mode is already enabled, you can modify its settings on this page.
![](https://qcloudimg.tencent-cloud.cn/raw/a5132b116946971febbefc1334c8fdaa.png)

## Configuration
### Origin server information
| Origin Server Information   | Description                                                         |
| ---------- | ------------------------------------------------------------ |
| Forwarding protocol   | RTMP, HTTP-FLV or HLS                          |
| HTTPS  | If the FLV or HLS protocol is used, you can enable HTTPS.<br>If you enable HTTPS, port 443 will be used. Post-redirection HTTPS is also supported. There are no port restrictions. |
| Primary origin server | The address of the primary origin server, which can be an IP address or domain. You can also configure a backup origin server. The addresses will be polled.          |
| Backup origin server | The address of the backup origin server (optional).                                         |

![](https://qcloudimg.tencent-cloud.cn/raw/0302a3257d93f247dd6ff9a70f779296.png)

### Host header
If the FLV or HLS protocol is used, you can configure an HTTP host header that specifies the exact domain that CSS accesses when pulling from the origin server.

#### Notes
The difference between an origin server address and a host header is as follows:
 - An origin server address is the IP address an origin-pull request is sent to.
 - A host header specifies the domain of the origin server address a request is sent to.

#### Configuration example
1. An origin server is configured for the playback domain `xx001.elementtest.org` as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/c5d4785c9d45d0bdda3b60ea23519a4c.png)
2. The process of pulling from the origin server would be as follows:
When the user accesses the resource by opening `http://xx001.elementtest.org/index.m3u8`, because the resource is not yet cached in Tencent Cloud, CSS will resolve the domain `test001.com` to get the server address of the origin server. Suppose it is `1.1.1.1`. CSS will access the `1.1.1.1` server, find the `index.m3u8` file in the web server `test002.com`, and then return the resource to the user.

### Remuxing
If the RTMP or HTTP-FLV protocol is used, you can enable HLS remuxing. Below are the formats of an RTMP, HTTP-FLV, and HLS address.
- RTMP: `rtmp://Playback domain/AppName/StreamName`
- FLV: `http://Playback domain/AppName/StreamName.flv`
- M3U8: `http://Playback domain/AppName/StreamName.m3u8`

#### Notes
- Number of HLS segments: Three by default. Value range: 3-10.
- HLS segment size: Three seconds by default. Value range: 3-10. The actual segments generated will not be smaller than the GOP size.

<img src="https://qcloudimg.tencent-cloud.cn/raw/5230d04d0b13d1ce0e83dae55cbfe8b7.png" width=600>

### HTTP configuration
If the HLS protocol is used, you can configure the following HTTP features in **More**.

| Item     | Description                                                         |
| ---------------- | ------------------------------------------------------------ |
| Redirection       | If you enable this, Tencent Cloud will not cache the 301 or 302 status code. When 301 or 302 is returned by the origin server, Tencent Cloud will automatically redirect until it obtains the requested resource (max 10 redirects) and return the resource to the user. No redirects are needed on the user end. <br>If you disable redirection, Tencent Cloud will return the 301 or 302 status code to the user end, which will redirect to get the resource.|
| Pass-through of origin server URL parameters  | By default, URL parameters are not passed through. If you enable this, Tencent Cloud parameters may be added to the URL. |
| HTTP request header pass-through | By default, HTTP request headers are not passed through. You can enable this to pass through the headers. Duplicate headers (case-insensitive) are not supported currently. |
| HTTP response header pass-through | By default, HTTP response headers are not passed through. You can enable this to pass through the headers. Duplicate headers (case-insensitive) are not supported currently. |

![](https://qcloudimg.tencent-cloud.cn/raw/4255b6cb743039ca7f38e8472ce0f87f.png)

### Cache configuration
If the HLS protocol is used, you can configure the resource cache time in **More**. After Tencent Cloud obtains the requested resource successfully from the origin server (status code 200), it will cache the index file and segments as configured.
<table id="setmess">
<tr><th width="14%">Item</th><th>Description</th>
</tr><tr>
<td>Index file cache time</td>
<td>The time to cache the index file when the origin server returns the 200 status code. The default cache time is 1,000 ms. The maximum time that can be set is 60,000 ms.
</ul></td>
</tr><tr>
<td>Segment cache time</td>
<td>The time to cache the TS/M4S/MP4 segments when the origin server returns the 200 status code. The default cache time is 1,000 ms. The maximum time that can be set is 60,000 ms.
</ul></td>
</tr><tr>
<td>Cache time by status code</td>
<td>When the origin server returns a non-200 status code, if it is unable to handle it immediately, and you don’t want to pass through all subsequent requests to the origin server, you can cache the status code and return it directly to the user. This can reduce the load on the origin server.
<br>Currently, the following status codes can be cached, regardless of the file type:
<li>4XX: 400, 403, 404, 405</li>
<li>5XX: 500, 503, 504</li>
</ul></td>
</tr></table>

![](https://qcloudimg.tencent-cloud.cn/raw/bce1ada7c00c5af0ec74bdd9a1bdd826.png)

### URL rewriting
If the HLS protocol is used, you can configure URL rewriting in **More**.
Tencent Cloud allows you to rewrite the actual URL CSS pulls from to a URL that better matches your origin server. Currently, you can only rewrite the URL path.

#### Notes
- **Original URL**: Requests are matched by prefix. For example, if you enter `/test01`, the rewriting rule will be applied to all requests under `/test01`. Regular expressions are not supported currently.
- **Target URL**: Requests are matched by prefix. For example, if you enter `/test01/test02`, all requests under `/test` will be rewritten to `/test01/test02`. Regular expressions are not supported currently.

![](https://qcloudimg.tencent-cloud.cn/raw/8251d53d1ef9a1ba170b161b730372f7.png)

#### Limits
- You can configure at most 10 rewriting rules for each playback domain.
- Spaces and the following special characters are not supported: < > " # { } | \ ^ ~ [ ] `
- You can re-arrange the rules to adjust their priorities. Rules at the top have higher priorities.

### Others
| Item     | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| Timeout     | The timeout period for establishing a TCP connection. The default time is 10,000 ms, and the value range is 2000-60000 (ms). Please set the timeout period according to your origin server conditions and network conditions. If the timeout period is too short, when a pull request fails due to network issues, CSS may switch origin servers too frequently. If the timeout period is too long, CSS may wait a long time before it tries a different origin server, causing playback failure at the client end.    |
| Retry attempts | The maximum number of retry attempts. If multiple origin server addresses have been configured, when a request fails, CSS will try a different address. |
| Timestamp correction   | This feature is available if the RTMP or FLV protocol is used. <Br>By default, timestamps are passed through. After you enable this, CSS will compare the current frame against the previous one. If the interval between the two exceeds 250 ms, CSS will add 10 ms to the timestamp of the previous frame and use the result as the timestamp of the current frame.  |

![](https://qcloudimg.tencent-cloud.cn/raw/040fe72429056474df265bdcb44560ee.png)

