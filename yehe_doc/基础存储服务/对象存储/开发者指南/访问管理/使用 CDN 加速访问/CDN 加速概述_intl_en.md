Content Delivery Network (CDN) can be used to accelerate mass download/deliver content stored in a COS bucket, which is ideal when the same content needs to be downloaded repeatedly. The origin-pull authentication feature allows CDN to accelerate content stored in a private-read bucket. The CDN authentication feature allows only the authorized users to download content to avoid data security risks and unnecessary traffic costs.


>? After you enable the CDN acceleration domain name, data downloads and access through it will generate CDN origin-pull traffic and CDN traffic. For more information, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776).


## CDN

#### CDN overview

CDN is a layer in the internet ecosystem, consisting of high-performance edge nodes distributed around the world. These nodes store your content according to the caching rules. When a user requests content, the request will be routed to the edge node closest to the user to speed up access and improve availability.

CDN involves caching and origin-pull. When a user accesses a URL, if the requested content is not cached on the edge node, or the cached content has expired, the content will be pulled from the origin.

#### Use cases

- Low latency and fast downloads are required.
- GB- to TB-level data needs to be transferred across regions, countries, or continents.
- The same content needs to be downloaded frequently.

#### Security options

- Origin-pull authentication: If the requested content is not cached on the edge node, the content will be pulled from the origin. If COS is used as the origin and origin-pull authentication is enabled, the CDN edge node will use a special service identity to access the COS origin to obtain and cache the data in the private bucket.
 - CDN service authorization: You can authorize the CDN service so that CDN edge nodes can use a special service identity to access the COS origin and pull content from it.
- CDN authentication: When a user accesses an edge node to acquire cached data, the edge node verifies the authentication field in the access URL based on the authentication configuration rules. This prevents unauthorized access and hotlinking, thereby improving the security and reliability of the data cached in the edge node.

## Access Nodes of COS

#### Definition of access node

An access node is a domain name assigned to a bucket according to the bucket’s region and name. You can access data stored in the bucket using this domain name.

If the static website feature is enabled, you will be provided a static website access node, which can be configured responses that are different from that of the default access node.

#### Access nodes

- Access node: When a bucket is created, COS will assign an XML access node to the bucket in the format of `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com`, which can be accessed using RESTful APIs. You can access the node and refer to the [API Documentation](https://intl.cloud.tencent.com/document/product/436/7751) to configure the bucket, or upload/download objects.
- Static website node: You can enable the static website feature on the **Basic Configurations** page of the bucket in the console. After this, you will be provided an access node formatted as `&lt;BucketName-APPID>.cos-website.&lt;Region>.myqcloud.com`. You can configure special index pages (IndexPage), error pages (ErrorPage), and redirects for your static website, which allows only object downloads. Users can obtain the content using the static website domain name.

#### Access permissions

- Public-read: If a bucket is set to public-read, everyone can access the bucket using its domain name. If you use a public-read bucket as the origin, you can enable CDN acceleration directly without enabling CDN authentication and origin-pull authentication.
- Private-read: If a bucket is set to private-read, you can create access policies to manage who can access the bucket and manage CDN authorization. If you use a private-read bucket as the origin and enable origin-pull authentication but not CDN authentication, unauthorized users can access the bucket via CDN. Therefore, **you are advised to enable both origin-pull authentication and CDN authentication for private-read buckets to ensure the data security**.

## Accelerating Access to COS Using CDN

You can use a custom domain name that has obtained an ICP filing number and use a COS bucket as the origin. This allows you to accelerate access to objects in the bucket using the custom CDN acceleration domain name.

>?A Tencent Cloud CDN acceleration domain name does not provide an IP address by default. To know more about the DNS of the domain name, run the `dig` command for query.

#### Public-read buckets

If a bucket is set to public-read and COS is used as the origin for CDN pulling, you don’t need to enable origin-pull authentication and CDN edge nodes can obtain and cache objects stored in the COS bucket.

You can still protect your objects in the bucket **to some extent** by enabling [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237) in the CDN console. Regardless of whether this feature is enabled, users who know the bucket access domain name can access all objects in the bucket. Whether users can access the public-read bucket in different CDN authentication configurations is described in the following table:

| CDN Authentication | Access with CDN Acceleration Domain Name | Access with COS Domain Name | Use Case |
| ------------ | ---------------- | ------------ | ----------------------------------------------- |
| Disabled (default) | Yes | Yes | Allowing all public access to the entire website via the CDN or origin |
| Enabled | URL authentication is required | Yes | Enabling hotlink protection for access via the CDN but not the origin server (not recommended) |

#### Private-read buckets

If a bucket is set to private-read (default) and COS is used as the origin for CDN pulling, CDN edge nodes **cannot obtain and cache any objects**. Therefore, you need to add the CDN service identity to the bucket policy and authorize the identity to perform the following operations:

- GET Object: downloads an object.
- HEAD Object: queries object metadata.
- OPTIONS Object: configures a CORS preflight request

You can authorize the identity quickly in either the [CDN console](https://console.cloud.tencent.com/cdn) or the [COS console](https://console.cloud.tencent.com/cos5) by clicking **Add CDN Service Authorization**. Then, enable **Origin-pull Authentication**. In this way, CDN edge nodes can use the service identity to access COS objects.

>!
>- If the bucket is set to private-read, you must add the service authorization and enable origin-pull authentication; otherwise, access to COS will be denied.
>- A CDN edge node will generate a service account for each root account. Therefore, the account authorization is only valid for the root account to which the acceleration domain name belongs. If the acceleration domain name is bound to another account, access will be denied.

After you added the CDN service authorization and enabled origin-pull authentication, CDN edge nodes can obtain and cache data. Therefore, you are advised to enable [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237) if you need to protect private data stored in the bucket. Whether users can access the private-read bucket in different CDN authentication configurations is described in the following table:

| CDN Authentication | Access with CDN Acceleration Domain Name | Access with COS Domain Name | Use Case |
| ------------ | ---------------- | --------------- | ----------------------------------- |
| Disabled (default) | Yes | COS authentication is required | Allowing direct access to CDN domain names to protect the content on the origin  |
| Enabled | URL authentication is required | COS authentication is required | Securing access comprehensively (hotlink protection for CDN authentication is supported) |

