Once your domain name is connected to LVB, the system will automatically assign it a CNAME domain name (suffixed with `.liveplay.myqcloud.com`), which cannot be accessed directly before you complete the CNAME configuration at your domain name service provider. After the configuration takes effect, LVB can be used properly. CNAME resolution is required for both playback domain name and push domain name.

## Precautions
- Please configure a CNAME record at your domain name resolution service provider. For detailed directions, please consult your service provider.
- The following describes how to configure a CNAME record at Tencent Cloud, Alibaba Cloud, Baidu Cloud, DNSPod, Wanwang, and Xinnet, respectively. The directions below are for your reference only, and the actual directions shall apply.

## Prerequisites
Log in to the LVB Console and enter **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** to view the domain name list and get the CNAME address of the domain name.

## Settings for Tencent Cloud
If your DNS service provider is Tencent Cloud, you can add a CNAME record in the following steps:
1. Log in to the [Tencent Cloud Domain Service Console](https://console.cloud.tencent.com/domain).
2. Select the domain name for which you want to add a CNAME record and click **Resolve**.
3. Go to the DNS page of the specified domain name and click **Add Record**.
4. In the new column, enter the domain name prefix as the host record, select CNAME as the record type, and enter the CNAME domain name as the record value.
	- Record Type: select `CNAME`.
	- Host Record: enter the prefix of the sub-domain names; for example, if the playback domain name is `play.myqcloud.com`, enter `play`; if you want to directly resolve the primary domain name `myqloud.com, enter `@`; and if you want to resolve a wildcard domain name, enter `\*`.
	- Resolution Route: you are recommended to select "Default".
	- Record Value: enter the CNAME value in the format of `domain.livecdn.liveplay.myqcloud.com` obtained on the **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** page in the Tencent Cloud Console.
	- TTL: you are recommended to enter `10 minutes`.
5. Click **Save**.
6. Verify whether the CNAME record is in effect. Once configured, it will take effect in about 15 minutes. If ![](https://main.qcloudimg.com/raw/bd92cce6703d3703582c0c2a194fd866.png) is displayed for it on the [Domain Management](https://console.cloud.tencent.com/live/domainmanage) page in the LVB Console, it is in effect. If it fails to take effect after a prolonged time, please see [CNAME Configuration Troubleshooting](https://intl.cloud.tencent.com/document/product/267/32478#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F).


## Settings for Alibaba Cloud
If your DNS service provider is Alibaba Cloud and you have obtained an ICP filing for your domain name, you can set up a CNAME record in the following steps:

1. Log in to the Alibaba Cloud Console and go to **Alibaba Cloud DNS** > **[DNS](https://dns.console.aliyun.com/#/dns/domainList)**.
2. Select the domain name for which you want to add a CNAME record and click **Resolution Settings**.
3. Select **Add Record** and set as follows:
	- Record Type: select `CNAME`.
	- Host Record: enter the prefix of the sub-domain names; for example, if the playback domain name is `play.myqcloud.com`, enter `play`; if you want to directly resolve the primary domain name `myqloud.com, enter `@`; and if you want to resolve a wildcard domain name, enter `\*`.
	- Resolution Route: you are recommended to select `Default`.
	- Record Value: enter the CNAME value in the format of `domain.livecdn.liveplay.myqcloud.com` obtained on the Domain Management page in the Tencent Cloud Console.
	- TTL: you are recommended to enter `10 minutes`.
4. Click **OK**.
4. Verify whether the CNAME record is in effect. Once configured, it will take effect in about 15 minutes. If ![](https://main.qcloudimg.com/raw/ca12667bfcfd9716639c27d51f3beed3.png) is displayed for it on the [Domain Management](https://console.cloud.tencent.com/live/domainmanage) page in the LVB Console, it is in effect. If it fails to take effect after a prolonged time, please see [CNAME Configuration Troubleshooting](https://intl.cloud.tencent.com/document/product/267/32478#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F).

>This document is based on the Alibaba Cloud version as of October 31, 2019. If the Alibaba Cloud Console is updated but this document has not been updated accordingly yet, please adjust the steps as needed. If you are unable to set up a record successfully, please contact [customer service](https://intl.cloud.tencent.com/support).

## Settings for Baidu Cloud
If your domain name service provider is Baidu Cloud and you have obtained an ICP filing for your domain name, you can set up a CNAME record in the following steps:
1. Log in to the Baidu Cloud Console and select **[Domain Management](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list)** to enter the domain management list page.
2. Select the domain name added to LVB and click **Resolve** in the "Operation" column to enter the DNS resolution page:
3. Add a resolution record and configure as follows:
 - Host Record: enter the prefix of the second-level domain names; for example, if the playback domain name is `play.myqcloud.com`, enter `play`; if you want to directly resolve the primary domain name `myqloud.com, enter `@`; and if you want to resolve a wildcard domain name, enter `\*`.
 - Record Type: select `CNAME`.
 - Resolution Route: you are recommended to select `Default`.
 - Record Value: enter the CNAME value in the format of `domain.livecdn.liveplay.myqcloud.com` obtained on the Domain Management page in the LVB Console.
 - TTL: you are recommended to enter `10 minutes`.
4. Click **OK** to submit.
5. Verify whether the CNAME record is in effect. Once configured, it will take effect in about 15 minutes. If ![](https://main.qcloudimg.com/raw/bd92cce6703d3703582c0c2a194fd866.png) is displayed for it on the Domain Management page in the LVB Console, it is in effect. If it fails to take effect after a prolonged time, please see [CNAME Configuration Troubleshooting](https://intl.cloud.tencent.com/document/product/267/32478#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F).

>This document is based on the Baidu Cloud version as of March 1, 2019. If the Baidu Cloud Console is updated but this document has not been updated accordingly yet, please adjust the steps as needed. If you are unable to set up a record successfully, please contact [customer service](https://intl.cloud.tencent.com/support).

## Settings for DNSPod
If your DNS service provider is DNSPod, you can add a CNAME record in the following steps:

## Settings for Wanwang
If your DNS service provider is Wanwang, you can add a CNAME record in the following steps:



## Settings for Xinnet
If your DNS service provider is Xinnet, you can add a CNAME record in the following steps:


## Verifying the Effect of a CNAME Record
The time needed for a CNAME record to take effect varies by DNS service provider (usually within 30 minutes). You can also check the effect of a record by running dig or nslookup on the command line. If a domain name suffixed with .myqcloud.com is displayed, the CNAME record has taken effect.
