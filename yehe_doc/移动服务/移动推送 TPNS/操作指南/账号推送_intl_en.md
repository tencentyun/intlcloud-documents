## Overview

After you get a batch of user accounts from a third-party data platform or business backend, when launching a marketing campaign for such users, you can use the **push to accounts** feature to push messages to a single or multiple accounts at a time.

>! The abovementioned **accounts** must be bound with a TPNS token. For detailed directions, please see [Binding an account (Android)](https://intl.cloud.tencent.com/document/product/1024/30715#binding-an-account) or [Adding account (iOS)](https://intl.cloud.tencent.com/document/product/1024/30727#adding-account).

## Directions

### Using the console

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns). 
2. Find the application for which to configure batch push and select **Create Push** in its **Operation** column to enter the **Create Push** page.
3. In the **Push Target** configuration item, select **Account**. You can choose to upload an account package file or manually enter accounts, as shown in the following figure:

>?Requirements for the uploaded account package are as follows:
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
1. When you call the [push API](https://intl.cloud.tencent.com/document/product/1024/33764), set `audience_type` (push target) to `account` (single account) or `account_list` (a list of accounts).
2. Set `account_type`. For account type details, see [Account Type Value Table](#quzhibiao).
3. Set `account_push_type` to specify whether to push to the **recent** or **all** devices bound to each account.
#### Sample push
```
{
    "audience_type": "account",
		 "account_list": [
       "12345"
     ]
	   "account_type":"991",
	   "account_push_type":0,
    "message_type": "notify",
    "message": {
        "title": "Push to a QQ account number",
        "content":"Get online to claim your prize!"		
    },

}
```

#### Push via file upload
**Step 1. Call the account package upload API**

Upload your account package file as instructed in [Account Package Upload API](https://intl.cloud.tencent.com/document/product/1024/33765). After the call succeeds, an `upload_id` will be returned, such as 11231.

**Step 2. Call the push API**

1. When you call the [push API](https://intl.cloud.tencent.com/document/product/1024/33764), set `audience_type` (push target) to `package_account_push` (account package push), enter the `upload_id`, for example, 11231, obtained in [Step 1](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0.E5.8F.B7.E7.A0.81.E5.8C.85.E6.8E.A5.E5.8F.A3).
2. Set `account_type`. For account type details, see [Account Type Value Table](#quzhibiao).
3. Set `account_push_type` to specify whether to push to the **recent** or **all** devices bound to each account.

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
    }
}
```

<span id="quzhibiao"></span>
## Account Type Value Table

| accountType Value | Account Type | Description | Example |
| --- | --- |--|--|
| 0 | Default | Type used if `accountType` is not passed in | - |
| 1-16 | Custom | Custom account that the business side binds with a token, for example, uin | - |
| 989 | TAID | Unique device fingerprint ID created by Tencent | - |
| 989 | QIMEI | Unique device ID provided by Tencent | - |
| 991 | QQ account number | 5-12 digits | 12345 |
| 992 | QQ account number - MD5 | Encrypted QQ account number. Before encryption, a QQ account number is a 5- to 12-character numeric string. After encryption, it becomes a 32-character case-insensitive alphanumeric string. | - |
| 993 | IDFA | Apple device ID, which is a 32-character uppercase alphanumeric string and divided into several parts by `-`. | 49E2084A-290C-41EF-AD20-E540CD6AE841 |
| 994 | IDFA - MD5 | Encrypted IDFA. Before encryption, it must be converted into a 32-character uppercase alphanumeric string; after encryption, it becomes a 32-character case-insensitive alphanumeric string. | Before encryption: FF1999CD-7177-4937-A474-74937A102630 <br>After encryption: 2c010ed96aef2fc34983e1e7e9176b7e
| 995 | MAC address | Hardware identifier. Its format: six sets of hexadecimal numbers, separated by `:`; the letters are uppercase. | 08:00:20:0A:8C:6D |
| 996 | MAC address - MD5 | Encrypted MAC address. Before encryption, the separator `:` must be removed and letters converted to uppercase. | Before encryption: a000002c9060f7 <br>After encryption: f2d5a650733ca8c27d502b1c08da14e5
| 997 | OAID | Anonymous device identifier set by the Mobile Security Alliance (MSA). Keep the original value without changing the case, and do not encode it with MD5. It is composed of numbers, letters, and hyphens. The format and length vary depending on the collection vendor and system version. For ID details, please see the MSA website. | - |
| 998 | OAID - MD5 | Encrypted OAID. It is a 32-character case-insensitive string. Directly process the original value of OAID with MD5, without changing the case or removing hyphens. | - |
| 999 | WeChat Union ID | Encrypted account ID of WeChat Open Platform, which is the unique WeChat Union ID of all Official Accounts/Mini Programs/mobile applications under an account on WeChat Open Platform | - |
| 1000 | IMEI | Android device ID, which is a 14- or 15-character numeric string, or a 14- or 15-character lowercase alphanumeric string | - |
| 1001 | IMEI - MD5 | Encrypted IMEI. Before encryption, it must be converted into a 14- or 15-character lowercase alphanumeric string; after encryption: it becomes a 32-character case-insensitive numeric string. | Before encryption: a000002c9060f7 <br>After encryption: f2d5a650733ca8c27d502b1c08da14e5 |
| 1002 | Mobile number | Mobile number in E.164 format `[+][country code or area code][subscriber number]` | +8613711112222, where there is a `+` sign in the front, `86` is the country code, and `13711112222` is the subscriber number |
| 1003 | WeChat OpenID | Unique identifier of a WeChat user under a WeChat Official account/ Mini Program AppID. The obtained OpenID varies depending on AppID. | - |
| 1004 | QQ OpenID |- |- |
| 1005 | Email |- |- |
| 1006 | Sina Weibo|- |- |
| 1007 | Alipay |- |- |
| 1008 | Taobao |- |- |
| 1009 | Douban |- |- |
| 1010 | Facebook |- |- |
| 1011 | Twitter |- |- |
| 1012 | Google |- |- |
| 1013 | Baidu |- |- |
| 1014 | JD |- |- |
| 1015 | LinkedIn |- |- |

