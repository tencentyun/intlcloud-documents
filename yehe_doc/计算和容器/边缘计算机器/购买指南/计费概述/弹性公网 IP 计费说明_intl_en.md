

An EIP is a public IP address used in an ECM instance. If it is idle, IP resource fees will be charged.
<dx-alert infotype="explain" title="">
An EIP that is not bound to an edge resource and thus idle will incur IP resource fees. If it is bound to an edge resource and takes effect, it will incur public network fees but not IP resource fees. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1119/43404).
</dx-alert>

## Billing
 IP resource fees are postpaid hourly, that is, the fees for an hour will be billed and charged in the next hour.

- Billing of the IP resource fees starts when the EIP is applied for, pauses when it is bound to an edge resource, resumes when it is unbound and becomes idle, and stops when it is released.
- Billing won't pause if the EIP is bound to an edge resource in the following status:
 - The EIP is bound to an ENI that is not bound to an instance.
 - The EIP is bound to a high-availability VIP that is not bound to an instance.



## Billing Formula

IP resource fees = EIP hourly unit price * billing period



## Pricing

| Region         | Price (CNY/Hour) |
| ------------ | --------------- |
| Chinese mainland | 0.20             |

<dx-alert infotype="notice" title="">
To avoid incurring unnecessary IP resource fees, bind your EIP to an edge resource immediately after applying for it and release it immediately after unbinding it from the resource.
</dx-alert>

