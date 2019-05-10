### Where can I find the key information such as APPID, SecretId and SecretKey?

The second half of a bucket name is the APPID. You can check it by logging in to the [COS Console](https://console.cloud.tencent.com/cos5/bucket). To check the information such as SecretId and SecretKey, log in to the CAM Console and go to [API Key Management](https://console.cloud.tencent.com/cam/capi).

### How long is a temporary key's validity period?

A temporary key is valid for 2 hours (7,200 seconds) at most. For more information on temporary keys, see [Temporary Key Generation and Usage Guide](https://cloud.tencent.com/document/product/436/14048).

### What should I do if the key information such as APPID and SecretId is leaked?

You can delete the leaked key and create a new one. For more information, see [Key Management](https://cloud.tencent.com/document/product/436/10074).

### Does COS support file encryption?

COS supports file encryption on the server side. For more information, see [Encryption on Server](https://cloud.tencent.com/document/product/436/18145).

### Are data backups available in COS Standard, COS Infrequent Access, and COS-Archive?

COS data is stored in the underlying layer in multi-replica or erasure code mode. The distributed storage engines are distributed across multiple availability zones in a region, thus ensuring a data reliability of 99.999999999%. The multi-replica and erasure code storages are based on underlying logic and are invisible to users.

### Will the large number of requests to a bucket affect the access to other buckets under the same account?

A large number of requests to a bucket will not affect the access to other buckets under the same account, but a high request frequency will. For more information, see [Request Rate and Performance Optimization](https://cloud.tencent.com/document/product/436/13653).

### What should I do if the error "403 Forbidden" occurs or the permission is rejected when I perform upload/download and other operations?

Troubleshoot the problems by following the steps below:

1. Check that your following configuration information is correct:
   BucketName, APPID, Region, SecretId, SecretKey, etc.
2. If the above information is correct, check whether a sub-account is used. If so, check whether the sub-account has been authorized by the primary account. If it has not been authorized, log in to the primary account to authorize the sub-account.
   For more information on authorization, see [Scenarios of Permission Settings](https://cloud.tencent.com/document/product/436/12514).
3. If a temporary key is used for operation, check whether the current operation is in the Policy set when obtaining the temporary key. Otherwise, modify the relevant Policy settings.
4. If the problem persists after all the above steps are completed, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1).

### When I access a Public Read/Private Write bucket using the default domain name, all the file information of the bucket is returned. How do I hide the file list information?

You can set a permission to deny anyone's Get Bucket operation for the bucket by following the steps below:

Log in to the [COS Console](https://console.cloud.tencent.com/cos5), and select **Bucket List** to go to the bucket's **Permission Management** page.

#### Method 1:

1. Locate **Policy Permission Settings**, and click **Add Policy** under **Graphic Settings**.
2. Configure the permission as shown below, and click **OK**.
   ![Polcy图形设置](https://main.qcloudimg.com/raw/c739d31636d117757449c7e0e106ad84.png)

#### Method 2:

Locate **Policy Permission Settings**, and click **Policy Syntax** -> **Edit**, and then enter the following expression:

```
{
	"version": "2.0",
	"Statement": [{
		"Principal": {
			"qcs": [
				"qcs::cam::anyone:anyone"
			]
		},
		"Effect": "deny",
		"Action": [
			"name/cos:GetBucket"
		],
		"Resource": [
			"qcs::cos:ap-beijing:uid/125000000:testbucket-125000000/*"
		]
	}]
}
```

>
>! Replace the information in "qcs::cos:ap-beijing:uid/125000000:testbucket-125000000/*" as follows:
>- Replace "ap-beijing" with the region in which your bucket resides.
>- Replace "125000000" with your APPID.
>- Replace "testbucket-125000000" with your bucket name.
>
> The second half of the bucket name is the APPID. You can check it by logging in to the [COS Console](https://console.cloud.tencent.com/cos5/bucket).

### How do I authorize a collaborator to access the specified bucket?

Collaborator account is a special sub-account. For more information, see [Access Policy Language Overview](https://cloud.tencent.com/document/product/436/18023).

### Can I isolate permissions by buckets or other dimensions if I have multiple services that need to work with buckets?

Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) to go to the **User Management** page, where you can enable sub-accounts for different services and grant different permissions for them.

### What should I do if the error "your policy or acl has reached the limit (Status Code: 400; Error Code: PolicyFull)" occurs when I upload files or create a bucket?

The total number of ACLs and Policies for COS cannot be greater than 1,000. When the limit is exceeded, this error occurs. It is recommended to delete the ACLs or Policies you do not need any more.

>! We do not recommend using the file-level ACLs or Policies. When you call APIs or SDKs, if you do not implement ACL control over files, it is recommended to leave the ACL-related parameters (such as x-cos-acl and ACL) empty to inherit the bucket permissions.

### How do I create sub-accounts for subsidiaries or employees and grant access to specific buckets for them?

For more information, see [Authorizing Sub-Accounts to Access COS](https://cloud.tencent.com/document/product/436/11714).

### How do I generate a time-bound access link for Private Read/Write files?

For more information, see [Temporary Key Generation and Usage Guide](https://cloud.tencent.com/document/product/436/14048).

### Are COS's ACL restrictions imposed on buckets or accounts? Can I specify permissions when uploading files?

The ACL restrictions are imposed on accounts, instead of buckets. It is not recommended to specify permissions when you upload files, because this may cause the number of ACLs or Policies to exceed 1,000 and thus cause an error.

### How do I authorize specific sub-accounts to only access a certain bucket?

To grant the sub-accounts the access to a specific bucket, you can add access paths for the sub-accounts. For more information, see [Access Bucket List](https://cloud.tencent.com/document/product/436/17061).

### How do I use account A to grant the account B the write access to the buckets under account A?

For more information, see [ACL Practices](https://cloud.tencent.com/document/product/436/12470) and [CAM Practices](https://cloud.tencent.com/document/product/436/12469).

