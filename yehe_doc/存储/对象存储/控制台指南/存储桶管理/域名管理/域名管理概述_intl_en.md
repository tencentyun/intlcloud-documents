## Overview

After an object is uploaded to the bucket, COS will automatically generate a URL (i.e., default domain name) for you to access this object directly. To use CDN or your domain name to access COS objects, you can bind your domain or CDN to the bucket where the objects are stored.

You can set a domain name to access objects as needed. To accelerate access using CDN, you can access using the URL generated with the CDN acceleration domain name.

## Description

You can quickly download and deliver objects in a bucket by managing the following domain names:

- Default domain name: COS origin domain name, which is automatically generated based on the bucket name and region when you create a bucket.
- Custom CDN acceleration domain name: you can bind for your bucket a custom domain name to Tencent Cloud Content Delivery Network (CDN), and access objects in your bucket using this domain name. (If you have enabled "User-defined domain name" in the legacy COS console, then the new console will continue to display "User-defined domain name" instead of “Custom CDN acceleration domain”.)
- Custom endpoint: Allows you to bind your own domain name as a custom endpoint to the bucket for access to the objects in it.

> !Currently, you must activate the CDN service to use a custom domain name in COS.
>- For content delivery in the Chinese mainland, ICP filing is required. You are not required to do so through Tencent Cloud though.
>- For content delivery outside the Chinese mainland, ICP filing is not required, but note that your data and operations in Tencent Cloud still need to comply with local laws and regulations as well as [General Service Level Agreements](https://intl.cloud.tencent.com/document/product/301/12905).

With CDN acceleration enabled for the custom CDN acceleration domain name, if the origin is a public-read bucket, the objects in the origin can be accessed via the custom CDN acceleration domain name. If the origin is a private-read bucket, we recommend you enable the CDN origin-pull authentication and CDN authentication configuration options.

- Origin-pull authentication (CDN service authorization must be added before it can be enabled): If the data requested by a user is not cached in the edge node, CDN fetches the data from the origin. If COS is used as the origin and origin-pull authentication is enabled, the CDN edge node accesses the COS origin using a special service identity (which must be authorized by CDN service) to acquire and cache the data in the private bucket.
- CDN authentication: When a user accesses an edge node to acquire cached data, the edge node verifies the authentication field in the access URL based on the authentication configuration rules. This prevents unauthorized access and hotlinking, thereby improving the security and reliability of the data cached in the edge node.

CDN authentication configuration and CDN origin-pull authentication do not conflict with each other, but whether to enable them can affect the level of data protection, as shown below:

| Bucket access permission | CDN origin-pull authentication | CDN authentication | Origin can be accessed via CDN acceleration domain name | Origin can be accessed via<br>COS endpoint | Scenarios |
| ------------------- | ------------ | ------------ | --------------- | --------------- | ------------ |
| Public read | Disabled | Disabled | Yes | Yes  | Site-wide public access |
| Public read | Enabled | Disabled | Yes | Yes | Not recommended |
| Public read | Disabled | Enabled | URL authentication is required | Yes | Not recommended |
| Public read | Enabled | Enabled | URL authentication is required | Yes | Not recommended |
| Private read + CDN service authorization | Enabled | Enabled | URL authentication required | COS authentication required | Full-linkage protection |
| Private read + CDN service authorization | Disabled | Enabled | URL authentication is required | COS authentication is required | Not recommended |
| Private read + CDN service authorization | Enabled | Disabled | Yes | COS authentication is required | Origin protection |
| Private read + CDN service authorization | Disabled | Disabled | No | COS authentication is required | Not recommended |
| Private read | Disabled | Enabled or disabled | No | COS authentication is required | CDN is unavailable |

> !
> - Take the first row in the above list as an example. If the origin bucket is public read, and neither CDN origin-pull authentication nor CDN authentication configuration is enabled, you can access CDN edge nodes and the origin bucket using the CDN domain name, and access the origin bucket using the COS domain name.
> - **Origin protection** is useful in cases where your data cached on CDN edge nodes may be maliciously pulled due to a lack of CDN authentication. Therefore, we strongly recommend you enable CDN authentication to mitigate data security issues.
> - After CDN acceleration is enabled for a domain name, anyone can directly access the origin via the domain name. Therefore, if you need to keep your data private, be sure to protect your data in the origin through **Authentication Configuration**.

## More

- [Enabling Custom Acceleration Domain Names](https://www.tencentcloud.com/document/product/436/31505)
- [Enabling Custom Origin Domain Names](https://intl.cloud.tencent.com/document/product/436/31507)
- [Granting a sub-account permissions to configure bucket acceleration domain names](https://intl.cloud.tencent.com/document/product/436/31712)
- [Supporting HTTPS for Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/11142)
