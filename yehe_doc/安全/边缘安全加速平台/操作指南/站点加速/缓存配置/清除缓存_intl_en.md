## Overview
Cache purge is to clear resources cached on nodes. After purge, when a user accesses a resource, the latest resource will be obtained through origin-pull for response.
>!After cache purge, as there is no cache of the resource on nodes, the resource can be obtained only through origin-pull, and the number of origin-pull requests will increase for a short period, which will compromise the acceleration effect. If many cached resources are purged, a large number of origin-pull requests will be generated, bringing pressure on the origin server.


## Use Cases
#### New resource release
When a resource is updated on the business origin server, you need to purge the old resource cached on nodes to prevent users from getting the old resource. After the cache is purged in the entire network, users can get the latest resource.

#### Non-compliant resource clearing
If there are non-compliant resources at your business site, you need to clear them and rectify your site promptly. As such resources may still be cached on nodes, you need to purge them from nodes.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **Cache configuration** on the left sidebar.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.
2. On the cache configuration page, select the target site and click **Purge cache** in the cache purge module.
![](https://qcloudimg.tencent-cloud.cn/raw/4488d444245ae27e789b8e62e1d56e37.png)
3. In the cache purge pop-up window, select a mode and target and content and click **OK**.	
![](https://qcloudimg.tencent-cloud.cn/raw/5ba36408f684f12e0131419535cab358.png)

Parameter description:
 - All cache: All cached resources of the site on nodes.
>! If a wildcard domain under the current site (example.com) such as `*.foo.example.com` is connected, this option cannot take effect, and you need to submit the cache purge task for each subdomain separately.
 - URL: Resources cached on nodes will be matched by URL.
 - Prefix: Resources cached on nodes will be matched by prefix path.
 - Hostname: Resources cached on nodes will be matched by hostname.

>! You cannot submit URLs in the format of `http://*.test.com/`; that is, domains cannot contain `*`. You need to specify the corresponding subdomains.


## Notes
### Content specifications
Check whether the submitted content meets the following specifications:
- Do not submit the content of a site that is disabled, locked, or not connected to the current account.
- If you choose file upload as the URL submission method, make sure that the file is in .txt format and doesn't exceed 10 MB in size.
- If the content contains non-ASCII characters, toggle **URL-encoding** on to convert the encoding.
>!
>- The encoding rules must comply with RFC 3986.
>- Spaces must be encoded to `%20` no matter where they are.
>- If encoding conversion is involved, only resources matched after encoding conversion will be purged.

### Submission limit
| Item | Maximum Quantity per Submission | Maximum Quantity per Day |
| -------- | ----------------- | ----------------- |
| All cache | -                 | 10,000            |
| Hostname | 1,000             | 10,000            |
| Prefix     | 1,000             | 10,000            |
| URL      | 10,000            | 200,000           |

>?If you select file upload as the URL submission method, there is no limit on the number of URLs that can be submitted each time, but the number of submitted URLs will be deducted from the daily quota.
