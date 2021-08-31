## Configuration Scenario

If the letter case of resource URL paths is irrelevant to the resource content in your business, you can enable "Ignore Cache Letter Case" to improve the hit rate.

## Configuration Guide

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Cache Configuration** tab, find the **Ignore Cache Letter Case**, which is disabled by default.
![](https://main.qcloudimg.com/raw/01f93aaa70c523ae0bb1ab5debae8558.png)

## Configuration Samples

When a CDN node caches resources, it will create indexes in `Key-Value` format. Here, the `Key` is the cache key (`Cache Key`) of the CDN node. In addition to configuring "Ignore Query String", you can also configure "Ignore Cache Letter Case" for optimization.
If the acceleration domain name is `cloud.tencent.com` and the user access conditions are as follows:

- User A accesses the resource `http://cloud.tencent.com/abc.JPG`.
- User B accesses the resource `http://cloud.tencent.com/abc.jpg`.
  

Suppose both user A and user B access the CDN node X, which does not cache the above two resources. By default, "Ignore Cache Letter Case" is disabled, and the access process will be as follows:
- For user A's access request, the image `http://cloud.tencent.com/abc.JPG` will be obtained from the origin server and cached on CDN node X, and its corresponding cache key will be `http://cloud.tencent.com/abc.JPG`.
- For user B's access request, the image `http://cloud.tencent.com/abc.jpg` will be obtained from the origin server and cached on CDN node X, and its corresponding cache key will be `http://cloud.tencent.com/abc.jpg`.
  

After "Ignore Cache Letter Case" is enabled, the access process in the scenario above will be as follows:
- For user A's access request, the image `http://cloud.tencent.com/abc.JPG` will be obtained from the origin server and cached on CDN node X, and its corresponding cache key will be `http://cloud.tencent.com/abc.jpg`.
- User B's access request will hit the corresponding resource on CDN node X and directly get the requested content.
