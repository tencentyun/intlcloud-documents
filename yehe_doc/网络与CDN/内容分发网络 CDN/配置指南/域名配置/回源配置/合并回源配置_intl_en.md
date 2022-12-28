
Origin-pull merging can help increase the cache hit rate, so as to lower the load pressure during peak hours like big online promotion events.

## Description
When multiple users request for the same resource that is not cached on the cache node, all requests are forward to the origin, leading to soaring bandwidth and connections. A slow or failed origin response that could affect access experience may even occur if the origin server reaches the performance limit.
When origin-pull merge is enabled, only one request is forwarded to the origin to retrieve the requested resource. Other similar requests are hold till the resource is ready on the cache node.
The following figure shows how this feature works. Three requests are sent to the same cache node requesting for the same resource. The first request is forwarded to the origin. The resource is then returned to the requester and cached on the cache node. Now, other awaiting requests can get the resource from the cache.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e448eeed5a105cec5d2cb77cf646f5a7.png" width="80%">

## Limits
1. It only supports response status code 200, 206 and 304.
2. Unsupported caching headers: "cache-control: no-cache", "no-store", "private" and "pragma: no-cache".
3. Unsupported data transfer methods: Chunked transfer encoding.
4. Supported HTTP request methods: GET.
5. "content-length" and "transfer-encoding" must be present in the HTTP response header.
6. Unsupported compression methods: Gzip and Brotli.

## Configuration
1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn).
2. Click **Domain Management** on the left sidebar to enter the domain name management list.
3. Select the target domain name and click **Manage** to enter the domain name configuration page.
4. Click the **Origin-pull Configuration** tab and find **Origin-pull merge**.
![]()
5. Origin-pull merge is disabled by default. You can enable it as needed.

## Configuration Sample
The following configuration sample shows how to enable origin-pull merge.
![]()



