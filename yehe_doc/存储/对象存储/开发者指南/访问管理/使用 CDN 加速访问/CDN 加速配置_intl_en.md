## Use Cases
- Low latency and fast downloads are required.
- GB- to TB-level data needs to be transferred across regions, countries, or continents.
- The same content needs to be downloaded frequently.

>!If the download request is from Tencent Cloud VPC (for example, using Tencent Cloud CVM to access a bucket), we recommend you use a standard COS domain name directly. If you use a CDN acceleration domain name, you will need to access the CDN node over a public network, which incurs additional fees such as CDN origin-pull traffic fees and traffic fees.
>

## Notes

For more information on domain name definition, CDN origin-pull authentication, and CDN authentication configuration, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).

CDN origin-pull authentication and CDN authentication configuration affect how CDN acceleration domain names and COS domain names access origin buckets. Find the details in the table below.

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

>!The **Origin protection** above is useful in cases where your data cached on CDN edge nodes may be maliciously pulled due to a lack of CDN authentication. Therefore, we strongly recommend you enable CDN authentication as well for data security concerns.

## Configuring CDN acceleration

The COS console provides two CDN acceleration options: default and custom.

### Default CDN acceleration

A default CDN acceleration domain name is a CDN acceleration domain name COS automatically assigns to a bucket in the format of `BucketName-APPID.file.myqcloud.com`. After it is enabled, you can use it to enjoy an accelerated access experience.

