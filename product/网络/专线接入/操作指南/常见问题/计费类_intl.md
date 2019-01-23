### How is Direct Connect product charged?
The charges for Direct Connect product include:


- Laying fee of Connection, which is charged by ISP or Tencent Cloud Direct Connect partner.
- One-off fee for connection to Tencent Cloud: 2,500 USD, including Tencent Cloud port fee and test fee.
- Fee for cross-city Dedicated Tunnel. For more information on charging standard, please see Price Overview.


### How to cancel Direct Connect?
Direct Connect services to be cancelled include:
1. Connection: You need to submit an application for cancellation to the ISP;
2. Dedicated Tunnel: You can apply to delete the Dedicated Tunnel in the console, and the fee for cross-city Dedicated Tunnel of that month is deducted at the beginning of next month;



### What is the billing method for creating multiple tunnels in non-VLAN mode?
If multiple tunnels are created without sub-APIs enabled (VLAN mode), these tunnels share the traffic bandwidth of a physical port, that is, the traffic data of all the tunnels in this Connection cannot be distinguished.

For the postpaid billing based on Monthly 95th Percentile, if multiple tunnels are created for a Connection in non-VLAN mode, including inter-city/cross-city tunnels, the Connection is charged as follows:

1. Object: Only the Dedicated Tunnel with the highest unit price is charged for this Connection.
2. Payment method: According to Monthly 95th Percentile billing for Dedicated Tunnel, the tunnel is billed on a monthly basis by calculating monthly 95th percentile bandwidth with the traffic collected from the physical port of this Connection.

Therefore, intra-city Direct Connect may be charged in non-VLAN mode. It is recommended to use VLAN mode to cut cost.

