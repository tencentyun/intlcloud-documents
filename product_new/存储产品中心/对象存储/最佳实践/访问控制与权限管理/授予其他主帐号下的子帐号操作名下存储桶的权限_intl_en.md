## Operation Scenarios

There are two buckets under root account A (APPID: `1250000000`): `examplebucket1-1250000000` and `examplebucket2-1250000000`, which sub-account B0 under root account B wants to manipulate to meet its business needs. This document describes how to authorize it to do so.


## Directions
#### Authorizing root account B to manipulate buckets under root account A

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) with root account A.
2. Click **Bucket List**, find the bucket to be authorized, and click its name to enter the bucket details page.
3. On the left sidebar, click **Manage Permission** to enter the bucket's permission management page.
4. Locate **Permission Policy Settings**, click **Add Policy**, and select or enter the items as shown below:
	- **Effect**: Allowed.
	- **User**: Click "Add User", select root account for user type, and enter root account B's UIN for account ID, such as 100000000002.
	- **Resource**: Select an option as needed (the entire bucket by default).
	- **Resource Path**: It needs to be entered only for specified resources.
	- **Operation**: Click "Add Operation" and select all operations. If you want to grant root account B permissions to only certain operations, you can also select one or more operations as needed.
	- **Filter**: Add a filter or leave it blank as needed.
	![](https://main.qcloudimg.com/raw/f7a35ecadb310f6871cc6eab37a9de9d.png)
5. Click **OK** to grant root account B specified permissions to the bucket.
6. If you need to authorize root account B to manipulate other buckets, repeat the above steps.

#### Authorizing sub-account B0 to manipulate buckets under root account A

1. Log in to the CAM Console with root account B and go to the [Policy](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create Custom Policy** > **Create by Policy Syntax**, select a blank template, and click **Next**.
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
Specifically, "1250000000" in `uid/1250000000` is the uid of root account A, and `examplebucket1-1250000000` is the bucket name to be authorized. The `examplebucket1-1250000000/*` bucket resource can be replaced with `*`, meaning that all buckets under root account A that root account B are authorized to manipulate will be authorized to sub-account B0.
![](https://main.qcloudimg.com/raw/fa7d470babcfb09bd5011599708e0d63.png)
4. Click **Create Policy**.
5. Locate the created policy in the **policy list** and click **Associate User/User Group** on the right.
![](https://main.qcloudimg.com/raw/430c7fb38b6da3fa9ddc59c14ca61d66.png)
6. In the **Associate User/User Group** pop-up window, select sub-account B0 and click **OK**.
![](https://main.qcloudimg.com/raw/887b766bd8027e0fcb72607e1b34feb3.jpg)
7. Then, the authorization is completed, and you can use the key of sub-account B0 to manipulate the bucket under root account A.
