## Billing Mode

- Intra-region peering connection is available for free.
- Cross-region peering connection is paid by the peering connection initiator. It supports:
  - Billing by daily peak bandwidth. See its description below.

### Billing by daily peak bandwidth

- Calculation formula:

  Daily fees=Peak bandwidth of the day*Applicable tiered price.

  > **Note:**
  > Peak bandwidth of the day is calculated as follows: Inbound/outbound bandwidth is captured every 5 minutes, and the maximum is taken as the peak bandwidth.

- **Billing period and calculation period:** Daily

- **Billing mode:** Postpaid on a daily basis

- **Price Overview**:

  | Feature | Billing Mode | Configuration | Price |                                                              |                                                              |
  | -------------- | ------------------------------------------------------------ | ----------------- | ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
  |                |                                                              |                   | Connection in Mainland China (all regions) | Connection between Mainland China (all regions) and regions outside Mainland China (Hong Kong, Korea, Frankfurt, Silicon Valley, Virginia, Mumbai, Singapore, Toronto, Bangkok) | Connection between regions outside Mainland China (Hong Kong, Korea, Frankfurt, Silicon Valley, Virginia, Mumbai, Singapore, Toronto, Bangkok) |
  | Intra-region peering connection | Free |                   |                          |                                                              |                                                              |
  | Cross-region peering connection | Billed by peak bandwidth of the day on a daily basis (USD/Mbps/day). Peak bandwidth is calculated using the average bandwidth per 5 minutes | (0 , 20] Mbps     | 3.19                     | 15                                                           | 15                                                           |
  |                |                                                              | (20 ,100] Mbps    | 1.98                     | 12                                                           | 12                                                           |
  |                |                                                              | (100 , 500] Mbps  | 1.48                     | 9                                                            | 9                                                            |
  |                |                                                              | (500 , 2000] Mbps | 1.19                     | 6                                                            | 6                                                            |
  |                |                                                              | Greater than 2000 Mbps | 0.82                     | 5                                                            | 5                                                            |

> **Notes:**
>
> 1. Please contact your sales rep for more information about regional pricing.
> 2. In the billing system, peering connection is as: bill for cross-region interconnection (mainland) and bill for peering connection of which both ends are in Mainland China.
> 3. Basic network cross-region interconnection is **not supported in the following regions**: Shanghai Finance, Shenzhen Finance and Silicon Valley.

- **An example of billing by daily peak bandwidth:**
  If the initiator and receiver of a peering connection locate in Shanghai and Guangzhou respectively, and the outbound and inbound peak bandwidth of the day are 20 Mbps and 30 Mbps respectively, the cost of the day is calculated as 30*1.98=59.4 USD, which shall be paid by the initiator.
