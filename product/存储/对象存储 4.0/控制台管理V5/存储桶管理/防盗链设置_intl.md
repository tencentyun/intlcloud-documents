## Overview
Tencent Cloud COS provides hotlink protection support for users to avoid unnecessary losses caused by malicious programs' cheating for public network traffic using resource URLs or stealing of resources by malicious means. It is recommended that you configure the blacklist/whitelist in Hotlink Protection Settings in the console for security protection.

## Procedure
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and then select the **Bucket List** in the left pane to go to the Bucket List page. Click the bucket (such as examplebucket-1250000000) for which you want to set hotlink protection to enter the bucket.
![](https://main.qcloudimg.com/raw/b373ba0eba6a1723236fce8e4a945c64.png)
2. Click **Basic Configuration**, find Hotlink Protection Settings, and click **Edit**.
![](https://main.qcloudimg.com/raw/97dceabb6297080878dfd871f143af79.png)
3. Modify the current status to Enabled, select a list type (blacklist or whitelist), enter applicable domain names, and then click **Save**.
![](https://main.qcloudimg.com/raw/619a86e9eb8b1f4fc9741abcebd915d8.png)

>?
>- After enabling Hotlink Protection, you must enter applicable domain names.
>- Blacklist: Domain names on this list are not allowed to access the default access address of the bucket. 403 is returned if any domain name on the list accesses such address.
>- Whitelist: Only domain names on this list are allowed to access the default access address of the bucket. 403 is returned if any domain name not on the list accesses such address.
>- In HTTP requests, the header referer can be left empty. (An HTTP request header without the field of referer is allowed or the referer field is empty.)
>- A maximum of 10 addresses including domain names and IPs are supported. Wildcard (*) in addresses is allowed and domain names with the same prefix are also subject to the list. One address per line.
  Examples (The following examples are for reference only):
  If `www.example.com` is specified, `www.example.com/123`, `www.example.com.cn`, and other addresses with the prefix of `www.example.com` will also be included in the list;
  Domain names and IPs with ports are supported, such as `www.example.com:8080` and `10.10.10.10:8080`.
  If ` * .example.com` is specified, such addresses as `a.b.example.com/123` and `a.example.com` are also included.
>- If accelerated access is implemented via CDN domain name, CDN hotlink protection rules will be executed before COS hotlink protection rules.


## Example
A user with the APPID of 1250000000 creates a bucket named examplebucket-1250000000 and places an image picture.jpg in the root directory, and COS generates the following default access address according to the rules:
```shell
examplebucket-1250000000.file.myqcloud.com/picture.jpg
```
User A owns a website:
```shell
www.example.com
```
and embeds the image into the homepage index.html.

Webmaster B manages a website:
```shell
www.fake.com
```
and wants to put this image on `www.fake.com'. But he doesn't want to pay for traffic costs. He directly links picture.jpg through the following address and places it into the homepage index.html on `www.fake.com`.
```shell
examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

To avoid losses of User A in such cases, we provide the following two methods to enable hotlink protection.

#### Method 1

Configure the **blacklist** by entering the domain name `*.fake.com`, and save.

#### Method 2

Configure the **whitelist** by entering the domain name `*.example.com`, and save.

#### Before enabled

The image is displayed normally when `http://www.example.com/index.html` is accessed.
The image is also displayed normally when `http://www.fake.com/index.html` is accessed.

#### After enabled

The image is displayed normally when `http://www.example.com/index.html` is accessed.
The image cannot be displayed when `http://www.fake.com/index.html` is accessed.
