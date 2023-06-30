
ECM instances use EIPs as their public IPs. When EIPs are in idle status, they will incur IP resource fees. 

<dx-alert infotype="explain" title="">
- An EIP is considered “Idle” when it’s not bound to any cloud resource, and an IP resource fee will incur. For details of the IP resource fee, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1119/43404).
- Starting from June 1, 2022 at 00:00 (UTC+8), Tencent Cloud Edge Compute Machine supports daily billing for the network bandwidth of EIPs. For details, see [ECM Billing Overview](https://intl.cloud.tencent.com/document/product/1119/43404). [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) if you have any questions. 
</dx-alert>

## Billing modes
 The IP resource fee is calculated and settled on an hourly basis. The fees for an hour will be billed and charged in the next hour.

- The billing of the IP resource fee starts from the EIP is assigned. It stops when the EIP is bound to a cloud resource, and resumes when the EIP becomes idle. When the EIP is released, the billing of IP resource fee stops. 
- The billing of IP resource fee does not stop if the EIP is bound to an edge resource in the following status:
 - The EIP is bound to an ENI that is not bound to an instance.
 - The EIP is bound to a high-availability VIP that is not bound to an instance.



## Billing Formula

IP resource fee = EIP hourly rate × Billable period



## Pricing

| Region         | Price (USD/Hour) |
| ------------ | --------------- |
| Chinese mainland | 0.031             |

<dx-alert infotype="notice" title="">
To avoid unnecessary costs, bind your EIPs with cloud resources after they’re assigned to your account immediately, and release them immediately after unbinding them with cloud resources.
</dx-alert>

