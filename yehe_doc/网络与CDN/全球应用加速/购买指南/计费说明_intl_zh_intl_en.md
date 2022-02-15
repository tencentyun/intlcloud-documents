The service fee of GAAP consists of basic items and value-added items. (For the billing information of other Tencent Cloud services, refer to related documentation or [contact us](https://intl.cloud.tencent.com/document/product/608/42346).

>? The fees of GAAP service in all Chinese mainland regions are collectively billed in Guangzhou. For regions outside the Chinese mainland, the fees are billed collectively in Singapore.

## Basic Billable Items
The following table lists the basic billable items and payment modes:

|Item | Payment Mode |
|--|--|
|Connection fee| Pay-as-you-go daily |
|Bandwidth fee| Pay-as-you-go daily|

### Connection fee

The connection fee refers to the cost of resources (server, IP, etc.) used to create an acceleration connection. The fee is related to the connection specification (number of concurrent connections/bandwidth). Each acceleration connection is billed separately on a daily basis. See below for details:

<table>
<thead>
<tr>
<th colspan="12"  style="text-align: center">Acceleration Connection Pricing<strong> (Unit: USD/Day)</strong></th>
</tr>
</thead>
<tbody><tr>
<th>Number of concurrent connections/Bandwidth</th>
<th>10 Mbps</th>
<th>20 Mbps</th>
<th>50 Mbps</th>
<th>100 Mbps</th>
<th>200 Mbps</th>
<th>500 Mbps</th>
<th>1,000 Mbps</th>
<th>2,000 Mbps</th>
<th>5,000 Mbps</th>
<th>8,000 Mbps</th>
<th>10,000 Mbps</th>
</tr>
<tr>
<td >20K</td>
<td>12.8</td>
<td>12.8</td>
<td>12.8</td>
<td>12.8</td>
<td>12.8</td>
<td>12.8</td>
<td>12.8</td>
<td>25.6</td>
<td>64</td>
<td>102.4</td>
<td>128</td>
</tr>
<tr>
<td>50K</td>
<td>19.2</td>
<td>19.2</td>
<td>19.2</td>
<td>19.2</td>
<td>19.2</td>
<td>19.2</td>
<td>19.2</td>
<td>25.6</td>
<td>64</td>
<td>64,512</td>
<td>128</td>
</tr>
<tr>
<td>100K</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>64</td>
<td>102.4</td>
<td>128</td>
</tr>
<tr>
<td>200K</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>102.4</td>
<td>128</td>
</tr>
<tr>
<td>300K</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>102.4</td>
<td>128</td>
</tr>
<tr>
<td>400K</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
</tr>
<tr>
<td>500K</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
</tr>
<tr>
<td>600K</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
</tr>
<tr>
<td>700K</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
</tr>
<tr>
<td>800K</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
</tr>
<tr>
<td>900K</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
</tr>
<tr>
<td>1000K</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
</tr>
</tbody></table>


#### Calculation and deduction
- The connection fee generated between 00:00:00-23:59:59 (UTC+8) of a day is billed before 18:00 on the following day (UTC+8).
- The connection fee is incurred whenever you create a connection, including creating new ones and re-creating old ones. 
- The connection specification can be changed once per day. The connection fee of the day is calculated according to the last modified specification.
>? When a connection is disabled, the bandwidth fee stops. But the connection fee continues. You need to delete the connection to stop the incurring of connection fee.
#### Billing example

Assume that a user creates a Beijing-Singapore acceleration connection on January 1, adjusts the connection specification, and deletes it at 18:00 on January 4. The connection fee is calculated as follows:

| **Date** | **Resource ID**    | **Maximum Connections (10K)** | **Maximum Bandwidth (Mbps)** | **Connection Fee (USD)** |
|-|-|-|-|-|
| Jan 1, 2021 | link-0tisfsxz | 2                 | 10                   | 12.8              |
| Jan 2, 2021 | link-0tisfsxz | 30                | 50                   | 96                |
| Jan 3, 2021 | link-0tisfsxz | 10                | 20                   | 32                |
| Jan 4, 2021 | link-0tisfsxz | 40                | 20                   | 128               |

### Bandwidth fee
The bandwidth fee refers to the cost of bandwidth consumed by acceleration connections and acceleration connection groups. Each acceleration connection is billed separately on a daily basis according to the tier range within which the actual peak bandwidth falls using the following tiered prices.

| **Bandwidth Tier**                 | **USD/Mbps/Day** |
|--|--|
| < 20 Mbps                     | 20.63            |
| 20-100 Mbps (100 Mbps excluded)    | 14.29            |
| 100-500 Mbps (500 Mbps excluded)   | 11.11            |
| 500-2,000 Mbps (2,000 Mbps excluded) | 9.52             |
| ≥ 2,000 Mbps                   | 7.94             |

#### Calculation and deduction

- The bandwidth fee generated between 00:00:00-23:59:59 (UTC+8) of a day is billed before 18:00 on the following day (UTC+8).
- The inbound and outbound bandwidth of the connection is collected every one minute. The highest value among all the collected samples is the billable bandwidth.

#### Billing example
Assume that a user creates a Beijing-Singapore acceleration connection on January 1, adjusts the connection specification, and deletes it at 18:00 on January 4. The bandwidth fee is calculated as follows:

| **Date** | **Resource ID**    | **Peak Bandwidth (Mbps)** | **Formula** | **Bandwidth Fee (USD)** |
|--|--|--|--|--|
| Jan 1, 2021 | link-0tisfskk | 7                    | =7×20.63     | 144.41            |
| Jan 2, 2021 | link-0tisfskk | 28                   | =28×14.29    | 400.12            |
| Jan 3, 2021 | link-0tisfskk | 158                  | =158×11.11   | 1,755.38           |
| Jan 4, 2021 | link-0tisfskk | 150                  | =500×9.52    | 4,760              |

###  


## Value-added Billable Item

The dedicated BGP network fee is incurred if you have used dedicated BGP network (Hong Kong) for GAAP acceleration.

Dedicated BGP network fee = Daily peak bandwidth × List price (3 USD/Mbps/day)

#### Billing example
Assume that a user creates a Hong Kong-Singapore connection over the dedicated BGP network on January 1 and deletes it on January 4. The fee is calculated as follows:

| **Date** | **Resource ID**   | **Peak Bandwidth (Mbps)** | **Formula** | **Dedicated BGP Network Fee (USD)** |
|-|-|-|-|-|
| Jan 1, 2021 | link-1tifgbp | 7                    | =7×3         | 21                   |
| Jan 2, 2021 | link-1tifgbp | 28                   | =28×3        | 84                   |
| Jan 3, 2021 | link-1tifgbp | 25                   | =25×3        | 75                   |
| Jan 4, 2021 | link-1tifgbp | 50                   | =50×3        | 150                  |

