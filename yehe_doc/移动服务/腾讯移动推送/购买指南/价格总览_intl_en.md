This document describes the pricing and discount policies of two TPNS billing modes: monthly subscription and pay-as-you-go.
>! The monthly subscription mode is currently in beta test. To use it, please [contact sales](https://intl.cloud.tencent.com/contact-sales).

## Glossary
- Daily connected devices: the number of deduplicated online devices connected to the SDK on a day (the SDK will connect to the TPNS server when the application is running in the foreground or background).
- Monthly peak of daily connected devices: the highest number of daily connected devices in a month.
- Service access point: the region where the TPNS cluster is located. The restrictions on data access vary by region. You can select an application service access point when creating an instance in the console.

## Monthly Subscription
### Notes
- The billing unit of monthly subscription is 10,000 daily connected devices. You should purchase the service for at least 10,000 daily connected devices.

### Pricing
Because service costs vary by service access point, the corresponding prices are also different.

| Service Access Point | Unit Price (USD/10,000 Daily Connected Devices/Month) |
|---|---|
| Guangzhou | 42.237 |
| Hong Kong (China) | 56.316 |
| Singapore | 56.316 |

### Discounts
| Monthly Peak of Daily Connected Devices | Purchase Duration: 1–5 Months | Purchase Duration: 6–11 Months | Purchase Duration: 1 Year | Purchase Duration: 2 Years |
|---|---|---|---|---|
| 10,000–499,999 | None | None | None | None | None |
| 500,000–1,999,999 | 10% off | 20% off | 35% off | 40% off |
| 2,000,000 and above | 30% off | 35% off | 40% off | 50% off |

### Billing examples
**Billing example 1**
- The service access point is Singapore.
- The monthly peak of daily connected devices for the application on Android is 600,000.
- The purchase duration of the package is 12 months.
The total fees of the package will be monthly fees * duration * discount = (60 * 56.316) * 12 * 0.65 = 26355.7944 USD.

**Billing example 2**
- The service access point is Guangzhou.
- The monthly peak of daily connected devices for the application on iOS is 100,000.
- The purchase duration of the package is 1 month.
The total fees of the package will be monthly fees * duration * discount = (10 * 42.237) * 1 * 1 = 422.37 USD.

## Pay-as-You-Go

### Pricing

- In daily pay-as-you-go billing mode:
	- Daily connected devices ≤ 1,000: no fees will be incurred for the day.
	- 1000 < daily connected devices ≤ 50,000: fees will be incurred and settled at the fixed prices as listed below.
	- Daily connected devices > 50,000: fees will be incurred and settled at the elastic prices as listed below.
	- The continuous usage duration is calculated from the day when the pay-as-you-go billing mode is enabled for the application for the first time, and will not be cleared if the service is suspended or terminated during use (if the number of daily connected devices on a day is less than or equal to 1,000 with no fees incurred, then the day will not be included in the continuous usage duration).
	
Because service costs vary by service access point, the corresponding prices are also different. Specific prices are listed in the table below.

#### 1,000 < daily connected devices ≤ 50,000: fixed pricing

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
| Continuous Usage Duration (Days) | Discount |
|:---|:---|
| 1–180 | None |
| 181–360 | 20% off |
| 361–720 | 35% off |
| > 720 | 40% off |

### Billing examples
- If the service access point is Singapore and the number of daily connected devices is less than or equal to 50,000, the daily fees will be fixed at 10.7 USD.
- If the service access point is Singapore and the number of daily connected devices is 70,000, then:
	- If the service has been used continuously for 90 days, there will be no discount, and the daily fees will be 70,000 * 0.000214 = 14.98 USD.
	- If the service has been used continuously for 200 days, then a 20% discount will be applied, and the daily fees will be 70,000 * 0.000214 * 0.8 = 11.984 USD.


