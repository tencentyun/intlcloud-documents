You can view all HAVIP details in a specific region on the HAVIP console.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/).
2. Select **IP and Interface** > **HAVIP** on the left sidebar to enter the HAVIP management page.
3. Select a target region to view the details of all HAVIPs you have applied for.
	The field description is as follows:
	+ ID/Name: ID refers to the auto-generated ID of the HAVIP after being created. You can click on it to view the basic information of the HAVIP. Name is defined by the user when the HAVIP is created.
	+ Status: indicates whether the HAVIP is specified as a floating IP address in the configuration file of the HA software on CVM. A successfully configured HAVIP will be in **Bound with CVM** status, otherwise it is in the **Not bound with CVM yet** status.
	+ Address: HAVIP address.
	+ Backend ENI: refers to the ENI ID of the bound CVM. If the HAVIP is not bound with CVM yet, this field will be displayed as **-**.
	+ Server: refers to the ID of the bound CVM. If the HAVIP is not bound with CVM yet, this field will be displayed as **-**.
	+ EIP: refers to the bound EIP. If the HAVIP is not yet bound with an EIP, this field will be displayed as **-**.
	+ Virtual Private Cloud: refers to the VPC of the HAVIP.
	+ Subnet: refers to the subnet of the HAVIP.
	+ Application Time: refers to the time when this HAVIP is applied for.
	+ Operation: refers to the supported operations, including **Bind**, **Unbind**, and **Release**.
	   +  Bind: binds an EIP
	   +  Unbind: unbinds an EIP
	   +  Release: releases the HAVIP
3. Enter ID, name or address in the search box on the right to quickly search for HAVIPs.
4. Click the icon next to the search box to refresh the page.
