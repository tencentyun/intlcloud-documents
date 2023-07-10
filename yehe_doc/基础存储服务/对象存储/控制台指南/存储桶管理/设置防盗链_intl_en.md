## Overview

Tencent Cloud COS provides hotlink protection to help users avoid unnecessary losses caused by malicious programs' stealing public network traffic using resource URLs or stealing resources. We recommend that you configure the blocklist/allowlist in Hotlink Protection Settings on the console to ensure security protection.

>! 
> - If a signature is carried in the access URL or headers, hotlink protection−based verification will not be performed.
>- When configuring hotlink protection, you can add your domain to the allowlist for the multipart upload request of large files.
> 

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). Click **Bucket List** on the left sidebar to open the **Bucket List** page.
2. Locate the bucket for which you want to set hotlink protection, and click its name to enter the bucket management page.
3. Click **Security Management** > **Hotlink Protection**, find the hotlink protection configuration item, and click **Edit**.
4. Switch the status to **Enable**, select a list type (blocklist or allowlist), enter the applicable domain names, and then click **Save**. The configuration items are described as follows:
![](https://main.qcloudimg.com/raw/6a02d7abf3ec8630ca9a89959554e2cd.png)
 > **Blocklist**: domain names on this list are **not allowed** to access the default access address of the bucket. 403 is returned if any domain name on the list accesses such address.
 - **Allowlist**: domain names on this list **are allowed** to access the default access address of the bucket. 403 is returned if any domain name not on the list accesses such address.
 - **Empty referer**: For an HTTP request, the header referer can be left empty (i.e., the HTTP request header has no referer field or the referer field is empty).
 - **Referer**: Enter up to 30 domain names or IP addresses (one per line). The wildcard `*` is supported, such as `*.test.com`. Examples are as follows:
    - If `www.example.com` is specified, `www.example.com/123`, `www.example.com.cn`, and other addresses with the prefix of `www.example.com` will also be included in the list.
    - Domain names and IPs with ports are supported, such as `www.example.com:8080` and `10.10.10.10:8080`.
    - If `*.example.com` is specified, addresses such as `a.b.example.com/123` and `a.example.com` are also included.
		
>? If accelerated access is implemented via a CDN endpoint domain name, CDN hotlink protection rules will be executed before COS hotlink protection rules.
>


## Example

A user with the APPID of 1250000000 creates a bucket named examplebucket-1250000000 and places an image picture.jpg in the root directory. COS has generated the following default access address according to the rules:

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

and wants to put this image on `www.fake.com`. But he doesn't want to pay for traffic costs. He creates a direct link to picture.jpg through the following address and places it into the homepage index.html on `www.fake.com`.

```plaintext
examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

In such cases, to avoid losses for User A, we provide the following two methods of enabling hotlink protection.

#### Method 1

Configure the **blacklist** by entering the domain name `*.fake.com`, and save.

#### Method 2

The **allowlist** method: Add `*.example.com` to the allowlist and save.

#### Before enabling hotlink protection

The image is displayed normally when `http://www.example.com/index.html` is accessed.
The image is also displayed normally when `http://www.fake.com/index.html` is accessed.

#### After enabling hotlink protection

The image is displayed normally when `http://www.example.com/index.html` is accessed.
The image cannot be displayed when `http://www.fake.com/index.html` is accessed.

## Notes for Mini Program

1. For network requests using Weixin Mini Programs, the referer value is fixed as `https://servicewechat.com/{appid}/{version}/page-frame.html`.
2. If hotlink protection is enabled for your bucket, to allow Weixin Mini Programs to load COS images, add `servicewechat.com` to your hotlink allowlist in the [COS console](https://console.cloud.tencent.com/cos5).

