CSS will adjust the pricing of relaying to third parties starting from **00:00 (UTC+8) on August 1, 2022**. The prices for relaying to third parties outside the Chinese mainland and Hong Kong will vary by region. For the Chinese mainland and Hong Kong, the price will remain the same.

The change will affect the billing of CSS. The billable item of sp_live_dcrelay will change from dcrelay_bandwidth_monthly to dcrelay_bandwidth_monthly_regional.

## Notes

- The new prices will take effect starting from 00:00 (UTC+8) on August 1, 2022. They will apply to your bill for August, which will be generated between September 1 and September 3.
- If you have signed a contract with Tencent Cloud, please contact your sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to learn about the prices that will apply for your account in the future.

## Billing of Relaying to Third Parties

You can use the relaying service of CSS to relay live streams to third-party addresses. Third-party relay fees are charged based on the highest bandwidth (Mbps) used for relaying in each billing period. The price varies depending on the region to which your streams are relayed.

- Application scope: Fees are charged only if you relay to an address that is not a CSS push URL of the current account (the account that created the relay task).
- Billing mode: Monthly pay-as-you-go
- Billing cycle: Monthly billing. Your bill for each month is generated between the 1st and 3rd day of the following month.
- Billing rules: By default, third-party relay fees are charged in the pay-as-you-go mode based on your average daily peak bandwidth usage (for all third-party relay tasks) in each month. If a different billing mode is used for the LVB service under your account, that mode will apply to third-party relay.

## Prices Before Change

Before the change, the price of relaying to third parties is the same for all regions.

| Billable Item       | Price (USD/Mbps/Month) | Description              |
| :------------- | :------------------- | :------------------------- |
| Relay to third parties | 12.67        | Billed by bandwidth usage |

## Prices After Change

After the change, the price for relaying to third parties will vary with region. If you use the relaying service in multiple regions in the same billing period, it will be charged separately based on your peak bandwidth usage in each region.

| Region             | Price (USD/Mbps/Month) |
| :--------------- | :------------------- |
| Chinese mainland | 12.67                |
| Hong Kong (China)        | 12.67                |
| Singapore           | 8.04                 |
| Frankfurt         | 7.1                  |
| Seoul             | 16.56                |
| India             | 23.66                |
| Thailand             | 13.01                |
| Silicon Valley         | 7.1                  |
| Virginia     | 7.1                  |
| Jakarta           | 17.4                 |
| Japan             | 13.01                |
| São Paulo           | 23.66                |
| Other regions             | 12.67                |

The price change will take effect starting from **August 1, 2022**. If you have any questions, feel free to [contact us](https://intl.cloud.tencent.com/contact-us).

2022-07-12
Tencent Cloud Team
