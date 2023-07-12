## Overview

COS allows you to configure hotlink protection for your bucket. You can set a blocklist and allowlist for access sources to prevent resource hotlinking. This document describes how to configure hotlink protection for a bucket.

## How Does Hotlink Protection Work

Hotlink protection works by checking the Referer address in the request header:

- Referer is a part of the header. When a browser sends a request to a web server, it usually carries a Referer to tell the server which page the request comes from, so that the server can decide to deny or allow the access to resources.
- If you open the file link `https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg` directly in a browser, the request header will not have a Referer.

For example, in the figure below, the image `1.jpg` is embedded in `https://127.0.0.1/test/test.html`, and a Referer pointing to the access origin will be carried when you access `https://127.0.0.1/test/test.html`:
![](https://main.qcloudimg.com/raw/ed5d4f915132b236eb9423d81881ffd4.jpg)

<span id="fenxi"></span>
## Hotlink Protection Case Study

User A uploaded the image resource `1.jpg` to COS, and the accessible link to the image is `https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg`.
- User A embedded the image in their webpage `https://example.com/index.html` and the image is accessible.
- User B saw the image on user A's webpage and decided to embed it in their own webpage `https://b.com/test/test.html`, and user B's webpage can also display the image properly.
In the above case, user A's image resource `1.jpg` was hotlinked by user B. User A doesn't know that their resource in COS is being used by user B's webpage and suffers from losses caused by extra traffic fees. 


## Solution

In the above [Hotlink Protection Case Study](#fenxi), user A can prevent user B from hotlinking their image by setting hotlink protection in the following way:
1. Set a hotlink protection rule for the bucket "examplebucket-1250000000". There are two options for preventing user B from hotlinking:
 - Option 1: configure a blacklist by entering the domain name `*.b.com`, and save it.
 - Option 2: configure a whitelist, enter `*.example.com` for the domain name, and save.
2. After hotlink protection is enabled:
 - The image can be displayed properly when `https://example.com/index.html` is accessed.
 - The image cannot be displayed when `https://b.com/test/test.html` is accessed, as shown below:
![](https://main.qcloudimg.com/raw/3374bd47b5cf2eff04d15cd6d1590aae.jpg)

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Select the bucket for which to configure hotlink protection and enter it.
![](https://main.qcloudimg.com/raw/66a106d2fd78632b65914f2fb6c096dc.png)
3. Click **Security Management** > **Hotlink Protection** on the left.
4. In the **Hotlink Protection** area, click **Edit**.
![](https://main.qcloudimg.com/raw/d726521ea58a99cfb3cf42dfae776f05.png)
5. Enable hotlink protection and configure the list type and domain name. Here, select Option 2 as detailed below:
 - **Type**: blocklist or allowlist
    - **Blocklist**: It prohibits domain names in the list to access the default access address of the bucket. If a domain name **in the list** accesses the default access address of the bucket, a 403 error will be returned.
    - **Allowlist**: It prohibits domain names not in the list to access the default access address of the bucket. If a domain name **not in the list** accesses the default access address of the bucket, a 403 error will be returned.
 - **Referer** : Up to 10 domain names can be set and they will be matched by a prefix. Domain names, IPs, and asterisk `*` are supported formats (one address per line). Below are configuration rule description and examples:
    - Domain names and IPs with a specific port are supported, such as `example.com:8080` and `10.10.10.10:8080`.
    - If `example.com` is configured, addresses prefixed with `example.com` can be hit, such as `example.com/123`.
    - If `example.com` is configured, addresses prefixed with `https://example.com` and `http://example.com` can be hit.
    - If `example.com` is configured, the domain name with a specific port can also be hit, such as `example.com:8080`. 
    - If `example.com:8080` is configured, the domain name `example.com` cannot be hit.
    - If `*.example.com` is configured, its second-level and third-level domain names can be restricted, such as `example.com`, `b.example.com`, and `a.b.example.com`.
>! After hotlink protection is **enabled**, the corresponding domain names must be entered.
6. After completing the configuration, click **Save**.
![](https://main.qcloudimg.com/raw/ab894ac9faf520c07454d87eb10c2b37.png)

## FAQs
For questions about hotlink protection, see the [Data Security](https://intl.cloud.tencent.com/document/product/436/40946) section in COS FAQs.
