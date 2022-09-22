This document describes the pricing and discount policies of two TPNS billing modes: monthly subscription and pay-as-you-go.
>! The monthly subscription mode is currently in beta. To use it, please [contact sales](https://intl.cloud.tencent.com/contact-sales).

## Glossary
- Daily active users (DAUs): the number of unique online devices connected to the SDK on a day (the SDK will connect to the TPNS server when the application is running in the frontend or backend).
- Monthly peak of DAUs: the highest number of DAUs in a month
- Service access point: the region where the TPNS cluster is located. The restrictions on data access vary by region. You can select an application service access point when creating an instance in the console.

## Monthly Subscription
### Notes
- Monthly subscription is billed per 10,000 DAUs, making 10,000 DAUs the minimum purchase required.

### Pricing description
Because service costs vary by service access points, their corresponding prices are also different.

| Service Access Point | Unit Price (USD/10,000 DAUs/Month)
| ---------- | --------------------------------- |
| Guangzhou | 42.237                            |
| Hong Kong (China) | 56.316                            |
| Singapore | 56.316                            |

### Discounts
| Monthly Peak of DAUs | Purchase Duration: 1−5 Months | Purchase Duration: 6−11 Months | Purchase Duration: 1 Year | Purchase Duration: 2 Years |
| ------------------ | --------------------- | ---------------------- | -------------- | -------------- |
| 10,000−490,000  | None | None | None | None |
| 500,000−1.99 million | 10% off | 20% off | 35% off | 40% off |
| 2 million or above  | 30% off | 35% off | 40% off | 50% off |

### Billing examples
**Billing example 1:**
- The service access point is Singapore.
- The monthly peak of DAUs for the application on Android is 600,000.
- The purchase duration of the package is 12 months.
The total package fees will be: Monthly fees x Duration x (1 - Discount) = (60 x 56.316) x 12 x 0.65 = 26355.7944 USD.

**Billing example 2:**
- The service access point is Guangzhou.
- The monthly peak of DAUs for the application on iOS is 100,000.
- The purchase duration of the package is 1 month.
The total package fees will be: Monthly fees x Duration x (1 - Discount) = (10 x 42.237) x 1 x 1 = 422.37 USD.

## Pay-as-you-go

### Pricing description

The following applies for the daily pay-as-you-go billing mode:
	- DAUs <= 1,000: No fees will be incurred for the day.
	- 1,000 < DAUs <= 10,000: Fees will be incurred and settled at the fixed prices listed below.
	- DAUs > 10,000: Fees will be incurred and settled at the elastic prices listed below.
	- The continuous usage duration starts on the day when an application enables pay-as-you-go billing for the first time. If the service is suspended or terminated during usage, the duration will not revert to 0. If the number of DAUs is less than or equal to 1,000 with no fees incurred, that day will not be included in the continuous usage duration.
	

Because service costs vary by service access points, their corresponding prices are also different, as shown below:

#### 1,000 < DAUs <= 10,000: fixed price

| Service Access Point | Unit Price (USD/Day) |
| ---------- | ----------------- |
| Guangzhou | 1.6               |
| Hong Kong (China) | 2.14              |
| Singapore | 2.14              |

>! 
>- The threshold for elastic pricing was lowered from 50,000 to 10,000 DAUs on January 4, 2021.
>- If the number of DAUs was less than 50,000 and pay-as-you-go billing was adopted before January 4, 2021, elastic pricing will be automatically applied from January 4, 2021.

#### DAUs > 10,000: elastic pricing
| Service Access Point | Unit Price (USD/DAU/Day)
| ---------- | ------------------------------ |
| Guangzhou  | 0.000160                       |
| Hong Kong (China) | 0.000214                       |
| Singapore | 0.000214                       |

### Discounts
| Continuous Usage Duration (Day) | Discount |
| :----------------- | :----- |
| 1−180            | None |
| 181−360          | 20% off   |
| 361−720          | 35% off |
| Over 720              | 40% off |

### Billing examples
- If the service access point is Singapore and the number of DAUs is less than or equal to 10,000, the daily fee will be fixed at 2.14 USD.
- If the service access point is Singapore and the number of DAUs is 70,000, then:
	- If the service has been used continuously for 90 days, there will be no discount, and the daily fee will be 70,000 x 0.000214 = 14.98 USD.
	- If the service has been used continuously for 200 days, then a 20% discount will be applied, and the daily fee will be 70,000 x 0.000214 x 0.8 = 11.984 USD.