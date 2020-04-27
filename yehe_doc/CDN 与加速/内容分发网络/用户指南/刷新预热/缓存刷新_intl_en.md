## Feature Overview
CDN is capable of configuring basic cache. Cache expiration time can be configured according to rules such as specified service types, directories, and specific URLs to regularly purge resources cached on nodes, pull latest resources from the origin server and cache them again.

In addition, CDN can purge cache for specified URLs or directories in batches:
- Purge URL: this deletes the cache of the corresponding resources on all CDN nodes.
- Purge directory: if you select **Purge updated resources**, when an end user accesses a resource under the corresponding directory, the `Last-Modify` information of the resource will be obtained from origin-pull. If it is the same as that of the currently cached resource, the cached resource will be directly returned; otherwise, the updated resource will be pulled from the origin server and cached again. If you select **Purge all resources**, when the user accesses a resource under the corresponding directory, the latest version of the resource will be directly pulled from the origin server and cached again.

>After a purge is successfully executed, the corresponding resource on the node will not have a valid cache. When the user initiates an access request again, the node will pull the required resource from the origin server and cache it on the node. If you submit a large number of purge tasks, many caches will be cleared, resulting in a surge in origin-pull requests and high pressure on the origin server.

## Use Cases
### New resource release
When a resource is overwritten by a new resource with the same name on the origin server, you can submit a request to purge the URL/directory and clear all caches so users can directly access the latest version of the resource. This will prevent users from accessing the legacy version of the resource cached on the node.

### Illegal resource cleanup
When illegal resources (such as resources related to pornography, drug, or gambling) are found on your origin server, they may still be accessible even after you delete them on the origin server because of node cache. To protect your network environment security, you can delete the cached resources through URL purge.

## Operation Guide
### How to use
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Purge and Prefetch** on the left sidebar, and submit a **Purge URL** or **Purge Directory** task:
![](https://main.qcloudimg.com/raw/a3442259ffa50bccb60dabf002ea6dfb.png)
![](https://main.qcloudimg.com/raw/d4b01354bab726ea890e8167ccdbaffe.png)
<span ID = "notes"></span>
In the **History** tab, you can query tasks by specified time period, term, and purge task type. Term queries only support querying a domain name or a complete purged URL/directory:
![](https://main.qcloudimg.com/raw/86e00c9652a635cf0a0007172119be92.png)

> The console can return up to 10,000 operation records at a time, which can be exported to Excel. If you have a high number of purge tasks, please query and export them in batches.

### Precautions

**URL purge:**
- Up to 10,000 URLs can be purged per day for each account, and up to 1,000 URLs can be submitted for purge at a time. For overseas CDN users, up to 10,000 global URLs can be purged per day. This quota is independent of the Mainland China URL purge quota.
- You need to add the `http://` or `https://` protocol identifier when submitting a purge task.
- URLs in the format of `http://*.test.com/` cannot be purged. Even if you connect a wildcard domain name to CDN, you need to submit the corresponding sub-domain names for purge.
- When submitting URLs for purge, domain names should have already been connected to CDN; otherwise, the submission will fail.
- URLs containing Chinese characters cannot be purged.
- By default, URLs will be purged by acceleration regions of domain names in the URLs.

**Directory Purge:**
- Up to 100 directories can be purged per day per account, and up to 20 directories can be submitted for purge at a time. For overseas CDN users, up to 100 global directories can be purged per day. This quota is independent of the Mainland China directory purge quota. 
- You need to add the `http://` or `https://` protocol identifier when submitting a purge task.
- Directories in the format of `http://*.test.com/` cannot be purged. Therefore, even if you connect a wildcard domain name to CDN, you need to submit the corresponding sub-domain names for purge.
- When submitting URLs for purge, domain names should have already been connected to CDN; otherwise, the submission will fail.
- URL directories containing Chinese characters cannot be purged.

**Sub-user permissions configuration:**
- Directory purge, URL purge, and purge history query have been integrated to the latest permission system and support permission configuration at the resource (domain name) level.
- For learn how to grant permissions, please see [Console Permissions](https://intl.cloud.tencent.com/document/product/228/35229).

## Use Cases

### Directory purge - purge updated resources
The acceleration domain name is purge-test-1251991073.file.myqcloud.com, the origin server is Tencent Cloud Object Storage (COS), and resources on the origin server are as follows:
![](https://main.qcloudimg.com/raw/ed694acc98a8d3114c8a9922f7374a1b.png)

1. Initiate requests to access resources `1.txt` and `2.txt` respectively. Nodes to be hit can be determined based on X-Cache-Lookup: Hit From Distank3 and Server: NWS_SPMid, resources will be directly returned by the nodes:
![](https://main.qcloudimg.com/raw/8e5e1d55743f83340b6801942011a951.jpg)
![](https://main.qcloudimg.com/raw/dc50a49f1177c0a671c0f10f874b0a0b.jpg)
2. On the origin server, replace `1.txt` with a file that has the same name, and the file’s last modified time changes, while `2.txt` stays the same:
![](https://main.qcloudimg.com/raw/798fd6a984813aa3a16eaf43856ff7c2.png)
![](https://main.qcloudimg.com/raw/bc0d40200fbc744ed34d8552a95c5671.png)
3. Initiate requests again. As the cache has not expired, the legacy content of the `1.txt` resource will be accessed:
![](https://main.qcloudimg.com/raw/f08fcfe681ff6684ef9ebf96d7a7b5ab.jpg)
4. Submit a directory purge task, select **Purge updated resources**, and wait for the purge to complete:
![](https://main.qcloudimg.com/raw/31346a963f189187852dde17a4bf0309.png)
5. After the purge is completed, because `Last-Modified` of `1.txt` has been changed, the request will be forwarded to the origin server. As `2.txt` has not been changed, even after a directory purge task is submitted, it will still be a cache hit and returned:
![](https://main.qcloudimg.com/raw/d1e83b5357fc878d6f1df56f0f1cd84b.jpg)
![](https://main.qcloudimg.com/raw/29e68b2f6207731a689e9c11ee1bf849.jpg)

