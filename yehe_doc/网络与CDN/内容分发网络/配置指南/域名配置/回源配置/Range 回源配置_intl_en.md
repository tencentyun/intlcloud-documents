## Configuration Overview
Tencent Cloud CDN divides a file into several shards to improve storage efficiency when caching resources. It also supports Range requests. For example, if a request carries HTTP header `Range: bytes = 0-999`, the first 1000 bytes of the file will be returned to the user.

After Range GETs is enabled, if a partial file requested by a user has expired, CDN will perform Range GETs to pull and cache the required partial file and return it to the user. After Range GETs is disabled, even if a user only requests a partial file, CDN will pull the entire file and then cache it before returning the requested partial file to the user.

Enabling Range GETs can greatly increase the delivery efficiency of large files, reduce the response time and the pressure on the origin server.

> ?
> - After Range GETs is enabled, resources will be cached in shards on the nodes. These shards have the same cache validity period and follow the cache validity rule defined by the user.
> - To enable the Range GETs configuration, please make sure that the origin server supports Range requests, or origin-pull may fail.

## Configuration Guide

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page. Open the **Origin-pull Configuration** tab to see the **Range GETs Configuration** section.

It is disabled by default. If the domain name is with a COS origin, the configuration is enabled by default. You can enable and disable it as needed.
![](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)



## Configuration Samples
If the Range GETs configuration of the domain name `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)
User A makes a request for the resource `http://cloud.tencent.com/test.apk`. After the node receives the request and finds that the cached file `test.apk` has already expired, it will initiate a Range GETs request to get and cache the resource by shards. If user B also makes a Range request at this time and the shards stored on the node match the specified byte segments in the Range request, the resource will be directly returned to user B even though the shards are not completely obtained.

