## Use Cases
- Scenarios with high requirements for response delay and download speed.
-  Scenarios where cross-region, cross-border or cross-continent data transfer reaching GB or TB-level is required.
- Scenarios where the same content needs to be downloaded frequently.

## Description
For more information about the domain name definition, CDN origin-pull authentication, and CDN authentication configuration, see [CDN Acceleration Overview](/document/product/436/18669).

The configurations of CDN origin-pull authentication and CDN authentication determine whether the access to a bucket on origin server via CDN accelerated domain name and COS domain name is possible, as shown below:

| Bucket Access Permission | CDN Origin-Pull Authentication | CDN Authentication | CDN Accelerated Domain Name | Scenarios |
| ------------------- | ------------ | ------------ | --------------- | --------------- | ------------ |
| Public read | Disabled | Disabled | Yes | Yes | Public access to the entire website |
| Public read | Enabled | Disabled | Yes | Yes | Not recommended |
| Public read | Disabled | Enabled | URL authentication is required | Yes | Not recommended |
| Public read | Enabled | Enabled | URL authentication is required | Yes | Not recommended |
| Private read + CDN service authorization | Enabled | Enabled | URL authentication is required | COS authentication is required | Protection throughout link |
| Private read + CDN service authorization | Disabled | Enabled | No | COS authentication is required | Not recommended |
| Private read + CDN service authorization | Enabled | Disabled | Yes | COS authentication is required | Origin server protection |
| Private read + CDN service authorization | Disabled | Disabled | No | COS authentication is required | Not recommended |
| Private read | Disabled | Enabled or disabled | No | COS authentication is required | CDN is unavailable |

## Configuring CDN Acceleration for Default Accelerated Domain Names

Default accelerated domain name (such as ` <bucketname>-<APPID>.file.mycloud.com`) is a CDN accelerated domain name automatically assigned by COS to a bucket. You can enable or disable it at your option.

