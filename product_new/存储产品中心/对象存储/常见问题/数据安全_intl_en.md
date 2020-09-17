## FAQs About Keys

### How can I view my key information including APPID, SecretId, and SecretKey? 

The second half of a bucket name is the APPID. You can check it by logging in to the [COS Console](https://console.cloud.tencent.com/cos5/bucket). To view SecretId and SecretKey, log in to the CAM Console and go to [API Key Management](https://console.cloud.tencent.com/cam/capi).

### How long is a temporary key valid for?

By default, a temporary key is valid for 30 min (1,800 s). The maximum duration is 2 h (7,200 s) for a root account, and 36 h (129,600 s) for a sub-account. Any requests that include expired temporary keys will be rejected. For more information on temporary keys, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

### What should I do if the key information such as APPID and SecretId is leaked?

You can delete the leaked key and create a new one.

### How do I generate a time-bound access link for private-read/write files?

For more information, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048). You can set the validity period for your key.

## FAQs About ACLs and Policies

### What should I do if the error ""403 Forbidden"" occurs or the access is denied when I perform upload/download and other operations?

Troubleshoot the problem by following the steps below:

1. Check whether the following configuration information is correct:
   BucketName, APPID, Region, SecretId, SecretKey, etc.
2. If the above information is correct, check whether a sub-account is used for operation, and if yes, check whether the sub-account has been authorized by the root account. If it hasn't yet, log in using the root account to authorize the sub-account.
   For more information on authorization, see [Cases of Permission Settings](https://intl.cloud.tencent.com/document/product/436/12514).
3. If a temporary key is used, check whether the current operation is in the policy set when the temporary key is obtained, and if no, modify the relevant policy settings.
4. If the problem persists after all the above steps are completed, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1).

### When I access a public-read bucket using its default domain name, the file list is returned. How can I hide the file list?

You can set the Get Bucket permission to deny anyone for the bucket by following the steps below:

Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click the bucket in the bucket list to enter its **permission management** page.

#### Method 1:

1. Locate **Bucket Policy** and click **Graphic Settings** > **Add Policy**.
2. Configure the permission as shown below and click **OK**.
   ![Policy graphic settings](https://main.qcloudimg.com/raw/6c9262116cb78654ea5c25d9ba483595.png)

#### Method 2:

Locate **Bucket Policy**, click **Policy Syntax** > **Edit**, and enter the following expression:
```
{
  ""Statement"": [
    {
      ""Action"": [
        ""name/cos:GetBucket"",
        ""name/cos:GetBucketObjectVersions""
      ],
      ""Effect"": ""Deny"",
      ""Principal"": {
        ""qcs"": [
          ""qcs::cam::anyone:anyone""
        ]
      },
      ""Resource"": [
        ""qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*""
      ]
    }
  ],
  ""version"": ""2.0""
}
```

>Replace the information in ""qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"" as follows:
> - Replace ""ap-beijing"" with the region where your bucket resides.
> - Replace ""1250000000"" with your APPID.
> - Replace ""examplebucket-1250000000"" with your bucket name.
>
> The second half of the bucket name is the APPID. You can view it by logging in to the [COS Console](https://console.cloud.tencent.com/cos5/bucket).

### Are the ACL restrictions in COS imposed on buckets or accounts? Can I specify the permission when uploading files?

The ACL limit is imposed at the account level. It is not recommended to specify ACL permission when you upload files, because this may make the number of your bucket ACLs exceed the upper limit of 1,000, and thus cause an error.

### How do I authorize a collaborator to access the specified bucket?

A collaborator account is a special sub-account. For more information, see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).

### Can I isolate permission by bucket or other factors if I have multiple businesses that need to perform operations on the same bucket?

Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and enter the user management page where you can enable sub-accounts for different businesses and grant them corresponding permission.


### How do I create sub-accounts for subsidiaries or employees and grant them access to the specified buckets?

For more information, see [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714).

### How do I authorize specific sub-accounts to only access a certain bucket?

To grant a sub-account access to a specific bucket, you can add access paths for the sub-account. For more information, see [Accessing Bucket List Using a Sub-account](https://intl.cloud.tencent.com/document/product/436/17061).

### How do I use account A to grant account B write access to the buckets under account A?

For more information, see [ACL Practices](https://intl.cloud.tencent.com/document/product/436/12470) and [Cloud Access Management Practices](https://intl.cloud.tencent.com/document/product/436/12469).

## FAQs About Hotlink Protection

### What should I do if hotlink protection configuration does not take effect when I enable CDN acceleration and use a CDN domain name to access resources?

If you use a CDN-accelerated domain name to access resources, factors such as cache in CDN may affect the stability of hotlink protection in COS. You are recommended to log in to the [CDN Console](https://console.cloud.tencent.com/cdn) to configure hotlink protection. For more information, see [Hotlink Protection Configuration](https://intl.cloud.tencent.com/document/product/228/6292).

### Can I set an allowlist to allow access and make a resource accessible when its link is opened in a browser?

When setting hotlink protection, you can choose to allow empty referer, so that access will be allowed when a resource link is opened in a browser even if an allowlist is configured.

### The allowlist hotlink protection for the bucket ""test"" is set to allow access by `a.com`, but the web player at `a.com` cannot play video files in the bucket. What should I do?

> When you open a video link and use Windows Media Player, Flash Player, or other players to play the video on the webpage, referer in the request will be empty, leading to a miss in the allowlist. It is recommended to allow empty referer when setting the allowlist.

## FAQs About Encryption and Backup

### Does COS support file encryption?

COS supports file encryption on the server side. For more information, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

### Is data backup available in COS standard storage, standard_IA storage, and archive storage?

COS data is stored at the underlying storage layer in multi-replica or erasure code mode. The distributed storage engines are distributed across multiple AZs in a region, thus ensuring a data reliability of 99.999999999%. The multi-replica and erasure code storage is based on underlying logic and imperceptible to users.

### Will a large number of requests to a bucket affect the access to other buckets under the same account?

No, but a high request frequency will. For more information, see [Request Rate and Performance Optimization](https://intl.cloud.tencent.com/document/product/436/13653).
