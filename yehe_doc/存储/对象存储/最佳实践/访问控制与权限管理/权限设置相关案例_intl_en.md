## Granting Permission via Bucket Policy

### Preparations

1. Create a bucket.
Granting permissions through a bucket policy involves specific buckets, so you need to [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) first. For authorization at the account level, see [Granting Permission via CAM](#cam) in this document.
2. Prepare the UIN of the account to be authorized.
This document assumes that the root account that owns the target bucket has a UIN of 100000000001 and its sub-account has a UIN of 100000000011. The sub-account needs to be authorized to access the destination bucket.
>?
>- To query sub-accounts created under the root account, log in to the CAM console and view them in the [User List](https://console.cloud.tencent.com/cam).
>- To create a sub-account, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
>
3. Open the **Add Policy** dialog.
Click the destination bucket and select **Permission Management** > **Permission Policy Settings** > **Visual Editor** > **Add Policy**. Then, you can configure a policy as instructed in the authorization cases below. For detailed directions, see [Adding a Bucket Policy](https://intl.cloud.tencent.com/document/product/436/30927).

The following lists several authorization cases, which you can configure as needed.

### Authorization cases

#### Case 1: Granting a sub-account full permissions for a specified directory
The configuration information is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Select **Allow**. |
| User | Select **Sub-account** and enter a sub-account UIN, which must be a sub-account under the current root account, such as `100000000011`. |
| Resource | Select a specific resource path, such as `folder/sub-folder/*`. |
| Actions | Select **All Actions**. |



#### Case 2: Granting a sub-account read permission for all files in a specified directory

The configuration information is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Select **Allow**. |
| User | Select **Sub-account** and enter a sub-account UIN, which must be a sub-account under the current root account, such as `100000000011`. |
| Resource | Select a specific resource path, such as `folder/sub-folder/*`. |
| Actions  | Select **Read Operation (listing objects is included)**. |



#### Case 3: Granting a sub-account read/write permission for specified files

The configuration information is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Select **Allow**. |
| User | Select **Sub-account** and enter a sub-account UIN, which must be a sub-account under the current root account, such as `100000000011`. |
| Resource | Select a specific object key, such as `folder/sub-folder/example.jpg`. |
| Actions | Select **All Actions**. |




#### Case 4: Granting a sub-account read/write permission for all files in a specified directory while denying read/write permission for specified files in the directory

For this case, you need to add an **allow** policy and a **deny** policy.

1. First, add the **allow** policy. The configuration information is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Select **Allow**. |
| User | Select **Sub-account** and enter a sub-account UIN, which must be a sub-account under the current root account, such as `100000000011`. |
| Resource | Specify a directory prefix, such as `folder/sub-folder/*`. |
| Actions | Select **All Actions**. |




2. Then, add the **deny** policy. The configuration information is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Select **Deny**. |
| User | Select **Sub-account** and enter a sub-account UIN, which must be a sub-account under the current root account, such as `100000000011`. |
| Resource | Specify the object key to be denied access, such as `folder/sub-folder/privateobject`. |
| Actions | Select **All Actions**. |




#### Case 5: Granting a sub-account read/write permission for files with a specified prefix

The configuration information is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Select **Allow**. |
| User | Select **Sub-account** and enter a sub-account UIN, which must be a sub-account under the current root account, such as `100000000011`. |
| Resource | Specify a prefix, such as `folder/sub-folder/prefix`. |
| Actions | Select **All Actions**. |




<span id=cam></span>

## Granting Permission via CAM

If you need to grant permissions at the account level, see the following documents:


- [Authorizing Sub-account Full Access to Specific Directory](https://intl.cloud.tencent.com/document/product/598/11084)
- [Authorizing Sub-account Read-only Access to Files in Specific Directory](https://intl.cloud.tencent.com/document/product/598/11085)
- [Authorizing Sub-account Read/Write Access to Specific File](https://intl.cloud.tencent.com/document/product/598/11086)
- [Authorizing Sub-account Read-only Access to COS Resources](https://intl.cloud.tencent.com/document/product/598/11087)
- [Authorizing a Sub-account Read/Write Access to All Files in Specified Directory Except Specified Files](https://www.tencentcloud.com/document/product/598/11088)
- [Authorizing Sub-account Read/Write Access to Files with Specified Prefix](https://intl.cloud.tencent.com/document/product/598/11090)
- [Authorizing Another Account Read/Write Access to Specific Files](https://www.tencentcloud.com/document/product/598/11091)

