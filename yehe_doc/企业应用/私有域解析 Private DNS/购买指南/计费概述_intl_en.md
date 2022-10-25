## Billing Overview
### Pay-as-you-go
Private DNS is billed by the number of private domains and DNS queries and settled by calendar day. If a private domain is deleted in less than 24 hours after creation, no fees will be charged for the domain itself, but fees will be charged for the DNS queries. The fees will be rounded to two decimal places.
The pricing is as follows:

- Fees based on the number of private domains: **0.015 USD/day/private domain**
- Fees based on DNS queries: **0.004 USD/10,000 queries**

### Billing of value-added services
Prepaid value-added services are provided on a pay-as-you-go basis. Value-added services will first be paid using the prepaid “domain package/traffic package” (if any) in the current account, and those out of the package will be settled on the next day. For more details, see [Value-Added Service Packages](https://www.tencentcloud.com/document/product/1097/50828).


## Billing

#### Billing example
- If you add three private domains under the account A: `qq.com`, `dnspod.cn` and `yun.help`.
- Account A receives 100,000 DNS queries from these three private domains in a day.


- Then, for account A, the usage fees for the day are as follows: **0.015 USD * 3 (basic configuration fees for 3 private domains) + 0.004 USD * 10 = 0.085 USD**

#### Notes
There is a cache TTL mechanism for DNS queries. The DNS queries in Private DNS are counted based on the actual origin-pull requests and billed. You need to set the local NSCD cache to reduce original pulls.


#### Example
If the TTL for querying `cloud.tencent.com` is set to 300s and 1,000 queries are made within the TTL, the query counted in the statistics and billed is only the original-pull request made after the TTL expires.
>?
- The longer the TTL, the lower the frequency of DNS origin-pull requests and the lower corresponding fees are, but the domain change takes effect more slowly.
- The shorter the TTL, the higher the frequency of DNS origin-pull requests and the higher corresponding fees are, but the domain change takes effect more quickly.


## Deduction from Value-Added Service Packages
Private DNS supports billing by deduction from value-added service packages. You can check the billable items on the [Private DNS buy page](https://buy.intl.cloud.tencent.com/privatedns) in the Private DNS console.
For use details, see [Value-Added Service Packages](https://www.tencentcloud.com/document/product/1097/50828).


## Overdue Payments
- After the payment is overdue for 24 hours, the Private DNS service will be locked and relevant features disabled, but added DNS queries will continue to take effect.
- After the payment is overdue for 7 days, the Private DNS service will be suspended and relevant features disallowed, and all private domains will no longer be resolved.
- You cannot operate private domain settings under an account with an overdue payment, and fees incurred during this period will be charged as required. The services will be resumed after the account is topped up.



## Deduction Order
#### Usage deduction order
![](https://qcloudimg.tencent-cloud.cn/raw/3e1d600a000c0396c266593f658bb0e1.png)

#### Deduction order example
An enterprise user of Private DNS purchases a value-added traffic package of 5 million DNS queries one day, and at this moment the user has a free tier of 5 million queries/month and 5 million queries in the traffic package. If the user uses the DNS service, the free tier will be deducted first; after the free tier is used up, the traffic package will be deducted; after the traffic package is used up, the service will be automatically charged on a pay-as-you-go basis.
>? If you have problems when using the product, please feel free to [contact us](https://intl.cloud.tencent.com/contact-sales).


