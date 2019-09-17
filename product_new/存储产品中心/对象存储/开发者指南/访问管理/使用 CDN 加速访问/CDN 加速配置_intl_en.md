## Applicable Scenarios
- Scenarios that requires low latency and high download speed.
- Scenarios where gigabytes to terabytes of data need to be transmitted across regions, countries, and continents.
- Scenarios where the same content needs to be downloaded frequently and repeatedly.

## Notes
For information on domain name definition, CDN origin-pull authentication, and CDN authentication configuration, see [CDN Acceleration Overview](/document/product/436/18669).

CDN origin-pull authentication and CDN authentication configuration affect how CDN accelerated domain names and COS domain names access origin server buckets. Please find the details in the table below.

| Bucket Access Permission | CDN Origin-pull Authentication | CDN Authentication Configuration | CDN Accelerated Domain Name | COS Domain Name | Scenario |
| ------------------- | ------------ | ------------ | --------------- | --------------- | ------------ |
| Public read | Disabled | Disabled | Accessible | Accessible | Site-wide public access |
| Public read | Enabled | Disabled | Accessible | Accessible | Not recommended |
| Public read | Disabled | Enabled | URL authentication required | Accessible | Not recommended |
| Public read | Enabled | Enabled | URL authentication required | Accessible | Not recommended |
| Private read + CDN service authorization | Enabled | Enabled | URL authentication required | COS authentication required | Full-linkage protection |
| Private read + CDN service authorization | Disabled | Enabled | Inaccessible | COS authentication required | Not recommended |
| Private read + CDN service authorization | Enabled | Disabled | Accessible | COS authentication required | Origin server protection |
| Private read + CDN service authorization | Disabled | Disabled | Inaccessible | COS authentication required | Not recommended |
| Private read | Disabled | Enabled or disabled | Inaccessible | COS authentication required | Unable to use CDN |

## Configuring CDN Acceleration for a Default Accelerated Domain Name

A default accelerated domain name is a CDN accelerated domain name COS automatically assigns to a bucket. The format is ` <BucketName-APPID>.file.mycloud.com`. You can **enable** or **disable** it as needed.

