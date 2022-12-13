## Overview
When origin-pull is requested, the redirect will be based on the 302/301 status code of the origin server, and you can specify the maximum number of redirects (which is 3 by default and can be 1–5).

## Use cases
Nodes do not cache 301/302 status codes by default. When an origin server returns a 301/302 request, the node will return the response to the client by default, and the client will be redirected to the corresponding resource for access.

You can enable redirect following during origin-pull. Then, when the 301/302 status code is returned, the request will be automatically redirected (for up to the maximum number of times that is set). If the requested resource is obtained, the node will return it to the client, which no longer needs to be redirected.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the **Rule engine** page, select the target site and configure the redirect following rule during origin-pull as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).

## Sample configuration
If the host `www.example.com` is configured with the redirect following rule during origin-pull as follows:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XZI8315_QQ20221116-121052.png)
Then, if user A requests a resource `http://www.example.com/a` not cached on the node, the node will request it from the origin server. If the HTTP response status code returned by the origin server is 302, and the redirect address is `http://www.example.com/b`, then:
<dx-steps>

1. The node sends a request to the `http://www.example.com/b` redirect address.
2. If the requested resource is obtained within three redirects, see 3; otherwise, see 4.
3. The resource is cached on the node and sent to user A. At this time, user B also sends a request for `http://www.example.com/a`, which will be directly hit on the node and returned to user B.
4. The 301/302 status code is returned to the user, and the client is redirected once more.
   </dx-steps>