>!Starting from May 9, 2022, COS will stop supporting default CDN acceleration domain names for buckets that have never used them. This change will not affect buckets that are using or once used default CDN acceleration domain names. However, we recommend you switch to custom CDN acceleration domain names instead. For more information on custom CDN acceleration domain names, see [Enabling Custom CDN Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

#### Directions

#### 1. Select a bucket
Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and click the name of the target bucket.

#### 2. Enter the configuration page
>!**Domain Management** is inaccessible if you have never used the CDN service. To activate it, go to the [CDN console](https://console.cloud.tencent.com/cdn).

Click **Domains and Transfer** > **Default CDN Acceleration Domain** and find the **Default CDN Acceleration Domain** section. By default, the value of **Status** is **Disabled**. Click **Edit** and enable it. Then, configure it as follows:
![](https://main.qcloudimg.com/raw/a027d3ae128de8349db903b8f1833019.png)

 - **Acceleration Domain Name**: A default CDN acceleration domain name is a CDN acceleration domain name COS automatically assigns to a bucket in the format of `BucketName-APPID.file.myqcloud.com`. After it is enabled, you can use it to enjoy an accelerated access experience.
 - **Acceleration Region**: CDN acceleration is supported for the Chinese mainland, outside the Chinese mainland, as well as global acceleration for buckets across all regions.
 - **Origin Server Type**: **Default Endpoint** is selected by default. If a static website is enabled for a bucket that serves as an origin, and you want to accelerate the static website, select **Static Website Endpoint**. For more information, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).
 - **Origin Domain**: COS origin's domain name, which is automatically generated based on the bucket name and region when you create a bucket. It's important to distinguish it from the default CDN acceleration domain name.

#### 3. Enable origin-pull authentication (optional)

>!For private-read buckets, if both origin-pull authentication and CDN service authorization are enabled, signature is not required for access to the origin from CDN edge nodes, and cached resources in CDN will be delivered over the public network, which will affect the data security. Therefore, we recommend you enable CDN authentication.

Origin-pull authentication is used to verify the service identity of the CDN edge node so as to prevent unauthorized access as detailed below:
- Public-read bucket: The CDN edge node can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
- Private-read bucket: The CDN edge node needs to go through origin-pull authentication to get its service identity verified before it can access the objects in the bucket.


(1) Complete the CDN service authorization.

>?Before enabling origin-pull authentication, you need to authorize the CDN service first.

The steps are as follows:
Adding CDN service authorization will enable the CDN edge node to assume the service identity which allows it to perform operations on a bucket as detailed below:
- Public-read bucket: The CDN edge node can access the bucket without any authorization, so there is no need to add CDN service authorization.
- Private-read bucket: The CDN edge node needs a special service identity to access the bucket. Click **Add CDN Service Authorization** to grant the CDN edge node the service identity, select **I agree to the above authorization**, and click **OK**.

After the CDN service authorization is completed, the CDN edge node can perform three operations on the bucket: `Get Object`, `Head Object`, and `Options Object`. The authorization will be automatically written into the bucket access policy (see below for an example). Then, the CDN edge node does not need to do anything else while forwarding traffic to the origin.

```xml
  {
    "Statement": [
      {
        "Action": [
          "name/cos:GetObject",
          "name/cos:HeadObject",
          "name/cos:OptionsObject"
        ],
        "Effect": "allow",
        "Principal": {
          "qcs": [
            "qcs::cam::uin/100000000001:service/cdn"
          ]
        },
        "Resource": [
          "qcs::cos:ap-chengdu:uid/1250000000:examplebucket-1250000000/*"
        ]
      }
    ],
    "version": "2.0"
  }
```

(2) After authorization, enable **Origin-pull Authentication**.

![](https://main.qcloudimg.com/raw/58c92ca577ca99d1fd5d9523e25dcec4.png)


#### 4. Enable CDN acceleration
After clicking **Save**, you will see that the default acceleration domain name is being deployed (which is expected to be completed in about five minutes).

#### 5. Configure CDN authentication

>!After CDN acceleration is enabled for a domain name, anyone can directly access the origin through the domain name. Therefore, if you want to keep your data private, be sure to protect your data on the origin by enabling **Authentication Configuration**.

 - After you enable the default CDN acceleration domain name and origin-pull authentication, the CDN authentication status will appear in the default CDN acceleration domain name management section. You can click **Authentication Configuration** to enter the **Access Control** page of the corresponding domain name for configuration.
![](https://main.qcloudimg.com/raw/a878861f79ea47e27c127c5b5dff4eb4.png)
 - Or, go to the [CDN console](https://console.cloud.tencent.com/cdn), click **Domain Management**, select the default CDN acceleration domain name, and click **Access Control** > **Authentication Configuration**. For detailed configuration directions, see [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237).

#### 6. Disable the feature

After the above steps are completed, default CDN acceleration is enabled. You can disable it in the following ways:

- On the **Default CDN Acceleration Domain** page, click **Edit**, change the status to **Disabled**, click **Save**, and wait about five minutes for the deployment to complete. After that, the domain name status will become **Closed** in the CDN console.
- You can disable or delete the domain name in the [CDN console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).

>!When you delete a domain name in the CDN console, only the CDN acceleration record of the default CDN acceleration domain name is deleted, but not the domain name itself. You can enable it again in the COS console as needed.



### Custom CDN acceleration


You can bind a custom domain name with a bucket in the COS console. After that, you can enable CDN acceleration to speed up access to the bucket through the custom domain name. When binding a custom domain name with a bucket, you need to add a CNAME record to it at your domain name service provider.

>! Currently, you must activate the CDN service to use a custom CDN acceleration domain name in COS.
1. For domain names connected to a CDN node in the Chinese mainland, you need to complete ICP filing. You are not required to do so through Tencent Cloud though.
2. For domain names connected to a CDN node outside the Chinese mainland, ICP filing is not required, but you need to note that your data and operations in Tencent Cloud still need to comply with local laws and regulations as well as [General Service Level Agreements](https://intl.cloud.tencent.com/document/product/301/12905).

#### Prerequisites

#### Custom domain name acquisition and ICP filing

1. Domain name registration. You can register your domain name with [Tencent Cloud](https://console.cloud.tencent.com/domain) or another service provider.
2. ICP filing application. For content delivery in the Chinese mainland, complete ICP filing.

#### Directions

>!You can add a custom domain name and enable CDN acceleration in either the COS or CDN console. For more information on how to do so in the CDN console, see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

#### 1. Select a bucket
Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and click the name of the target bucket.

#### 2. Add a custom CDN acceleration domain name
Click **Domains and Transfer** > **Custom CDN Acceleration Domain**. Under the **Custom CDN Acceleration Domain** configuration item, click **Add Domain**.
- **Domain Name**: Enter the domain name you have purchased (such as `www.example.com`).
- **Acceleration Region**: CDN acceleration is supported for the Chinese mainland, outside the Chinese mainland, as well as global acceleration for buckets across all regions.
- **Origin Server Type**: **Default Endpoint** is selected by default. If a static website is enabled for a bucket that serves as an origin, and you want to accelerate the static website, select **Static Website Endpoint**.

#### 3. Enable origin-pull authentication (optional)
Origin-pull authentication is used to verify the service identity of the CDN edge node so as to prevent unauthorized access as detailed below:

- Public-read bucket: The CDN edge node can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
- Private-read bucket: The CDN edge node needs to go through origin-pull authentication to get its service identity verified before it can access the objects in the bucket. Click to enable **Origin-pull Authentication**.
![](https://main.qcloudimg.com/raw/da5fe7285a8a2932cfb015c361472202.png)
>!For private-read buckets, if origin-pull authentication is enabled, signature is not required for access to the origin from CDN edge nodes, and cached resources in CDN will be delivered over the public network, which will affect the data security. Therefore, we recommend you enable CDN authentication.

After enabling **Origin-pull Authentication**, click **Save** on the right. In about five minutes, the added custom domain name and CDN acceleration will be deployed.

#### 4. Configure CDN authentication
>!After CDN acceleration is enabled for the custom domain name, anyone can directly access the origin through the domain name. Therefore, if you want to keep your data private, be sure to protect your data on the origin by enabling authentication configuration.

After the custom domain name is deployed, a CDN authentication configuration link will appear in the CDN authentication column. Click **Set** to directly enter the CDN console for CDN authentication configuration. For detailed directions, see [Instruction](https://intl.cloud.tencent.com/document/product/228/35237).

#### 5. Configure automatic CDN cache purge
After this feature is enabled, when a file in the COS bucket is updated, the CDN cache will be automatically purged. You can go to the **Function Service** section in the COS console to configure this feature as instructed in [CDN Cache Purging](https://intl.cloud.tencent.com/document/product/436/37273).


#### 6. Resolve the domain name

After the custom domain name is added to CDN, the system will automatically assign you a CNAME domain name suffixed with `.cdn.dnsv1.com`. You need to complete the CNAME configuration at your domain name service provider. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

>!The CNAME domain name cannot be accessed directly.


#### 7. Configure the certificate (optional)

To add an HTTPS certificate for the custom domain name, go to the [CDN console](https://console.cloud.tencent.com/cdn/certificate). 

#### 8. Disable the feature

After the above steps are completed, you can use the custom domain name to accelerate access to resources in the bucket. You can disable it in the following ways:

On the **Custom CDN Acceleration Domain** page, click **Edit** to change the status of the domain name from **online** to **offline**, click **Save**, and wait about five minutes for the deployment to complete. After that, the status of the custom acceleration domain name will become **Closed** in the CDN console.

>!You can delete a custom domain name only after changing its status to **offline**. To disable or delete a CDN domain name, go to the [CDN console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).


