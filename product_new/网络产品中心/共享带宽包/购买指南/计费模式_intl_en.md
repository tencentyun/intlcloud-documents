## Billing Description
- **Billing date**
The first day of the calendar month immediately after the current billing cycle. For example, the BWP bill for usage in May (2019-05-01 00:00:00 to 2019-05-31 23:59:59) is generated on June 1st.
- **Settlement date**
After the bill is generated, the charge is automatically deducted from your account balance to settle the bill. Therefore, ensure that your account balance is sufficient at the time of settlement to avoid going into arrears.
- **Billing scope**
BWP charges by region. One BWP covers a single region.
- **Usage details**
BWP provides usage details at the minute level. You can download usage details from the console or contact after-sales service for help.
- **Activation conditions**
For the time being, monthly 95th percentile billing is only available to customers with monthly consumption greater than 15,000 USD. 

## Calculation Formula
Postpaid BWP fee = BWP monthly peak x Number of valid days x Unit price of the product/Number of days of the billed month.
>The calculation formula for monthly 95th percentile billing is the same as that for the monthly top 5 peaks method. The only difference is how the monthly peak is calculated. For details, see **Parameter Description** below.

## Parameter Description
- **Top 5 monthly peaks** 
 - Daily peak: Every five minutes, the highest BWP bandwidth value per minute is collected. At the end of the day, the collected values are sorted in descending order, and the fifth highest value is used as the daily peak.
>The daily peak is collected for inbound and outbound traffic respectively to calculate the monthly peak for inbound and outbound traffic.
 - Monthly peak: When the billed month is over, the collected daily peaks are sorted in descending order, and the average value of the top 5 peaks is used as the monthly peak.
>The monthly peak is collected for inbound and outbound traffic respectively, and the higher one is used as the monthly peak.
 - Valid days: the number of days in which bandwidth is not zero.
 - Unit price of the product: see BWP [Pricing](https://intl.cloud.tencent.com/document/product/684/15254).
 - Days of the billed month: the actual number of days during the month in which BWP is used.
- **Monthly 95th percentile**
 - Monthly peak: Every five minutes, the highest BWP bandwidth value per minute is collected. When the billed month is over, the collected values are sorted from high to low. After the top 5% values are eliminated, the highest value is used as the monthly peak.
>Monthly peak is collected for inbound and outbound traffics respectively and the higher one is used as the monthly peak of the current billed month.
 - Valid days: the number of days in which the bandwidth is not zero.
 - Unit price of the product: see BWP [Pricing](https://intl.cloud.tencent.com/document/product/684/15254) for details.
 - Days of the billed month: the actual number of days during the month in which BWP is used.
