## Use Cases
- Low latency and fast downloads are required.
- GB- to TB-scale data needs to be transferred across regions, countries, or continents.
- The same content needs to be downloaded frequently.

>!If the download request is from a Tencent Cloud VPC (for example, using a CVM to access a COS bucket), we recommend you use the COS domain directly. If you use a CDN acceleration domain, you will need to access the CDN node over a public network, which incurs additional fees such as CDN origin-pull fees and CDN traffic fees.
>


## Notes
For information on domain name definition, CDN origin-pull authentication, and CDN authentication configuration, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).

CDN origin-pull authentication and CDN authentication configuration affect how CDN acceleration domain names and COS domain names access origin buckets. Find the details in the table below.

| Bucket access permission | CDN origin-pull authentication | CDN authentication | Origin can be accessed via <br>CDN acceleration domain name | Origin can be accessed via <br>COS endpoint | Scenarios |
| ------------------- | ------------ | ------------ | --------------- | --------------- | ------------ |
| Public read | Disabled | Disabled | Accessible | Accessible | Site-wide public access |
| Public read | Enabled | Disabled | Yes | Yes | Not recommended |
| Public read | Disabled | Enabled | URL authentication is required | Yes | Not recommended |
| Public read | Enabled | Enabled | URL authentication is required | Accessible | Not recommended |
| Private read + CDN service authorization | Enabled | Enabled | URL authentication required | COS authentication required | Full-linkage protection |
| Private read + CDN service authorization | Disabled | Enabled | URL authentication is required | COS authentication is required | Not recommended |
| Private read + CDN service authorization | Enabled | Disabled | Yes | COS authentication is required | Origin protection |
| Private read + CDN service authorization | Disabled | Disabled | No | COS authentication is required | Not recommended |
| Private read | Disabled | Enabled or disabled | No | COS authentication is required | CDN is unavailable |

>!**Origin protection** is useful in cases where your data cached on CDN edge nodes may be maliciously pulled due to lack of CDN authentication. Therefore, we strongly recommend you enable CDN authentication to mitigate data security issues.

## Configuring CDN Acceleration for Default Acceleration Domain Names

A default acceleration domain name is a CDN acceleration domain name COS automatically assigns to a bucket. The format is `BucketName-APPID.file.myqcloud.com`. You can **enable** or **disable** it as needed.

### Enable the feature
#### 1. Select a bucket
Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and click the name of a bucket that you want to enable acceleration for.

#### 2. Enter the configuration page
>!If you have never used Tencent Cloud's CDN service, **Domain Management** will not be available. To activate the CDN service, go to the [CDN console](https://console.cloud.tencent.com/cdn).

Click **Domains and Transfer** > **Default CDN Acceleration Domain** and find the **Default CDN Acceleration Domain** area. By default, the value of **Status** is **Disabled**. Click **Edit** and enable it.
![](https://main.qcloudimg.com/raw/a027d3ae128de8349db903b8f1833019.png)
**Acceleration Region**: Supports acceleration for the Chinese mainland, outside the Chinese mainland, as well as global acceleration (global acceleration means acceleration for buckets across all regions).
**Origin Server Type**: **Default Endpoint** is selected by default. If a static website is enabled for a bucket that serves as an origin, and you want to accelerate the static website, select **Static Website Endpoint**. For more information, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).

#### 3. Add CDN service authorization (optional)

Adding CDN service authorization will enable the CDN edge node to assume the service identity which allows it to perform operations on a bucket. Find the details below.

- Public-read bucket: The CDN edge node can access the bucket without any authorization, so there is no need to add CDN service authorization.
- Private-read bucket: The CDN edge node needs a special service identity to access the bucket. Click **Add CDN Service Authorization** to grant the CDN edge node the service identity, indicate your agreement to the authorization, and click **OK**.

After the authorization is added, the CDN edge node can perform `Get Object`, `Head Object`, and `Options Object` on the bucket.

