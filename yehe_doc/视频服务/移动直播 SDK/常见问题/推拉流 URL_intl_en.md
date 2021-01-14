### Prerequisites
- You have signed up for a Tencent Cloud account and activated the [LVB service](https://intl.cloud.tencent.com/zh/product/LVB).
- You have added push/playback domain names in the **LVB console** > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**. For detailed directions, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have [configured CNAME](https://intl.cloud.tencent.com/document/product/267/31057) for your domain names.

### How to manually generate live streaming URLs?  
1. Log in to the LVB console.	
2. Go to **LVB Toolkit** > [**Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**, and do the following:
	1. Select a domain type.
	2. Select the domain name you have added in **Domain Management**.
	3. Enter a custom `AppName` value (`live` by default). This is used to differentiate the paths of different applications under the same domain name.
	4. Enter a custom `StreamName` value.
	5. Select an expiration time for the address.
6. Click **Generate Address** to generate your push/playback address.
![](https://main.qcloudimg.com/raw/b92179a1020d676d5e93e7ea4bfd6c37.png)
 >? 
 >- `AppName` is a custom value and can contain only letters, numbers, and symbols.
 >- Here is another method to generate push addresses: in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, find the push domain name you want use to generate a push address, click **Manage**, select **Push Configuration**, enter the expiration time of the address and a custom `StreamName value`, and click **Generate Push Address**.

### How to view the sample code of the push address?
Go to the **LVB console** > [**Domain Management**](https://console.cloud.tencent.com/live/domainmanage)**, find the push domain name you created, click **Manage**, and select **Push Configuration**. Scroll down and you will find **Push Address Sample Code** (for PHP and Java). The code demonstrates how to generate a hotlink protection address. For detailed directions, see [Push Configuration](https://intl.cloud.tencent.com/document/product/267/31059).

### How to automatically splice push URLs?
If you run a large number of live streaming rooms, it is impossible to manually generate a push and playback URL for each host. In such cases, you can use the server to automatically **splice** the addresses. Any URL that meets Tencent Cloud standards can be used for push. A standard push URL consists of four parts, as shown below:
![](https://main.qcloudimg.com/raw/095b7c120b62ac8a171603d4fff67cb2.png)
- **Domain**
Push domain name, which can be the default push domain name provided by Tencent Cloud LVB or a push domain name that you have added and created a CNAME record for.
- **AppName**
LVB application name, which is a custom value and `live` by default.
- **StreamName (stream ID)**
Custom stream name, which is the unique ID of a live stream. We recommend that you use a random numeric or alpha-numeric string for this parameter.
- **Authentication key (optional)**
An authentication key consists of `txSecret` and `txTime`: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.
If push authentication is enabled, the URL used for push must contain a authentication key. If push authentication is disabled, the push URL used ends before “?”.
 - **txTime (address validity period)** 
It indicates when the URL expires, which is expressed as a hexadecimal Unix timestamp.
	
	>?For example, `5867D600` means that the URL expires at 00:00:00, January 1, 2017. The validity period should neither be too short nor too long. Most of our clients set `txTime` to a point 24 hours or longer from the current time. If the validity period is too short, after a host is disconnected due to network problems during a live broadcast, it may be impossible to resume the push due to expiration of the push URL.
 - **txSecret (hotlink protection signature)**
The `txSecret` signature serves to prevent attackers from forging a backend to generate push URLs. For the calculation method, see [Best Practice - Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).


### How to automatically splice playback URLs?
A playback address consists of a playback protocol prefix, domain name (`domain`), application name (`AppName`), stream name (`StreamName`), playback protocol suffix, authentication key, and other custom parameters. Below are a few examples.	

```	
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time) 	
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)	
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)	
```

- **Playback protocol prefix **	
<table>
    <tr><th>Playback Protocol</th><th>Playback Prefix</th><th>Notes</th></tr>
    <tr>
        <td>RTMP</td>
        <td><code>rtmp://</code> </td>
        <td>Not recommended as it has poor instant streaming performance and does not support high concurrency</td>
    </tr><tr>
        <td>HTTP-FLV</td>
				<td><code>http://</code> or <code>https://</code></td>
        <td>Recommended as it fares well on instant streaming and supports ultra high concurrency</td>
    </tr><tr>
        <td>HLS (m3u8)</td>
        <td><code>http://</code> or <code>https://</code></td>
        <td>Recommended for mobile and desktop Safari</td>
    </tr>
</table>
- **Domain**	
	Playback domain name, a domain name you have added and created a CNAME record for.
- **AppName**	
  LVB application name, used to differentiate the storage path of a live streaming media file. It is a custom value and `live` by default.
- **StreamName (stream ID)<span id="streamname"></span>**	
  Custom stream name, which is the unique ID of a live stream. We recommend that you use a random numeric or alpha-numeric string for this parameter.
- **Authentication key (optional)**	
	An authentication key consists of `txSecret` and `txTime`: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.
If playback authentication is enabled, the URL used for playback must contain an authentication key. If it is disabled, the playback URL ends before “?”.
 - **txTime (address validity period):** it indicates when the URL expires, which is expressed as a hexadecimal Unix timestamp.
 - **txSecret (hotlink protection signature):** it serves to prevent attackers from forging a backend to generate playback URLs. For the calculation method, see [Best Practice - Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).
