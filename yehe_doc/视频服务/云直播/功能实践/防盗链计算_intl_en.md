
Security hotlink protection refers to the `txSecret` field in the push and playback URLs, which is used to prevent attackers from forging your backend for push URL generation or stealing your playback address for illegal profit.

## How It Works
In order to prevent an attacker from forging your server to generate push and playback URLs, you can configure the hotlink protection encryption key in the CSS Console as shown below (do not disclose this key), so that the attacker cannot easily fake valid push and playback URLs, as shown in the figure below.

![](https://main.qcloudimg.com/raw/ea3a932bd9e4e35fc95560cfbc4b3241.jpg)

## Calculation Process
### Step 1. Authentication key
First, you need to configure an encryption key in the console, which is used to generate the hotlink protection signature on your server. Since Tencent Cloud holds the same key as you do, it can decrypt and confirm the signature you generate.

 An encryption key can be either a push hotlink protection key or a playback hotlink protection key. The former is used to generate a push hotlink protection URL, while the latter a playback hotlink protection URL. Go to **CSS Console** > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click a domain name or **Manage**, and select **Push Configuration** to configure a push hotlink protection key, as shown in the figure below.

![](https://main.qcloudimg.com/raw/0833ac9f646507a3bf1f288709dddd20.png)

For more information on the playback hotlink protection key, please see [How can I enable playback hotlink protection?](https://intl.cloud.tencent.com/document/product/267/35598#que6). 

### Step 2. Generate `txTime`
The plaintext in the signature is `txTime`, which is the validity period of the link. For example, if the current time is 2018-12-29 11:13:45, and the URL to be generated is expected to be valid for 3 hours, then `txTime` should be set to 2018-12-29 14:13:45.
However, it is obviously inappropriate to put such a long string of time in the URL. In actual use, we convert 2018-12-29 14:13:45 to a UNIX timestamp first, i.e., 1546064025 (you can call a time function in your programming language for conversion and processing), and then convert it to a hexadecimal string to further reduce the character length, i.e., txTime = 1546064025 (decimal) = 5C271099 (hexadecimal). Using a decimal string is also supported.

>!
>- The actual end time will be `txTime` plus authentication validity period. Modifying authentication validity period will not affect the generation of URL.
>- The expiration time should be neither too early nor too late:
	- If it is too early, when the host encounters network jitters during live streaming, the push will not be resumed because the push URL will have expired.
	- If it is too late, there are risks of unauthorized push.

### Step 3. Generate `txSecret`
The generation method of `txSecret` is `MD5(KEY + StreamName + txTime)`. `KEY` is the encryption key configured in step 1. `StreamName`, also known as stream ID, is Test in this example (we recommend using a random number or a user ID). `txTime` is the 5C271099 calculated in last step, and MD5 is a standard irreversible one-way MD5 hash algorithm.
For example:
```
KEY is e12c46f2612d5106e2034781ab261ca3
Then txSecret = MD5(e12c46f2612d5106e2034781ab261ca3test5C271099) = f85a2ab363fe4deaffef9754d79da6fe
```

### Step 4. Construct a hotlink protection URL
A push URL that conforms to the Tencent Cloud standards consists of the following four parts:
![](https://main.qcloudimg.com/raw/679602c838e8dfd3b61acefebb221d13.jpg)
We can create a standard URL using `txTime` (which informs Tencent Cloud of the expiration time of a push/playback URL), `txSecret` (that only Tencent Cloud can decrypt and verify), `StreamName`, and a push domain name (e.g. "livepush.tcloud.com"). In this example, the push URL is:

```
rtmp://livepush.tcloud.com/live/test?txSecret=f85a2ab363fe4deaffef9754d79da6fe&txTime=5C271099
```


## Sample Push Code
Go to **CSS Console** > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, select a pre-configured push domain name, click **Manage** > **Push Configuration** to display the **Push Address Sample Code** (for both PHP and Java) that demonstrates how to generate a hotlink protection address. For details, please see[Push Configuration](https://intl.cloud.tencent.com/document/product/267/31059#sample-code-of-push-url).
