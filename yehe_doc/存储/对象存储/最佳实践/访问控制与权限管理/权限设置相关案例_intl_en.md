## Granting authorization through bucket policies 

### Preparations

1. Create a bucket.
Granting authorization through bucket policy (Policy) only targets specified buckets, and you need to [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) first. For authorization on account dimension, please refer to [Granting authorization through access management (CAM)](#cam) in this document.
2. Prepare the UIN of the account to be authorized
This document assumes that the root account that owns the target bucket has a UIN of 100000000001, and that its sub-account has a UIN of 100000000011. The sub-account needs to be authorized to access the destination bucket.
>?
>- To query sub-accounts created under the main account, log in to the CAM Console and view them under [User List](https://console.cloud.tencent.com/cam).
>- To create a new sub-account, please refer to the [Create New Sub-User](https://intl.cloud.tencent.com/zh/document/product/598/13674) document.
3. Open the **Add Policy** dialog box
Click the destination bucket and then select **Permission Management** > **Permission Policy Settings > Visual editor** > **Add Policy**. Then, you can configure by referring to the cases in this document. For detailed directions, please see [Adding Bucket Policies](https://intl.cloud.tencent.com/document/product/436/30927).

The following lists several authorization cases, which you can configure according to your actual needs.

### Authorization cases

#### Case 1: Granting a sub-account full permission for a specified directory
The configuration is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Allow |
| User type | Sub-account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified resource |
| Resource path | Specified directory prefix, such as `folder/sub-folder/*` |
| Operation name | All operations |




#### Case 2: Granting a sub-account read permission for all files in a specified directory
The configuration is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Allow |
| User type | Sub-account |
| Account ID | UIN of the sub-account, which must be a sub-account under the current root account, such as `100000000011` |
| Resource | Specified resource |
| Resource path | Specified directory prefix, such as `folder/sub-folder/*` |
| Operation name  | Read operations (including listing the object list) |



#### Case 3: Granting a sub-account read and write permission for specified files
The configuration is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Allow |
| User type | Sub-account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified resource |
| Resource path | Specified object key, such as `folder/sub-folder/example.jpg` |
| Operation name | All operations |





#### Case 4: Granting a sub-account read and write permission for all files in a specified directory while denying read and write permission for specified files in the directory

For this case, we need to add two policies: an **Allow** policy and a **Deny** policy.

1. First add the **allow** policy. The configuration information is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Allow |
| User type | Sub-account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified resource |
| Resource path | Specified directory prefix, such as `folder/sub-folder/*` |
| Operation name | All operations |



2. Then add the **Deny** policy. The configuration information is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Deny |
| User type | Sub-account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified resource |
| Resource path | Object keys to be denied, such as `folder/sub-folder/privateobject` |
| Operation name | All operations |




5. Granting a sub-account read and write permission for files with specified prefixes
The configuration is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Allow |
| User type | Sub-account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified resource |
| Resource path | Specified prefix, such as `folder/sub-folder/prefix` |
| Operation name | All operations |




<span id=cam>

## Granting authorization through access management (CAM)

If you need to authorize account dimension, please refer to the following documents:

- [Authorizing sub-account full access to COS resources under the account](https://intl.cloud.tencent.com/document/product/598/11083)
- [Authorizing sub-account full access to specific directory](https://intl.cloud.tencent.com/document/product/598/11084)
- [Authorizing sub-account read-only access to files in specific directory](https://intl.cloud.tencent.com/document/product/598/11085)
- [Authorizing sub-account read/write access to specific file](https://intl.cloud.tencent.com/document/product/598/11086)
- [Authorizing sub-account read-only access to COS resources](https://intl.cloud.tencent.com/document/product/598/11087)
- [Authorizing sub-account read/write access to all files in specified directory except specified files](https://intl.cloud.tencent.com/document/product/598/11088)
- [Authorizing sub-account read/write access to files with specified prefix](https://intl.cloud.tencent.com/document/product/598/11090)
- [Authorizing cross-account read/write access to specified file](https://intl.cloud.tencent.com/document/product/598/11091)
