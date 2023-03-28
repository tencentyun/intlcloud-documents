
Hotlink protection is achieved using the `txSecret` field in a push or playback URL. It can prevent attackers from forging your push URLs or using your playback URLs for profit without authorization.

## How It Works
You can configure an encryption key in the CSS console (do not disclose this key) to prevent attackers from forging your push and playback URLs:
![](https://main.qcloudimg.com/raw/ea3a932bd9e4e35fc95560cfbc4b3241.jpg)

## Directions
### Step 1. Configure the key
First, you need to configure an encryption key in the CSS console. This is the key used to generate hotlink protection signatures on your server. Because Tencent Cloud has this key, it will be able to decrypt the signatures generated.

 A push hotlink protection key is used for push URLs, and a playback hotlink protection key is used for playback URLs. To configure a key for push URLs, go to the CSS console, click [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar, and select **Push Configuration**.
![](https://main.qcloudimg.com/raw/0833ac9f646507a3bf1f288709dddd20.png)
For how to configure a playback hotlink protection key, see [How can I enable hotlink protection?](https://intl.cloud.tencent.com/document/product/267/35598). 

### Step 2. Generate `txTime`
The plaintext in the signature is `txTime`, which is the validity period of the URL. For example, if the current time is `2018-12-29 11:13:45`, and you want your push URL to expire in three hours, `txTime` should be `2018-12-29 14:13:45`.
To simplify the URL generated, the time string is converted to a Unix timestamp (you can perform this by calling the time API), and to further shorten the string, the timestamp is converted to a hexadecimal or decimal string. Therefore, in the example above, `txTime` should be `1546064025` (decimal) or `5C271099` (hexadecimal).

>!
>- The actual expiration time of a URL is `txTime` plus the validity period of the authentication key. Modifying the validity period of the key will not change the URL generated. 
>- Make sure you specify an appropriate validity period (not too long or too short) for the URL:
    - If the validity period is too short, when a host is disconnected during a live stream, they may be unable to resume publishing due to expiration of the push URL.
    - If the validity period is too long, your URL may be hotlinked.

### Step 3. Generate `txSecret`
`txSecret` is generated using `MD5(KEY + StreamName + txTime)`. MD5 is a one-way hashing algorithm. `KEY` is the encryption key configured in step 1. `StreamName` is the stream ID. We recommend you set it to a random number or the user ID. In the example below, `StreamName` is set to `test`, and `txTime` is the hexadecimal string calculated in step 2.
Example:
```
Suppose `KEY` is `e12c46f2612d5106e2034781ab261ca3`.
txSecret = MD5(e12c46f2612d5106e2034781ab261ca3test5C271099) = f85a2ab363fe4deaffef9754d79da6fe
```

### Step 4. Generate a hotlink protection URL
A push URL that conforms to the Tencent Cloud standard consists of the following four parts:
![](https://main.qcloudimg.com/raw/679602c838e8dfd3b61acefebb221d13.jpg)
Now that we have the URL expiration time `txTime`, the signature `txSecret` (which only Tencent Cloud can decrypt), the stream ID `StreamName`, and the push domain (suppose it’s `livepush.tcloud.com`), we can generate a hotlink protection push URL:
```
rtmp://livepush.tcloud.com/live/test?txSecret=f85a2ab363fe4deaffef9754d79da6fe&txTime=5C271099
```


## Sample Code
 We offer sample code for the generation of hotlink protection URLs. In the CSS console, click [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar, select a push domain, and click **Push Configuration**. Scroll down, and you will find sample code for PHP, Java, and Go. For details, see [Push Configuration](https://www.tencentcloud.com/document/product/267/31059).
