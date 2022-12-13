## Overview
URL pre-warming caches the resource at the matched URL from the origin server to a node in advance, so that users' resource requests can be responded to directly on the node. This enhances the acceleration effect and mitigates the pressure on the origin server.
>!
>- During resource pre-warming, a request will be simulated to pull the corresponding resource from the origin server. If there are many submitted pre-warming tasks, a large number of origin-pull requests will be generated, increasing the origin server bandwidth usage.
>- If a pre-warmed resource conflicts with a resource cached on the node (that is, the node already cached a resource with the same name that hasn't expired), the cached resource will remain effective and won't be overwritten by the pre-warmed resource. If the cached resource changes, you can purge the corresponding node cache before pre-warming.
>- Resources are pre-warmed to edge nodes by default, and traffic generated at the edge layer is billed as normal traffic.



## Use Cases
#### Installation package release
Before formally releasing the installation or upgrade package of a new version, you can pre-warm the installation package resources to nodes. After formal release, when users request to download the package, they can directly get it from the nodes, which speeds up download and alleviates the pressure on the origin server.

#### Operational event
Before holding an operational event formally, you can pre-warm static resources including webpages and images used on event webpages to nodes. After the event formally starts, static resources requested by users will be directly returned by nodes to accelerate the page access and improve the user experience.
## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site Acceleration** > **Cache configuration** on the left sidebar.
2. On the **Cache configuration** page, select the target site and click **Pre-warm resource** in the **Pre-warm URL** module.
![](https://qcloudimg.tencent-cloud.cn/raw/3ae33206ff4be6b287f5216cf24f6e5b.png)
3. In the pop-up window, enter or upload URLs and click **OK**.
4. Click **View history** to view the history in a specified time period.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9Wg7988_QQ20221116-120324%402x.png)

## Notes
### Content specifications
Check whether the submitted content meets the following specifications:
- Do not submit the content of a site that is disabled, locked, or not connected to the current account.
- You cannot submit URLs in the format of `http://*.test.com/`; that is, domains cannot contain `*`. You need to specify the corresponding subdomains.
- If you submit tasks by file upload, make sure that the file is in .txt format and doesn't exceed 10 MB in size.
- If the content contains non-ASCII characters, toggle **URL-encoding** on to convert the encoding.
 - The encoding rules must comply with RFC 3986.
 - Spaces must be encoded to `%20` no matter where they are.
 - If encoding conversion is involved, only resources matched after encoding conversion will be pre-warmed.

### Submission limit
- Different plans have different quotas. For billing details, see [Billing Overview](https://www.tencentcloud.com/document/product/1145/48705).
- If you select file upload as the URL submission method, there is no limit on the number of URLs that can be submitted each time, but the number of submitted URLs will be deducted from the daily quota.
