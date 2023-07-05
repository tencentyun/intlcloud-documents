## Overview

CDN is capable of configuring basic cache. Cache validity can be configured according to rules such as specified service types, directories, and specific URLs to regularly purge resources cached on nodes, pull the latest resources from the origin server, and cache them again.

In addition, CDN can purge cache for specified URLs or directories in batches:

- Purge URL: this deletes the cache of the corresponding resources on all CDN nodes.
- Purge directory: if you select **Purge updated resources**, when an end user accesses a resource under the corresponding directory, the `Last-Modify` information of the resource will be pulled from the origin server. If it is the same as that of the cached resource, the cached resource will be directly returned; otherwise, the updated resource will be pulled from the origin server and cached again. If you select **Purge all resources**, when the user accesses a resource under the corresponding directory, the latest version of the resource will be directly pulled from the origin server and cached again.

> ?After a purge is successfully executed, the corresponding resource on the node will not have a valid cache. When the user initiates an access request again, the node will pull the required resource from the origin server and cache it on the node. If you submit a large number of purge tasks, many caches will be cleared, resulting in a surge in origin-pull requests and high pressure on the origin server.

## Application Scenarios

### New resource releases

When a resource is overwritten by a new resource with the same name on the origin server, you can submit a request to purge the URL/directory and clear all caches so users can directly access the latest version of the resource. This will prevent users from accessing the legacy version of the resource cached on the node.

### Illegal resource cleanup

When illegal resources (such as resources related to pornography, drug, or gambling) are found on your origin server, they may still be accessible even after you delete them on the origin server because of node cache. To protect your network environment security, you can delete the cached resources through URL purge.

## Operation Guide



Log in to the [CDN console](https://console.cloud.tencent.com/cdn), click **Purge and Prefetch** on the left sidebar, and submit a **Purge URL** or **Purge Directory** task:
- CDN and ECDN URLs/directories can be purged together.
- Task can be submitted by direct input or TXT file upload.

![]()


### Content specifications
Check whether the submitted content meets the following specifications:
- URLs must contain a protocol identifier "http://" or "https://", such as `http://www.test.com/test.html`, and should be entered one per line.
- Do not submit a domain name that is disabled, locked, or not connected to the current account.
- If you submit tasks by file upload, make sure that the file is in .txt format and doesn't exceed 10 MB in size.
- URLs in the format of "http://*.test.com/" cannot be submitted. Even if you connect a wildcard domain name to CDN, you need to submit the corresponding subdomain names.
- Wildcards are not allowed in URLs to purge.
- For a URL with Chinese characters, enable "URL Encode" to encode the Chinese characters.

### Submission limit
- **URL purge:**
Up to 10,000 URLs can be purged per day for each account. For users who use CDN service outside the Chinese mainland, up to 10,000 global URLs can be purged per day, which is independent of the URL purge quota for the Chinese mainland.
	- Up to 1,000 URLs can be submitted at a time by direct input.
	- There is no limit on the number of URLs that are submitted by file upload, but the submissions will be deducted from your daily quota.
>? When you are running out of daily purge quota, you can increase it on your own in the Tencent Cloud CDN console.
>- The new quota will take effect immediately. The page will be refreshed automatically. You don’t need to click the refresh button frequently.
>- Each quota can only be increased once a day.
>- Each quota is increased independently for each region.
- **Directory purge:**
	Up to 100 directories can be purged per day for each account. For users who use CDN service outside the Chinese mainland, up to 100 global directories can be purged per day, which is independent of the directory purge quota for the Chinese mainland.
	- Up to 20 directories can be submitted at a time by direct input.
	- There is no limit on the number of URLs that are submitted by file upload, but the submissions will be deducted from your daily quota.
	

By default, URLs will be purged by acceleration regions of domain names in the URLs. If the domain names are accelerated globally, quotas for regions both in and outside the Chinese mainland will be consumed.
<span ID = "notes"></span>
To query your operation records, please see [History](https://intl.cloud.tencent.com/document/product/228/42176).


### Sub-user permissions configuration

 URL purge, directory purge, and purge history query have been integrated within the permission system which supports permission configuration at the resource (domain name) level. For more information, see [Console Permissions](https://intl.cloud.tencent.com/document/product/228/35229).


## Examples

### Directory purge - purge updated resources

The acceleration domain name is `purge-test-1251991073.file.myqcloud.com`, the origin server is Tencent Cloud Object Storage (COS), and resources on the origin server are as follows:
![]()

1. Initiate requests to access resources `1.txt` and `2.txt` respectively. Nodes to be hit can be determined based on `X-Cache-Lookup: Hit From Disktank3` and `Server: NWS_SPMid`, resources will be directly returned by the nodes:
   ![](https://main.qcloudimg.com/raw/9b307b80e7d1c759bb073eb9f2cf4b6c.png)
   ![](https://main.qcloudimg.com/raw/5fed8bff43d699f47235e5d0db1f2447.png)
2. On the origin server, replace `1.txt` with a file that has the same name, and the file’s last modified time changes, while `2.txt` stays the same:
   ![](https://main.qcloudimg.com/raw/798fd6a984813aa3a16eaf43856ff7c2.png)
   ![](https://main.qcloudimg.com/raw/bc0d40200fbc744ed34d8552a95c5671.png)
3. Initiate requests again. As the cache has not expired, the legacy content of the `1.txt` resource will be accessed:
![](https://qcloudimg.tencent-cloud.cn/raw/394a84d8f9974ed72cb629b11aac7206.png)
4. Submit a directory purge task, select **Purge updated resources**, and wait for the purge to complete:
   ![]()
5. After the purge is complete, because `Last-Modified` of `1.txt` has been changed, the request will be forwarded to the origin server. As `2.txt` has not been changed, even after a directory purge task is submitted, it will still be hit and returned:
   ![](https://main.qcloudimg.com/raw/0ea8c1e0e7caac970b3875d4b3987687.png)
   ![](https://main.qcloudimg.com/raw/84e599b1c9c655e62497fb4bdc8e7918.png)
