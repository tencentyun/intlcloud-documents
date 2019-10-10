**Overview**

A reserved instance (RI) is not a cloud virtual machine (CVM). However, RIs provide discounts for running pay-as-you-go CVMs. If the attributes of your CVM matches that of the RI, your CVM is automatically eligible for the discount provided by that RI. You can purchase and activate a RI for your existing CVM or buy one before even purchasing a CVM. Once the deposit is paid, the RI automatically applies its discount to your instance usage within the valid period. Compared to monthly subscription or pay-as-you-go billing modes, RIs provide you flexibility and save you money with significant discounts.

**Supported Products**

CVM

**Purchasing RIs**

- RIs let you choose the type of CVM that best fits your needs and budget. You can choose type (model and configuration), payment method, region, validity period, and quantity of your RI.

- Currently, you can purchase RIs through TencentCloud API. For more information, see the CVM product description;

-   RIs are non-refundable.

**RI-supported Instance Types and Prices:**

For more information about the configurations, matching rules and pricing of the RI-supported instance types, see the CVM product documentation.

**Payment Method (Currently only support All Upfront)**

- All Upfront: All fees are prepaid at the time of purchase and no additional fees will be incurred during the usage of RIs. This option provides the biggest discount compared to the pricing of on-demand instances described below.

- Partial Upfront: A prepayment of a lower amount is made at the time of purchase, and the instance fees are paid at the monthly rate or the discounted hourly rate during the usage of RIs;

- No Upfront: No fees are charged at the time of purchase, and the instance fees are paid at the monthly rate or the discounted hourly rate during the usage of RIs;

Note: When using RIs, you will be charged for the entire period of purchase regardless of the actual usage.

**Validity Period Type**

1 year.

For example, if you successfully purchase a CVM RI with a validity period of one year at 11:15:24, May 25, 2019, it will be valid from 12:00:00, May 25, 2019 to 12:00:00, May 24, 2020.

Note: After RIs expire, the matched pay-as-you-go instances will run normally but on longer enjoy a discount.

**Billing Rules**

- The settlement cycle of RIs is per hour (3,600 seconds), and the bill is generated on the dot of each hour (e.g., 10:00:00-10:59:59). Multiple pay-as-you-go physical instances can be matched to the same RI at the same time in the same settlement cycle. The amounts charged for physical instances successfully matching RI and those failing to match RI will be detailed in your bill;

- After successfully purchased, a RI will become valid on the dot of the next hour. you will need to pay for the RI during its validity period, no matter whether a pay-as-you-go instance is matched or not. You can choose the appropriate payment method and validity period based on your budget and resource conditions. The effective time of a RI is calculated on the hour, and the expiry time is the corresponding hour on the expiry date. For example, if you successfully purchase a CVM RI with a validity period of one year at 11:15:24, May 25, 2019, its effective time and billing start time is 12:00:00, May 25, 2019, and its expiry time is 12:00:00, May 24, 2020. If you already have a matching CVM resource when you purchase this RI, fees will be charged starting from 11:00:00-11:59:59, May 25, 2019 at the hourly rate.

**RI Discount:**

The discount on the purchase of RIs is supported.
