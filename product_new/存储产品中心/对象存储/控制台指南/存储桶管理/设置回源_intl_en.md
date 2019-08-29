## Overview
You can set origin-pull rules for buckets through the COS Console. When the object you requested does not exist in the bucket, or a specific request needs to be redirected, you can set the origin-pull rules to access corresponding data from COS. Origin-pull settings are mainly used for live migration of data and redirection of specific requests. You can set them as needed.

The success rate of origin-pull data depends on the network environment.

![](https://main.qcloudimg.com/raw/f63a74cf70a9f6582e52e13a2b16e72a.png)
## Procedure
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), select **Bucket List** from the left sidebar to go to the Bucket List page. Click the bucket for which you want to set the origin-pull.

![](https://main.qcloudimg.com/raw/3797a80a4d8ec0d49d64754530f8fe4d.png)

2. Click **Basic Configuration** to locate the origin-pull settings, change the status to **Enabled**, enter the origin server address, and click **Save**. The configuration items are as follows:
 **Origin server address**: Only enter the domain name or IP address without `http://` or `https` (not supported). You can also add the port number after the domain name or IP address.
Example of a correct address:

```shell
abc.example.com
abc.example.com:8080
10.10.10.10
10.10.10.10:8080
```


## Example
**Background**
A user with APPID of 1250000000 created a bucket named "examplebucket-1250000000", and enabled the CDN accelerated domain name:

```shell
examplebucket-1250000000.file.myqcloud.com
```

​	Set the origin server address for the bucket to:
```shell
abc.example.com
```
Store the image picture.jpg at the origin server `http://abc.example.com`.

**The first access from the client**:
```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```
When COS finds that the object cannot be hit, it returns the HTTP status code 302 to the client and is redirected to the following address:
```shell
http://abc.example.com/picture.jpg
```
Then the origin server provides the object to the client to ensure the access, and COS copies picture.jpg from the origin server and saves it to the root directory of the bucket "example".

**The second access**:
```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```
COS directly hits the object picture.jpg in the root directory and returns it to the client.