### Enabling the Feature
#### 1. Select a bucket
Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the bucket to be accelerated to enter the bucket.
![](https://main.qcloudimg.com/raw/7537a96a0276f31d7ec0a33a6a7a79b1.png)

#### 2. Enter the configuration page
>If you have never used Tencent Cloud CDN service before, please log into the CDN Console and activate the CDN service first.

Click **Domain Name Management** at the top of the page. The default status is off. Click **Edit** and toggle it on. 
![](https://main.qcloudimg.com/raw/a027d3ae128de8349db903b8f1833019.png)
**Origin Server Type**: The **Default origin server** is selected by default. If a static website is enabled for the bucket serving as the origin server and you want to accelerate the static website, you can set the origin server type to **Static website origin server**. For more information, see [CDN Acceleration Overview](https://cloud.tencent.com/document/product/436/18669).

#### 3. Add a CDN service authorization (optional)

Adding a CDN service authorization is to grant a CDN edge server the service identity which allows it to perform operations on a bucket. Please find the details below.

- Public read bucket: the CDN edge server can access the bucket without any authorization, so there is no need to add a CDN service authorization.
- Private read bucket: the CDN edge server needs a special service identity to access the bucket. Click **Add a CDN Service Authorization** to grant the CDN edge sever the service identity, select **I agree to the authorization above**, and click **OK**.

After the authorization is added, the CDN edge server can perform GET Object, Head Object, and Options Object on the bucket.

![](https://main.qcloudimg.com/raw/ca62b2f78b7587245efbe0b03f84adee.png)

After the authorization is granted, it will be automatically written into the bucket access policy (see below for an example). Then the CDN edge server does not need to do anything else while forwarding traffic to the origin.

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
>You need to add the CDN service authorization before you can enable origin-pull authentication.

Origin-pull authentication is used to verify the service identity of the CDN edge server so as to prevent unauthorized access. Please find the details below.
- Public read bucket: the CDN edge server can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
- Private read bucket: the CDN edge server needs to be verified by origin-pull authentication. Only verified edge server can access the objects in the bucket. To enable the authentication, toggle on **Origin-pull Authentication** and click **Save**.
![](https://main.qcloudimg.com/raw/58c92ca577ca99d1fd5d9523e25dcec4.png)

>For private read buckets, after origin-pull authentication and CDN service authorization are enabled, the CDN edge server will no longer need to carry a signature when accessing the origin server, and the resources cached by CDN will be delivered over the public network. In such case, data security will be under threat. Therefore, it is highly recommended to enable CDN authentication.

#### 5. Enable CDN acceleration
After clicking **Save**, you will see that the default accelerated domain name is being deployed (which is expected to be completed in about 5 minutes).

### Configuring Authentication
>After CDN acceleration is enabled for the default domain name, anyone can access the origin server through this domain name. If your data requires privacy, please be sure to enable the authentication to protect your data on the origin server.

After the default accelerated domain name and origin-pull authentication are enabled, a CDN authentication status prompt will appear on the default accelerated domain name management page. You can click **authentication configuration** in the prompt to enter the CDN security configuration page for the corresponding domain name.
![](https://main.qcloudimg.com/raw/a878861f79ea47e27c127c5b5dff4eb4.png)

You can also go to this page from the [CDN Console](https://console.cloud.tencent.com/cdn) by clicking **Domain Name Management** > **Management** (for the corresponding domain name) > **Security Configuration**. For detailed configuration directions, see [Authentication Configuration](https://cloud.tencent.com/document/product/228/33115).


### Disabling the Feature
- On the default accelerated domain name management page, click **Edit**, toggle the status from **on** to **off**, and click **Save**. The change will be deployed in around 5 minutes. After that, the domain name will be displayed as **Deactivated** in the CDN Console.
![](https://main.qcloudimg.com/raw/7a3033a50a1d6260a6ae508c7d903a28.png)

- You can deactivate or delete the domain name in the [CDN Console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://cloud.tencent.com/document/product/228/5736).
>When you delete a domain name in CDN console, you are deleting a CDN acceleration record of the default accelerated domain name, not the domain name itself. You can activate it again in the COS console.


## Configuring CDN Acceleration for a Custom Accelerated Domain Name
You can bind a custom domain name with a bucket in the COS Console. After that, you can enable CDN acceleration to speed up access to the bucket through the custom domain name. When binding a custom domain name with a bucket, you need to add a CNAME record to it at your domain name service provider.
>Currently, you need to enable CDN service to use a custom domain name in COS.
1. For domain names connected to a CDN node in Mainland China, you need to complete ICP filing. You are not required to do so through Tencent Cloud though.
2. For domain names connected to a CDN node outside Mainland China, ICP filing is not required, but please note that your data and operations in Tencent Cloud still need to comply with local laws and regulations as well as [Tencent Cloud Service Agreement](https://cloud.tencent.com/document/product/301/1967).

### Enabling the Feature
>You can add a custom domain name and enable CDN acceleration in both COS Console and CDN Console. For more information on how to do so in the CDN Console, see [Connect a Domain Name](https://cloud.tencent.com/document/product/228/5734).

#### 1. Select the bucket to be bound with a custom domain name
Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the bucket to be accelerated to enter the bucket.
![](https://main.qcloudimg.com/raw/51b356eb56cd09e3a3dc05725dd87ed8.png)

#### 2. Add a custom domain name
Click **Domain Name Management** to enter the domain name management page. Click **Add a Domain Name** in the custom domain name section to start the configuration.
**Domain Name**: Enter the domain name you have purchased (such as `www.example.com`).
**Origin Server Type**: The **Default origin server** is selected by default. If a static website is enabled for the selected bucket and you want to accelerate the static website, you can set the origin server type to **Static website origin server**.
![](https://main.qcloudimg.com/raw/4aaaf12e011af85f8e76c24309f625c3.png)

#### 3. Enable origin-pull authentication (optional)
Origin-pull authentication is used to verify the service identity of the CDN edge server so as to prevent unauthorized access. Please find the details below.

- Public read bucket: the CDN edge server can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
- Private read bucket: the CDN edge server needs to be authenticated by origin-pull authentication. Only verified edge server can access the objects in the bucket. To enable the authentication, toggle on **Origin-pull Authentication**.
![](https://main.qcloudimg.com/raw/da5fe7285a8a2932cfb015c361472202.png)

>For private read buckets, after origin-pull authentication is enabled, the CDN edge server will no longer need to carry a signature when accessing the origin server, and the resources cached by CDN will be delivered over the public network. In such case, data security will be under threat. Therefore, it is highly recommended to enable CDN authentication.

#### 4. Enable CDN acceleration

Click **Save** on the right. In about 5 minutes, the added custom domain name and CDN acceleration will be deployed.

### Configuring Authentication
>After CDN acceleration is enabled for the custom domain name, anyone can directly access the origin server through this domain name. If your data requires privacy, please be sure to enable the authentication configuration to protect your data on the origin server.

After the custom domain name is deployed, a CDN authentication configuration link will appear in the CDN Authentication column. Click **Settings** to directly enter the CDN Console for CDN authentication configuration. For detailed directions, see [Authentication Configuration](https://cloud.tencent.com/document/product/228/33115).
![](https://main.qcloudimg.com/raw/b0e9b2e0febc4b480a16a11f06498740.png)


### Resolving a Domain Name
After the custom domain name is connected to CDN, you will be assigned a CNAME domain name (suffixed with `.cdn.dnsv1.com`). You will need to complete the CNAME configuration through your domain name service provider. For more information, see [CNAME Configuration](https://cloud.tencent.com/document/product/228/3121).

>! You will not be able to directly access the CNAME domain name.
![CNAME](https://main.qcloudimg.com/raw/b0e9b2e0febc4b480a16a11f06498740.png)

### Disabling the Feature
On the accelerated custom domain name management page, click **Edit** to change the domain name status from **Enabled** to **Disabled**, click **Save**, and wait for the deployment to be completed in around 5 minutes. After that, the status of the accelerated custom domain name will be **Deactivated** instead of **Activated** in the CDN Console.

>You can only delete a custom domain name when its status is **disabled**. If the status is **enabled**, you will need to change it to **disabled** first. ![](https://main.qcloudimg.com/raw/dd5505b7e0cea498c23ae187dcaa539d.png)

You can deactivate or delete domain names in the [CDN Console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://cloud.tencent.com/document/product/228/5736).
![](https://main.qcloudimg.com/raw/39a93646587daf22120777a53b225515.png)
