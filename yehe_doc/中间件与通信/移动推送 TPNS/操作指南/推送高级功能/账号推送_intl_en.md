## Overview

After you get a batch of user accounts from a third-party data platform or business backend, when launching a marketing campaign for such users, you can use the **push to accounts** feature to push messages to a single or multiple accounts at a time.

>! The abovementioned **accounts** must be bound with a TPNS token. For detailed directions, please see [Binding an account (Android)](https://intl.cloud.tencent.com/document/product/1024/30715#binding-an-account) or [Adding account (iOS)](https://intl.cloud.tencent.com/document/product/1024/30727#adding-account).
>

## Directions

### Using the console

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns). 
2. Find the application for which to configure batch push and select **Create Push** in its **Operation** column to enter the **Create Push** page.
3. In the **Push Target** field, select **Account** and upload an account package file or manually enter accounts.
>? Requirements for the uploaded account package:
> - Account package filename: [1, 100] characters
> - Account package format and size: `.zip`, `.txt`, or `.csv` file within 100 MB
> - `.zip` file requirements: can contain a single `.txt` or `.csv` file but not folders
> - `.txt` file requirements: encoded in UTF-8; one account ([2, 100] characters) per row
> - `.csv` file requirements: one column only; one account ([2, 100] characters) per row
> 
4. Select the account type. You can obtain the account type from service developers. If no account type is specified, the default type is used.
5. Click **Preview**. After confirming that the push configuration is correct, click **Confirm**.


### Using RESTful APIs

#### Push to a single or multiple accounts
When you call the [push API](https://intl.cloud.tencent.com/document/product/1024/33764), set `audience_type` (push target) to `account` (single account) or `account_list` (a list of accounts) and enter a proper account type as instructed in [Account Type Value Table](https://intl.cloud.tencent.com/document/product/1024/40598).

#### Sample push

```
{
    "audience_type": "account",
		"account_list": [
			 "123456"
	 ],
	"account_type":1,
    "account_push_type":0,
    "message_type": "notify",
    "message": {
        "title": "Congrats on winning in the campaign",
        "content":"Get online to claim your prize!"
    }
}
```

#### Uploading an account package file for push
**Step 1. Call the API for uploading an account package file**

Upload your account package file as instructed in [Account Package Upload API](https://intl.cloud.tencent.com/document/product/1024/33765). After the call succeeds, an `upload_id` will be returned, such as `11231`.

**Step 2. Call the push API**

1. When you call the [push API](https://intl.cloud.tencent.com/document/product/1024/33764), set `audience_type` (push target) to `package_account_push` (push to accounts in the package).
2. Enter the `upload_id` obtained in [Step 1](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0.E5.8F.B7.E7.A0.81.E5.8C.85.E6.8E.A5.E5.8F.A3), such as `11231`.
3. Enter a proper account type as instructed in [Account Type Value Table](https://intl.cloud.tencent.com/document/product/1024/40598).
4. Set `account_push_type` to specify whether to push to the **recent** or **all** devices bound to each account.

#### Sample push

The following sample pushes a message to users who have won prizes in a marketing campaign:

```
{
    "audience_type": "package_account_push",
    "upload_id": 11231,
	"account_type":1,
    "account_push_type":0,
    "message_type": "notify",
    "message": {
        "title": "Congrats on winning in the campaign",
        "content":"Get online to claim your prize!"
    }
}
```
