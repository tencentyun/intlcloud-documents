## Granting authorization through bucket policies 

### Preparations

1. Create a bucket.
Granting authorization through bucket policies only targets specified buckets, so you need to first [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309). For authorization on account dimension, please refer to [Granting authorization through access management (CAM)] (#cam) in this document.
2. Prepare the UIN of the account to be authorized
This document assumes that the root account that owns the target bucket has a UIN of 100000000001, and that its sub-account has a UIN of 100000000011. The sub-account needs to be authorized to access the destination bucket.
>
>- To query the sub-accounts created under the main account, log in to the CAM Console and view them under [User List](https://console.cloud.tencent.com/cam).
>- To create a new sub-account, please see [Creating a Custom Sub-User](https://cloud.tencent.com/document/product/598/35978).
3. Open the [Add Policy] dialog box
Enter the [Permission Management] page of the destination bucket and scroll down to [Permission Policy Settings]. Click [Add Policy], and then configure following the examples outlined in this document. For detailed instructions on how to add policies, see [Adding Bucket Policies](https://intl.cloud.tencent.com/document/product/436/30927).

The following lists several authorization cases, which you can configure according to your actual needs.

### Authorization Cases

#### Case 1: Granting a sub-account full permission for a specified directory
The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified directory prefix, such as `folder/sub-folder/`, need to end with `/` |
| Operation Name | All Operations |



#### Case 2: Granting a sub-account read permission for the files in a specified directory
The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified directory prefix, such as `folder/sub-folder/`, need to end with `/` |
| Operation Name | Read operation (including list of objects) |



#### Case 3: Granting a sub-account read and write permission for specified files
The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified object key, such as `folder/sub-folder/exampleobject` |
| Operation Name | All Operations |



#### Case 4: Granting a sub-account read and write permission for all files in a specified directory while prohibiting read and write permission for specified files in the directory

For this case, we need to add two policies: an **allow** policy and a **prohibit** policy.

1. First add the **allow** policy. The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified directory prefix, such as `folder/sub-folder/`, need to end with `/` |
| Operation Name | All Operations |




2. Then add the **prohibit** policy. The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Prohibit |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified Resource |
| Resource path | Object keys for which access needs to be prohibited, such as `folder/sub-folder/privateobject` |
| Operation Name | All Operations |




5. Granting a sub-account read and write permission for files with specified prefixes
The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account; the sub-account in question must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified prefix, such as `folder/sub-folder/prefix |
| Operation Name | All Operations |




<span id=cdm>

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
