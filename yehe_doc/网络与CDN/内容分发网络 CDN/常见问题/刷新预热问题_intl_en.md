[](id:q6)
### When do I need to use the features of purge and prefetch?
- Purge: to ensure that your users are always served with fresh resources and the domain name configuration is always up to date, you can submit a purge task. For more information, see [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299).
- Prefetch: schedules a prefetch task for marketing activities or launching of installation/upgrade packages, so as to cache static resources to CDN cache node in advance to reduce pressure of original server, improve service availability and user experience. For more information, see [Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000).

[](id:q1)
### What are differences between purge and prefetch?
- Once a resource is purged, its cache on all CDN nodes across the entire network will be deleted. When a user request arrives at a node, the node will pull the corresponding resource from the origin server, return it to the user, and cache it to the node to ensure that the user can obtain the latest resource.
- When a resource is prefetched, it will be cached in advance to all CDN nodes across the entire network. When a user request arrives at a node, the resource can be directly obtained on the node.

[](id:q2)
### What are requirements for purge and prefetch? How long do they take to take effect?
- Purge Cache
	- URL purge: a maximum of 10,000 URLs can be purged each day and a maximum of 1,000 URLs can be submitted for each purge. It takes about 5 minutes for the purge to take effect. If the cache validity period configured for the file is less than 5 minutes, we recommend you wait for the timeout and update instead of using the purge tool.
	- Directory purge: a maximum of 100 directories can be purged each day and a maximum of 20 URL directories can be submitted for each purge. It takes about 5 minutes for the purge to take effect. If the cache validity period configured for the folder is less than 5 minutes, we recommend you wait for the timeout and update instead of using the purge tool.
- Prefetch Resource
	- URL prefetch: A maximum of 1,000 URLs can be prefetched each day, and a maximum of 20 URLs can be submitted for each prefetch task. It takes about 5 to 30 minutes for the prefetch to take effect, depending on the file size.

[](id:q3)
### Will the cached content on CDN cache nodes be updated in real time?
No. The cached content on CDN cache nodes are updated based on the [Cache Expiration Configuration](https://intl.cloud.tencent.com/document/product/228/38424) you configured in the console. If you need to update a file's cache in real time, use [Cache Purge](https://intl.cloud.tencent.com/document/product/228/6299).



[](id:q5)
### How do I view the purge and prefetch history?
You can check the purge and prefetch history in the CDN console. For more information, see [History](https://intl.cloud.tencent.com/document/product/228/42176).

[](id:q6)
### Can I bring a custom request header to prefetch?
Not supported.

