

HTTPDNS is daily pay-as-you-go by the number of DNS queries. DNS queries performed from 00:00:00 to 23:59:59 on a day will be billed at 8:00:00 the next day.

## Pay-As-You-Go

### Calculation method

The number of HTTP DNS queries encrypted with DES under the current account for each natural day is calculated as follows:

- **1 HTTPS DNS query = 5 HTTP DNS queries encrypted with DES**
- **1 HTTP DNS query encrypted with AES = 3 HTTP DNS queries encrypted with DES**

>?The number of DNS queries is calculated per domain. One HTTP DNS request for one domain is recorded as one DNS query, and one HTTP DNS request for N domains is recorded as N DNS queries. For HTTPS DNS requests, the quantity will be N * 5.
> 



| Billing Mode | Cycle | Price |
| ------------------ | -------- | -------------- |
| Pay-as-you-go (postpaid) | Daily | 0.006 USD/10,000 queries |


### Pricing examples

For example, with the HTTPDNS service, if the number of DNS queries over the HTTP protocol with DES encryption is 1 million on the first day of this month, and the number of DNS queries over the HTTP protocol with DES encryption is 0.8 million and the number of DNS queries over the HTTPS protocol is 0.2 million on the second day of this month, then the number of HTTP DNS queries with DES encryption is 1 million on the first day and 0.8 million + 5 * 0.2 million = 1.8 million on the second day.

The total pay-as-you-go fees are 0.006 USD/10,000 queries * (1 million + 1.8 million) = 1.68 USD.

>?
If you encounter problems when using the product, contact [online customer service](https://intl.cloud.tencent.com/contact-us) for assistance.