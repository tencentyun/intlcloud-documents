After you add a private domain, it will not immediately override the corresponding domain name that exists on the public network. Only after it is associated with a VPC will it override the public network domain name when its resolved domain name is accessed in the VPC.

If you want to add a private domain DNS record that can resolve both private domains with DNS records configured in Private DNS and public domain names that are not configured in Private DNS, please enable the [subdomain recursive DNS](https://intl.cloud.tencent.com/document/product/1097/40566) feature.

The following is an example, and you should operate according to your actual situation:
### Step 1. Add a private domain (tencent.com)
After `tencent.com` is added as a private domain, if it is not associated with a VPC, it doesn't exist in any VPC. Therefore, when `tencent.com` is resolved, the DNS result on the public network will be returned.

### Step 2. Add a DNS record
If you want to associate the added private domain `tencent.com` with a VPC, you must add a corresponding DNS record for it. This is to avoid the situation where private network hijacking occurs for the domain being resolved when a private domain without DNS records is directly associated with a VPC.

Therefore, before associating a VPC, be sure to add the domain name you are accessing as a private domain. For detailed directions, please see [Creating Private Domain](https://intl.cloud.tencent.com/document/product/1097/40558).

### Step 3. Associate a VPC
>?If you have already associated a VPC when creating a private domain, ignore this step.
>
Please associate a private domain with the VPC where the CVM instance that needs to access the private domain is located. After the association, the DNS records of the private domain will override the domain name being resolved on the public network.

For example, the DNS record set for `tencent.com` in Private DNS is as follows:
>?For more information on how to add records, please see [Setting DNS Record](https://intl.cloud.tencent.com/document/product/1097/40569).
>
| Private Domain | Record Type | Record Value | TTL | 
|---------|---------|---------|---------|
| tencent.com | A | 1.1.1.1 | 300|

Then, when `tencent.com` is pinged on a CVM instance in the corresponding VPC, the displayed address will be `1.1.1.1`, and the resolved address of `www.tencent.com` on the public network will be overridden. 
