RUM is billed by reports and provides a free tier of 500,000 reports per day for each application. After the free tier is exceeded, the system will start billing according to the following rules by default:

## Billing Rules
Currently, only the hourly pay-as-you-go (postpaid) billing mode is supported.
The billable item of RUM is data report, and each data entry stored in RUM is counted as a report, including the number of PVs, API counts, static resource counts, error log counts, and custom reports.
- A free tier of 500,000 reports per day is provided for each application.
- Reports exceeding the free tier (500,000) will be billed.


## Product Pricing and Calculation Formula
**Daily report fees per business system:**

| Billable Item | Price (USD) |
|---------|---------|
| Data reports (in 0000's) | 0.08 |


Calculation formula = number of data reports (in 0000's) * unit price per 10000 reports


## Estimated RUM Fees
### Estimated daily reports
Calculation formula = (PVs + API counts + static resource counts + error log counts + custom reports) - 500000

### Example
Suppose your application has 1 million PVs, 5 million API counts, 900,000 static resource counts, 100,000 error log counts, and 200,000 custom reports per day on average, then the monthly fees are calculated as follows:
Total reports = [(1000000 + 5000000 + 900000 + 100000 + 200000 ) - 500000 (daily free tier per application)] * 30 days = 201000000 reports
Amount (in USD) = 20100 * 0.08 USD = 1608 USD