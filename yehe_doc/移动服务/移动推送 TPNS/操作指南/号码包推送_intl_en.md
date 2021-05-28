
## Use Cases

After you get a batch of user accounts from a third-party data platform or business backend, when launching a marketing campaign for such users, you don't need to call the **single account push** API separately; instead, you can directly use the **batch account push** feature to push messages to accounts in batches.

>! The abovementioned **accounts** must be bound to a TPNS token. For detailed directions, please see [Binding an account (Android)](https://intl.cloud.tencent.com/document/product/1024/30715#binding-an-account) or [Adding account (iOS)](https://intl.cloud.tencent.com/document/product/1024/30727#adding-account).

## Directions

### Console

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns). 
2. Find the application for which to configure batch push and select **Create Push** in its **Operation** column to enter the **Create Push** page.
3. In the **Push Target** configuration item, select **Batch accounts**, upload an account package file, and choose to push to the **recent** or **all** devices bound to each account as shown below:
![](https://main.qcloudimg.com/raw/f82192f04eb01a6426382d28d1f5976b.png)
>? Requirements for the uploaded account package:
> - Account package file name: [1, 100] characters
> - Account package format and size: `.zip`, `.txt`, or `.csv` file within 100 MB
> - `.zip` file requirements: can contain a single `.txt` or `.csv` file but not folders
> - `.txt` file requirements: encoded in UTF-8; one account ([2, 100] characters) per row
> - `.csv` file requirements: one column only; one account ([2, 100] characters) per row
> 
2. Click **Preview**. After confirming that the push configuration is correct, click **Confirm** to complete the account package push task.


### RESTful API

#### Step 1. Call the account package upload API

Upload your account package file as instructed in [Account Package Upload API](https://intl.cloud.tencent.com/document/product/1024/33765). After the call succeeds, an `upload_id` will be returned, such as 11231.

#### Step 2. Call the push API

When you call the [push API](https://intl.cloud.tencent.com/document/product/1024/33764), set `audience_type` (push target) to `package_account_push` (account package push), enter the `upload_id` (such as 11231) obtained in [Step 1](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0.E5.8F.B7.E7.A0.81.E5.8C.85.E6.8E.A5.E5.8F.A3), and choose to push to the **recent** or **all** devices bound to each account by setting the `account_push_type` field.

#### Sample push

The following sample pushes a message to users who have won prizes in a marketing campaign:

```
{
    "audience_type": "package_account_push",
    "upload_id": 11231,
	"account_push_type":0,
    "message_type": "notify",
    "message": {
        "title": "Congrats on winning in the campaign",
        "content":"Get online to claim your prize!"		
    },
    "platform": "android"
}
```

