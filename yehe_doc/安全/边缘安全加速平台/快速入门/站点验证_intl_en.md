## Overview
You may need to pass site verification to prove your ownership of a site in the following cases:

- You discover that a site has already been added by another account when adding it.
- You select the CNAME connection method when adding a site.
- You switch the NS connection method of a site to CNAME connection in the DNS service menu.

>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Directions
EdgeOne uses a TXT record to verify your domain ownership. The steps are as follows:
1. Log in at your DNS service provider.
2. Add a TXT record and the specified host record and record value as required.
3. Wait for the system to automatically complete the verification. If the record does not take effect after a long time, you can click **Refresh** to trigger system verification.
4. After the record takes effect, click **Complete Verification** to complete site verification.
![](https://qcloudimg.tencent-cloud.cn/raw/13501666d4cc178c7552ca31ce090f7b.png)
