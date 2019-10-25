
### Why do I need a domain name with ICP filing to access the LVB service?
LVB does not provide domain name service, so you need to use your own domain name with ICP filing for push and playback. If you don't have one, you can use [Tencent Cloud Domain Service](https://intl.cloud.tencent.com/product/cns) to register one.
### If my domain name doesn't have ICP filing, can I use it in LVB?
Pursuant to the State Council Decree No.292 "Administrative Measures for Internet Information Services" and the Ministry of Industry and Information Technology Order No.33 "Measures for the Archival Administration of Non-operational Internet Information Services", China implements a licensing system for operational internet information services and filing system for non-operational internet information services. Internet information services shall not be provided before the license or filing is obtained; otherwise, it would be illegal. Therefore, a domain name with no ICP filing cannot be connected to the LVB service, and you should start the application process as soon as possible.
### What is ICP filing?
ICP filing includes filing for websites and filing for domain names, of which the latter is required if you want to use your domain name for LVB. Communications administrations in different provinces may have different requirements for ICP filing application. For more information, see [Requirements of Provincial Communications Administrations](https://intl.cloud.tencent.com/document/product/1022/31671). If you have any questions on ICP filing for your domain name, see [Domain Name ICP Filing Guidelines](https://intl.cloud.tencent.com/document/product/1022/31659).

### How to apply for ICP filing?
Tencent Cloud can help you apply for ICP filing for your website with a server located in Mainland China. For more information, see [Website ICP Filing Application](https://intl.cloud.tencent.com/product/icp). You can also complete the application process through other cloud service providers or on the website of [the Ministry of Industry and Information Technology] on your own.

### How to add a ICP filed domain name to LVB?
Go to the [LVB Console](https://console.cloud.tencent.com/live) > **Domain Management**, where you can add your own push or playback domain name. For more information, see [Domain Name Management](https://intl.cloud.tencent.com/document/product/267/31056). Then, you need to complete CNAME configuration as instructed in [CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057). After successful configuration, you can use your domain name for push and playback.

### Why CNAME is still displayed as not configured after configuration?
After you configure CNAME as instructed in [CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057), please wait patiently because it takes 15-30 minutes for the configuration to take effect. In addition, you can also check whether CNAME configuration is successful by following the steps below:
1. Linux/Mac OS: Run the `dig` command in the format of `dig domain name`.
Below is an example. If the first row displays that the destination domain name provided by LVB (.livecdn.liveplay.myqcloud.com) is resolved, CNAME configuration is successful.
![](https://main.qcloudimg.com/raw/bcec06bf22b040aad2ed798508b13209.png)

2. Windows: Click **Start** > **Run**, enter `cmd`, press Enter, and then enter `nslookup your own domain name` on the command line.
Below is an example. If the destination domain name provided by LVB (.livecdn.liveplay.myqcloud.com) is resolved, CNAME configuration is successful.
![](https://main.qcloudimg.com/raw/f0b305804f0e8c1084471881aa3377dc.png)

>? DNS resolution must be performed over the public network on Linux/Mac OS/Windows.

### What if I don't add my own domain name?
If you activated the LVB service after October 17, 2018, you are required to add your own domain name for playback; otherwise, you cannot play back the live streaming content. If you activated the service before then, LVB provided a default domain name for you, but you are recommended to replace it with your own domain name with ICP filing. Tencent Cloud has started phasing out the default domain names since December 31, 2018.
>!Default domain names are system domain names assigned by LVB in the format of bizid.livepush.myqcloud.com and bizid.liveplay.myqcloud.com.

### What if my live broadcasting business is outside Mainland China?
If you only distribute your content outside Mainland China, you don't need ICP filing for your domain name for the time being as there are no specific requirements by applicable authorities.
Otherwise, you need to add your own filed domain name.

### I have configured special items for the default domain name. Can my own domain name be resolved to the default one?
To use a new domain name, connect it to LVB from scratch. You are recommended to add and configure your own domain name in the LVB Console.
