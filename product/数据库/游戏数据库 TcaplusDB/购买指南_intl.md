[//]: # (chinagitpath:XXXXX)

## Billing Rules
Daily cost of TcaplusDB = Daily capacity fees + Daily fees for reserved writes + Daily fees for reserved reads

## Glossary
Capacity: The names of both primary key column and attribute column are counted into the data size of each record line.

Reserved read: One 4 KB single-line read operation per second is one reserved read CU (capacity unit).

Reserved write: One 4 KB single-line write operation per second is one reserved write CU.

CU calculation rule: A CU is calculated separately at the end of each request and response process. CUs are accumulated and calculated according to the larger value between the request and the response. Data smaller than 4 KB is rounded up to the nearest 4 KB, and data larger than 4 KB is calculated in multiples of 4 KB. For example, if a 9 KB response is returned for a 1 KB request within a second, because the size of the response is larger than that of the request, the number of CUs is calculated according to the value of response. 9 KB is about two 4 KB sets, and the remaining 1 KB is counted as 4 KB, so the total number of CUs is 2+1=3.

## Billing Method
Postpaid.

## Price List

| Region | Capacity (USD/GB/day) | Reserved Read (USD/GB/day) | Reserved Write (USD/GB/day) |
|---------|---------|---------|---------|
| Mainland China | 0.0052 | 0.0019 | 0.0048 |
| North America | 0.0058 | 0.0020 | 0.0055 |
| Canada | 0.0058 | 0.0022 | 0.0055 |
| Frankfurt | 0.0060 | 0.0022 | 0.0057 |
| Singapore | 0.0061 | 0.0025 | 0.0061 |
| Hong Kong | 0.0055 | 0.0019 | 0.0055 |
| Japan | 0.0055 | 0.0019 | 0.0055 |

>! The capacity, reserved read and reserved write of a single table should be between 1 GB to 300 GB, 60 CUs to 800,000 CUs, and 20 CUs to 260,000 CUs, respectively. To apply for more quota, [contact customer service](https://intl.cloud.tencent.com/contact-sales) to sign an off-line contract.

- When you apply for the storage product, the system will calculate whether the balance in your account is enough. If so, a specified amount (capacity*unit price) will be frozen for one day when you create a table; otherwise, the creation will fail.
- The fees of the previous day will be deducted at 00:00 in the morning each day.
- Insufficient balance will trigger denial of access to the service. When your account is in arrears, data will be kept for 7 days. If you fail to make the payment within 7 days, the data will be cleaned.

## Settlement Cycle
Fees are charged on a daily basis, and those generated in the current day will automatically be deducted on next day. Any bill-related dispute should be resolved through negotiation. When negotiation fails, the resolution shall be based on the system data.


