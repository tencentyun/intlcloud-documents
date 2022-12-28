## Overview

After an object is uploaded to the bucket, COS will automatically generate a URL (i.e., default endpoint) for you to access the object directly. To use CDN or your own domain name to access COS objects, you can bind your own domain or CDN acceleration domain to the bucket where the objects are stored.

You can set a domain name to access objects as needed. If you want to access a file through CDN acceleration, you need to access it by using the URL generated with the CDN acceleration domain name.

## Description

You can quickly download and deliver objects in a bucket by managing the following domain names:

- **Default Endpoint**: COS origin's domain name, which is automatically generated based on the bucket name and region when you create a bucket. 
- **Custom CDN Acceleration Domain**: You can bind for your bucket a custom domain name to Tencent Cloud Content Delivery Network (CDN) and access objects in your bucket using this domain name. (If you have enabled **Custom Domain** in the legacy COS console, **Custom Domain** will be displayed in the new console instead of **Custom CDN Acceleration Domain**.)
- **Custom Endpoint**: You can bind your own domain name as a custom endpoint to the bucket for access to the objects in it.

> !Currently, you must activate the CDN service to use **Custom CDN Acceleration Domain** in COS.
>- For domain names connected to a CDN node in the Chinese mainland, you need to complete ICP filing. You are not required to do so through Tencent Cloud though.
>- For domain names connected to a CDN node outside the Chinese mainland, ICP filing is not required, but you need to note that your data and operations in Tencent Cloud still need to comply with local laws and regulations as well as [General Service Level Agreements](https://intl.cloud.tencent.com/document/product/301/12905).

With CDN acceleration enabled for **Custom CDN Acceleration Domain**, if the origin is a public-read bucket, the objects on the origin can be accessed via **Custom CDN Acceleration Domain**. If the origin is a private-read bucket, we recommend you enable origin-pull authentication and CDN authentication.

- **Origin-pull Authentication** (CDN service authorization must be added before it can be enabled): If the data requested by a user is not cached on the edge node, CDN will fetch the data from the origin. If COS is used as the origin and origin-pull authentication is enabled, the CDN edge node will access the COS origin server by using a special service identity (which must be authorized by the CDN service) to get and cache the data in the private bucket.
- **CDN Authentication**: When a user attempts to acquire cached data by accessing an edge node, the edge server will verify the authentication field in the accessed URL based on the authentication configuration rules to prevent unauthorized access and realize hotlink protection, thus improving the security and reliability of the data cached on the edge node.

CDN authentication and origin-pull authentication do not conflict with each other, but whether to enable them can affect the level of data protection as shown below:

| Bucket access permission | CDN origin-pull authentication | CDN authentication | Origin can be accessed via <br>CDN acceleration domain name | Origin can be accessed via <br>COS endpoint | Scenarios |
| ------------------- | ------------ | ------------ | --------------- | --------------- | ------------ |
| Public read | Disabled | Disabled | Yes | Yes | Site-wide public access |
| Public read | Enabled | Disabled | Yes | Yes | Not recommended |
| Public read | Disabled | Enabled | URL authentication is required | Yes | Not recommended |
| Public read | Enabled | Enabled | URL authentication is required | Yes | Not recommended |
| Private read + CDN service authorization | Enabled | Enabled | URL authentication is required | COS authentication is required | Full-linkage protection |
| Private read + CDN service authorization | Disabled | Enabled | URL authentication is required | COS authentication is required | Not recommended |
| Private read + CDN service authorization | Enabled | Disabled | Yes | COS authentication is required | Origin protection |
| Private read + CDN service authorization | Disabled | Disabled | No | COS authentication is required | Not recommended |
| Private read | Disabled | Enabled or disabled | No | COS authentication is required | CDN is unavailable |

> !
> - Take the first row in the above list as an example. If the origin bucket is public read, and neither origin-pull authentication nor CDN authentication is enabled, then you can directly access CDN edge nodes and the origin bucket by using the CDN acceleration domain name, and directly access the origin bucket by using the COS domain name.
> - The **Origin protection** above is useful in cases where your data cached on CDN edge nodes may be maliciously pulled due to a lack of CDN authentication. Therefore, we strongly recommend you enable CDN authentication as well for data security concerns.
> - After CDN acceleration is enabled for a domain name, anyone can directly access the origin via the domain name. Therefore, if you need to keep your data private, be sure to protect your data on the origin through **Authentication Configuration**.

## Related Operations

- [Enabling Custom CDN Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/436/31506)
- [Enabling Custom Origin Domains](https://intl.cloud.tencent.com/document/product/436/31507)
- [Granting a Sub-Account Permission to Configure Bucket Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31712)
- [Supporting HTTPS for Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/11142)
