## Scenarios
- Scenarios that require low latency and high download speed.
- Scenarios where gigabytes to terabytes of data need to be transferred across regions, countries, and continents.
- Scenarios where the same content needs to be downloaded frequently and repeatedly.

## Notes
For information on domain name definition, CDN origin-pull authentication, and CDN authentication configuration, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).

The configuration of CDN origin-pull authentication and CDN authentication may determine whether the access to a bucket on origin server via CDN acceleration domain name and COS endpoint is possible, as shown below:

| Bucket access permission | CDN origin-pull authentication | CDN authentication | Origin server can be accessed via CDN acceleration domain name | Origin server can be accessed via<br>COS endpoint | Scenarios |
| ------------------- | ------------ | ------------ | --------------- | --------------- | ------------ |
| Public read | Disabled | Disabled | Yes | Yes | Site-wide public access |
| Public read | Enabled | Disabled | Yes | Yes | Not recommended |
| Public read | Disabled | Enabled | URL authentication is required | Yes | Not recommended |
| Public read | Enabled | Enabled | URL authentication is required | Accessible | Not recommended |
| Private read + CDN authorization | Enabled | Enabled | URL authentication is required | COS authentication is required |  Full link protection |
| Private read + CDN authorization | Disabled | Enabled | URL authentication is required | COS authentication is required | Not recommended |
| Private read + CDN authorization | Enabled | Disabled | Yes | COS authentication is required | Origin server protection |
| Private read + CDN authorization | Disabled | Disabled | No | COS authentication is required | Not recommended |
| Private read | Disabled | Enabled/Disabled | No | COS authentication is required | CDN is unavailable |

>!The **Origin site protection** above is useful in cases where your data cached on CDN edge nodes may be maliciously pulled due to lack of CDN authentication. Therefore, it is strongly recommended to enable CDN authentication as well for data security concerns.

## Using Default CDN Acceleration Domain Name

A default CDN acceleration domain name is automatically assigned by COS to a bucket in the format of `<BucketName-APPID>.file.mycloud.com`. You can choose whether to enable it as needed.

