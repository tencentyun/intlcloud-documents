The LVB Console provides an address generator. You can use the generator to quickly generate push/playback addresses by entering address splicing information in the Console. The live streaming address is mainly composed of a domain name (`domain`), an application name (`AppName`), a stream name (`StreamName`) and an authentication key (`Key`).
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)
After an address is generated, you can **select the address and copy it**, **click the button at the end of the address to copy it**, or **scan the QR code at the end of the address to get it**.


## Notes
- LVB does not provide the address generation history, so please copy an address once it is generated.
- If you need to generate multiple live streaming addresses, we recommend that you splice addresses as instructed in [How to Splice a Push URL](https://intl.cloud.tencent.com/document/product/267/32480).
- LVB provides a test domain name `xxxx.livepush.myqcloud.com` by default. You can use it for push testing, but we do not recommend using it as the push domain name for your real business.



##  Prerequisites
You have logged in to the [LVB Console](https://console.cloud.tencent.com/live/livestat), and have added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).

## Configuration Parameters

<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Domain Type</td>
<td>Select <strong>push domain</strong> or <strong>playback domain</strong>.</td>
</tr><tr><td>AppName</td>
<td>LVB application name, used to identify the live stream file storage path. Default value: `live`.<br>It contains only letters, digits, and symbols.</td>
</tr><tr><td>StreamName</td>
<td>Custom stream name. It is a unique identifier of a live stream.<br>It contains only letters, digits, and symbols.</td>
</tr><tr><td>Expiration Time</td>
<td><li>The expiration time of playback address is the setting timestamp plus the playback authentication expiration time.<li>The push address expiration time is the setting time.</td>
</tr><tr><td>Transcoding Template</td>
<td><li>Valid when you select <strong>playback domain</strong>.<li>If you select a <a href="https://intl.cloud.tencent.com/document/product/267/31071">transcoding template</a>, the generated playback address will be the live streaming address after transcoding. If you want to play the original live stream, you don't need to select a transcoding template to generate the address.</td>
</tr>
</tbody></table>

<h2 id="push">Generating a Push Address</h2>

### Directions
1. Log in to the LVB Console, select **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** to open the Address Generator.
2. Select **Push domain** as the domain type, and select a push domain name that you have added on the domain management page.
3. Enter an **AppName**. It is `live` by default.
4. Enter a **StreamName**, such as `liveteststream`.
5. Select the expiration time of the address, such as `2020-06-09 15:36:04`.
6. Click **Generate Address**.
![](https://main.qcloudimg.com/raw/3e9c45467ba07c5cac3250bd58ad3223.png)

### Push address description
LVB supports RTMP push. You can use the address generator to generate a push address prefixed with `rtmp://`.
![](https://main.qcloudimg.com/raw/9e2bd3bbb6c15fe4cd46a905c0fe0c27.png)


<h2 id="play">Generating a Playback Address</h2>

### Directions
1. Log in to the LVB Console, select **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** to open the Address Generator.
2. Select **Playback domain** as the domain type, and select a playback domain name that you have added on the domain management page.
3. Enter an **AppName**. It is `live` by default.
4. Enter a **StreamName**, such as `liveteststream`.
5. Select the expiration time of the address, such as `2020-06-09 15:36:04`.
6. Select whether to import a created transcoding template.
7. Click **Generate Address**.

![](https://main.qcloudimg.com/raw/10afad65da657a02a6f175e7d2afdc7c.png)

### Playback address description
If you select a transcoding template, the generated playback address will be the live streaming address after transcoding. RTMP, FLV and HLS live streaming addresses are supported. The address generator can generate an address prefixed with `rtmp://` or `http://`.

![](https://main.qcloudimg.com/raw/a5b5ab5183a44e78ac7eabc757c8d16e.png)













