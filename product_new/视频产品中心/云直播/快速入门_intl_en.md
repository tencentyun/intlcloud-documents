Thank you for choosing Tencent Cloud. This tutorial will guide you through the LVB service.
## Definitions
- **Stream**: A stream in LVB refers to a group of audiovisual data that is continuously sent, such as audiovisual data collected by the camera and continuously sent to the other party in a WeChat video call. A push is to send such data to a specified address which usually points to a group of CVM instances.
- **Signature and authentication**: In LVB, a signature is used to encrypt the content sent using your own private key to ensure that others cannot forge the content. The authentication refers to the process where Tencent Cloud decrypts your signed content, verifies the legitimacy of the content, and denies requests that cannot be decrypted or contain invalid content, so as to ensure only legitimate clients can obtain the corresponding services.
- **StreamName**: ID of a stream, which is usually used to uniquely identify the stream together with a domain name.

## Getting Started
The nature of LVB is a broadcast process, similar to the live broadcast of TV channels sent to audience through cable networks. In order to complete this process, LVB needs to have a capture and push device (similar to a camera), a cloud live broadcast service (similar to a cable network), and a playback device (similar to a TV set). These devices can be smart devices such as mobile phones, PCs, and tablets as well as web browsers. We provide complete software demos for different types of devices. For detailed push methods, see [Best Practices - LVB Push](https://intl.cloud.tencent.com/document/product/267/31558).


Below is a walkthrough of the LVB service, which can be used in the following steps:
1. [Activate the LVB service](#step1)
1. [Add a domain name](#step2)
1. [Add a CNAME record for the domain name](#step3)
1. [Get a push address](#step4)
1. [Push](#step5)
1. [Get a playback address and start playback](#step6)

#### <span id="step1">1. Activate the LVB service</span>
Click **Get Started** on the [LVB product page](https://intl.cloud.tencent.com/product/lvb), tick the checkbox to agree to the  "Tencent Cloud Service Agreement" and "LVB Billing Instructions", and click **Apply** to activate the LVB service as shown below:
![](https://main.qcloudimg.com/raw/73af20989054bdec40a41fb79b343a16.png)

#### <span id="step2">2. Add a domain name</span>
- To use LVB, you should have at least two domain names, one as the push domain name, and the other as the playback domain name. Push and playback cannot use the same domain name.
- If you do not have a domain name, you can register and purchase one through Tencent Cloud **Cloud Products** > **Domain Name and Website** > [**Domain Name Registration**](https://buy.cloud.tencent.com/domain?from=console). You can also purchase one at another domain name service provider.
- If you have already purchased domain names, you should apply for ICP filing for them according to the regulations of the Ministry of Industry and Information Technology. You can do so through Tencent Cloud's [ICP Filing Registration](https://cloud.tencent.com/product/ba) service or through another domain name service provider. Generally, the application takes several business days, so we recommend applying in advance.
- If your domain names have already obtained ICP filing, you need to add a push domain name and a playback domain name through **Domain Management** > **Add Domain** in the LVB Console.

Suppose that your push domain name is push.livetest.myqcloud.com and playback domain name is play.livetest.myqcloud.com.
Add a push domain name:
![](https://main.qcloudimg.com/raw/7ad78c635e1bde8e37191c81a82fae12.png)
Add a playback domain name:
![](https://main.qcloudimg.com/raw/8c9bb01084c524deb80a1e33f01ce421.png)

If your domain names have already obtained ICP filing, they can be viewed in the domain name list once successfully added.
![](https://main.qcloudimg.com/raw/531788169a78be258b51df6621a27ac6.png)
The push domain name number.livepush.myqcloud.com in the domain name list is a test domain name provided by us. You can use it for push testing, but we strongly recommend against using it as the push domain name for your real business.

#### <span id="step3">3. Add a CNAME record for the domain name</span>
After a domain name is successfully added, it needs to point to the cloud service cluster of LVB. You need to resolve the CNAME record of the domain name at your domain name registrar to the CNAME address of the corresponding domain name in the domain name list in the LVB Console as prompted. For more information on how to add a CNAME record, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057).
> After a CNAME record is successfully added, it generally takes some time to take effect. If the CNAME configuration fails, you cannot use LVB.

![](https://main.qcloudimg.com/raw/7e1f7b93a84a6d830e289150f24890ed.png)
If the CNAME configuration failure persists, consult your domain name registrar.

#### <span id="step4">4. Get the push address</span>
Go to **Domain Management**, click the domain name push.livetest.myqcloud.com or **Manage** after the domain name to enter **Push Configuration**. Enter your stream name in StreamName (e.g., liveteststream), click **Generate Push URL**, and you will get a push address as shown below:
```
rtmp://push.livetest.myqcloud.com/live/liveteststream?txSecret=2f7927c99345d4df37ac3a8a81831fb1&txTime=5E0CC1FF
```
In the address structure, txSecret is the signature of the push and txTime is the expiration time of the push address (equal to the time in **Time Setting**). If you have enabled playback authentication, the actual expiration time is txTime + authentication expiration time. For more information, see [Configuration Sample](https://intl.cloud.tencent.com/document/product/267/31060#.E9.85.8D.E7.BD.AE.E6.A1.88.E4.BE.8B).
![](https://main.qcloudimg.com/raw/7cf645e40a13d256c7be9f55c681a7a4.png)
#### <span id="step5">5. Push</span>
Paste the push address to the push address field in your push software.

If OBS push is used on a PC, the push FMS URL is:
```
rtmp://push.livetest.myqcloud.com/live/
```

The playback path/LVB code is:
```
liveteststream?txSecret=2f7927c99345d4df37ac3a8a81831fb1&txTime=5E0CC1FF
```


#### <span id="step6">6. Get a playback address and start playback</span>
Once the push is successful, you can view the push status in the list in **Stream Management** > **Online Stream** or the room list in **Channel Access**.
![](https://main.qcloudimg.com/raw/c2d65a14c41b22f7cea243b3a738a2ab.png)
After a playback domain name with the correct CNAME record is successfully added, you can play back the stream in **Operation** > **Test** or share the playback link in apps such as WeChat, QQ, and Weibo by clicking **Share URL**.
LVB does not require the playback domain name and push domain name to be in one-to-one correspondence. To obtain a playback address corresponding to the play domain name, go to **Domain Management**, click the corresponding domain name or **Manage** in the Action column, and click **Playback Configuration**. You can see the playback addresses in RTMP, FLV, and HLS formats. Replace the **StreanName* in italics with the StreamName of the stream you want to play back.
- The RTMP protocol has higher real-time performance and thus is often used for video streams requiring low latency; however, it has a high risk of lagging.
- The HLS protocol has a relatively higher latency but offers a better watching experience. Plus, it is natively supported by Apple's Safari browser.
- The FLV protocol is a relatively balanced option with an even latency and lag performance. It is widely used by users in Mainland China.

After the playback address is obtained, enter it into the address bar of the player and the stream can be watched.

## Note
- Before testing and using LVB, we recommend reading the [Pricing Overview](https://cloud.tencent.com/document/product/267/2818) document of LVB to get familiar with the fees and prices.
- If you have any questions, see [FAQs](https://intl.cloud.tencent.com/document/product/267/7968).



