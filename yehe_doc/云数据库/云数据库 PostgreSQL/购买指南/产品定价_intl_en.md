## Billing Mode

TencentDB for PostgreSQL offers the following two billing modes:

| Billing Mode | Payment Method                                                     | Use Case                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Pay-as-you-go | [Postpaid](https://intl.cloud.tencent.com/document/product/555/30328). You can request for resources on-demand and will be charged based on the actual usage upon settlement. | Suitable for businesses with fluctuating demands. Instances can be released immediately after use to reduce costs. |

The pay-as-you-go tiered pricing model is based on usage duration.

| Usage Duration              | Tiered Price             |
| ---------------------- | -------------------- |
| 0 hours<duration≤96 hours   | Tier 1 rate applies |
| 96 hours<duration≤360 hours | Tier rate applies |
| Duration>360 hours          | Tier 3 rate applies |

## Instance Price

### Billing formula

**Total fee = Memory fee + Disk fee**


### Pay-as-you-go price
#### Memory price

|   Tier   | Guangzhou, Shanghai, Beijing<br>Nanjing, Tianjin, Shenzhen, Chengdu<br>(USD/GB/hr)  | Hong Kong (China)<br>(USD/GB/hr)  | Silicon Valley, Virginia, Frankfurt<br>(USD/GB/hr)  |  Moscow, Seoul, Bangkok<br>(USD/GB/hr) | Singapore (USD/GB/hr) |
| ------ |--------------- | -------------- | -------------- |--------------- |--------------- |
| Tier 1 |          0.052        |         0.069        |      0.055        | 0.056  | 0.07 |
| Tier 2 |           0.039        |         0.052        |      0.041         | 0.042  | 0.053 |
| Tier 3 |             0.026         |         0.034        |      0.028      | 0.028  | 0.035 |

>?If a pay-as-you-go instance configuration is adjusted, it will be start charging from the tier-1 price again.

#### Disk price

|                Region                   | Price (USD/GB/hr) |
| :--------------------------------: | :----------------:         |
| Guangzhou, Shanghai, Beijing, Nanjing, Tianjin, Shenzhen, Chengdu      |       0.0005        |
|  Silicon Valley, Virginia                   |       0.00019   |
|Frankfurt                   |0.00028|
|  Moscow                                                |       0.00031  |
|  Bangkok                                                   |       0.00024 |
|  Seoul, Singapore, Hong Kong (China)                                |       0.00024  |


## Value-Added Services
- **Backup and log capacity**: you will receive 50% of the instance capacity for free to use as backup and log capacity. Any usage exceeding this complimentary capacity is currently free as well.
- **Public network traffic**: this is the traffic sent from the TencentDB instance to the client over a public network, which is currently free.

## Billing Example

**Pay-as-you-go billing example**: suppose you purchase a pay-as-you-go TencentDB for PostgreSQL instance with 32 GB memory and 500 GB disk capacity in the Singapore region and you use this instance for 400 hours.
The fees are calculated as follows:

Tier 1 fee: (32 GB x 0.07 USD/GB/hr + 500 GB x 0.00024 USD/GB/hr) x 96 hours = 226.56 USD
Tier 2 fee: (32 GB x 0.053 USD/GB/hr + 500 GB x 0.00024 USD/GB/hr) x 264 hours = 479.556 USD
Tier 3 fee: (32 GB x 0.035 USD/GB/hr + 500 GB x 0.00024 USD/GB/hr) x 40 hours = 49.6 USD
Your instance fees = Tier 1 fee + Tier 2 fee + Tier 3 fee = 755.716 USD
