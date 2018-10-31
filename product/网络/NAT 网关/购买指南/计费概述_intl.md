This document describes the charges and pricing standards for NAT gateways.

## Billing

Charges for a NAT gateway include charges for the gateway (billed by the hour) and fees for traffic generated during access to the Internet.

- For the charges for the gateway, see **Billing Method**.
- For the traffic fees, see bill-by-traffic in [CVM Network Fee](/document/product/213/10578).

## Billing Method

Charges for a NAT gateway include a gateway rental fee (billed by the hour) and fees for traffic generated during access to the Internet. The pricing is shown below:

| Billing Item | Specification | Mainland China (all regions) | Hong Kong, Singapore, Korea, Frankfurt, Silicon Valley, Bangkok | Toronto, Mumbai | Virginia |
| ---------------------------------- | ------------------------ | -------------------- | ------------------------------------------------------------ | --------------- | -------- |
| "Rental fee for gateway (USD/hour)" | Small (a maximum of 1,000,000 connections) | 0.089 | 0.13 | 0.14 | 0.18 |
| (Merge cells of this column) | Medium (a maximum of 3,000,000 connections) | 0.28 | 0.39 | 0.42 | 0.54 |
| (Merge cells of this column) | Large (a maximum of 5,000,000 connections) | 0.89 | 1.3 | 1.4 | 1.8 |

The fees for traffic generated during access to the Internet are as follows: 

| Billing Item | Mainland China (all regions), Hong Kong, Korea | Toronto, Frankfurt, Silicon Valley | Singapore | Virginia, Mumbai | Bangkok |
| ---------------------------------- | -------------------------------------- | ---------------------------------- | --------- | ---------------- | ------- |
| Fees for traffic generated during access to the Internet (USD/GB) | 0.12 | 0.077 | 0.081 | 0.1 | 0.075 |

> Notes:
>
> - For accounts with a bandwidth package for bandwidth sharing, the fee for the outbound traffic from the NAT gateway is covered by the bandwidth package (the network traffic fee is not charged additionally). It is recommended that you set a limit on the outbound bandwidth of the NAT gateway to avoid high bandwidth package fees due to excessive use of the outbound bandwidth of the NAT gateway. For more information, see [Bill by Bandwidth Package](/document/product/213/10578).
> - Arrear logic: [Consistent with the postpaid CVM](/document/product/213/2181).
> - As the NAT gateway features master/slave hot backup, the system sends a 5 KB detection packet to the master/slave servers of the NAT gateway every three seconds. This results in a traffic of 0.2747 GB each day.


