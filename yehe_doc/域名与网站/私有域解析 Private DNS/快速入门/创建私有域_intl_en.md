## Overview
This document describes how to create a private domain in the Private DNS console.


## Directions
1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns/domains) and click **Private Domain List** on the left sidebar to enter the private domain list.
2. In the **Private Domain List**, click **Create Private Domain** as shown below:
![](https://main.qcloudimg.com/raw/fda429c0062f6ce58b90cb5297604551.png)
3. On the **Create Private Domain** page, enter the private domain information as shown below:
![](https://main.qcloudimg.com/raw/402b8e8dc02c1a937086654393d6bab4.png)
 - **Domain Name**: enter the custom private domain name you want to create, i.e., the private domain name you want to associate with and use in a VPC.
>?
>- You can only create standard TLD domain names that comply with the IANA specifications.
>- After creating the private domain name, you need to set a DNS record for it and associate it with a VPC, and the record takes effect only in the associated VPC.
>
 - **Associated VPC**: select a VPC created in one of the regions currently supported by Private DNS for association. Private domain names with the same name cannot be associated with the same VPC.
>?
>- For a better experience, we recommend you create a private domain name and set a DNS record for it first before associating a VPC.
>- If no VPCs are displayed in the currently selected region, please create one in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1/).
>- If existing VPCs cannot meet your needs, you can modify them in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1/).
>- VPC regions currently supported for association include Beijing, Shanghai, Chengdu, Chongqing, Guangzhou, and Silicon Valley.
>
 - **Tag**: select a tag, through which you can categorize, search for, and aggregate Tencent Cloud resources. For more information, please see [Product Overview](https://intl.cloud.tencent.com/document/product/651/13334).
 - **Remarks**: enter the remarks of the private domain.
 - **Subdomain Recursive DNS**: select an option as needed. This feature is **disabled** by default. For more information, please see [Subdomain Recursive DNS](https://cloud.tencent.com/document/product/1338/50547).
4. Click **OK** to create the private domain.

## Subsequent Operations
For a private domain that has DNS records added, the value of **Records** in the private domain list represents the number of DNS records of the private domain.
In the [Private DNS console](https://console.cloud.tencent.com/privatedns/domains), click the name of the "private domain" you need to resolve to enter the DNS records page, where you can add records for the private domain. For detailed directions, please see [Setting DNS Record](https://cloud.tencent.com/document/product/1338/50538).


