This document describes rates and billing for NAT gateways.

## Billing

NAT gateway charges include two parts: the gateway fee (billed by hour) and the Internet access traffic fees.

- For gateway fee, see **Billing Method**.
- For traffic fees, see bill-by-traffic in [CVM Network Fee](/document/product/213/10578).

## Billing Method

NAT gateway charges include two parts: the gateway rental fee (billed by hour) and the Internet access traffic fees. Below is the gateway rates:

| Billable Item | Specification | Mainland China (all regions) | Hong Kong, Singapore, Korea, Frankfurt, Silicon Valley & Bangkok | Toronto & Mumbai | Virginia |
| ---------------------------------- | ------------------------ | -------------------- | ------------------------------------------------------------ | --------------- | -------- |
| Gateway Rental Fee | Small (1,000,000 connections maximum) | 0.089 | 0.13 | 0.14 | 0.18 |
| Gateway Rental Fee | Medium (3,000,000 connections maximum) | 0.28 | 0.39 | 0.42 | 0.54 |
| Gateway Rental Fee | Large (5,000,000 connections maximum) | 0.89 | 1.3 | 1.4 | 1.8 |

Internet access traffic rates are as follows: 

| Billable Item | Mainland China (all regions), Hong Kong & Korea | Toronto, Frankfurt & Silicon Valley | Singapore | Virginia & Mumbai | Bangkok |
| ---------------------------------- | -------------------------------------- | ---------------------------------- | --------- | ---------------- | ------- |
| Internet access traffic fees (USD/GB) | 0.12 | 0.077 | 0.081 | 0.1 | 0.075 |

> Notes:
>
> - If your account has the bandwidth package for bandwidth sharing, your bandwidth package will cover the NAT gateway-generated outbound traffic (network traffic fee will not be charged additionally). It is recommended that you set a limit on the outbound bandwidth of the NAT gateway to avoid high bandwidth package fees due to excessive use of the outbound bandwidth of the NAT gateway. For more information, see [Bill by Bandwidth Package](/document/product/213/10578).
> - Arrear is determined in the same way as [Postpaid CVM](/document/product/213/2181).
> - As the NAT gateway features master/slave hot backup, the system sends a 5 KB detection packet to the master/slave servers of the NAT gateway every three seconds. This results in a traffic of 0.2747 GB each day.