### Directions
#### 1. Select a bucket
Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the bucket you want to enter the bucket management page.
![](https://main.qcloudimg.com/raw/7537a96a0276f31d7ec0a33a6a7a79b1.png)


#### 2. Go to Domain Management
>!**Domain Management** is inaccessible if you have never used the Tencent Cloud CDN service before. To activate it, go to the [CDN Console](https://console.cloud.tencent.com/cdn).

Click **Domain Management** on the left, and find **Default CDN Acceleration Domain**, whose status is **Off** by default. Change the status to “on”.
![](https://main.qcloudimg.com/raw/a027d3ae128de8349db903b8f1833019.png)
**Acceleration Region**: includes “Chinese mainland”, “outside Chinese mainland”, and “global”, where the global acceleration applies to buckets across all regions.
**Origin Server Type**: the **Default origin server** is selected by default. If a static website is enabled for your bucket, you can set this field to **Static website origin server**. For more information, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).

#### 3. Add CDN authorization (optional)

Adding CDN authorization is to grant a CDN edge server the service identity which allows it to perform operations on a bucket. Please find the details below.

- Public read bucket: the CDN edge server can access the bucket without any authorization, so there is no need to add CDN authorization.
- Private read bucket: the CDN edge server needs a granted service identity to access the bucket. Click **Add CDN Service Authorization** to grant such service identity, select **I agree to the above authorization**, and click **OK**.

After the authorization is added, the CDN edge server can perform GET Object, Head Object, and Options Object on the bucket.

![](https://main.qcloudimg.com/raw/ca62b2f78b7587245efbe0b03f84adee.png)

After the permission is granted, it will be automatically written into the bucket access policy (see below for an example). Then, you will not need to do anything else as the CDN edge server pulls data from COS.

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
>!You need to add the CDN authorization before you can enable origin-pull authentication.

Origin-pull authentication is used to verify the service identity of the CDN edge server so as to prevent unauthorized access. Please find the details below.
- Public read bucket: the CDN edge server can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
- Private read bucket: the CDN edge server needs to be verified by origin-pull authentication. Only then can the edge server access the objects in a COS bucket. To enable the authentication, toggle on **Origin-pull Authentication** and click **Save**.
![](https://main.qcloudimg.com/raw/58c92ca577ca99d1fd5d9523e25dcec4.png)


>!For private read buckets enabled for origin-pull authentication and CDN authorization, the CDN edge server need not include a signature in its access request to your origin server. However, your resources cached on CDN will be distributed over public network, putting your data security under threat. Therefore, it is highly recommended to enable CDN authentication.

#### 5. Enable CDN acceleration
After clicking **Save**, you will see that the default CDN acceleration domain is being deployed (which is expected to be completed in about 5 minutes).

### Configuring CDN authentication
>!After a default CDN acceleration domain name is enabled, anyone can access your origin server through this domain name. If your data on the origin server requires privacy, please be sure to enable CDN authentication.

Once you enable the default CDN acceleration domain and origin-pull authentication, you can click on the **authentication configuration** link next to **CDN Authentication** to open the CDN console and configure CDN authentication.
![](https://main.qcloudimg.com/raw/a878861f79ea47e27c127c5b5dff4eb4.png)

You can also directly configure it from the [CDN Console](https://console.cloud.tencent.com/cdn) by clicking **Domain Management** > **Management** (for the corresponding domain name) > **Security Configuration**. For detailed configuration directions, see [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237).


### Disabling the domain
- Change the status of **Default CDN Acceleration Domain** to **Off**, and click **Save**. The change will be deployed in around 5 minutes. After that, the domain name will be displayed as **Disabled** in the CDN Console.
![](https://main.qcloudimg.com/raw/7a3033a50a1d6260a6ae508c7d903a28.png)

- You can disable or delete the domain name in the [CDN Console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).
>!When you delete a custom CDN acceleration domain name in the CDN console, you are actually only deleting its CDN acceleration record, not the domain name itself. You can enable it again using the COS console.


## Using Custom CDN Acceleration Domain Name
You can bind a custom CDN domain name with a bucket in the COS Console to speed up access to the bucket through this domain. You will also need to add a CNAME record for this domain at your domain service provider.
>! Currently, you must enable Tencent Cloud CDN service to use a custom CDN domain name in COS.
1. For domain names connected to a CDN node in Chinese mainland, you need to complete ICP filing. You are not required to do so through Tencent Cloud though.
2. For domain names connected to a CDN node outside Chinese mainland, ICP filing is not required, but please note that your data and operations in Tencent Cloud still need to comply with local laws and regulations as well as [General Service Level Agreements](https://intl.cloud.tencent.com/document/product/301/12905).

### Directions
>!You can add a custom CDN acceleration domain name in both COS Console and CDN Console. For more information on how to do so in the CDN Console, see [Connecting Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

#### 1. Select a bucket
Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the bucket to be accelerated to enter the bucket.
![](https://main.qcloudimg.com/raw/7537a96a0276f31d7ec0a33a6a7a79b1.png)


#### 2. Add a custom CDN acceleration domain name
Click **Domain Management** to enter the configuration page. Click **Add Domain** in the Custom CDN Acceleration Domain section to start the configuration.
- **Domain Name**: enter the domain name you have purchased (such as `www.example.com`).
- **Acceleration Region**: supports CDN acceleration for Chinese mainland, Hong Kong, China, and overseas regions, and global acceleration for buckets across all regions.
- **Origin Server Type**: the **Default origin server** is selected by default. If a static website is enabled for the selected bucket, you can set this field to **Static website origin server**.

![](https://main.qcloudimg.com/raw/4aaaf12e011af85f8e76c24309f625c3.png)


#### 3. Enable origin-pull authentication (optional)
Origin-pull authentication is used to verify the service identity of the CDN edge server so as to prevent unauthorized access. Please find the details below.

- Public read bucket: the CDN edge server can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
- Private-read bucket: a CDN edge server needs to be verified by origin-pull authentication before it can access the objects in the bucket.
![](https://main.qcloudimg.com/raw/da5fe7285a8a2932cfb015c361472202.png)
>!For private read buckets enabled for origin-pull authentication and CDN authorization, the CDN edge server need not include a signature in its access request to your origin server. However, your resources cached on CDN will be distributed over public network, putting your data security under threat. Therefore, it is highly recommended to enable CDN authentication.

#### 4. Enable CDN acceleration

Click **Save** under **Actions**. In about 5 minutes, this new custom CDN acceleration domain name will be deployed.

### Configuring CDN authentication
>!After a default CDN acceleration domain name is enabled, anyone can access your origin server through this domain name. If your data on the origin server requires privacy, please be sure to enable CDN authentication.

After the custom domain name is deployed, a CDN authentication configuration link will appear next to **CDN authentication**. To configure it, click the link to go to the CDN Console. For detailed directions, see [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237).
![](https://main.qcloudimg.com/raw/b0e9b2e0febc4b480a16a11f06498740.png)


### Domain resolution
Once a custom domain name is added to Tencent Cloud CDN, a CNAME domain suffixed with `.cdn.dnsv1.com` will be automatically assigned to you. You need to record this CNAME at your domain service provider. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

>!You will not be able to directly access the CNAME domain name.
![](https://main.qcloudimg.com/raw/b0e9b2e0febc4b480a16a11f06498740.png)

### Disabling the domain
Click **Edit** under **Actions**, change the status to **offline**, and click **Save**. The domain will then be disabled in around 5 minutes. After that, the domain will be displayed as **Disabled** in the CDN Console.

>!You can delete a custom CDN domain name only after changing its state to **offline**. Alternatively, you can go to the [CDN Console](https://console.cloud.tencent.com/cdn) to disable or delete it. For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).



