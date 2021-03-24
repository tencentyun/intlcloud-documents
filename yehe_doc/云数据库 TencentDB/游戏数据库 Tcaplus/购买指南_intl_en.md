## Billing Rule
**Daily TcaplusDB fees = daily capacity fees + daily reserved read fees + daily reserved write fees**

**Definitions**
- **Capacity**: the names of both primary key column and attribute column are counted into the size of each data row.
- **Reserved read**: one 4 KB single-row read operation per second is counted as one reserved read capacity unit (CU).
- **Reserved write**: one 4 KB single-row write operation per second is counted as one reserved write capacity unit (CU).
- **CU calculation rule**: a CU is counted separately at the end of each request and response process. CUs are accumulated and calculated based on the request or response (whichever is greater). Data smaller than 4 KB is rounded up to the nearest 4 KB, and data larger than 4 KB is calculated in multiples of 4 KB. For example, if a 9 KB response is returned for a 1 KB request within one second, because the size of the response is larger than that of the request, the number of CUs will be calculated based on the value of the response. 9 KB is about two 4 KB sets, and the remaining 1 KB is counted as 4 KB, so the total number of CUs will be 2 + 1 = 3.

## Billing Mode
The pay-as-you-go (postpaid) billing mode is adopted.

## Price List

| Region | Capacity (USD/GB/Day) | Reserved Read (USD/CU/Day) | Reserved Write (USD/CU/Day) |
|---------|---------|---------|---------|
| Shanghai (China) | 0.0052 | 0.0019 |  0.0048 |
| Silicon Valley (West US) | 0.006289| 0.002 |0.0055 |
| Virginia (East US) | 0.006289| 0.002 |0.0055 |
| Frankfurt (Germany) | 0.006 | 0.0022 | 0.0057 |
| Singapore | 0.0061 | 0.0025 | 0.0061 |
| Hong Kong (China) | 0.0055 |	0.0019 | 0.0055|
| Tokyo (Japan) | 0.0055 |	0.0019|0.0055 |
| Seoul (South Korea) | 0.006289 | 0.0025 | 0.00599 |


>- The following limits apply to tables:
> - The capacity of one table can be 1–300 GB.
>  - The reserved reads of one table can be 60–800,000 CUs.
>  - The reserved writes of one table can be 20–260,000 CUs.
> - If the storage you apply for exceeds the above limits, please [contact us](https://intl.cloud.tencent.com/contact-sales) to sign a contract offline.

- When this product is used, the system will calculate whether the balance in your account is enough, and if yes, an amount equal to capacity * unit price will be frozen for one day when you create a table; otherwise, the creation will fail.
- The fees of the previous day will be deducted at 00:00 each day.
- Insufficient balance will trigger denial of access to the service. After your account becomes overdue, data will be retained for 7 days. If you fail to top up your account within 7 days, your data will be cleared.

## Settlement Cycle
Fees are charged daily, and those incurred on the current day will automatically be deducted on the next day. Any disputes related to bills shall be resolved through negotiation. If the negotiation fails, the system statistics shall prevail.

## Billing Example
Suppose you created a table in the Shanghai region with the default reserved read, reserved write, and capacity parameters used, i.e., 80 reserved reads per second, 26 reserved writes per second, and 1 GB reserved capacity.

Within the first 10 days after the table was created, your application's read and write access frequency peaks did not exceed 80 reads per second (one 4 KB single-row read per second counted as one read operation) and 26 writes per second (one 4 KB single-row write per second counted as one write operation), and the total data volume in the table was less than 1 GB.

On the 11th day, the interactions between your application and the table grew as business promotions led to an increase in access requests. The read and write frequencies got close to and eventually exceeded the caps, peaking at 100 reads per second and 30 writes per second, respectively, and the data volume reached 1.5 GB. TcaplusDB does not block traffic surges that exceed the reserved write/read request caps; instead, it allows a small proportion of requests to exceed the caps, and you are recommended to expand the capacity. However, if there are massive volumes of excessive requests, it will return an error code for traffic limit.

On the 12th day, you chose to expand the capacity of the table to 800 reserved reads per second, 500 reserved writes per second, and 5 GB reserved capacity based on your needs. In the following 10 days, access requests became stable and stood below the raised caps till the 30th day.

The usage and corresponding fees for the 1st–30th days (the current month) are as follows:

| Time Range (Days) | Capacity (GB) | Read Request (CUs) | Write Request (CUs) | Fees Calculation | Description |
|---------|---------|---------|---------|-------|-------|
| 1–10 | 1 | 80 |  26 | (1 GB * 0.0052 USD/GB/day + 80 CUs * 	0.0019 USD/CU/day + 26 CUs * 0.0048 USD/CU/day) * 10 days = 2.82 USD | As the reserved value caps were not exceeded, fees were calculated based on the reserved values |
| 11 | 1.5 | 100 |  30 | (1.5 GB * 0.0052 USD/GB/day + 100 CUs * 	0.0019 USD/CU/day + 30 CUs * 0.0048 USD/CU/day) * 1 day = 0.3418 USD  | Although the reserved value caps were exceeded, the increase was below 200%; therefore, the fees were calculated based on the actual access peaks |
| 12–30 | 5 | 800 |  500 | (5 GB * 0.0052 USD/GB/day + 800 CUs * 0.0019 USD/CU/day + 500 CUs * 0.0048 USD/CU/day) * 19 days = 74.974 USD | After the reserved values were adjusted, fees were calculated based on the new reserved read, write, and capacity values |
| Total fees |- |- |- | 2.82 USD + 0.3418 USD + 74.974 USD = 78.1358 USD | -|
