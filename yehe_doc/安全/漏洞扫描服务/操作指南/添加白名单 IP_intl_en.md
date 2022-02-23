This document describes how to add the monitoring IPs of VSS to the allowlist.
## Overview

VSS simulates hacker intrusion attacks to conduct asset discovery and risk monitoring over the public network. If your server has security protection or monitoring services such as WAF and SOC deployed, we recommend you add the monitoring IPs of VSS to the allowlist and grant them scanning access, so that the monitoring service can work smoothly. Such service node scanning IPs include:
119.28.101.45
119.28.101.51
150.109.12.53 
101.32.239.31
101.32.242.117
If your website can be accessed only after login, you need to suspend the security policy (to ensure that the website can be accessed from all IPs) and resume it after your cookie validity is verified.  

## Directions

### Method 1: allow IPs through IP query

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/ip/query) and select **IP Management** > **IP Query** on the left sidebar to enter the IP query page.
2. On the IP query page, enter the IP address to be queried, click **Query**, and the query result will be displayed.
3. Click **Add to Blocklist/Allowlist** to enter the **Add Blocked/Allowed IP** page, where you can manually add IPs to the allowlist. Select **Allowlist** as the category, enter the IP address to be allowed, select the expiration time of the allowlist, and click **Add**.

### Method 2: add IPs directly to the allowlist
Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/ip/list) and select **IP Management** > **IP Blocklist/Allowlist** on the left sidebar to enter the IP blocklist/allowlist page.
- **Method 1**: manually add IPs to the allowlist.
 1. On the IP blocklist/allowlist page, click **Add to Blocklist/Allowlist**, and the **Add Blocked/Allowed IP** window will pop up.
 2. In the **Add Blocked/Allowed IP** window, select **Allowlist** as the category, copy the scanning node IPs of VSS into the IP address input box, select the expiration time of the allowlist, and click **Add**.
>?Up to 100 IP addresses can be entered and separated by line break.

- **Method 2**: batch import IPs to the allowlist.
	1. On the IP blocklist/allowlist page, click **Import Data**, and the **Import IP List** window will pop up.
	2. In the **Import IP List** window, click **Import**, select the allowlist file to be imported, and click **Confirm Import** after successful upload.
>?
>- Import file format: only .xlsx and .xls files are supported.
>- Quantity: currently, only one single file can be uploaded.
>- Content: the file must include three columns: category, IP address, and end time. For more information on the format, see the exported Excel file.
>- The end time must be before 2033/12/30 23:59:59 in the format of `YYYY/MM/DD HH:MM:SS`.



### Method 3: add blocked IPs to the allowlist.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/ip/record) and select **IP Management** > **IP Blocking Status** on the left sidebar to enter the IP blocking status page.
2. On the IP blocking status page, enter the relevant information, click **Query** to query the relevant IPs of VSS, and then add them to the allowlist.
