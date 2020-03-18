## Granting authorization through bucket policy (Policy)

### Preparations

#### 11. Creating Bucket
Granting authorization through bucket policy (Policy) only targets specified buckets, and you need to [create a bucket] first (https://intl.cloud.tencent.com/document/product/436/13309). For authorization on account dimension, please refer to [Granting authorization through access management (CAM)](#cam) in this document.
2. Prepare UIN of the account to be authorized
This document assumes that the primary account who owns the target bucket has a UIN of 100000000001, and that for its sub-account is 100000000011. The sub-account needs to be authorized to access the destination bucket.
>
>- To query sub-accounts created under the main account, log into the CAM Console and view them under [User List](https://console.cloud.tencent.com/cam).
>- To create a new sub-account, please refer to the [Create New Sub-User](https://intl.cloud.tencent.com/document/product/598/13674) document.
3. Open the [Add Policy] dialog box
Enter [Permission Management] of the destination bucket, select [Policy Permission Settings]> [Graphic Settings], click to open the [Add Policy] dialog box, and then configure following the authorization cases in this document. For detailed instructions on how to add policies, see the [Add Bucket Policy](https://intl.cloud.tencent.com/document/product/436/30927) document.

The following lists several authorization cases, which you can configure according to actual needs.

### Authorization Cases

#### Case 1: Granting sub-accounts all permissions to a specified directory
The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account, which must be a sub-account under the current main account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified directory prefix, such as `folder/sub-folder/`, need to end with `/` |
| Operation Name | All Operations |





#### Case 2: Granting sub-accounts read permissions to files in specified directories
The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account, which must be a sub-account under the current main account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified directory prefix, such as `folder/sub-folder/`, need to end with `/` |
| Operation Name | Read operation (including list of objects) |



#### Case 3: Granting sub-accounts read and write permissions to specified files
The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account, which must be a sub-account under the current main account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified object key, such as `folder/sub-folder/exampleobject` |
| Operation Name | All Operations |





#### Case 4: Granting sub-accounts read and write permissions to all files in a specified directory, and prohibiting read and write permissions to specified files in that directory

For this case, we need to add two policies: **allow** policy and **prohibit** policy.

1. First add the **allow** policy. The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account, which must be a sub-account under the current main account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified directory prefix, such as `folder/sub-folder/`, need to end with `/` |
| Operation Name | All Operations |




2. Then add **prohibit** policy. The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Prohibit |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account, which must be a sub-account under the current main account, such as 100000000011 |
| Resource | Specified Resource |
| Resource path | Object keys to be prohibited, such as `folder/sub-folder/privateobject` |
| Operation Name | All Operations |




5. Granting sub-accounts read and write permissions to files with specified prefixes
The configuration information is as follows:

| Configuration Item | Configuration Value |
|------|------|
| Effect | Allow |
| User Type | Sub-Account |
| Account ID | UIN of the sub-account, which must be a sub-account under the current main account, such as 100000000011 |
| Resource | Specified Resource |
| Resource Path | Specified prefix, such as `folder/sub-folder/prefix |
| Operation Name | All Operations |




<span id=cdm>

## Granting authorization through access management (CAM)

If users need to authorize the account dimension, please refer to the following documents for configuration:

- [Authorizing sub-account full access to COS resources under the account](https://intl.cloud.tencent.com/document/product/598/11083)
- [Authorizing sub-account full access to specified directory](https://intl.cloud.tencent.com/document/product/598/11084)
- [Authorizing sub-account read-only access to files in specified directory](https://intl.cloud.tencent.com/document/product/598/11085)
- [Authorizing sub-account read/write access to specified file](https://intl.cloud.tencent.com/document/product/598/11086)
- [Authorizing sub-account read-only access to COS resources](https://intl.cloud.tencent.com/document/product/598/11087)
- [Authorizing sub-account read/write access to all files in specified directory except specified files](/document/product/598/11088)
- [Authorizing sub-account read/write access to files with specified prefix](https://intl.cloud.tencent.com/document/product/598/11090)
- [Authorizing cross-account read/write access to specified file](https://intl.cloud.tencent.com/document/product/598/11091)
