>? The monthly subscription mode is currently in beta. Prices published here are for reference only. Refer to your bills for final prices. To use this billing option, please [contact sales](https://intl.cloud.tencent.com/contact-sales).
>

## Adjusting Public Network Bandwidth

<table>
<tr><th>Network Billing Mode</th><th>CVM Billing Mode</th><th>Adjust Bandwidth</th></tr>
<tr><td>Monthly bandwidth subscription</td><td>Monthly subscription</td><td>Supports bandwidth upgrade only, and you have the option to set the changes to take effect immediately or at a specified time.</td></tr>
<tr><td rowspan=2>Bill-by-traffic</td><td>Monthly subscription</td><td rowspan=2>Bandwidth can be upgraded or downgraded, and the changes take effect immediately. The network fee is calculated based on traffic usage. </td></tr>
<tr><td>Pay as you go</td></tr>
</table>

## Changing Billing Mode

<table>
<tr><th>Network Billing Mode</th><th>CVM Billing Mode</th><th>Change Network Billing Mode</th></tr>
<tr><td>Monthly bandwidth subscription</td><td>Monthly subscription</td><td>Not supported.</td></tr>
<tr><td rowspan=2>Bill-by-traffic</td><td>Monthly subscription</td><td>Supports an irreversible change to monthly bandwidth subscription for each CVM.</td></tr>
<tr><td>Pay as you go</td><td>Not supported.</td></tr>
</table>


## Billing Sample

The bandwidth unit price is listed in [Public Network Billing](https://intl.cloud.tencent.com/zh/document/product/213/10578).
>? This sample only calculates the network cost. CVM and other device fees will be settled separately.

### Adjusting the bandwidth

#### Upgrading bandwidth for **Monthly bandwidth subscription**

Assume you purchased the monthly subscription bandwidth of 2 Mbps for one CVM instance in Beijing region on November 1, 2018. You upgraded the bandwidth from 2 Mbps to 5 Mbps between November 20 and 29, 2018 for a total of 10 days.![](https://main.qcloudimg.com/raw/a8ea05b86a9c2e5bda630928585acbe5.png)
The payable bandwidth fee for the original monthly bandwidth subscription in November will be: bandwidth \* unit price = 2Mbps \* 2.86 USD/Mbps = 5.72 USD
Additional fees after upgrading the bandwidth will be: bandwidth difference before and after the upgrade \* number of days with upgraded bandwidth/billable days in the month (sum of days in multiple months) = (3.57 USD/Mbps \* 3 Mbps + 2.86 USD/Mbps \* 2Mbps - 2.86 USD/Mbps \* 2Mbps) \* 10 days/30 days = 3.57 USD

#### Upgrading or downgrading bandwidth for **bill-by-traffic**

You can adjust the bandwidth cap for bill-by-traffic CVM instances at no additional cost whenever you need. The public network is billed on the actual traffic.

### Changing public network billing

#### Changing from **bill-by-traffic** to **monthly bandwidth subscription**

The traffic fee will be settled hourly at the time of change. To change the billing option, you only need to pay the monthly bandwidth subscription fees.