## Applicable Scenarios
- Scenarios with high requirements for response latency and download speed.
- Scenarios where gigabytes to terabytes of data needs to be transmitted across regions, countries, and continents.
- Scenarios where the same contents needs to be download frequently and repeatedly.

## Notes
For more information on domain name definition, CDN origin-pull authentication, and CDN authentication configuration, see [CDN Overview](https://intl.cloud.tencent.com/document/product/436/18669).

CDN origin-pull authentication and CDN authentication configuration affect the access modes of the CDN accelerated domain name and COS domain name to the origin server bucket as shown below:

| Bucket Access | CDN Origin-pull Authentication | CDN Authentication Configuration | CDN Accelerated Domain Name | COS Domain Name | Scenario |
| ------------------- | ------------ | ------------ | --------------- | --------------- | ------------ |
| Public read | Disabled | Disabled | Accessible | Accessible | Full-website public access |
| Public read | Enabled | Disabled | Accessible | Accessible | Not recommended |
| Public read | Disabled | Enabled | URL authentication required | Accessible | Not recommended |
| Public read | Enabled | Enabled | URL authentication required | Accessible | Not recommended |
| Private read + CDN service authorization | Enabled | Enabled | URL authentication required | COS authentication required | Full-link protection |
| Private read + CDN service authorization | Disabled | Enabled | Inaccessible | COS authentication required | Not recommended |
| Private read + CDN service authorization | Enabled | Disabled | Accessible | COS authentication required | Origin server protection |
| Private read + CDN service authorization | Disabled | Disabled | Inaccessible | COS authentication required | Not recommended |
| Private read | Disabled | Enabled or disabled | Inaccessible | COS authentication required | Unable to use CDN |

## Configuring CDN Acceleration for a Default Accelerated Domain Name

A default accelerated domain name is a CDN accelerated domain name that COS automatically assigns to a bucket, such as <BucketName-APPID>.file.mycloud.com`, which you can **enable** or **disable**.

### Enabling the Feature
#### 1. Select a bucket
Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the bucket to be accelerated to enter the bucket.
![](https://main.qcloudimg.com/raw/7537a96a0276f31d7ec0a33a6a7a79b1.png)

#### 2. Enter the configuration page
> If you have never used the Tencent Cloud CDN service, you will not be able to enter **Domain Name Management**. In this case, you need to click the external link to enter the CDN Console and activate the CDN service.

Click **Domain Name Management** at the top of the page. The default accelerated domain name is **disabled** by default. Click **Edit** to change the current status to **enabled**.
![](https://main.qcloudimg.com/raw/a027d3ae128de8349db903b8f1833019.png)
**Origin Server Type**: The **Default origin server** is selected by default. If a static website is built in the bucket as origin server and you want to accelerate the static website, you can set the origin server type to **Static website origin server**. For more information, see [CDN Overview](https://intl.cloud.tencent.com/document/product/436/18669).

#### 3. Add a CDN service authorization (optional)

Adding a CDN service authorization is to grant the CDN edge server permission to manipulate the bucket as shown below:

- Public read bucket: The CDN edge server can access the bucket directly without any authorization required, so there is need to add the CDN service authorization.
- Private read bucket: The CDN edge server needs to be granted a special service identity to access the bucket. Click **Add a CDN Service Authorization** to grant the CDN edge sever the service identity, select **I agree to the authorization above**, and click **OK**.

After the authorization is added, the CDN edge server can perform three operations on the bucket: GET Object, Head Object, and Options Object.

![](https://main.qcloudimg.com/raw/ca62b2f78b7587245efbe0b03f84adee.png)

After the authorization is granted, the system will automatically write a bucket access policy (see below for an example), and then the CDN edge server does not need to do anything else during origin-pull.

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

#### 4. Enable origin-pull authentication (optional)
> You need to add the CDN service authorization before you can enable origin-pull authentication.

Origin-pull authentication is used to verify the service identity of the CDN edge server so as to prevent unauthorized access as shown below:
- Public read bucket: The CDN edge server can access the bucket directly without any authorization required, so there is need to enable origin-pull authentication.
- Private read bucket: The CDN edge server needs to be authenticated by origin-pull authentication for its service identity and can access objects in the bucket only after successful authentication. Toggle on **Origin-pull Authentication** and click **Save**.
![](https://main.qcloudimg.com/raw/58c92ca577ca99d1fd5d9523e25dcec4.png)

> For private read buckets, after origin-pull authentication and CDN service authorization are enabled, the CDN edge server does not need to carry a signature when accessing the origin server, and the resources cached by CDN will be delivered over the public network, which may affect the data security. Therefore, it is highly recommended to enable CDN authentication.

#### 5. Enable CDN acceleration
After clicking **Save**, you can see that the default accelerated domain name is being deployed (which is expected to be completed in about 5 minutes).

### Configuring Authentication
> After CDN acceleration is enabled for the default domain name, anyone can directly access the origin server through this domain name. If your data requires privacy, please be sure to enable the authentication configuration to protect your data on the origin server.

After the default accelerated domain name and origin-pull authentication are enabled, a CDN authentication status prompt will appear at the bottom of the default accelerated domain name management page. You can click **authentication configuration** in the prompt to enter the CDN security configuration page of the corresponding domain name.
![](https://main.qcloudimg.com/raw/a878861f79ea47e27c127c5b5dff4eb4.png)

You can also go to this page by clicking **Domain Name Management** > the corresponding domain name > **Management** > **Security Configuration** in the [CDN Console](https://console.cloud.tencent.com/cdn). 


### Disabling the Feature
- On the default accelerated domain name management page, click **Edit**, toggle the status from **on** to **off**, and click **Save**. The deployment will be completed in around 5 minutes. After that, the domain name will be displayed as **Disabled** in the CDN Console.
![](https://main.qcloudimg.com/raw/7a3033a50a1d6260a6ae508c7d903a28.png)

- You can disable and delete the domain name in the [CDN Console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).
> Only the CDN acceleration record of the default accelerated domain name instead of the domain name itself will be deleted in the CDN Console. The domain name can be enabled again there.


## Configuring CDN Acceleration for a Custom Accelerated Domain Name
You can bind a custom domain name to a bucket in the COS Console. After binding, you can enable CDN acceleration to speed up access to the bucket through the custom domain name. When binding a custom domain name, you need to add a CNAME record to it first at your domain name service provider.
> Currently, CDN has to be enabled before COS can use a custom domain name. Please note the following points based on your actual situation:
1. If your domain name is connected to a CDN node in Mainland China, you need to obtain an ICP filing for it. However, you are not required to do so through Tencent Cloud, and it is okay as long as your domain name has obtained the ICP filing.
2. If your domain name is connected to a CDN node outside Mainland China, you do not need to obtain an ICP filing for it. However, it should be noted that your data and operations in Tencent Cloud should comply with local laws and regulations as well as [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248).

### Enabling the Feature
> You can add a custom domain name and enable CDN acceleration in both the COS Console and the CDN Console. For more information on how to do so in the CDN Console, see [Domain Name Access](https://intl.cloud.tencent.com/document/product/228/5734).

#### 1. Select the bucket to be bound to a custom domain name
Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the bucket to be accelerated to enter the bucket.
![](https://main.qcloudimg.com/raw/51b356eb56cd09e3a3dc05725dd87ed8.png)

#### 2. Add a custom domain name
Click **Domain Name Management** to enter the domain name management page and click **Add a Domain Name** in the custom domain name section to enter the configurable page.
**Domain Name**: Enter the domain name you have purchased (such as `www.example.com`).
**Origin Server Type**: The **Default origin server** is selected by default. If a static website is built in the selected bucket and you want to accelerate the static website, you can set the origin server type to **Static website origin server**.
![](https://main.qcloudimg.com/raw/4aaaf12e011af85f8e76c24309f625c3.png)

#### 3. Enable origin-pull authentication (optional)
Origin-pull authentication is used to verify the service identity of the CDN edge server so as to prevent unauthorized access as shown below:

- Public read bucket: The CDN edge server can access the bucket directly without any authorization required, so there is need to enable origin-pull authentication.
- Private read bucket: The CDN edge server needs to be authenticated by origin-pull authentication for its service identity and can access objects in the bucket only after successful authentication. Toggle on **Origin-pull Authentication**.
![](https://main.qcloudimg.com/raw/da5fe7285a8a2932cfb015c361472202.png)

> For private read buckets, after origin-pull authentication is enabled, the CDN edge server does not need to carry a signature when accessing the origin server, and the resources cached by CDN will be delivered over the public network, which may affect the data security. Therefore, it is highly recommended to enable CDN authentication.

#### 4. Enable CDN acceleration

Click **Save** on the right and wait for about 5 minutes for the custom domain name and CDN acceleration to be completely deployed.

### Configuring Authentication
> After CDN acceleration is enabled for the custom domain name, anyone can directly access the origin server through this domain name. If your data requires privacy, please be sure to enable the authentication configuration to protect your data on the origin server.

After the custom domain name is deployed, a CDN authentication configuration link will appear in the CDN Authentication column. Click **Settings** to directly enter the CDN Console for CDN authentication configuration.
![](https://main.qcloudimg.com/raw/b0e9b2e0febc4b480a16a11f06498740.png)


### Resolving a Domain Name
After the custom domain name is connected to CDN, the system will automatically assign you a CNAME domain name (suffixed with `.cdn.dnsv1.com`). You need to complete the CNAME configuration for it at your domain name service provider. 

> The CNAME domain name cannot be accessed directly.
![CNAME](https://main.qcloudimg.com/raw/b0e9b2e0febc4b480a16a11f06498740.png)

### Disabling the Feature
On the custom accelerated domain name management page, click **Edit** to change the domain name status from **enabled** to **disabled**, click **Save**, and wait for the deployment to be completed in around 5 minutes. After that, the status of the custom accelerated domain name is changed from **enabled** to **disabled** as shown in the CDN Console.

> If you want to delete the custom domain name, you have to change its status to **disabled** if it is **enabled** before you can do so. 

You can disable and delete the domain name in the [CDN Console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).
![](https://main.qcloudimg.com/raw/39a93646587daf22120777a53b225515.png)

