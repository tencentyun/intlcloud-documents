>!Starting from May 9, 2022, Cloud Object Storage (COS) will stop supporting default CDN acceleration domains for buckets that have never used them. This change will not affect buckets that are using or once used default CDN acceleration domains. However, we recommend you switch to custom CDN acceleration domains instead. For operation guide on custom CDN acceleration, see [Enabling Custom CDN Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

### Configuration instructions

A default CDN acceleration domain name is a CDN acceleration domain name COS automatically assigns to a bucket in the format of `BucketName-APPID.file.myqcloud.com`. After it is enabled, you can use it to enjoy an accelerated access experience.

#### Directions

#### 1. Select a bucket
Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and click the name of a bucket that you want to enable acceleration for.

#### 2. Enter the configuration page
>!**Domain Management** is inaccessible if you have never used the CDN service. To activate it, go to the [CDN console](https://console.cloud.tencent.com/cdn).

Click **Domains and Transfer** > **Default CDN Acceleration Domain** and find the **Default CDN Acceleration Domain** area. By default, the value of **Status** is **Disabled**. Click **Edit**, change the status to **Enabled**, and set other configuration items as described below.

 - **Acceleration Domain Name**: A default CDN acceleration domain name is a CDN acceleration domain name COS automatically assigns to a bucket in the format of `BucketName-APPID.file.myqcloud.com`. After it is enabled, you can use it to enjoy an accelerated access experience.
 - **Acceleration Region**: Supports acceleration for the Chinese mainland, outside the Chinese mainland, as well as global acceleration (global acceleration means acceleration for buckets across all regions).
 - **Origin Server Type**: **Default Endpoint** is selected by default. If a static website is enabled for a bucket that serves as an origin, and you want to accelerate the static website, select **Static Website Endpoint**. For more information, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).
 - **Origin Domain**: COS origin's domain name, which is automatically generated based on the bucket name and region when you create a bucket. It’s important to distinguish it from the default CDN acceleration domain name.

#### 3. Enable origin-pull authentication (optional)

>! For private-read buckets, after origin-pull authentication and CDN service authorization are enabled, the CDN edge node will no longer need to carry a signature when accessing the origin, and the resources cached by CDN will be delivered over the public network. In such case, data security will be under threat. Therefore, we recommend that you enable CDN authentication.

Origin-pull authentication is used to verify the service identity of the CDN edge node so as to prevent unauthorized access. Find the details below.
- Public-read bucket: The CDN edge node can access the bucket without any authorization, so there is no need to enable origin-pull authentication.
- Private-read bucket: The CDN edge node needs to go through origin-pull authentication to get its service identity verified before it can access the objects in the bucket.


(1) Complete the CDN service authorization.

>?Before enabling origin-pull authentication, you need to add the CDN service authorization.

Follow the steps below:
Adding CDN service authorization will enable the CDN edge node to assume the service identity which allows it to perform operations on a bucket. Find the details below.
- Public-read bucket: The CDN edge node can access the bucket without any authorization, so there is no need to add CDN service authorization.
- Private-read bucket: The CDN edge node needs a special service identity to access the bucket. Click **Add CDN Service Authorization** to grant the CDN edge node the service identity, indicate your agreement to the authorization, and click **OK**.

After the CDN service authorization is completed, the CDN edge node can perform three operations on the bucket: `Get Object`, `Head Object`, and `Options Object`. The authorization will be automatically written into the bucket access policy (see below for an example). Then, the CDN edge node does not need to do anything else while forwarding traffic to the origin.

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

(2) After authorization, enable **Origin-pull Authentication**.




#### 4. Enable CDN acceleration
After clicking **Save**, you will see that the default acceleration domain name is being deployed (which is expected to be completed in about 5 minutes).

#### 5. Configure CDN authentication

>! After the default CDN acceleration is enabled, anyone can access the origin through this domain name. If your data requires privacy, be sure to enable the authentication to protect your data on the origin.

 - After you enable the default CDN acceleration domain and origin-pull authentication, the CDN authentication status will appear in the **Default CDN Acceleration Domain** area. You can click **Authentication Configuration** to go to the **Access Control** page of the corresponding domain.

 - Alternatively, you can log in to the [CDN console](https://console.cloud.tencent.com/cdn), click **Domain Management**, select **Default CDN Acceleration Domain**, and click **Access Control** > **Authentication Configuration**. For detailed configuration directions, see [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237).

#### 6. Disable the feature

After the above steps are completed, default CDN acceleration is enabled. You can disable it in the following ways:

- On the **Default CDN Acceleration Domain** page, click **Edit**, change the status to **Disabled**, click **Save**, and wait for about 5 minutes for the deployment to complete. After that, the domain status will be changed to **Deactivated** in the CDN console.
- You can deactivate or delete the domain name in the [CDN console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).



>! When you delete a domain name in the CDN console, you are deleting a CDN acceleration record of the default CDN acceleration domain name, not the domain name itself. To enable CDN acceleration, you can activate the domain name again in the COS console.
>


