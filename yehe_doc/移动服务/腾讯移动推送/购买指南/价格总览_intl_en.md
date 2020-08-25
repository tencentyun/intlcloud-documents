This document describes the pricing and discount policies of two TPNS billing modes: monthly subscription and pay-as-you-go.
>! Monthly subscription is currently in beta. If you wish to use this billing option, please [contact sales](https://intl.cloud.tencent.com/contact-sales)

## Glossary
- Daily connected devices: the number of deduplicated online devices connected to the SDK on a day (SDK will connect to the TPNS server when the application is running in the foreground or background).
- Monthly peak of daily connected devices: the highest number of daily connected devices in a month.
- Service access point: the region where the TPNS cluster is located. The restrictions on data access vary by regions. You can select an application service access point when creating an instance on the console.

## Monthly Subscription
### Notes
- The billing unit of monthly subscription is 50,000 daily connected devices. You should purchase the service for at least 50,000 daily connected devices.
- The value of the "monthly peak of daily connected devices" must be a multiple of 5. Otherwise, the system will round down the value.

### Pricing
Because service costs vary by service access points, the corresponding prices are also different.

| Service Access Point | Unit Price (USD/50,000 Daily Connected Devices/Month) |
|---|---|
| Guangzhou | 211.184 |
| Hong Kong (China) | 281.579 |
| Singapore | 281.579 |

### Discounts
| Monthly Peak of Daily Connected Devices | Purchase Duration: 1–5 Months | Purchase Duration: 6–11 Months | Purchase Duration: 1 Year | Purchase Duration: 2 Years |
|---|---|---|---|---|
| 50,000–450,000 | None | None | None | None | None |
| 500,000–1.95 million | 10% off | 20% off | 35% off | 40% off |
| 2 million–100 million | 30% off | 35% off | 40% off | 50% off |

### Billing Example
- If the service access point is Singapore, the monthly peak of daily connected devices is 600,000, and the package duration is 12 months, the total package fee will be:
`Monthly fees * Duration * Discount` = 
(60 / 5 * 281.579) * 12 * 0.65 = 26,355.7944 USD.
- Suppose the service access point is Singapore, the monthly peak of daily connected devices is 40,000, and the package duration is 2 months. As the minimum billing unit of monthly subscription is 50,000 daily connected devices, the monthly fee will be 281.579 USD and the total package fee will be:
`Monthly fees * Duration * Discount` = 281.579 * 2 * 1 = 563.158 USD.

## Pay-as-you-go
### Notes
- For pay-as-you-go billing mode, the minimum purchase quantity is 50,000 daily connected devices. If the actual number of daily connected devices is less than 50,000, it will be calculated as 50,000.
- The continuous usage duration starts on the day when an application has pay-as-you-go billing enabled for the first time. If the service is suspended or terminated during usage, the duration will not revert to 0.

### Pricing
Because service costs vary by service access points, the corresponding prices are also different.

#### Daily connected devices ≤ 50,000: fixed price

| Service Access Point | Unit Price (USD/Day) |
|---|---|
| Guangzhou | 8 |
| Hong Kong (China) | 10.7 |
| Singapore | 10.7 |

#### Daily connected devices > 50,000: elastic pricing
| Service Access Point | Unit Price (USD/Daily Connected Devices/Day) |
|---|---|
| Guangzhou | 0.000160 |
| Hong Kong (China) | 0.000214 |
| Singapore | 0.000214 |

### Discounts
| Continuous Usage Duration (Day) | Discount |
|:---|:---|
| 1–180 | None |
| 181–360 | 20% off |
| 361–720 | 35% off |
| > 720 | 40% off |

### Billing Example
- If the service access point is Singapore and the number of daily connected devices is less than or equal to 50,000, the daily fee will be fixed at 10.7 USD.
- If the service access point is Singapore and the number of daily connected devices is 70,000, then:
	- If the service has been used continuously for 90 days, there will be no discount, and the daily fee will be 70,000 * 0.000214 = 14.98 USD.
	- If the service has been used continuously for 200 days, then a 20% discount will be applied, and the daily fee will be 70,000 * 0.000214 * 0.8 = 11.984 USD.
