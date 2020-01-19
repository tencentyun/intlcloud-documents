>
>- CDN supports Range GETs configuration, where Range is the HTTP request header used for the request of a specified part of a file. For example, `Range: bytes = 0-999` can be used to request the first 1,000 bytes of a file. Enabling Range GETs configuration can increase the delivery efficiency and response speed of large files.
>- The origin server needs to support Range requests, or origin-pull will fail.
>-  When Range GETs configuration is enabled, resources will be cached in segments on the node, and these segments have the same cache expiration time and follow user-defined cache expiration rule.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page. Find the desired domain name and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/550d0afcc410204314cbeb443644529a.png)
2. Click **Origin Configuration** and you will see the **Range GETs Configuration** module. The feature is enabled by default.
 ![img](https://main.qcloudimg.com/raw/d4a9d9fb15b14f1bef7b79f5c56c45c4.png)

## Sample Case
- If the Range GETs configuration of the `www.test.com` domain name is as follows:
![img](https://main.qcloudimg.com/raw/98a3484bd477caa749311c13bfc26984.png)
When user A makes a request for the `http://www.test.com/test.apk` resource, after the node receives the request and finds that the cached `test.apk` file has already expired, it will initiate a Range GETs request to obtain and cache the resource by segments; if user B also makes a Range request at this time and the segments stored on the node match the specified byte segments in the Range request, the resource will be directly returned to the user without having to wait until all segments are obtained.
- If the Range GETs configuration of the `www.test.com` domain name is as follows:
![img](https://main.qcloudimg.com/raw/5b97ad9950896ef43f60e04f41db2f52.png)
  When user A makes a request for the `http://www.test.com/test.apk` resource, after the node receives the request and finds that the cached `test.apk` file has already expired, it will initiate an origin-pull request to directly obtain the entire resource from the origin server and then return it to the user.
