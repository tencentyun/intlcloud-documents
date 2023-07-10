## Use Cases

- Low latency and fast downloads are required.
- GB- to TB-scale data needs to be transferred across regions, countries, or continents.
- The same content needs to be downloaded frequently.

>!If the download request is from a Tencent Cloud VPC (for example, using a CVM to access a COS bucket), we recommend you use the COS domain directly. If you use a custom CDN acceleration domain, you will need to access the CDN node over a public network, which incurs additional fees such as CDN origin-pull fees and CDN traffic fees.
>

## Notes

For information on domain name definition, CDN origin-pull authentication, and CDN authentication configuration, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).

CDN origin-pull authentication and CDN authentication configuration affect how custom CDN acceleration domain names and COS domain names access origin buckets. Please find the details in the table below.

| Bucket access permission | CDN origin-pull authentication | CDN authentication | Origin can be accessed via custom CDN acceleration domain name | Origin can be accessed via COS endpoint | Scenarios |
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

>!**Origin protection** is useful in cases where your data cached on CDN edge nodes may be maliciously pulled due to lack of CDN authentication. Therefore, we strongly recommend you enable CDN authentication to mitigate data security issues.

## Setting CDN Acceleration


You can bind a custom domain name with a bucket in the COS console. After that, you can enable CDN acceleration for the custom domain name to speed up access to the bucket through the custom domain name. When binding a custom domain name with a bucket, you need to add a CNAME record to it at your domain name service provider.

> !Currently, you must activate the CDN service to use a custom acceleration domain name in COS.
1. For content delivery in the Chinese mainland, ICP filing is required. You are not required to do so through Tencent Cloud though.
2. For content delivery outside the Chinese mainland, ICP filing is not required, but note that your data and operations in Tencent Cloud still need to comply with local laws and regulations as well as [General Service Level Agreements](https://intl.cloud.tencent.com/document/product/301/12905).

### Prerequisites


1. Domain name registration. You can register your domain name with [Tencent Cloud](https://console.cloud.tencent.com/domain) or another service provider.
2. ICP filing application. For content delivery in the Chinese mainland, complete ICP filing.

### Directions

>!You can add a custom domain name and enable CDN acceleration in both COS console and CDN console. For more information on how to do so in the CDN console, see [Connecting Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

#### 1. Select a bucket
Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and click the name of a bucket that you want to enable CDN acceleration.

#### 2. Add a custom CDN acceleration domain name

Click **Domains and Transfer** > **Custom CDN Acceleration Domain**. Under the **Custom CDN Acceleration Domain** configuration item, click **Add Domain**.
  - **Domain Name**: Enter the target custom domain name (such as `www.example.com`). Make sure that an ICP filing has been obtained and a CNAME record has been configured at the DNS service provider for the entered domain. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121). If the custom CDN acceleration domain you are connecting is in the following situations, you need to verify your domain ownership as instructed in [Domain Name Ownership Verification](https://intl.cloud.tencent.com/document/product/228/42693).
     - The domain name is being connected for the first time.
     - The domain name has been connected by another user.
     - The domain name is a wildcard domain name.
  - **Acceleration Region**: CDN acceleration is supported for regions in the Chinese mainland, outside the Chinese mainland, and globally, with global acceleration for buckets across all regions.
  - **Origin Server Type**: **Default Endpoint** is selected by default. If a static website is enabled for a bucket that serves as an origin, and you want to accelerate the static website, select **Static Website Endpoint**. For more information, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).
  - **Authentication**: Enable origin-pull authentication. For private-read buckets, enable origin-pull authentication to protect the origin.
>!
>For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, signature is not required for accessing the origin via CDN, and cached resources in CDN will be distributed on the public network, which will affect the data security. Therefore, we recommend that you enable CDN authentication.
>
  - Enabling origin-pull authentication
Origin-pull authentication is used to verify the service identity of the CDN edge node so as to prevent unauthorized access. Find the details below.
     - Public-read bucket: The CDN edge node can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
     - Private-read bucket: A CDN edge node needs to go through origin-pull authentication to get its service identity verified before it can access the objects in the bucket. Click to enable **Origin-pull Authentication**.

After enabling **Origin-pull Authentication**, click **Save** on the right. In about five minutes, the added custom domain name and CDN acceleration will be deployed.
  - Enabling CDN authentication
>!
>After CDN acceleration is enabled for the custom domain name, anyone can access the origin via the domain name. Therefore, if you need to keep you data private, be sure to protect your data in the origin by enabling CDN authentication.
>
After the custom domain name is deployed, a CDN authentication configuration link will appear in the CDN authentication column. Click **Set** to directly enter the CDN console for CDN authentication configuration. For detailed directions, see [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237).

  - **Automatic CDN Cache Purge**: After this feature is enabled, when a file in the COS bucket is updated, the CDN cache will be automatically purged. You can go to the **Function Service** section in the COS console to configure this feature as instructed in [Setting CDN Cache Purge](https://intl.cloud.tencent.com/document/product/436/37273).
  - **HTTPS Certificate**: To add an HTTPS certificate for the custom domain name, go to the [CDN console](https://console.cloud.tencent.com/cdn/certificate).


#### 3. Resolve the domain name

After the custom domain name is added to the CDN, the system will automatically assign you a CNAME domain name suffixed with `.cdn.dnsv1.com`. You need to complete the CNAME configuration at the domain name service provider. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

>! You will not be able to directly access the CNAME domain name.



#### 4. Disable the feature

After the above steps are completed, you can use the custom domain name to accelerate access to resources in the bucket. You can disable it in the following ways:

On the **Custom CDN Acceleration Domain** page, click **Edit** to change **Status** from **online** to **offline**, click **Save**, and wait for about 5 minutes for the deployment to complete. After that, the status of the custom acceleration domain name will be changed to **Deactivated** in the CDN console.

>!You can delete a custom domain name only after changing its status to **Offline**. To disable or delete a CDN domain name, go to the [CDN console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).


