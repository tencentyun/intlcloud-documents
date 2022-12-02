Tencent Cloud EdgeOne provides pay-as-you-go subscriptions. **The service is activated once you connect your site with EdgeOne and specify the subscription plan**. The subscription fee is charged at the end of the billing cycle.


## Billable Items
The bill of EdgeOne includes costs of the subscription plan, out-of-plan usage and value-added services.
- Subscription plan (required): Specify a plan for each site. The subscription plan includes the basic features, with the configured quota.
- Out-of-plan usage: When the quota of the subscription plan is used up, you need to pay for the exceeding parts additionally based on the corresponding prices.
- Value-added services (optional): EdgeOne provides many VASs, such as HTTP/3 (QUIC). These services are billed separately. You can activate them as needed.

## Billing Cycle
EdgeOne is billed on a calendar month basis. The bill of the current month is generated on the 1st day of the next calendar month. For example, a bill for January (2021-01-01 00:00:00 to 2021-01-31 23:59:59) is generated on February 1st.

## EdgeOne Plans
EdgeOne provides the Standard and Enterprise plans. You can only specify one plan for one site. The details of the two plans are listed as below:

|    Item                                  |                            Standard                            |                            Enterprise                            |
| :----------------------------------- | :----------------------------------------------------------: | :----------------------------------------------------------: |
| Price                                 |                         Chinese mainland: 590 USD/month<br/>Global (outside the Chinese mainland): 699 USD/month                         | [Contact us](https://intl.cloud.tencent.com/contact-us) |
| Traffic                                 |                             3 TB                             |                          	Customizable                          |
| Number of HTTP/HTTPS requests                    |                           50 million                           |                         	Customizable                          |
| CDN |                              ✓                               |                              ✓                               |
| Smart acceleration                             |                              ✓                               |                              ✓                               |
| L4 proxy via CNAME                 |                              ✕                               |                              ✓                               |
| L4 proxy via static IP                |                              ✕                               |                              ✓                               |
| DDoS mitigation                            |                              ✓                               |                              ✓                               |
| Enterprise DDoS mitigation (customizable)    |                              ✕                               |                              ✓                               |
| Web protection - Managed rules                  |                              ✓                               |                              ✓                               |
| Web protection - Rate limiting rules              |                             5                              |                          Customizable                          |
| Web protection - Custom rules                |                             20                             |                          Customizable                          |
| Bot management                         |                             Optional                             |                             Optional                             |
| Bot intelligence           |                Free for a limited time                  |                 Free for a limited time                  |
| Verification (JavaScript challenge and CAPTCHA) |                              ✓                               |                              ✓                               |
| Upload size limit                         |               500 MB (cannot be disabled)               |                           Unlimited                           |
| External certificate on edge node             |                              ✓                               |                              ✓                               |
| Load balancing tasks                       |                             5                              |                             10                             |
| Node cache TTL                         |                      Down to the second level                      |                      Down to the second level                     |
| Browser cache TTL                       |                      Down to the second level                   |                      Down to the second level                    |
| Purge cache (free for a limited time)                 | Matching type: Host and Prefix<br>Quota per request: 1,000<br>Daily quota: 10,000 | Matching type: Host and Prefix<br>Quota per request: 1,000<br>Daily quota: 20,000 |
| Prefetch URL (free for a limited time)                 |             Quota per request: 1,000<br>Daily quota: 50,000              |      Quota per request: 5,000<br>Daily quota: 100,000      |
| WebSockets                           |                     Default timeout: 1-120s                     |                     Default timeout: 1-300s                     |
| Max data query period                 |                            90 days                             |                            180 days                             |
| Real-time logging                             |                           2 tasks                            |                           5 tasks                            |
| Rule engine rules                       |                            100                             |                            200                             |
| DNS records                           |                             500                              |                             1,000                             |

>!
>- All features offered in Standard plan are included in the Enterprise plan.
>- If the capability of the Enterprise plan still cannot meet your needs, [contact us](https://intl.cloud.tencent.com/contact-us).

## Notes
If the usage %your plan serves for less than one month, you are billed based on **the actual plan duration and usage**. Providing you subscribed to a Standard plan on the 15th of this month, which has 30 days, then your subscription fee is $349.5 (699 x 15/30), and your monthly traffic usage is 1.5 TB (3 TB x 15/30) and on the number of requests is 25,000K (50,000K x 15/30).

## Out-of-plan Usage
### Standard plan - Security acceleration traffic
If the security acceleration requests exceed your Standard plan's limit, you are billed at the following tiered prices.

<table>
<thead>
<tr>
<th width="60%">Monthly Traffic</th>
<th width="40%">Price (USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td align="left">[0,10) TB</td>
<td align="center">0.165</td>
</tr>
<tr>
<td align="left">[10,50) TB</td>
<td align="center">0.1568</td>
</tr>
<tr>
<td align="left">[50,100) TB</td>
<td align="center">0.1485</td>
</tr>
<tr>
<td align="left">[100,250) TB</td>
<td align="center">0.1403</td>
</tr>
<tr>
<td align="left">[250,750) TB</td>
<td align="center">0.1320</td>
</tr>
<tr>
<td align="left">[750,1500) TB</td>
<td align="center">0.1238</td>
</tr>
<tr>
<td align="left">[1500,2000) TB</td>
<td align="center">0.1155</td>
</tr>
<tr>
<td align="left">≥ 2,000 TB</td>
<td align="center">0.1073</td>
</tr>
</tbody></table>


### Standard plan- Security acceleration requests
If the security acceleration requests exceed your Standard plan's limit, you are billed at the following tiered prices.

<table>
<thead>
<tr>
<th width="60%">Monthly requests</th>
<th width="40%">Price (USD/10K requests)</th>
</tr>
</thead>
<tbody><tr>
<td align="left">0 - 1 billion (exclusive)</td>
<td align="center">0.05</td>
</tr>
<tr>
<td align="left">1 billion - 5 billion (exclusive)</td>
<td align="center">0.03</td>
</tr>
<tr>
<td align="left">≥ 5 billion</td>
<td align="center">0.024</td>
</tr>
</tbody></table>


### Enterprise plan - Unit pricing
For the out-of-plan fee of Enterprise plans, [contact us](https://intl.cloud.tencent.com/contact-us). 

## Value-added Services
EdgeOne provides additional value-added services for enhanced capabilities.

### HTTP/3 (QUIC) requests
QUIC requests adopt monthly linear pricing model. The details are as below:

<table>
<thead>
<tr>
<th width="50%">Value-added Service</th>
<th width="30%">Billing Mode</th>
<th width="20%">Price (USD)</th>
</tr>
</thead>
<tbody><tr>
<td align="left">QUIC requests</td>
<td align="left">Billed by the number of QUIC requests</td>
<td align="left">0.008 USD/10K requests/month</td>
</tr>
</tbody></table>



### Real-time logging

Real-time logging is in free beta, which is plan to end on September 2022. We will notify user about the pricing in when the free beta ends.

### Bot management
Fees are charged for the selected value-added features and excessive requests.

The value-added feature quota varies by the subscription plan type. The details are as below:

<table>
<thead>
<tr>
<th width="50%">Value-added Service</th>
<th width="30%">Billing Mode</th>
<th width="20%">Price (USD)</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Bot management for Standard plan<br>30,000K requests/month</td>
<td align="left">Monthly linear pricing</td>
<td align="left">1,250 USD/month</td>
</tr>
<tr>
<td align="left">Bot management for Enterprise plan<br>≥ 80,000K requests/month</td>
<td align="left">Monthly linear pricing</td>
<td align="left"><a href="https://intl.cloud.tencent.com/contact-us">Contact us</a></td>
</tr>
</tbody></table>


Requests in excess of the value-added feature quota are charged on a tiered basis. View the table below:

<table>
<thead>
<tr>
<th width="60%">Requests (in 10K)</th>
<th width="40%">Price (USD)</th>
</tr>
</thead>
<tbody><tr>
<td align="left">[0, 4000) * 10K</td>
<td align="center">0.16 USD/10K requests/month</td>
</tr>
<tr>
<td align="left">[4000, 8000) * 10K</td>
<td align="center">0.13 USD/10K requests/month</td>
</tr>
<tr>
<td align="left">[800,12000) * 10K</td>
<td align="center">0.11 USD/10K requests/month</td>
</tr>
<tr>
<td align="left">[12000,32000) * 10K</td>
<td align="center">0.07 USD/10K requests/month</td>
</tr>
<tr>
<td align="left">[32000,92000) * 10K</td>
<td align="center">0.06 USD/10K requests/month</td>
</tr>
<tr>
<td align="left">[92000,192000)</td>
<td align="center">0.04 USD/10K requests/month</td>
</tr>
<tr>
<td align="left">≥ 192,000 * 10K</td>
<td align="center">0.02 USD/10K requests/month</td>
</tr>
</tbody></table>


### Web protection rule pack
L4 proxy is also billed using fixed monthly pricing.

<table>
<thead>
<tr>
<th width="50%">Value-added Service</th>
<th width="30%">Billing Mode</th>
<th width="20%">Price (USD)</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Web protection rule pack (20 custom rules and 5 rate limiting rules)</td>
<td align="left">Monthly linear pricing</td>
<td align="left"><a href="https://intl.cloud.tencent.com/contact-us">Contact us</a></td>
</tr>
</tbody></table>


### L4 proxy quota

L4 proxy is also billed using fixed monthly pricing.

<table>
<thead>
<tr>
<th width="50%">Value-added Service</th>
<th width="30%">Billing Mode</th>
<th width="20%">Price (USD)</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Static IP-based L4 proxy</td>
<td align="left">Monthly linear pricing</td>
<td align="left"><a href="https://intl.cloud.tencent.com/contact-us">Contact us</a></td>
</tr>
<tr>
<td align="left">CNAME-based L4 proxy</td>
<td align="left">Monthly linear pricing</td>
<td align="left"><a href="https://intl.cloud.tencent.com/contact-us">Contact us</a></td>
</tr>
</tbody></table>

### Smart acceleration
All SCDN subdomain names use smart acceleration to optimize the access experience of your users. After smart acceleration is enabled, the client traffic and upstream and downstream traffic of EdgeOne nodes (client Tencent Cloud ⇋ EdgeOne node server) will be billed.
