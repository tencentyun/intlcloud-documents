>?
>COSBrowser for iOS v2.7.6 is used as an example here. For other versions, see [Changelog](https://github.com/TencentCloud/cosbrowser/blob/master/changelog_mobile.md).
>



<span id="ViewTheBucketList"></span>
## Viewing Bucket List

COSBrowser Mobile Version displays bucket lists by region. You can view buckets by region and click **Resources** at the bottom to view created buckets.


<span id="AddAccessPath"></span>
## Adding an Access Path

If you log in with a sub-account that has no access to the bucket list, you can add the specified path to a bucket or directory to manage resources by tapping **Add Access Path** in the upper-right corner of the bucket list page.

>? This feature is supported only for sub-accounts.


#### Directions

1. Go to the bucket list page and click **+** in the top-right corner.
2. In the pop-up operation list, click **Add Access Path** and enter an access path authorized by the root account.


<span id="CreateBucket"></span>
## Creating a Bucket

You can create a bucket by specifying the bucket name, region, and access permissions on COSBrowser Mobile Version.

#### Directions

1. In the bucket list, tap **+** in the top-right corner.
2. In the pop-up operation list, tap **Create Bucket**.
3. On the bucket creation page, configure the following information:
 - **Name**: A custom bucket name, which cannot be modified once configured. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).
 - **Region**: a COS region corresponding to the physical location where your business or users are distributed. This parameter cannot be modified once configured. For more information about regions, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
 - **Access Permissions**: Three access permissions are available for buckets by default: "Private Read/Write", "Public Read/Private Write", and "Public Read/Write". You can modify it if needed. For more information, please see [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).
4. After confirming that everything is correct, tap **OK**.
On the bucket list page, you can view the newly created bucket.


<span id="SearchBucket"></span>
## Searching for Bucket

If you have many buckets, you can enter a bucket name in the search box at the top of the bucket list page to fuzzy search for buckets.


<span id="ViewBucketBasicInfor"></span>
## Viewing Bucket's Basic Information

1. On the bucket list page, tap **...** on the right of the target bucket.
2. In the pop-up operation list, tap **Details** to view the bucket's basic information.
**Basic Information** includes bucket name, region, creation time, and MAZ status.


<span id="BucketPrivilegeManagement"></span>
## Managing Bucket Permission

You can use the COS app to set or modify bucket access permissions of the following two types.
- **Public permissions**: include private read/write, public read/private write and public read/write. For more information, see **Types of Permission** under [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).
- **User ACLs**: the root account has all bucket permissions (full control) by default. You can add sub-accounts and grant them permissions including read/write, read/write ACL, and even **full control**.


1. Go to the bucket list page and tap **...** on the right of the target bucket.
2. In the pop-up operation list, tap **Permission** to enter the bucket permission page.


<span id="ModifyPublicPermissions"></span>
### Modifying public permission

On the bucket permission page, tap a public permission configuration item to modify it.

<span id="SetUserPermissions"></span>
### Setting user permissions

On the bucket permission page, tap **Add User** to set bucket access permissions.


<span id="EditDeleteUserPermissions"></span>
### Editing or deleting bucket permission

Select the target user permission, swipe left, and click the displayed **Edit** or **Delete** button to edit or delete the user permission.


<span id="OpenGlobalAcceleration"></span>
## Enabling Global Acceleration

You can enable the global acceleration feature for your bucket on COSBrowser Mobile Version. It allows users across the world to quickly access the bucket and improves your business access success rate and stability. It can accelerate both uploads and downloads.
>? Enabling global acceleration will not affect the existing default bucket domain name. You can still use them.
>


#### Directions

1. Go to the bucket list page and tap **...** on the right of the target bucket.
2. In the pop-up operation list, tap **Transfer** to enter the transfer list page.
3. Tap the global acceleration configuration item to enable or disable it as needed.


<span id="BucketTransportConfig"></span>
## Configuring Bucket Transfer

You can enable data transfer via a custom domain name for a bucket on the **Transfer** list page.

<span id="SetUploadDomainName"></span>
### Setting upload domain name

After global acceleration is enabled for a bucket, you can specify the global acceleration endpoint for file upload to a bucket, which will be used first for file uploads once configured.

<span id="SetDownloadDomainName"></span>
### Setting download domain name

After a custom endpoint is set for a bucket, you can specify it for file download from a bucket, which will be used first for file downloads once configured.

