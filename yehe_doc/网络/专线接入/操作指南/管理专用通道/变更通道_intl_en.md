After you create a dedicated tunnel connected to different Direct Connect gateways, you can change the tunnel parameters in the Direct Connect Console. This document describes how to do so.
## Prerequisites
You need to [apply for a tunnel](https://intl.cloud.tencent.com/document/product/216/19250) before you can modify it.
## Directions

1. Log in to the [Direct Connect Console](https://console.cloud.tencent.com/dc/conn).
2. On the "Dedicated Tunnel" page, find the tunnel whose parameters need to be changed, and select **More** > **Tunnel Change** in the "Operation" column on the right.
3. In the "Tunnel Change" pop-up window, you can change the following parameters:
	- Bandwidth cap: changing the bandwidth cap will not interrupt the business, and the system will automatically overwrite the original configuration.
>?In the shared connection mode, you cannot apply for a bandwidth change for a dedicated tunnel; instead, such a change can only be applied for by the connection owner.
	- Tencent Cloud Perimeter IP: changing the Tencent Cloud perimeter IP will interrupt the business.
	- Secondary Tencent Cloud Perimeter IP: changing the secondary Tencent Cloud perimeter IP will interrupt the business.
	- User Perimeter IP: changing the user perimeter IP will interrupt the business.
	- User IDC IP Range (Static Routing): you can modify the user IDC IP range. After the modification is completed, the system will automatically deliver the new configuration.
	- BGP ASN (BGP Routing): changing the BGP ASN will interrupt the business.
	- BGP Key (BGP Routing): changing the BGP key will not interrupt the business, and the system will automatically overwrite the original configuration.
	>?The BGP key cannot contain ?, &, space, ", \, and +.
4. After changing the parameters, click **OK**.
>?After the tunnel change request is submitted, the system will complete the device configuration within a few minutes (subject to the network conditions).

## Use Limits on Large IP Range
To ensure the fine-grained scheduling capability of your network, do not publish the following routes:
`9.0.0.0/8`, `1,0.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12`, `192.168.0.0/16`.
>!If a large IP range route is published, the direct connect gateway will directly reject it.

 You can split the above routes as follows for distribution:
 
 - <strong>`9.0.0.0/8`</strong>
should be split into `9.0.0.0/9` + `9.128.0.0/9`.
 - <strong>`10.0.0.0/8`</strong>
should be split into `10.0.0.0/9` + `10.128.0.0/9`.
 - <strong>`172.16.0.0/12`</strong>
should be split into `172.16.0.0/13` + `172.24.0.0/13`.
 - <strong>`192.168.0.0/16`</strong>
should be split into `192.168.0.0/17` + `192.168.128.0/17`.
 - <strong>`100.64.0.0/10`</strong>
should be split into `100.64.0.0/11` + `100.96.0.0/11`.
 - <strong>`131.87.0.0/16`</strong>
should be split into `131.87.0.0/17` + `131.87.128.0/17`.
 - <strong>`172.16.0.0/12`</strong>
should be split into `172.16.0.0/13` + `172.24.0.0/13`.
 - <strong>`192.168.0.0/16 `</strong>
should be split into `192.168.0.0/17` + `192.168.128.0/17`.
