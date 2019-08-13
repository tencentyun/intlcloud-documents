
Security hotlink protection refers to the txSecret field in the push and playback URLs, which is used to prevent attackers from forging your backend for push URL generation or stealing your playback address for illegal profit.

## How It Works
In order to prevent an attacker from forging your server to generate push and playback URLs, you can configure the hotlink protection encryption key in the LVB Console as shown below (do not disclose this key), so that the attacker cannot easily fake valid push and playback URLs:
![](//mccdn.qcloud.com/static/img/4ea1512fd335f68f30cca0a01e902966/image.png)

## Calculation Process
- **Step 1: Exchange keys**
First, you need to configure an encryption key in the console, which is used to generate the hotlink protection signature on your server. Since Tencent Cloud holds the same key as you do, it can decrypt and confirm the signature you generate.

 An encryption key can be either a push hotlink protection key or a playback hotlink protection key. The former is used to generate a push hotlink protection URL, while the latter a playback hotlink protection URL. Currently, you can configure a push hotlink protection key in the [LVB Console](https://console.cloud.tencent.com/live) in a self-service manner as shown below:
![](https://main.qcloudimg.com/raw/638fcbb8eac12cbbabc247fd6a1323f2.jpg)
For more information on the playback hotlink protection key, see [Best Practices - LVB Playback](https://cloud.tencent.com/document/product/267/32733).

- **Step 2: Generate txTime**
The plaintext in the signature is txTime, which means the validity period of the link. For example, if the current time is 2018-12-29 11:13:45, and the URL to be generated is expected to be valid for 3 hours, then txTime should be set to 2018-12-29 14:13:45.
However, it is obviously inappropriate to put such a long string of time in the URL. In actual use, we convert 2018-12-29 14:13:45 to a UNIX timestamp first, i.e., 1546064025 (matters related to the conversion and various backend programming languages are all taken care of by a time function), and then convert it to a hexadecimal string to further reduce the character length, i.e., txTime = 1546064025 (decimal) = 5C271099 (hexadecimal). Using a decimal string is surely supported too.
>! You are recommended not to set the txTime to be too long or too short:
>- If the expiration time is too short, when the host encounters network jitters during a live broadcast, the push cannot be resumed because the push URL expires.
>- If the expiration time is too long, there may be a risk of hotlinking.

- **Step 3: Generate txSecret**
The generation method of txSecret is MD5(KEY + StreamName + txTime) where KEY is the encryption key configured in step 1, StreamName is also called stream ID (which is Test in this example; preferably, use a random number or user ID for it), txTime is the 5C271099 calculated in last step, and MD5 is a standard irreversible one-way MD5 hash algorithm.
For example:
```
KEY is e12c46f2612d5106e2034781ab261ca3
Then txSecret = MD5(e12c46f2612d5106e2034781ab261ca3test5C271099) = f85a2ab363fe4deaffef9754d79da6fe
```

- **Step 4: Splice the hotlink protection URL**
  A push URL that conforms to the Tencent Cloud standard consists of the following four parts:
	![](https://main.qcloudimg.com/raw/fa8d64bd2a314efece3ecb355187dd6a.png)
	Now that we have a push (or playback) that tells Tencent Cloud the URL expiration time (txTime) and only Tencent Cloud can decrypt and verify the txSecret, StreamName, and push domain name (assumed as livepush.tcloud.com), we can splice a standard URL. In this example, the push URL is:
```
rtmp://livepush.tcloud.com/live/test?txSecret=f85a2ab363fe4deaffef9754d79da6fe&txTime=5C271099
```
	

## Sample Code
Go to [**LVB Console**](https://console.cloud.tencent.com/live) > **Domain Management**, select a pre-configured push domain name, click **Manage** > **Push Configuration** to display the **Push Address Sample Code** (for both PHP and Java) that demonstrates how to generate a hotlink protection address.
