## Overview

If the object you request doesn't exist in the bucket, or a specific request needs to be redirected, you can configure origin-pull rules in the COS console to access corresponding data via COS. Origin-pull configurations are mainly used for migrating hot data and redirecting specific requests.

>?
>- The success rate of data origin-pull depends on your network environment.
>- Buckets in finance zones don't support origin-pull configurations.
>

<img src="https://main.qcloudimg.com/raw/f63a74cf70a9f6582e52e13a2b16e72a.png" width="90%">


## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the target bucket to enter the bucket details page.
4. Select **Basic Configurations** > **Origin-Pull** on the left and click **Add Rule**.
![](https://main.qcloudimg.com/raw/69fc0f3042e59c3e9c2667d06aa068fa.png)
5. In the pop-up window, configure the following information and click **Next**:

 - **Origin-Pull Mode**: Select an origin-pull mode as needed.
    - **Async Origin-Pull**: If the requested file doesn't exist in COS, COS will search for it on the specified origin and upload it to the bucket without returning it to the client.
    - **Sync Origin-Pull**: If the requested file doesn't exist in COS, COS will search for it on the specified origin, return it to the client, and upload it to the bucket.
    - **Redirect**: If a specified error is reported when accessing the bucket, COS will return the redirection address to the client but will not save the file from the origin. The client can request the resource from the origin at the redirection address.
 - **Origin-Pull Condition**: Specify all conditions that must be met at the same time for triggering origin-pull.
    - **HTTP Status Code 404**: If you select **Async Origin-Pull** or **Sync Origin-Pull**, this parameter is required and cannot be canceled, and origin-pull will be triggered when the HTTP status code is 404. If you select **Redirect**, you can enter an HTTP status code ranging from 400 to 599.
    - **File name prefix**: When the requested file matches the prefix, the origin-pull rule will be triggered. For example, if you set this option to `prefix`, when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg` and the returned HTTP status code is 404, the origin-pull rule will be triggered.
 - **Origin-Pull Protocol**: Select the protocol used by COS to access the specified origin. Options include **Force HTTPS**, **Force HTTP**, and **Follow request protocol**.
    - If you select **Force HTTPS** or **Force HTTP**, COS will access the origin over HTTPS or HTTP respectively.
    - If you select **Follow request protocol**, COS will access the origin over the protocol used in the request.
 - **Request Parameter**: Specify whether to pass through the `queryString` request parameter carried when accessing COS to the origin.
 - **Passthrough specifies the request header**: Specify the request headers you want to pass through to the origin. If you select **Redirect** as the origin-pull mode, do not set this parameter.
 - **New request header**: You can add additional request headers to be carried during origin-pull. If you select **Redirect** as the origin-pull mode, do not set this parameter.
6. Configure the following information based on the selected origin-pull mode and click **Next**:

<dx-tabs>
::: Async origin-pull

 - **Origin-Pull Address**: Enter the domain name or IP address without the `http://` or `https://` prefix. You can also add the port number at the end.
Examples of correct addresses:
```shell
abc.example.com
abc.example.com:8080
202.96.128.86
202.96.128.86:8080
```
 - **Standby forwarding address**: You can enter a domain name or IP address as configured below:
    - **Fixed file**: Specify a fixed file to which all requests are redirected when the origin-pull rule is triggered.
    - **Specified prefix**: Specify the prefix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the prefix is specified as `test`, and the origin-pull rule is triggered when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`, then the request will be redirected to `<origin-pull address>/test/prefix123.jpg`.
    - **Specified suffix**: Specify the suffix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the suffix is specified as `.jpg`, and the origin-pull rule is triggered when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`, then the request will be redirected to `<origin-pull address>/prefix123.jpg`.

  <b>Note：</b>
      - If you select **Fixed file**, other fields cannot be used.
      - **Specified prefix** and **Specified suffix** can be used at the same time.
 
 - **3xx Following Policy**: If this policy is enabled, when your origin returns a 3xx redirect status code, COS will follow it to pull data from another origin.
:::
::: Sync origin-pull

 - **Origin-Pull Address**: Enter the domain name or IP address without the `http://` or `https://` prefix. You can also add the port number at the end.
Examples of correct addresses:
```shell
abc.example.com
abc.example.com:8080
202.96.128.86
202.96.128.86:8080
```
 - **Standby forwarding address**: You can enter a domain name or IP address as configured below:
    - **Fixed file**: Specify a fixed file to which all requests are redirected when the origin-pull rule is triggered.
    - **Specified prefix**: Specify the prefix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the prefix is specified as `test`, and the origin-pull rule is triggered when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`, then the request will be redirected to `<origin-pull address>/test/prefix123.jpg`.
    - **Specified suffix**: Specify the suffix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the suffix is specified as `.jpg`, and the origin-pull rule is triggered when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`, then the request will be redirected to `<origin-pull address>/prefix123.jpg`.

  <b>Note：</b>
      - If you select **Fixed file**, other fields cannot be used.
      - **Specified prefix** and **Specified suffix** can be used at the same time.
 
 - **3xx Following Policy**: If this policy is enabled, when your origin returns a 3xx redirect status code, COS will follow it to pull data from another origin.
 - **Packet of origin site**: After this feature is enabled, the packet from the origin will be directly returned, including the status code and other information.
:::
::: Redirect

 - **Origin-Pull Address**: Enter the domain name or IP address without the `http://` or `https://` prefix. You can also add the port number at the end.
Examples of correct addresses:
```shell
abc.example.com
abc.example.com:8080
202.96.128.86
202.96.128.86:8080
```
 - **Standby forwarding address**: You can enter a domain name or IP address as configured below:
    - **Fixed file**: Specify a fixed file to which all requests are redirected when the origin-pull rule is triggered.
    - **Specified prefix**: Specify the prefix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the prefix is specified as `test`, and the origin-pull rule is triggered when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`, then the request will be redirected to `<origin-pull address>/test/prefix123.jpg`.
    - **Specified suffix**: Specify the suffix for the file to which a request is redirected when the origin-pull rule is triggered. For example, if the suffix is specified as `.jpg`, and the origin-pull rule is triggered when you access `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`, then the request will be redirected to `<origin-pull address>/prefix123.jpg`.

  <b>Note：</b>
      - If you select **Fixed file**, other fields cannot be used.
      - **Specified prefix** and **Specified suffix** can be used at the same time.

 - **Redirect Code**: You can select 301 (default value), 302, or 307.
:::
</dx-tabs>

7. Confirm that the configured origin-pull rule is correct and click **OK**.
By default, COS always uses the most recent rule first for origin-pull. To change the rule priority manually, click the edit icon in the **Priority** column in the rule list.
![](https://main.qcloudimg.com/raw/3fa148b2e43f30fb891adee75ff255db.png)


## Samples

**Background**
A user with APPID 1250000000 created a bucket named `examplebucket-1250000000` and enabled the CDN acceleration domain name:

```shell
examplebucket-1250000000.file.myqcloud.com
```

Set the origin-pull address of the bucket to:

```shell
abc.example.com
```

Store the image `picture.jpg` on the origin `http://abc.example.com`.

**First access by client (with sync origin-pull not enabled)**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

When COS finds that the object cannot be hit, it will return the HTTP status code 302 to the client and redirect to the following address:

```shell
http://abc.example.com/picture.jpg
```

**First access by client (with sync origin-pull enabled)**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

When COS finds that the object cannot be hit, it will return the HTTP status code 200 to the client and redirect to the following address:

```shell
http://abc.example.com/picture.jpg
```

The origin then provides the object to the client to ensure normal access, and COS copies `picture.jpg` from the origin and saves it to the root directory of the bucket `example`.

**Second-time access**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

COS directly hits the `picture.jpg` object in the root directory and returns it to the client.

