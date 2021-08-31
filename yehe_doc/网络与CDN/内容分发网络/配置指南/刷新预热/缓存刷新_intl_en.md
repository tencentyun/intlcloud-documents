## Feature Overview

CDN is capable of configuring basic cache. Cache validity can be configured according to rules such as specified service types, directories, and specific URLs to regularly purge resources cached on nodes, pull the latest resources from the origin server, and cache them again.

In addition, CDN can purge cache for specified URLs or directories in batches:

- Purge URL: this deletes the cache of the corresponding resources on all CDN nodes.
- Purge directory: if you select **Purge updated resources**, when an end user accesses a resource under the corresponding directory, the `Last-Modify` information of the resource will be pulled from the origin server. If it is the same as that of the cached resource, the cached resource will be directly returned; otherwise, the updated resource will be pulled from the origin server and cached again. If you select **Purge all resources**, when the user accesses a resource under the corresponding directory, the latest version of the resource will be directly pulled from the origin server and cached again.

>? After a purge is successfully executed, the corresponding resource on the node will not have a valid cache. When the user initiates an access request again, the node will pull the required resource from the origin server and cache it on the node. If you submit a large number of purge tasks, many caches will be cleared, resulting in a surge in origin-pull requests and high pressure on the origin server.

## Use Cases

### New resource releases

When a resource is overwritten by a new resource with the same name on the origin server, you can submit a request to purge the URL/directory and clear all caches so users can directly access the latest version of the resource. This will prevent users from accessing the legacy version of the resource cached on the node.

### Illegal resource cleanup

When illegal resources (such as resources related to pornography, drug, or gambling) are found on your origin server, they may still be accessible even after you delete them on the origin server because of node cache. To protect your network environment security, you can delete the cached resources through URL purge.

## Directions

### How to use

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Purge and Prefetch** on the left sidebar, and submit a **Purge URL** or **Purge Directory** task. You can purge CDN and ECDN URLs/directories together.
![](https://main.qcloudimg.com/raw/a3442259ffa50bccb60dabf002ea6dfb.png)
![](https://main.qcloudimg.com/raw/d4b01354bab726ea890e8167ccdbaffe.png)
>? If the URL encode feature is enabled, Chinese characters will be converted to URL encoded format during URL and directory purge.

<span ID = "notes"></span>
In the **History** tab, you can query tasks by specified time period, keyword, and task type. Keyword queries only support querying with a domain name or a complete purged URL/directory:
![](https://main.qcloudimg.com/raw/86e00c9652a635cf0a0007172119be92.png)

>? The console can return up to 10,000 logs at a time, which can be exported to an Excel file. If you have more than 10,000 purge tasks, please query and export them in batches.

### Precautions

**URL purge:**

- Up to 10,000 URLs can be purged per day for each account with the acceleration service within or outside the Chinese mainland, and up to 1,000 URLs can be purged at a time. For each account using the global CDN service, the daily URL purge quota for acceleration service within and outside the Chinese mainland is 10,000 each.
>?	
>- When you are running out of daily purge quota, you can increase it on your own in the Tencent Cloud CDN console.
>- The new quota will take effect immediately. The page will be refreshed automatically. You don’t need to click the refresh button frequently.
>- The quota can only be increased once a day. 
>- The quota increase in different regions is independent of each other.
- You need to add the "http://" or "https://" protocol identifier when submitting a purge task.
- URLs in the format of "http://*.test.com/" are not supported. Even if you connect a wildcard domain name to CDN, you need to submit the corresponding subdomain names for purge.
- When you submit URLs for purge, domain names should have already been connected to CDN; otherwise, the submission will fail.
- By default, URLs will be purged by acceleration regions of domain names in the URLs.

**Directory purge:**

- The upper limit for purged directories is 100 per account per day. The limit is set for the acceleration service within and outside the Chinese mainland separately. Up to 20 directories can be purged at a time. 
- You need to add the "http://" or "https://" protocol identifier when submitting a purge task.
- Directories in the format of "http://*.test.com/" cannot be purged. Even if you connect a wildcard domain name to CDN, you need to submit the corresponding subdomain names for purge.
- When you submit URLs for purge, domain names should have already been connected to CDN; otherwise, the submission will fail.

**Sub-user permissions configuration:**

- Directory purge, URL purge, and purge history query have been integrated to the latest permission system and support permission configuration at the resource (domain name) level.
- For permission assignment method, please see [Console Permissions](https://intl.cloud.tencent.com/document/product/228/35229).

## Use Cases

### Directory purge - purge updated resources

The acceleration domain name is `purge-test-1251991073.file.myqcloud.com`, the origin server is Tencent Cloud Object Storage (COS), and resources on the origin server are as follows:
![](https://main.qcloudimg.com/raw/ed694acc98a8d3114c8a9922f7374a1b.png)

1. Initiate requests to access resources `1.txt` and `2.txt` respectively. Nodes to be hit can be determined based on `X-Cache-Lookup: Hit From Disktank3` and `Server: NWS_SPMid`, resources will be directly returned by the nodes:
   ![](https://main.qcloudimg.com/raw/9b307b80e7d1c759bb073eb9f2cf4b6c.png)
   ![](https://main.qcloudimg.com/raw/5fed8bff43d699f47235e5d0db1f2447.png)
2. On the origin server, replace `1.txt` with a file that has the same name, and the file’s last modified time changes, while `2.txt` stays the same:
   ![](https://main.qcloudimg.com/raw/798fd6a984813aa3a16eaf43856ff7c2.png)
   ![](https://main.qcloudimg.com/raw/bc0d40200fbc744ed34d8552a95c5671.png)
3. Initiate requests again. As the cache has not expired, the legacy content of the `1.txt` resource will be accessed:
   ![](https://main.qcloudimg.com/raw/b5769a3d7fddaeadfda229115ac59bb8.png)
4. Submit a directory purge task, select **Purge updated resources**, and wait for the purge to complete:
   ![](https://main.qcloudimg.com/raw/31346a963f189187852dde17a4bf0309.png)
5. After the purge is complete, because `Last-Modified` of `1.txt` has been changed, the request will be forwarded to the origin server. As `2.txt` has not been changed, even after a directory purge task is submitted, it will still be hit and returned:
   ![](https://main.qcloudimg.com/raw/0ea8c1e0e7caac970b3875d4b3987687.png)
   ![](https://main.qcloudimg.com/raw/84e599b1c9c655e62497fb4bdc8e7918.png)
