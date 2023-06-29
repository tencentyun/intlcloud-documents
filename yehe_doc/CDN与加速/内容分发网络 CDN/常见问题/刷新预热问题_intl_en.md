[](id:q6)
### When do I need to purge and prefetch?
- Purge: To ensure that users access to the latest resources when there are resources to update, restricted resources to remove, or domain name configurations to change on your origin server, you can submit a purge task, which can prevent user access to old resources or old configurations from the node cache. For more details, see [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299).
- Prefetch: For operating activities, installation packages or upgrade packages to release, you can submit a prefetch task to prefetch static resources to CDN acceleration nodes, which will reduce strain on the origin server and improve the service availability and user experience. For more details, see [Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000).

[](id:q1)
### What are the differences between purge and prefetch?
- Once a resource is purged, its cache on all CDN nodes across the entire network will be deleted. When a user request arrives at a node, the node will pull the corresponding resource from the origin server, return it to the user, and cache it to the node to ensure that the user can obtain the latest resource.
- When a resource is prefetched, it will be cached in advance to all CDN nodes across the entire network. When a user request arrives at a node, the resource can be directly obtained on the node.

[](id:q2)
### What are limits for purge and prefetch? How long do they take to take effect?
- Purge Cache
 - URL purge: a maximum of 10,000 URLs can be purged each day and a maximum of 1,000 URLs can be submitted for each purge. It takes about 5 minutes for the purge to take effect. If the cache validity period configured for the file is less than 5 minutes, we recommend you wait for the timeout and update instead of using the purge tool.
 - Directory purge: a maximum of 100 directories can be purged each day and a maximum of 500 URL directories can be submitted for each purge. It takes about 5 minutes for the purge to take effect. If the cache validity period configured for the folder is less than 5 minutes, we recommend you wait for the timeout and update instead of using the purge tool.
- Prefetch Resource
 - URL prefetch: A maximum of 1,000 URLs can be prefetched each day, and a maximum of 500 URLs can be submitted for each prefetch task. It takes about 5 to 30 minutes for the prefetch to take effect, depending on the file size.

[](id:q3)
### If the resource changes on the origin server, will the cache on CDN cache nodes be updated in real time?
No. The cache on CDN cache nodes will not be updated in real time.
- If the resource changes on the origin server and the cache is still valid, CDN cache nodes will not perform origin-pull to update the cache, and thus the resource on the origin server is different from the cache. In this case, you can specify a proper [cache validity period](https://intl.cloud.tencent.com/document/product/228/35317) in the console.
- If the cache validity period is too short, CDN will frequently pull the content from the origin server and more traffic will be consumed on the origin server. If it is too long, the cache will be updated slowly.
- If you need to update the cache of a resource, you can [purge the cache](https://intl.cloud.tencent.com/document/product/228/6299), and then perform [prefetch](https://intl.cloud.tencent.com/document/product/228/39000) so that CDN pulls the latest resource from the origin server. You can also send a request to CDN for the latest resource.



[](id:q5)
### How do I view the purge and prefetch history?
You can check the purge and prefetch history in the CDN console. For more information, see [History](https://intl.cloud.tencent.com/document/product/228/42176).

[](id:q6)
### Can I prefetch with custom request headers?
No. 


### How do I increase the daily quota limit for purge and prefetch?
After checking your quota usage at [Quota Management](https://intl.cloud.tencent.com/document/product/228/46738) in the CDN console, you can request a temporary or permanent quota as needed. The following quota types are supported: URL purge quota, directory purge quota, and URL prefetch quota.
- Temporary quota is a quota that can be applied on a temporary basis and used within a validity period. When it expires, the quota type will end up as permanent.
- Permanent quota is a quota that can be used for an indefinite period. As the permanent quota application takes a long time to process, we recommend requesting a temporary quota to meet your needs.


### What should I pay attention to when prefetching?
When you prefetch the file whose cache is still valid, CDN will not perform origin-pull to update the file. We recommend you purge the cache before submitting a prefetch task.
- During prefetching, CDN will pull the required content from the origin server. If you submit a large batch of prefetch tasks, the bandwidth usage of the origin server will greatly increase. Therefore, a proper number of prefetch tasks is suggested.
- CDN provides a dual acceleration structure of edge and middle-layer nodes. If resources are prefetched in the Chinese mainland, they are prefetched to middle-layer nodes in the Chinese mainland, while for those prefetched outside the Chinese mainland, they are prefetched to edge nodes outside the Chinese mainland. Note that traffic incurred when resources are prefetched to edge nodes will be billed.