![](https://main.qcloudimg.com/raw/ca62b2f78b7587245efbe0b03f84adee.png)

After the authorization is granted, it will be automatically written into the bucket access policy (see below for an example). Then the CDN edge node does not need to do anything else while forwarding traffic to the origin.

```xml
  {
    "Statement":[
      {
        "Action":[
          "name/cos:GetObject",
          "name/cos:HeadObject",
          "name/cos:OptionsObject"
        ],
        "Effect": "allow",
        "Principal":{
          "qcs":[
            "qcs::cam::uin/100000000001:service/cdn"
          ]
        },
        "Resource":[
          "qcs::cos:ap-chengdu:uid/1250000000:examplebucket-1250000000/*"
        ]
      }
    ],
    "version": "2.0"
  }
```

#### 4. Enable origin-pull authentication (optional)
>! You need to add the CDN service authorization before you can enable origin-pull authentication.

Origin-pull authentication is used to verify the service identity of the CDN edge node so as to prevent unauthorized access. Find the details below.
- Public-read bucket: The CDN edge node can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
- Private-read bucket: The CDN edge node needs to go through origin-pull authentication to get its service identity verified before it can access the objects in the bucket.

After authorization, enable **Origin-pull Authentication**.

![](https://main.qcloudimg.com/raw/58c92ca577ca99d1fd5d9523e25dcec4.png)


>! For private-read buckets, after origin-pull authentication and CDN service authorization are enabled, the CDN edge node will no longer need to carry a signature when accessing the origin, and the resources cached by CDN will be delivered over the public network. In such case, data security will be under threat. Therefore, we recommend that you enable CDN authentication.

#### 5. Enable CDN acceleration
After clicking **Save**, you will see that the default acceleration domain name is being deployed (which is expected to be completed in about 5 minutes).

### Configure authentication
>! After CDN acceleration is enabled for the default domain name, anyone can access the origin through this domain name. If your data requires privacy, be sure to enable the authentication to protect your data on the origin.

After you enable the default CDN acceleration domain and origin-pull authentication, the CDN authentication status will appear in the **Default CDN Acceleration Domain** area. You can click **Authentication Configuration** to go to the CDN security configuration page of the corresponding domain.
![](https://main.qcloudimg.com/raw/a878861f79ea47e27c127c5b5dff4eb4.png)

You can also go to this page from the [CDN console](https://console.cloud.tencent.com/cdn) by clicking **Domain Management** > **Manage** (for the corresponding domain name) > **Security Configuration**. For detailed configuration directions, see [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237).


### Disable the feature
You can disable the default CDN acceleration domain in either of the following ways:

- On the **Default CDN Acceleration Domain** page, click **Edit**, change the status to **Disabled**, click **Save**, and wait for about 5 minutes for the deployment to complete. After that, the domain status will be changed to **Deactivated** in the CDN console.
- You can deactivate or delete the domain name in the [CDN console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).
>! When you delete a domain name in CDN console, you are deleting a CDN acceleration record of the default accelerated domain name, not the domain name itself. You can activate it again in the COS console.


## Configuring CDN Acceleration for a Custom Domain
You can bind a custom domain name with a bucket in the COS Console. After that, you can enable CDN acceleration to speed up access to the bucket through the custom domain name. When binding a custom domain name with a bucket, you need to add a CNAME record to it at your domain name service provider.
>! Currently, you need to enable CDN service to use a custom domain name in COS.
1. For content delivery in the Chinese mainland, ICP filing is required. You are not required to do so through Tencent Cloud though.
2. For content delivery outside the Chinese mainland, ICP filing is not required, but note that your data and operations in Tencent Cloud still need to comply with local laws and regulations as well as [General Service Level Agreements](https://intl.cloud.tencent.com/document/product/301/12905).

### Custom domain name acquisition and ICP filing

1. Domain name registration. You can register your domain name with DNSPod or another service provider.
2. ICP filing application. For content delivery in the Chinese mainland, complete ICP filing as instructed in [ICP Filing Guide].

### Enable the feature
>!You can add a custom domain name and enable CDN acceleration in both COS console and CDN console. For more information on how to do so in the CDN console, see [Connecting Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

#### 1. Select a bucket
Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and click the name of a bucket that you want to enable acceleration.

#### 2. Add a custom CDN acceleration domain name
Click **Domains and Transfer** > **Custom CDN Acceleration Domain**. Under the **Custom CDN Acceleration Domain** configuration item, click **Add Domain**.
- **Domain Name**: Enter the domain name you have purchased (such as `www.example.com`).
- **Acceleration Region**: Supports acceleration for the Chinese mainland, outside the Chinese mainland, as well as global acceleration (global acceleration means acceleration for buckets across all regions).
- **Origin Server Type**: **Default Endpoint** is selected by default. If a static website is enabled for the selected bucket and you want to accelerate the static website, select **Static Website Endpoint**.


#### 3. Enable origin-pull authentication (optional)
Origin-pull authentication is used to verify the service identity of the CDN edge node so as to prevent unauthorized access. Find the details below.

- Public-read bucket: The CDN edge node can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
- Private-read bucket: A CDN edge node needs to go through origin-pull authentication to get its service identity verified before it can access the objects in the bucket. Click to enable **Origin-pull Authentication**.
![](https://main.qcloudimg.com/raw/da5fe7285a8a2932cfb015c361472202.png)
>! For private-read buckets, after origin-pull authentication is enabled, the CDN edge node will no longer need to carry a signature when accessing the origin, and the resources cached by CDN will be delivered over the public network. In such case, data security will be under threat. Therefore, we recommend that you enable CDN authentication.

#### 4. Enable CDN acceleration

Click **Save** on the right. In about 5 minutes, the added custom domain name and CDN acceleration will be deployed.

### Configure authentication
>! After CDN acceleration is enabled for the custom domain name, anyone can directly access the origin through this domain name. If your data requires privacy, be sure to enable the authentication configuration to protect your data on the origin.

After the custom domain name is deployed, a CDN authentication configuration link will appear in the CDN authentication column. Click **Set** to directly enter the CDN console for CDN authentication configuration. For detailed directions, see [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237).
![](https://main.qcloudimg.com/raw/b0e9b2e0febc4b480a16a11f06498740.png)


### Resolve domain names
After the custom domain name is added to the CDN, the system will automatically assign you a CNAME domain name suffixed with `.cdn.dnsv1.com`. You need to complete the CNAME configuration at the domain name service provider. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

>! You will not be able to directly access the CNAME domain name.


### Disable the feature
On the **Custom CDN Acceleration Domain** page, click **Edit** to change **Status** from **online** to **offline**, click **Save**, and wait for about 5 minutes for the deployment to complete. After that, the status of the custom acceleration domain will be changed to **Deactivated** in the CDN console.

>!You can delete a custom domain name only after changing its status to **Offline**. To disable or delete a CDN domain name, go to the [CDN console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).



