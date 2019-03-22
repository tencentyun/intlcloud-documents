## Web Application Firewall (WAF) Billing



### Billing method

Pay-as-you-go with a daily billing cycle

### Billing formula

Daily bill = Daily peak QPS x QPS rates

### Tiered pricing

Notes:

(1) Daily peak QPS

Daily peak QPS is based on data between 00:00:00 and 23:59:59 in one day. Website QPS is the total number of requests per second for your domain received by the WAF. Counting starts once domain name is configured.

(2) QPS rates

See below for tiered QPS rates:

```
If peak QPS is between 5-50 (number less than 5 will be counted as 5), per QPS rate is 0.2 USD/day.
If peak QPS is between 50-200, per QPS rate is 0.18 USD/day.
If peak QPS is between 200-1,000, per QPS rate is 0.15 USD/day.
If peak QPS is greater than 1,000, per QPS rate is 0.12 USD/day.
```

Tiered Price Table:

| Peak QPS | QPS Rates |
| -----------: | ----------: |
|      < 5 QPS | 0.2 USD/day |
|     5-50 QPS | 0.2 USD/day |
|   50-200 QPS | 0.18 USD/day |
| 200-1000 QPS | 0.15 USD/day |
|   > 1000 QPS | 0.12 USD/day |

For example, if the website peak QPS today is 15, today's bill will be 15 x 0.2=3 USD.

Note:
WAF service will be suspended one day after your account falls into arrears, and WAF resources will be repossessed after 7 days. You can pay off the outstanding fees before repossession to resume service.

