## Web Application Firewall (WAF) Billing



### Billing method

Postpaid on a daily basis

### Billing formula

Day bill = Daily peak QPS x QPS rates

### Tiered pricing

Notes:

(1) Daily peak QPS

Daily peak QPS is based on data between 00:00:00 and 23:59:59 in one day. Website QPS is the total number of requests per second for your domain received by the WAF. Counting starts once domain name is configured.

(2) QPS rates

See below for tiered QPS rates:

```
If the peak QPS is between 5-50 (number less than 5 will be counted as 5), per QPS rates is 0.2 USD/day.
If the peak QPS is between 50-200, per QPS rates is 0.18 USD/day.
If the peak QPS is between 200-1,000, per QPS rates is 0.15 USD/day.
If the peak QPS is greater than 1,000, per QPS rates is 0.12 USD/day.
```

List of tiered prices:

| Peak QPS | QPS Billing Factor |
| -----------: | ----------: |
|      < 5 QPS | 0.2 USD/day |
|     5-50 QPS | 0.2 USD/day |
|   50-200 QPS | 0.18 USD/day |
| 200-1000 QPS | 0.15 USD/day |
|   > 1000 QPS | 0.12 USD/day |

Billing example: Suppose that today's peak QPS of the website is 15, the billing amount of today is 15 x 0.2=3 USD.

Note:
In the case of insufficient account balance, the WAF service will be suspended one day after the account is in arrears, and the WAF resources will be released in 7 days. You can pay off the arrears before the release of resources to resume defense service.

