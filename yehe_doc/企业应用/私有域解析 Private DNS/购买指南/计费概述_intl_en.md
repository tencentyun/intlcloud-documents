# Pricing
### Billing mode

Private DNS is pay-as-you-go. It is billed by **the numbers of private domains and DNS requests** and settled by calendar day. If a private domain is deleted in less than 24 hours after creation, no fees will be incurred.

### Billing rule

Number of private domains: 0.015 USD/domain/day
Number of DNS requests: 0.004 USD/10,000 requests

#### Billing example
- Three private domains are added to account A: `test.com`, `host01.demo.com`, and `inner.example.com`.
- Account A receives 100,000 DNS queries from these three private domains on the next day.
- Then, account A's usage fees for one day are: 0.015 USD * 3 (basic configuration fees for 3 private domains) + 0.004 USD * 10 = 0.085 USD


#### Note
There is a TTL caching mechanism for DNS queries. The number of daily DNS requests in Private DNS is the number of requests minus the number of TTL cache hits. For example, if the TTL for requesting `www.test.com` is set to 30 seconds, and the internal access to `www.test.com` generates 1,000 DNS requests per second, then the requests within 30 seconds will hit the TTL cache, which are free of charge; the TTL expires after 30 seconds, and then DNS will request `www.test.com` once at the origin server; therefore, only this origin-pull request is billable.

>?
>- The longer the TTL value, the lower the frequency of DNS origin-pull requests, the slower the domain name change takes effect, and the lower the corresponding fees.
>- The shorter the TTL value, the higher the frequency of DNS origin-pull requests, the faster the domain name change takes effect, and the higher the corresponding fees.

### Overdue payment
- Once your account has overdue payments, Private DNS will keep running for 24 hours and then get suspended.
- After the service is suspended, billing will also stop. If you pay the past due charges within 24 hours, your service will not be affected by the suspension. If you fail to make the payment in 7 days, the service will be released.
- An alert will be sent by SMS/email one day before the service is released. Once the service is released, the configuration and data related to your private domains will be permanently deleted and cannot be restored.
- If you pay the past due charges within 7 days, the service will automatically resume.