### Enable the feature
#### 1. Select a bucket
Log in to the [COS Console](https://console.cloud.tencent.com/cos5), go to the **Bucket List** in the left pane, and then click the bucket for which you want to accelerate the content delivery to enter the bucket details page.
![](https://main.qcloudimg.com/raw/688c1dc518cb417461bc9d4645e4c41c.png)

#### 2. Enter the configuration page
Go to the **Domain Name Management** tab from the top of the bucket page. The initial status of the default accelerated domain name is **Disabled**.
![](https://main.qcloudimg.com/raw/bd56dc4366b69e9fc63729135099985f.png)

> **Notes:**
> If you have never used Tencent Cloud CDN service, you need to go to the CDN Console by clicking the external link and activate the CDN service before you can access **Domain Name Management**.
> ![](https://main.qcloudimg.com/raw/4c8b820c51746a91e837559d9325134a.png)

#### 3. Select the origin server type
Click **Edit** to change the current status to **Enabled**.

At this point, you need to select the origin server type, which defaults to XML node. If static website is enabled for the bucket which is used as the origin server, and you want to accelerate content delivery of a static website, you can set the origin server type to the static website node. For more information, see [CDN Acceleration Overview](/document/product/436/18669).
![](https://main.qcloudimg.com/raw/542a778a7177e3aae0e49580aaefe348.png)

#### 4. Add CDN service authorization (optional)

Adding a CDN service authorization is to grant a CDN edge server the service identity to perform operations on a bucket, as described below:

- Public-read bucket: A CDN edge server can access the bucket directly without any authorization. No CDN service authorization is required.

- Private-read bucket: A CDN edge server need to be granted a special service identity to access the bucket. Click **Add CDN Service Authorization** to grant the service identity to the CDN edge server, and then select **Confirm To Grant the Authorization** and click **OK**.

After the authorization is added, the CDN edge server can perform operations (GET Object, Head Object, and Options Object) on the bucket.

![](https://main.qcloudimg.com/raw/a4654ca919ad72479143a47017fba34b.png)

  When the authorization is granted, the system automatically writes it to the bucket access policy as shown below, and then a CDN node does not need to perform any operation before the origin-pull.

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
            "qcs::cam::uin/************:service/cdn"
          ]
        },
        "Resource": [
          "qcs::cos:ap-chengdu:uid/**********:sdobc-**********/*"
        ]
      }
    ],
    "version": "2.0"
  }
```

#### 5. Enable origin-pull authentication (optional)
>**Note:**
> You need to add the CDN service authorization before you can enable origin-pull authentication.

Origin-pull authentication is used to verify the service identity of a CDN edge server to prevent unauthorized access, as described below:
- Public-read bucket: A CDN edge server can access the bucket directly without any authorization. No CDN service authorization is required.
- Private-read bucket: A CDN edge server needs to go through origin-pull authentication to get its service identity verified before it can access the objects in the bucket. Click to enable **Origin-Pull Authentication**.
![](https://main.qcloudimg.com/raw/9b662fe72d91ff15e2e664ef4ffbc1c0.png)

> **Notes:**
> For private-read buckets, if origin-pull authentication and CDN service authorization are enabled, CDN edge servers can access the origin server without a signature, and cached resources in CDN are delivered over the Internet. This will affect the data security. Therefore, it is highly recommended to enable CDN authentication.

#### 6. Enable CDN acceleration
The deployment of CDN acceleration is completed 5 minutes after you click **Save**.

### Configure authentication
After the default acceleration domain name and origin-pull authentication are enabled, the status of CDN authentication is displayed at the bottom of management interface of the default accelerated domain name. You can directly go to the CDN security configuration page of the domain name by clicking **Authentication Configuration**.
![](https://main.qcloudimg.com/raw/f836aa8efc9b07b79d47a203c697aa49.png)

You can go to CDN authentication configuration page from [CDN Console](https://console.cloud.tencent.com/cdn) by clicking **Domain Name Management** -> **Management** for the domain name -> **Security Configuration**.

For more information, see [Authentication Configuration](https://cloud.tencent.com/document/product/228/13677).

#### Note
After CDN acceleration is enabled for the default domain name, anyone can access the origin server via the domain name. Therefore, if you need to keep you data private, be sure to protect your data in the origin server by enabling **Authentication Configuration**.

### Disable the feature
- In the management interface of the default accelerated domain name, click **Edit** to change its status from **Enabled** to **Disabled**, and then click **Save**. It takes about 5 minutes to complete the deployment. After the deployment is completed, the status of the domain name will change from **Enabled** to **
- Disabled** on the CDN Console.
![](https://main.qcloudimg.com/raw/e7dfd0da74d0d8d48f7e53425b0adde0.png)

- You can disable/delete the domain name in the [CDN Console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://cloud.tencent.com/document/ Product/228/5736).
  > **Notes:**
  > Only the records of the default accelerated domain name during CDN acceleration are deleted from the CDN Console. The default accelerated domain name is not deleted. You can enable it again in the COS console.

![](https://main.qcloudimg.com/raw/4d3f7485a78be5f18c3e3ac3ec0a4447.png)

## Configuring CDN Acceleration for Custom Accelerated Domain Name
You can bind a custom domain name to the bucket through the COS Console. After binding, you can enable CDN acceleration to accelerate the access to the bucket via the custom domain name. When binding a custom domain name, you need to add CNAME resolution at the service provider of the custom domain name.
> **Notes:** 
> The custom domain name you bind to the bucket needs to go through the [filing](https://cloud.tencent.com/product/ba) procedures with MIIT before it can be accessed. 

### Enable the feature
> **Notes:**
> You can add custom domain name and enable CDN acceleration in both the COS Console and CDN Console. To add the custom domain name on the CDN Console, see [Adding Domain Names to CDN](https://cloud.tencent.com/document/product/228/5734).

#### 1. Select the bucket to be bound to custom domain name
Log in to the [COS Console](https://console.cloud.tencent.com/cos5), go to the **Bucket List** in the left pane, and then click the bucket for which you want to set the domain name to enter the bucket details page.
![](https://main.qcloudimg.com/raw/688c1dc518cb417461bc9d4645e4c41c.png)

#### 2. Add custom domain name
Go to the **Domain Management** tab, and click **Add Domain Name** in the second column **Custom Accelerated Domain Name**, and then enter the custom domain name to be bound.
![](https://main.qcloudimg.com/raw/c1c93c254856864e7a9f3879ebad4820.png)

#### 3. Select the origin server type
The origin server type usually defaults to XML node. If static website is enabled for the selected bucket, and you want to accelerate the content delivery of a static website, you can set the origin server type to static website node. For more information about XML and static website nodes, see the "Overview".
![](https://main.qcloudimg.com/raw/826d747660b2bad5f4aaeddc6e26e697.png)

#### 4. Enable origin-pull authentication (optional)
Origin-pull authentication is used to verify the service identity of a CDN edge server to prevent unauthorized access, as described below:

- Public-read bucket: A CDN edge server can access the bucket directly without any authorization. No CDN service authorization is required.
- Private-read bucket: A CDN edge server needs to go through origin-pull authentication to get its service identity verified before it can access the objects in the bucket. Click to enable **Origin-Pull Authentication**.
![](https://main.qcloudimg.com/raw/610dbfab9d3f9f20288f286b099e7fbe.png)

> **Notes:**
> For private-read buckets, if origin-pull authentication is enabled, CDN edge servers can access the origin server without a signature, and cached resources in CDN are delivered over the Internet. This will affect the data security. Therefore, it is highly recommended to enable CDN authentication.

#### 5. Enable CDN acceleration

The addition of custom domain name and deployment of CDN acceleration are completed 5 minutes after you click **Save** on the right.

### Configure authentication
After the custom domain name is added, the domain name status will become **Enabled**. The link for setting CDN authentication feature will be displayed in the CDN authentication column. Click **Settings** to enter the CDN Console to configure CDN authentication. For more information, see [Authentication Configuration](https://cloud.tencent.com/document/product/228/13677).
![](https://main.qcloudimg.com/raw/2b6cca677934b91874657bea693cb7f5.png)

#### Note
- After CDN acceleration is enabled for the default domain name, anyone can access the origin server via the domain name. Therefore, if you need to keep you data private, be sure to protect your data in the origin server by enabling **Authentication Configuration**.

### Resolve domain names
After the custom domain name is added to the CDN, the system will automatically assign you a CNAME domain name suffixed with `.cdn.dnsv1.com`. You need to complete the CNAME configuration at the domain name service provider. For more information, see [CNAME Configuration](https://cloud.tencent.com/document/product/228/3121).

> **Notes:**
> CNAME domain cannot be accessed directly.
![](https://main.qcloudimg.com/raw/ce416e52cac3a86a8c73955d208ad26e.png)

### Disable the feature
-  In the management interface of default accelerated domain name, click **Edit** to change the domain name status from **Enabled** to **Disabled**. The feature is disabled about 5 minutes after you click **Save**. The status of the custom accelerated domain name on the CDN Console will change from **Enabled** to **Disabled**.

  > **Notes:**
  > A custom domain name with a status of **Enabled** cannot be deleted. You need to change its status to **Disabled** to delete it.
  ![](https://main.qcloudimg.com/raw/c6e92d1bfbf799cb5dfc1c94cff7ce6a.png)

- You can disable/delete the domain name in the [CDN Console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://cloud.tencent.com/document/product/228/5736).
  ![](https://main.qcloudimg.com/raw/4d3f7485a78be5f18c3e3ac3ec0a4447.png)

