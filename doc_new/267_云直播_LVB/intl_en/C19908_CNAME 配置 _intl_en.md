Once your domain name is connected to LVB, the system will automatically assign it a CNAME domain name (suffixed with .liveplay.myqcloud.com), which cannot be accessed directly before you complete the CNAME configuration at your domain name service provider. After the configuration takes effect, LVB can be used properly. CNAME resolution is required for both playback domain name and push domain name.

## Settings for Tencent Cloud
If your DNS service provider is Tencent Cloud, you can add a CNAME record in the following steps:
1. Log in to the [Domain Name Service Console](https://console.cloud.tencent.com/domain) and click **Resolve** to the right of the domain name for which you want to add a CNAME record.
![](https://main.qcloudimg.com/raw/418d01dad6a985c9f43995aafe48c95b.png)

2. Go to the DNS page of the specified domain name and click **Add a Record**.
![](https://main.qcloudimg.com/raw/d0448ff0f3a6c74706e5e70dd8a52f53.png)
3. Enter a domain name prefix in **Host Record** (such as www; if you want to directly resolve the primary domain name, enter @; if you want to resolve a wildcard domain name, enter \*), set the **Record Type** to CNAME, enter the CNAME domain name in **Record Value**, and click **Save** to add the CNAME record.
![](https://main.qcloudimg.com/raw/b734c87a34556a2be4bf3144d1549a50.png)

## Settings for Alibaba Cloud
If your domain name service provider is Alibaba Cloud and you have obtained an ICP filing for your domain name, you can set up a CNAME record in the following steps:
1. Log in to the Tencent Cloud Console and go to the [LVB](https://console.cloud.tencent.com/live) service in the navigation bar. Click **Domain Name Management** in the left sidebar to enter the domain name management page and get the CNAME address.
![](https://main.qcloudimg.com/raw/2fe116b9f76a910c84f162f9e80baf04.png)

2. Log in to the Alibaba Cloud Console and go to the [Domain Name Service](https://dns.console.aliyun.com/#/dns/domainList) in the navigation bar. Click **Cloud DNS** in the left sidebar to enter the domain name management page.
![](https://main.qcloudimg.com/raw/bd8dd79b92fd4e1200f76df1366dc47e.png)

3. Click **Resolution Settings** in the "Action" column to enter the DNS page as shown below:
![](https://main.qcloudimg.com/raw/af1df31710fa114949efdc334678308f.png)

4. Select the domain name to be configured and click **Add a Record** in the top-right corner as shown below:
![](https://main.qcloudimg.com/raw/2f3b789874c7c7968679e6282c14f260.png)

 - Record Type: Select CNAME.
 - Host Record: Enter the prefix of the sub-domain names; for example, if the playback domain name is play.myqcloud.com, enter "play"; if you want to directly resolve the primary domain name myqloud.com, enter @; and if you want to resolve a wildcard domain name, enter \*.
 - Resolution Route: It is recommended to select "Default".
 - Record Value: Enter the CNAME value obtained on the domain name management page in the Tencent Cloud Console in the format of domain.livecdn.liveplay.myqcloud.com.
 - TTL: It is recommended to select 10 minutes.
Click **OK** to submit.

5. Verify whether the CNAME record is in effect. Once configured, the CNAME record will take effect in about 15 minutes. If <img src="https://main.qcloudimg.com/raw/8283d3a1d6e6993df5b81f5034b3bbb9.png"  style="margin:0;"> is displayed for the CNAME value of the corresponding domain name on the domain name management page of LVB, the CNAME record is successful. If the record does not take effect after a prolonged time, see [CNAME Configuration Troubleshooting](https://cloud.tencent.com/document/product/267/30010#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F).

> This document is based on the Alibaba Cloud version as of March 1, 2019. If the Alibaba Cloud Console is updated but this document has not been updated accordingly yet, please adjust the steps as needed. If you are unable to set up a record successfully, please contact our [customer service](https://cloud.tencent.com/about/connect).

## Settings for Baidu Cloud
If your domain name service provider is Baidu Cloud and you have obtained an ICP filing for your domain name, you can set up a CNAME record in the following steps:
1. Log in to the Tencent Cloud Console and go to the [LVB](https://console.cloud.tencent.com/live) service in the navigation bar. Click **Domain Name Management** in the left sidebar to enter the domain name management page and get the CNAME address.
![](https://main.qcloudimg.com/raw/d5e022e12c9904cb482fb469dd73510b.png)

2. Log in to the Baidu Cloud Console and go to the [Domain Name Service](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list) in the navigation bar. Click **Domain Name Management** in the left sidebar to enter the domain name management list page.
![](https://main.qcloudimg.com/raw/3e992eb24f22f68f36cb987813a1b6cd.png)

3. Select the domain name added to LVB and click **Resolve** in the "Action" column to enter the DNS page as shown below:
![](https://main.qcloudimg.com/raw/f139c87b258c48981075de341c92e603.png)

4. Add a resolution record as shown below:
![](https://main.qcloudimg.com/raw/e7c11bc00e33e59676eb2945f1a4f963.png)
 - Host Record: Enter a second-level domain name, i.e., the domain name prefix; for example, if the playback domain name is play.myqcloud.com, enter "play"; if you want to directly resolve the primary domain name myqloud.com, enter @; and if you want to resolve a wildcard domain name, enter \*.
 - Record Type: Select CNAME.
 - Resolution Route: It is recommended to select "Default".
 - Record Value: Enter the CNAME value obtained on the domain name management page in the LVB Console in the format of domain.livecdn.liveplay.myqcloud.com.
 - TTL: It is recommended to select 10 minutes.
Click **OK** to submit.

5. Verify whether the CNAME record is in effect. Once configured, the CNAME record will take effect in about 15 minutes. If <img src="https://main.qcloudimg.com/raw/8283d3a1d6e6993df5b81f5034b3bbb9.png"  style="margin:0;"> is displayed for the CNAME value of the corresponding domain name on the domain name management page of LVB, the CNAME record is successful. If the record does not take effect after a prolonged time, see [CNAME Configuration Troubleshooting](https://cloud.tencent.com/document/product/267/30010#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F).

> This document is based on the Baidu Cloud version as of March 1, 2019. If the Baidu Cloud Console is updated but this document has not been updated accordingly yet, please adjust the steps as needed. If you are unable to set up a record successfully, please contact our [customer service](https://cloud.tencent.com/about/connect).

## Settings for DNSPod
If your DNS service provider is DNSPod, you can add a CNAME record in the following steps:
![](https://main.qcloudimg.com/raw/c78f494c6b550562ddb49a255f1caf0d.png)

## Settings for Wanwang
If your DNS service provider is Wanwang, you can add a CNAME record in the following steps:
![](https://main.qcloudimg.com/raw/2d5e7afc347f2dd549c2e83c5e2c3f46.png)
![](https://main.qcloudimg.com/raw/0640d16350ad8d8e54ff5d8cf2230c8b.png)



## Settings for Xinnet
If your DNS service provider is Xinnet, you can add a CNAME record in the following steps:
![](https://main.qcloudimg.com/raw/caaa0fb6c0af5d58cc8012e9d090b5b9.png)


## Verifying the Effect of a CNAME Record
The time needed for a CNAME record to take effect varies by DNS service provider (usually within 30 minutes). You can also check the effect of a record by running dig or nslookup on the command line. If a domain name suffixed with .myqcloud.com is displayed, the CNAME record has taken effect.
![](https://main.qcloudimg.com/raw/cc49dc693d41eefdc0130f0b8b3439e1.png)
