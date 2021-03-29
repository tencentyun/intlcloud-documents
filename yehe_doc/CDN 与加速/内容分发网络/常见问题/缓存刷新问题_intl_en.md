[](id:q1)

### What is cache purge?
Cache purge includes URL purge, directory purge, and URL prefetch. For more information, please see [Cache Purge](https://intl.cloud.tencent.com/document/product/228/6299).
- URL purge means to purge the cache on a file-by-file basis.
- Directory purge means to purge all files under a directory on a file-by-file basis.
- URL prefetch means to prefetch resources on a file-by-file basis.

Purge vs. Prefetch:
- Once a resource is purged, its cache on all CDN nodes across the entire network will be deleted. When a user request arrives at a node, the node will pull the corresponding resource from the origin server, return it to the user, and cache it to the node to ensure that the user can obtain the latest resource.
- When a resource is prefetched, it will be cached in advance to all CDN nodes across the entire network. When a user request arrives at a node, the resource can be directly obtained on the node.

[](id:q2)
### What are the requirements for cache purge? How long does it take effect?
Cache purge includes URL purge, directory purge, and URL prefetch.
- URL purge: a maximum of 10,000 URLs can be purged each day and a maximum of 1,000 URLs can be submitted for each purge. It takes about 5 minutes for the purge to take effect. If the cache validity period configured for the file is less than 5 minutes, we recommend you wait for the timeout and update instead of using the purge tool.
- Directory purge: a maximum of 100 directories can be purged each day and a maximum of 20 URL directories can be submitted for each purge. It takes about 5 minutes for the purge to take effect. If the cache validity period configured for the folder is less than 5 minutes, we recommend you wait for the timeout and update instead of using the purge tool.
- URL prefetch: If the resource has already been cached to the node and has not expired, it will not be updated to the latest one. If you need to update the resources on all CDN nodes to the latest ones, you can purge them before prefetch. A maximum of 1,000 URLs can be prefetched each day and a maximum of 20 URLs are allowed to be submitted for each prefetch. It takes about 5 to 30 minutes for the prefetch to take effect, depending on the file size.

[](id:q3)
### Will the cached content on CDN cache nodes be updated in real time?
No. The cached content on CDN cache nodes are updated based on the [Cache Expiration Configuration](https://intl.cloud.tencent.com/document/product/228/35317) you configured in the console. If you need to update a file's cache in real time, use [Cache Purge](https://intl.cloud.tencent.com/document/product/228/6299).

[](id:q4)
### Does CDN support directory purge?
Yes. CDN supports URL purge, directory purge, and URL prefetch.
Method 1: You can perform directory purge in the [CDN console](https://console.cloud.tencent.com/cdn/refresh). For more information, please see [Cache Purge](https://intl.cloud.tencent.com/document/product/228/6299).
Method 2: Purge URL by calling the [PurgePathCache](https://intl.cloud.tencent.com/document/product/228/33602) API.

[](id:q5)
### How do I view the purge cache history?
You can check the purge cache history in the CDN Console. For more information, please see the **Operation Guide** in [Cache Purge](https://intl.cloud.tencent.com/document/product/228/6299#notes).

