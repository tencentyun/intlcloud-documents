Thank you for choosing Tencent Cloud. This tutorial will guide you through the LVB service.
## Definitions
- **Stream**: A stream in LVB refers to a group of audiovisual data that is continuously sent, such as audiovisual data collected by the camera and continuously sent to the other party in a WeChat video call. A push is to send such data to a specified address which usually points to a group of CVM instances.
- **Signature and authentication**: In LVB, a signature is used to encrypt the content sent using your own private key to ensure that others cannot forge the content. The authentication refers to the process where Tencent Cloud decrypts your signed content, verifies the legitimacy of the content, and denies requests that cannot be decrypted or contain invalid content, so as to ensure only legitimate clients can obtain the corresponding services.
- **StreamName**: ID of a stream, which is usually used to uniquely identify the stream together with a domain name.

## Getting Started
The nature of LVB is a broadcast process, similar to the live broadcast of TV channels sent to audience through cable networks. In order to complete this process, LVB needs to have a capture and push device (similar to a camera), an LVB service (similar to a cable network), and a playback device (similar to a TV set). These devices can be smart devices such as mobile phones, PCs, and tablets as well as web browsers. We provide complete software demos for different types of devices. For detailed push methods, see [Best Practices - LVB Push](https://cloud.tencent.com/document/product/267/32732).


Below is a walkthrough of the LVB service, which can be used in the following steps:
1. [Activate the LVB service](#step1)
1. [Add a domain name](#step2)
1. [Add a CNAME record for the domain name](#step3)
1. [Get a push address](#step4)
1. [Push](#step5)
1. [Get a playback address and start playback](#step6)

#### <span id="step1">1. Activate the LVB service</span>
Click **Use Now** on the [LVB product page](https://cloud.tencent.com/product/lvb), check the "Tencent Cloud Service Agreement", and click **Apply for Activation** to activate the LVB service as shown below:
![](https://main.qcloudimg.com/raw/c26dd5411d2977f5f0f675da45538603.png)
After the service is successfully activated, you will be gifted 20 GB of free broadcast traffic for trial. However, we recommend that you click **Overview** > **Used Package Traffic** > **Purchase** in the LVB Console and purchase an appropriate traffic package according to the audience size of your business, so as to avoid situations where the traffic is used up and your account balance is automatically deducted, leading to possible arrears and service interruption.

#### <span id="step2">2. Add a domain name</span>
- To use LVB, you should have at least two domain names, one as the push domain name, and the other as the playback domain name. Push and playback cannot use the same domain name.
- If you do not have a domain name, you can register and purchase one through Tencent Cloud **Cloud Products** > **Domain Name and Website** > [**Domain Name Registration**](https://buy.cloud.tencent.com/domain?from=console). You can also purchase one at another domain name service provider.
- If you have already pupurchased domain names, you should apply for ICP filing for them according to the regulations of the Ministry of Industry and Information Technology. You can do so through Tencent Cloud's [ICP Filing Registration](https://cloud.tencent.com/product/ba) service or through another domain name service provider. Generally, the application takes several business days, so it is recommended that you apply for ICP filing in advance.
- If your domain names have already obtained ICP filing, you need to add a push domain name and a playback domain name through **Domain Management** > **Add Domain** in the LVB Console.

Suppose that your push domain name is push.livetest.myqcloud.com and playback domain name is play.livetest.myqcloud.com.
Add a push domain name:
![](https://main.qcloudimg.com/raw/6f2cba99a0bd66fd8742ce9f2df7c8a0.png)
Add a playback domain name:
![](https://main.qcloudimg.com/raw/6f68d0b6773137fb579fbcb0f9031462.png)

If your domain names have already obtained an ICP filing, they can be viewed in the domain name list once successfully added.
![](https://main.qcloudimg.com/raw/2f6f6482644703e14a40b8bc94fea1b9.png)
The push domain name number.livepush.myqcloud.com in the domain name list is a test domain name provided by us. You can use it for push testing, but it is strongly recommended that you not use it as the push domain name for your real business.

#### <span id="step3">3. Add a CNAME record for the domain name</span>
After a domain name is successfully added, it needs to point to the cloud service cluster of LVB. You need to resolve the CNAME record of the domain name at your domain name registrar to the CNAME address of the corresponding domain name in the domain name list in the LVB Console as prompted. For more information on how to add a CNAME record, see [CNAME Configuration](https://cloud.tencent.com/document/product/267/30560).
>! After a CNAME record is successfully added, it generally takes some time to take effect. If the CNAME configuration fails, you cannot use LVB.

![](https://main.qcloudimg.com/raw/27f83cf6e6685197c95fe458023dbf22.png)
If the CNAME configuration failure persists, consult your domain name registrar.

#### <span id="step4">4. Get the push address</span>
Go to **Domain Management**, click the domain name push.livetest.myqcloud.com or **Manage** after the domain name to enter **Push Configuration**. Enter your stream name in StreamName (e.g., liveteststream), click **Generate Push URL**, and you will get a push address as shown below:
```
rtmp://push.livetest.myqcloud.com/live/liveteststream?txSecret=2f7927c99345d4df37ac3a8a81831fb1&txTime=5E0CC1FF
```
In the address structure, txSecret is the signature of the push and txTime is the expiration time of the push address (equal to the time in **Time Setting**). If you have enabled playback authentication, the actual expiration time is txTime + authentication expiration time. For more information, see [Configuration Sample](https://cloud.tencent.com/document/product/267/32463#.E9.85.8D.E7.BD.AE.E6.A1.88.E4.BE.8B).
![](https://main.qcloudimg.com/raw/cc647a203a129707e88445506cf8f983.png)
#### <span id="step5">5. Push</span>
Paste the push address to the push address field in your push software.

If [OBS push](https://cloud.tencent.com/document/product/267/32726) is used on a PC, the push FMS URL is:
```
rtmp://push.livetest.myqcloud.com/live/
```

The playback path/LVB code is:
```
liveteststream?txSecret=2f7927c99345d4df37ac3a8a81831fb1&txTime=5E0CC1FF
```


To test a push on a mobile device, download and install the [Tencent Video Cloud Demo](https://cloud.tencent.com/document/product/454/6555), select **Debugging Tools** > **RTMP Push**, enter the push address generated in step 4 into the push address field or directly scan its QR code, and tap the triangle icon in the lower-left corner to start the push. You can also search for the "Tencent Video Cloud" Mini Program in WeChat and test the push by entering the push address into **Debugging Tools** > **RTMP Push**.

Customized apps can integrate with the [MLVB SDK](https://cloud.tencent.com/document/product/454) provided by Tencent Cloud to implement the push function.

#### <span id="step6">6. Get a playback address and start playback</span>
Once the push is successful, you can view the push status in the list in **Stream Management** > **Online Stream** or the room list in **Channel Access**.
![](https://main.qcloudimg.com/raw/df4627bd526b8a1ee0dbc79ad1b1018f.png)
After a playback domain name with the correct CNAME record is successfully added, you can play back the stream in **Operation** > **Test** or share the playback link in apps such as WeChat, QQ, and Weibo by clicking **Share URL**.
LVB does not require the playback domain name and push domain name to be in one-to-one correspondence. To obtain a playback address corresponding to the play domain name, go to **Domain Management**, click the corresponding domain name or **Manage** in the Action column, and click **Playback Configuration**. You can see the playback addresses in RTMP, FLV, and HLS formats. Replace the **StreanName* in italics with the StreamName of the stream you want to play back.
- The RTMP protocol has higher real-time performance and thus is often used for video streams requiring low latency; however, it has a high risk of lagging.
- The HLS protocol has a relatively higher latency but offers a better watching experience. Plus, it is natively supported by Apple's Safari browser.
- The FLV protocol is something in between with a good balance between latency and lag and widely used by users in Mainland China.

After the playback address is obtained, enter it into the address bar of the player and the stream can be watched.

## Note
- Before testing and using LVB, it is recommended that you read the [Pricing Overview](https://cloud.tencent.com/document/product/267/2818) document of LVB to get familiar with the charges and prices and avoid confusions.
- If you have any questions, see [FAQs](https://cloud.tencent.com/document/product/267/7968).



