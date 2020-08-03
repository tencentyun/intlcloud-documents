## Overview
Tencent Cloud COS provides hotlink protection support for users to avoid unnecessary losses caused by malicious programs' cheating for public network traffic using resource URLs or stealing of resources by malicious means. It is recommended that you configure the blocklist/allowlist in Hotlink Protection Settings in the console for security protection.

>Hotlink protection-based verification is not required for object access requests with signed URL or headers.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Locate the bucket for which you want to set hotlink protection, and click its name to enter the bucket.
![](https://main.qcloudimg.com/raw/4f30dc2b51d5f1e549b485f7ef004213.png)
3. Click **Basic Configuration**, find **Hotlink Protection**, and click **Edit** to edit it.
![](https://main.qcloudimg.com/raw/235d3158684e32b4b92daf0e81bd6db6.png)
3. Switch “Status” to Enabled, select a list type (blocklist or allowlist), enter applicable domain names, and then click **Save**. The configuration items are described as follows:
 > **Blocklist**: **domain names on this list** are not allowed to access the default access address of the bucket. 403 is returned if any domain name on the list accesses such address.
 - **Allowlist**: **only domain names on this list** are allowed to access the default access address of the bucket. 403 is returned if any domain name not on the list accesses such address.
 - **Empty referer**: in HTTP requests, the header referer can be left empty. (An HTTP request header without the field of referer is allowed or the referer field is empty.)
 - **Referer**: you can enter up to 10 domain names matched by prefix, with a domain name per line. Supported address formats include domain name, IP address and the wildcard `*`, with examples as shown below:
    - If `www.example.com` is specified, `www.example.com/123`, `www.example.com.cn`, and other addresses with the prefix of `www.example.com` will also be included in the list.
    - Domain names and IPs with ports are supported, such as `www.example.com:8080` and `10.10.10.10:8080`.
    - If `*.example.com` is specified, such addresses as `a.b.example.com/123` and `a.example.com` are also included.
![](https://main.qcloudimg.com/raw/6a02d7abf3ec8630ca9a89959554e2cd.png)

>If accelerated access is implemented via CDN domain name, CDN hotlink protection rules will be executed before COS hotlink protection rules.


## Samples
A user with the APPID of 1250000000 creates a bucket named examplebucket-1250000000 and places an image picture.jpg in the root directory, and COS generates the following default access address according to the rules:
```plaintext
examplebucket-1250000000.file.myqcloud.com/picture.jpg
```
User A owns a website:
```plaintext
www.example.com
```
and embeds the image into the homepage index.html.

Webmaster B manages a website:
```plaintext
www.fake.com
```
and wants to put this image on `www.fake.com'. But he doesn't want to pay for traffic costs. He creates a direct link to picture.jpg through the following address and places it into the homepage index.html on `www.fake.com`.
```plaintext
examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

To avoid losses of User A in such cases, we provide the following two methods to enable hotlink protection.

#### Method 1

Configure the **blocklist** by entering the domain name `*.fake.com`, and save.

#### Method 2

Configure the **allowlist** by entering the domain name `*.example.com`, and save.

#### Before enabled

The image is displayed normally when `http://www.example.com/index.html` is accessed.
The image is also displayed normally when `http://www.fake.com/index.html` is accessed.

#### After enabled

The image is displayed normally when `http://www.example.com/index.html` is accessed.
The image cannot be displayed when `http://www.fake.com/index.html` is accessed.

## About WeChat Mini Programs

1. For network requests using Wechat Mini Program, the referer value is fixed as `https://servicewechat.com/{appid}/{version}/page-frame.html`.
2. If hotlink protection is enabled for your bucket, to allow Wechat Mini Program to load COS images, add `servicewechat.com` to your hotlink allowlist in the [COS console](https://console.cloud.tencent.com/cos5).
