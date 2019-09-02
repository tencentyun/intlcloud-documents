Once your domain name is connected to LVB, the system will automatically assign it a CNAME domain name (suffixed with .liveplay.myqcloud.com) which you cannot access directly. You need to complete the CNAME configuration at your domain name service provider. After the configuration takes effect, LVB can be used properly. CNAME resolution is required for both playback domain name and push domain name.

## Settings for Tencent Cloud
If your DNS service provider is Tencent Cloud, you can add a CNAME record in the following steps:
1. Log in to the [Domain Name Service Console](https://console.cloud.tencent.com/domain) and click **Resolve** to the right of the domain name for which you want to add a CNAME record.


2. Go to the DNS page of the specified domain name and click **Add a Record**.

3. Enter a domain name prefix in **Host Record** (such as www; if you want to directly resolve the primary domain name, enter @; if you want to resolve a wildcard domain name, enter \*), set the **Record Type** to CNAME, enter the CNAME domain name in **Record Value**, and click **Save** to add the CNAME record.


