## Overview

There are two buckets under root account A (`APPID`: `1250000000`): `examplebucket1-1250000000` and `examplebucket2-1250000000`, which sub-account B0 under root account B wants to manipulate to meet its business needs. This document describes how to authorize it to do so.


## Directions
#### Authorizing root account B to manipulate buckets under root account A

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) with root account A.
2. Click **Bucket List**, find the bucket to be authorized, and click its name to enter the bucket details page.
3. On the left sidebar, click **Permission Management** to enter the bucket's permission management page.
4. Find the **Permission Policy Settings** configuration item, click **Add Policy**, select a custom policy, and click **Next**.
5. Fill in the form as shown below:
  - **Policy ID**: Optional.
  - **Effect**: Allowed.
  - **User**: Click "Add User", select root account for user type, and enter root account B's UIN for account ID, such as 100000000002.
  - **Resource**: Select an option as needed (the entire bucket by default).
  - **Resource Path**: It needs to be entered only for specified resources.
  - **Operation**: Click "Add Operation" and select all operations. If you want to grant root account B permissions to only certain operations, you can also select one or more operations as needed.
  - **Filter**: Add a filter or leave it blank as needed.
6. Click **Finish** to grant root account B specified permissions to the bucket.
7. If you need to authorize root account B to manipulate other buckets, repeat the above steps.

#### Authorizing sub-account B0 to manipulate buckets under root account A

1. Log in to the CAM Console with root account B and go to the [Policy](https://console.cloud.tencent.com/cam/policy) page.
2. Select **Create by Policy Syntax** > **Create by Policy Syntax** > **Blank Template** and click **Next**.
>?Root account B can grant its sub-account B0 permissions only using a custom policy, but not a preset policy.
3. Fill in the form as shown below:
	- **Policy Name**: Designate a unique and meaningful name for the policy, such as `cos-child-account`.
	- **Remarks**: Optional; add remarks as needed.
	- **Policy Content**:
```shell
{
    "version": "2.0",
    "statement": [
        {
            "action": "cos:*",
            "effect": "allow",
            "resource": "qcs::cos::uid/1250000000:examplebucket1-1250000000/*"
        }
    ]
}
```
`1250000000` in `uid/1250000000` is the `APPID` of root account A, and `examplebucket1-1250000000` is the name of the bucket to authorize. `examplebucket1-1250000000/*` means that all buckets under root account A that have been authorized to root account B will be authorized to its sub-account B0.
4. Click **Complete**.
5. Locate the created policy in the **policy list** and click **Associate User/User Group/Role** on the right.
6. In the pop-up window, select sub-account B0 and click **OK**.
7. Then, the authorization is completed, and you can use the key of sub-account B0 to manipulate the bucket under root account A.
