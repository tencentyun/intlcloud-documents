You can view all HAVIP details in a specific region on the HAVIP console.
>? HAVIP is now only available for beta users. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>


## How It Works
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/).
2. Select **IP and ENI** > **HAVIP** on the left sidebar to enter the HAVIP management page.
3. Select a target region.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/imK6454_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230330100432.png)
	The field description is as follows:
	+  **ID/Name**: An ID is generated automatically when an HAVIP is created. You can set a custom name for the HAVIP. Click on the ID to view the basic information of the HAVIP. 
	+ **Status**: It indicates whether the HAVIP is specified as a floating VIP in the configuration file of the HA software on CVM. If yes, the status of the HAVIP is **Bound with CVM** status, otherwise the status is **Not bound with CVM yet**.
	+ **Address**: HAVIP address.
	+ **Backend ENI**: ENI ID of the bound CVM. If it is not bound with a CVM, this field is **-**.
	+ **Server**: ID of the bound CVM. If it is not bound with a CVM, this field is **-**.
	+ **EIP**: EIP bound with the HAVIP. If it is not bound with an EIP, this field is **-**.
	+ **Network**: VPC of the HAVIP.
	+ **Subnet**: Subnet of the HAVIP.
	+ **Application time**: The time when this HAVIP is applied for.
	+ **Operation**: Bind/Unbind an EIP to/from the HAVIP; release the HAVIP
	    
	    
	    
3. Enter ID, name or address in the search box on the right to quickly search for HAVIPs.
4. Click the icon next to the search box to refresh the page.
