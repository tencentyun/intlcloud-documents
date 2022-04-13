## Overview
URL prefetch caches the resource at the matched URL from the origin server to a node in advance, so that users' resource requests can be responded to directly on the node. This enhances the acceleration effect and mitigates the pressure on the origin server.
>!
>- During resource prefetch, a request will be simulated to pull the corresponding resource from the origin server. If there are many submitted prefetch tasks, a large number of origin-pull requests will be generated, increasing the origin server bandwidth usage.
>- If a prefetched resource conflicts with a resource cached on the node (that is, the node already cached a resource with the same name that hasn't expired), the cached resource will remain effective and won't be overwritten by the prefetched resource. If the cached resource changes, you can purge the corresponding node cache before prefetch.
>- Resources are prefetched to edge nodes by default, and traffic generated at the edge layer is billed as normal traffic.



## Use Cases
#### Installation package release
Before formally releasing the installation or upgrade package of a new version, you can prefetch the installation package resources to nodes. After formal release, when users request to download the package, they can directly get it from the nodes, which speeds up download and alleviates the pressure on the origin server.

#### Operational event
Before holding an operational event formally, you can prefetch static resources including webpages and images used on event webpages to nodes. After the event formally starts, static resources requested by users will be directly returned by nodes to accelerate the page access and improve the user experience.
## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **Cache configuration** on the left sidebar.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

2. On the cache configuration page, select the target site and click **Prefetch resource** in the URL prefetch module.
![](https://qcloudimg.tencent-cloud.cn/raw/3ae33206ff4be6b287f5216cf24f6e5b.png)
3. In the URL prefetch pop-up window, enter or upload URLs and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/5820581c8c397618adb4402d51caabe1.png)

## Notes
### Content specifications
Check whether the submitted content meets the following specifications:
- Do not submit the content of a site that is disabled, locked, or not connected to the current account.
- You cannot submit URLs in the format of `http://*.test.com/`; that is, domains cannot contain `*`. You need to specify the corresponding subdomains.
- If you choose file upload as the URL submission method, make sure that the file is in .txt format and doesn't exceed 10 MB in size.
- If the content contains non-ASCII characters, toggle **URL-encoding** on to convert the encoding.

>!
>- The encoding rules must comply with RFC 3986.
>- Spaces must be encoded to `%20` no matter where they are.
>- If encoding conversion is involved, only resources matched after encoding conversion will be prefetched.

### Submission limit
| Item | Maximum Quantity per Submission | Maximum Quantity per Day |
| -------- | ----------------- | ----------------- |
| URL      | 10,000            | 200,000           |

>? If you select file upload as the URL submission method, there is no limit on the number of URLs that can be submitted each time, but the number of submitted URLs will be deducted from the daily quota.
