Accelerating COS with CDN allows you to mass download and deliver the content in a bucket, especially in the scenarios where the same content is repeatedly downloaded. With the origin-pull authentication feature, the delivery of content in a Public-Read bucket can be accelerated using CDN, and with the CDN authentication feature, the content can only be downloaded by legitimate users, thus avoiding data security problem and high traffic cost caused by unrestricted download access.

## Content Delivery Network (CDN)

### Definition of CDN

Content Delivery Network (CDN) is a layer of network architecture built on the Internet that is composed of globally distributed servers which work together to provide faster delivery of Internet content. These high-performance cache nodes store your Internet content based on a certain caching policy. When your user makes a request for your Internet content, the request will be routed to the server closest to the user. Then the server responds to the request directly, greatly reducing the user's access delay and improving availability.

Caching and origin-pull will occur on a CDN. When a user accesses a URL, if the requested content is not cached on the edge server to which the access request is directed, or the cached content has expired, the request will be returned to the origin server to get the content.

### Use cases

- Scenarios with high requirements for response delay and download speed.
- Scenarios where cross-region, cross-border or cross-continent data transfer reaching GB or TB-level is required.
- Scenarios where the same content needs to be downloaded frequently.

### Security options

- Origin-pull authentication: If the data requested by a user is not cached in the edge server, CDN fetches the data from the origin server. If COS is used as the origin server and origin-pull authentication is enabled, the CDN edge server accesses the COS origin server using a special service identity to acquire and cache the data in the private bucket.
  - CDN service authorization: A CDN edge server can access the COS origin server with a special service identity by adding a CDN service authorization. Origin-pull authentication can only be enabled after the CDN service authorization is added.
- CDN authentication: When a user attempts to acquire cached data by accessing an edge server, the edge server verifies the authentication field in the accessed URL based on the authentication configuration rules to prevent unauthorized access and realize hotlink protection, thus improving the security and reliability of the data cached in the edge server.

## Access Nodes of COS

### Definition of access node

An access node is an access domain name that is assigned to a bucket based on the region and name of the bucket when it is created. The domain name can be used to access the data in the bucket.

If the static website feature is enabled, you can get an access node for a static website to present the specially configured response content that is different from that of the default node.

### Access nodes

- XML node: After a bucket is created, COS assigns an XML access node to the bucket, such as `<bucketname>-<APPID>.cos.<region>.myqcloud.com`. It is suitable for RESTful API calls. With an XML access node, you can configure a bucket or upload/download objects as described in [API documentation](https://cloud.tencent.com/document/product/436/7751).
- Static website node: You can enable the static website hosting feature in the basic configuration interface of bucket in the console. After the feature is enabled, an access node in the form of ` <bucketname>-<APPID>.cos-website.<region>.myqcloud.com` is provided. Static websites support special index pages (IndexPage), error pages (ErrorPage), and redirects, and only allow the download of objects. You can obtain content through static website nodes.

#### Access permissions

- Public Read: When a bucket is set to "Public Read", anyone can access it using the bucket's access domain name. If you use a public-read bucket as the origin server, you can enable CDN acceleration directly without using CDN authentication and origin-pull authentication.
- Private Read: When a bucket is set to "Private Read", you can manage accessing users and CDN service authorizations by creating access policies. When you use a private-read bucket as the origin server, if origin-pull authentication is enabled but CDN authentication is not, unauthorized users can access the bucket via CDN. Therefore, it is highly recommended to enable both origin-pull authentication and CDN authentication for private-read buckets to ensure the data security.

## Accelerating Access to COS Using CDN

You can accelerate access to COS by managing the following two domain names:

- Default accelerated domain name: COS provides a default CDN accelerated domain name (such as ` <bucketname>-<APPID>.file.mycloud.com`). You can enable or disable it at your option.
- Custom domain name: You can use a custom domain name which has gone through ICP filing, with a COS bucket as the origin server. This allows you to accelerate the access to the objects in the bucket with your custom domain name.

> **Notes:**
> Default accelerated domain name and custom domain name can be collectively referred to as CDN accelerated domain names.

### Public-read buckets

When a bucket is set to allow public access, and the CDN origin server is set to the COS access node, the CDN edge servers can acquire and cache the object data in the bucket without you enabling origin-pull authentication.

You can provide **limited** protection for the data in the bucket by enabling [Authentication Configuration](https://cloud.tencent.com/document/product/228/13677) in the CDN Console. This is because that regardless of whether this feature is enabled in the CDN, the users who know the bucket access domain name can access all objects in the bucket. Whether the access to public-read buckets is possible via different domain names when CDN authentication is enabled or disabled is as follows:

| CDN Authentication | CDN Accelerated Domain Name | COS Domain Name | Scenarios |
| ------------ | ---------------- | ------------ | ----------------------------------------------- |
| Disabled (default) | Yes | Yes | Public access to the entire website via CDN or origin server is allowed. |
| Enabled | URL authentication is required | Yes | Hotlink protection is enabled for access via CDN access, but not for access via origin server (not recommended) |

### Private-read buckets

When a bucket defaults to Private Read, and the CDN origin server is set to the COS access node, the CDN edge nodes are **unable to get and cache any data**. Therefore, you need to add the CDN service identity to the Bucket Policy and authorize the identity to perform the following operations:

- GET Object - Acquire objects.
- HEAD Object - Acquire the metadata of objects.
-  OPTIONS Object - Initiate a preflight request.

You can complete quick authorization in both the CDN Console and the COS Console by simply clicking **Add CDN Service Authorization**. Then you need to enable **Origin-Pull Authentication**. After that, a CDN edge server can access the data in the COS with its service identity.

> **Notes:**
> 1. If the bucket is set to Private Read, you must add an authorization and enable origin-pull authentication, otherwise COS will deny the access to it.
> 2. A CDN edge server will generate a unique service account for each root account. Therefore, the account authorization is only valid for the root account to which the accelerated domain name belongs. Cross-account binding of an accelerated domain name will cause the access via the domain name to be denied.

After the CDN service authorization is added and origin-pull authentication is enabled, the CDN edge nodes are able to directly get and cache the data. Therefore, it is highly recommended to enable [Authentication Configuration](https://cloud.tencent.com/document/product/228/13677) to protect the private data in a bucket. Whether the access to private-read buckets is possible via different domain names when CDN authentication is enabled or disabled is as follows: 

| CDN Authentication | CDN Accelerated Domain Name | COS Domain Name | Scenarios |
| ------------ | ---------------- | --------------- | ----------------------------------- |
| Disabled (default) | Yes | COS authentication is required | Direct access to CDN domain names is allowed to protect the data on origin server. |
| Enabled | URL authentication is required | COS authentication is required | Full stack strict SSL secured connection. Hotlink protection for CDN authentication is supported. |

