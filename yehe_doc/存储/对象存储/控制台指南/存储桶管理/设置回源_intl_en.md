## Overview

You can configure an origin-pull rule for your bucket through the COS Console. This rule allows you to pull data from another origin for COS to access if the object you request does not exist in your bucket, or a specific request needs to be redirected. The use cases include migrating hot data, redirecting specific requests, and any other scenario you see fit.

>? The origin-pull success rate depends on your network environment.

<img src="https://main.qcloudimg.com/raw/f63a74cf70a9f6582e52e13a2b16e72a.png" width="90%">


## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the Bucket List page. Click the bucket for which you want to configure origin-pull to enter the bucket details page.
2. Go to **Basic Configurations** > **Origin-pull Configurations**, and click **Add origin-pull rule**.
![](https://main.qcloudimg.com/raw/69fc0f3042e59c3e9c2667d06aa068fa.png)
3. Configure the following and click **OK**.
 - **Origin-pull condition**: specifies all conditions as needed that must be met at the same time for triggering origin-pull.
    - **HTTP Status Code 404**: the only HTTP status code that triggers origin-pull currently. This field is required and cannot be canceled manually.
    - **File name prefix**: triggers the origin-pull rule when the requested file name matches this prefix. For example, if this field is set to `prefix`, then the origin-pull is triggered when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg` and an HTTP status code 404 is returned.
 - **Origin-Pull Protocol**: the protocol used for COS to access the specified origin server. The options include `Follow request protocol`, `Force HTTPS`, and `Force HTTP`.
    - If you select “Force HTTPS/HTTP”, COS will access your origin server using HTTPS/HTTP protocol.
    - If you select “Follow request protocol”, COS will access your origin server using the protocol that you used for your request.
 - **Origin-pull Address**: allows only a domain name or IP address without the `http://` or `https` prefix. You can optionally append a port number to the address.
   An example correct address:

```shell
abc.example.com
abc.example.com:8080
202.96.128.86
202.96.128.86:8080
```

You can configure a specific origin-pull address using the following fields:

   - **Fixed file**: specifies a fixed file to which all requests are redirected when the origin-pull rule is triggered.
   - **Specified prefix**: specifies the prefix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the prefix is specified as `test`, the request is redirected to the `<origin-pull address>/test/prefix123.jpg` when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`, and the origin-pull rule is triggered.
   - **Specified suffix**: specifies the suffix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the suffix is specified as `.jpg`, the request is redirected to the `<origin-pull address>/prefix123.jpg` when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`, and the origin-pull rule is triggered.
     >!
     >- If you select “Fixed file”, the other fields cannot be used by default.
     >- “Specified prefix” and “Specified suffix” can be used at the same time.
 
 - **Sync back-to-source**: once enabled, COS will not return 3XX status code when pulling data from an origin server. This option is currently only available for buckets in Beijing, Shanghai, Singapore, and Mumbai regions.    
 - **3xx Following Policy**: if this policy is enabled, when your origin server returns a 3XX redirect, COS will follow it by default to another origin server to pull data from.
 - **Origin-Pull Parameter**: specifies whether to pass through COS request parameters when accessing the origin server.
 - **Origin-pull header**: specifies the custom headers that you can add for COS to access your origin server. Currently, up to 10 of them can be added. 
   ![](https://main.qcloudimg.com/raw/0049d66f20bd79f4edb673cb8c8c7185.png)
   
4. By default, COS always gives the highest priority to the most recent rule, by which it performs origin-pull. To change the priority manually, you can click the “Edit” icon under the “Priority” column in the rule list.
![](https://main.qcloudimg.com/raw/3fa148b2e43f30fb891adee75ff255db.png)


## Examples

**Background**
A user whose APPID is 1250000000 created a bucket named "examplebucket-1250000000", and enabled CDN acceleration domain name:

```shell
examplebucket-1250000000.file.myqcloud.com
```

The origin-pull address for the bucket was set to:

```shell
abc.example.com
```

The image `picture.jpg` was stored at the origin server `http://abc.example.com`.

**First access by the client**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

When COS finds that the object cannot be hit, it returns HTTP status code `302` and redirects the user to the following address:

```shell
http://abc.example.com/picture.jpg
```

Now, the object is provided by the origin server for access. Meanwhile, COS copies this `picture.jpg` from the origin server to the root directory of the bucket `example`.

**Second access**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

COS directly hits the `picture.jpg` object in the root directory and returns it to the client.
