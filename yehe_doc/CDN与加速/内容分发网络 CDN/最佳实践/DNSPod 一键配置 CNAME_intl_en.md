

Tencent Cloud CDN and [DNSPod](https://console.dnspod.cn/) . If a domain name has been hosted on Tencent Cloud DNSPod, you can configure CNAME with a few steps through [CDN console](https://console.cloud.tencent.com/cdn/domains). Thus, you can reduce steps, save time and enable CDN acceleration service quickly.

>! It is only available on the Chinese site but not on the international site.

## Background

After a domain name is connected to CDN, the system will automatically assign a CNAME domain name suffixed with `.cdn.dnsv1.com` which can be viewed on the [Domain Management](https://console.cloud.tencent.com/cdn/domains) page on the CDN console. It cannot be accessed directly. Instead, you need to complete the CNAME configuration with the domain name service provider first. When the CNAME record takes effect, you can enable the CDN acceleration service.

## Scenarios

Users who use both Tencent Cloud CDN and DNSPod can configure CNAME record to enable the CDN acceleration service.

## Operation Guide

### Hosting domain names on DNSPod

You need to host the domain name resolution on DNSPod first. For more information, see [Hosting Domain Name Resolution on DNSPod](https://docs.dnspod.cn/dns/60b99ba0e90008112f815bde/).

### Using CDN service

#### Adding a domain name

Log in to [CDN console](https://console.cloud.tencent.com/cdn), click **Domain Management** in the left sidebar, and click **Create a Distribution** to add the domain name you want to accelerate. For more information, see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

#### Configuring CNAME

Log in to [CDN console] and go to the [Domain Management] page(https://console.cloud.tencent.com/cdn/domains). Find the domain name you want to accelerate, and hover over the icon in front of CNAME to view the note. Click **Quick Configure** to configure CNAME.



To enable acceleration service for the selected domain name, we will take following actions to process the resolution record for the domain name in DNSPod.

1. If the domain name has not configured any resolution record, add a Tencent Cloud CDN CNAME record with default line type. The default TTL is 600.
2. If the domain name has configured a resolution record, pause all configured resolution records and add a Tencent Cloud CDN CNAME record with default line type. The default TTL is 600.
**Note: pause all configured resolution records for a domain name may affect existing DNS resolution service for the domain name.**


1. You can log in to the [DNSPod console](https://console.dnspod.cn/dns/list) to manage resolution records.


>! Please ensure current account has management permissions for the corresponding domain name.
> If it is a sub-account or collaborator account, please contact master account to get authorization. For example, you should get the write permission and QcloudDNSPodFullAccess permission corresponding to CDN acceleration domain name.

### Completing CNAME settings

After submitting resolution for quick configuration, it will take about 1 minute to take effect. You can refresh [Domain Name Management] page(https://console.cloud.tencent.com/cdn/domains) in CDN console. When the CNAME status changes to activated, you can hover over the icon in front of CNAME to view a note, i.e. acceleration service is in normal operation.

>? If you do not want to use this feature, you can configure CNAME by yourself. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

## Others
If you delete the corresponding acceleration domain name, we will not operate your resolution records in DNSPod. Please modify resolution records as needed.

