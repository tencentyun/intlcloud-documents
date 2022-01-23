## Overview

You can configure origin-pull rules for buckets in the COS console. If the object you request does not exist in the bucket, or a specific request needs to be redirected, you can configure origin-pull rules to access corresponding data via COS. Origin-pull configurations are mainly used for hot data migration, redirecting specific requests, and other relevant scenarios.

>?
> - The success rate of data origin-pull depends on your network environment.
>

<img src="https://main.qcloudimg.com/raw/f63a74cf70a9f6582e52e13a2b16e72a.png" width="90%">


## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket for which you want to set origin-pull.
4. Select **Basic Configurations** > **Origin-Pull** on the left, and click **Add Rule**.
![](https://main.qcloudimg.com/raw/69fc0f3042e59c3e9c2667d06aa068fa.png)
5. In the pop-up window, configure the following information and click **Next**:

 - **Origin-Pull Condition**: specify all conditions that must be met at the same time for triggering origin-pull.
    - **HTTP Status Code 404**: the only HTTP status code that triggers origin-pull currently. This option must be selected and cannot be cleared.
    - **File name prefix**: triggers the origin-pull rule when the requested file name matches this prefix. For example, if this field is set to `prefix`, origin-pull is triggered when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg` and an HTTP status code 404 is returned.
 - **Origin-Pull Protocol**: the protocol used by COS to access the specified origin server. The options include `Force HTTPS`, `Force HTTP`, and `Follow request protocol`.
    - If you select `Force HTTPS` or `Force HTTP`, COS will access the origin server using HTTPS or HTTP respectively.
    - If you select `Follow request protocol`, COS will access the origin server with the protocol used in the request.
 - **Request Parameter**: specify whether to pass through the queryString request parameters carried when accessing COS to the origin server.
 - **Request Header to Pass Through**: specify the request headers you want to pass through to the origin server.
 - **New Request Header**: add the additional request headers to carry when COS accesses the origin server.
6. Configure the following information and click **Next**:

 - **Origin-Pull Address**: Enter the domain name or IP address without the `http://` or `https` prefix. You can also add the port number after the domain name or IP address.

Example of a correct address:
```shell
abc.example.com
abc.example.com:8080
202.96.128.86
202.96.128.86:8080
```

You can configure a specific origin-pull address using the following fields:
 - **Fixed file**: specifies a fixed file to which all requests are redirected when the origin-pull rule is triggered.
 - **Specified prefix**: specifies the prefix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the prefix is specified as `test`, the request is redirected to `<origin-pull address>/test/prefix123. jpg` when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`, and the origin-pull rule is triggered.
 - **Specified suffix**: specifies the suffix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the suffix is specified as `.jpg`, the request is redirected to `<origin-pull address>/prefix123.jpg` when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`, and the origin-pull rule is triggered.

>!
> - If you select `Fixed file`, the other fields cannot be used.
> - `Specified prefix` and `Specified suffix` can be used at the same time.

 - **Standby Forwarding Address**: When this feature is enabled, you can add a backup origin server. When the primary origin server returns an error code such as 5xx, COS will access the backup origin server.
 - **Sync Origin-Pull**: When this feature is enabled, COS will not return 3xx status code when pulling data from an origin server. This option is currently available only for buckets in Beijing, Shanghai, Singapore, and Mumbai regions.
 - **3xx Following Policy**: If this policy is enabled, when your origin server returns a 3xx redirect, COS will follow it to pull data from another origin server.

7. Confirm that the configured origin-pull rule is correct and click **OK**.
By default, COS always gives the highest priority to the most recent rule, by which it performs origin-pull. To change the priority manually, you can click the “Edit” icon under the “Priority” column in the rule list.
![](https://main.qcloudimg.com/raw/3fa148b2e43f30fb891adee75ff255db.png)


## Example

**Background**
A user whose APPID is 1250000000 created a bucket named "examplebucket-1250000000", and enabled CDN acceleration endpoint domain name:

```shell
examplebucket-1250000000.file.myqcloud.com
```

Configure the origin-pull address of the bucket to be:

```shell
abc.example.com
```

Store the image picture.jpg at the origin server `http://abc.example.com`.

**First access by client (without sync origin-pull enabled)**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

When COS finds that the object cannot be hit, it returns HTTP status code `302` to the client and is redirected to the following address:

```shell
http://abc.example.com/picture.jpg
```

**First access by client (with sync origin-pull enabled)**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

When COS finds that the object cannot be hit, it returns the HTTP status code 200 to the client and is redirected to the following address:

```shell
http://abc.example.com/picture.jpg
```

The origin server then provides the object to the client to ensure access, and COS copies picture.jpg from the origin server and saves it to the root directory of the bucket "example".

**Second-time access**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

COS directly hits the picture.jpg object in the root directory and returns it to the client.
