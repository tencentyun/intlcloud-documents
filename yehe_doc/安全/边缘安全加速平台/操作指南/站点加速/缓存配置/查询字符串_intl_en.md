## Overview
You can adjust the query string in resource URLs to optimize the node cache and load requested resources more quickly.

#### How does the query string affect the node cache?
The query string is the string (containing one or multiple parameters separated with `&`) after `?` in the request URL, such as `color=blue&amp;size=large` in `https://www.example.com/images/example.jpg?color=blue&amp;size=large`.

When a node responds to a resource request, it will use the complete request URL as the cache key to match the cached resource. For example, even though the two request URLs of `https://www.example.com/images/example.jpg?time=1` and `https://www.example.com/images/example.jpg?time=2` have the same path, as they carry different query strings, the node will cache the `example.jpg` image twice and match two node caches for the requests respectively. If the resource is not on the node, the request will be forwarded for origin-pull, which increases the origin-pull traffic.

If `example.jpg` does not vary by query string parameters (that is, `example.jpg` will match the same image even if the `time` parameters are different), you can ignore the entire query string in the two request URLs to unify the requests to match the same node cache. For example, both `https://www.example.com/images/example.jpg?time=1` and `https://www.example.com/images/example.jpg?time=2` match the cached resource `https://www.example.com/images/example.jpg`.

Check the impact of the query string on resources in business resource URLs and use the **query string** feature to optimize the cache accordingly.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **Cache configuration** on the left sidebar.
2. On the cache configuration page, select the target site and click **Settings** in the query string module.
![](https://qcloudimg.tencent-cloud.cn/raw/a418b7dd7ce1cf87d60abf0c18292bbc.png)
3. In the query string pop-up window, select a mode and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/bd7347dc4a9e33445b27a6bfc84734cb.png)
Parameter description:
 - Retain all (default configuration): The complete query string will be retained, and once the query string changes, the request URL will be considered different.
>?In which cases are query strings considered different?
>- They have a different parameter value, such as `?sign=x;time=y` and `?sign=z;time=y`.
>- They have the same parameter values but their parameters are in different orders, such as `?sign=x;time=y` and `?time=y;sign=x`.
>- They have the same parameter values in different letter cases, such as `?sign=A` and `?sign=a`. If you want to identify them as the same query string, you can enable the [case ignoring](https://intl.cloud.tencent.com/document/product/1145/46181) feature.
 - Ignore all: The entire query string will be ignored.
 - Retain specified parameters: Only specified parameters in the query string will be retained.
    - You can specify only parameter names and separate them with semicolons, such as `param1;param2`.
    - You can enter up to ten parameters. 
 - Ignore specified parameters: Only specified parameters in the query string will be ignored.
    - You can specify only parameter names and separate them with semicolons, such as `param1;param2`.
    - You can enter up to ten parameters.

## Notes
1. This feature doesn't affect origin-pull request URLs and only changes the cache key of request on nodes. The origin-pull request URLs are the same as the URLs of original requests initiated by clients.
2. If different parameters in the query string in request URLs are separated with other characters rather than `&`, they cannot be identified normally.
