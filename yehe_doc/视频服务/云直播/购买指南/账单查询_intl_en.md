To view your CSS bills and payment details, go to **Billing Center** > **Bills** > **[Bill Details](https://console.cloud.tencent.com/expense/bill/summary)** in the Tencent Cloud console.
The Bill Details page includes the **Bill by Instance** and **Bill Details** tabs:
- Bill by Instance: displays aggregated bills by instance.
- Bill Details: displays one record per bill without performing aggregation.
<span id="resources_id"></span>
## Bill by Instance
1. Click the **Bill by Instance** tab.
2. Click **All products** and then select **CSS** to view the CSS bills.

![](https://main.qcloudimg.com/raw/9db167f7285dfaf82d83a9028d589ad8.png)

#### Bill fields

<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Transaction type</td>
<td><ul style="margin:0;">
    <li>Daily billing cycle: fees are deducted daily</li>
    <li>Monthly billing cycle: fees are deducted monthly</li>
    </td>
</tr>
<tr>
<td>Configuration description</td>
<td>CSS sub-features and their usage in this month. CSS sub-features include: <ul style="margin:0;">
    <li>Live transcoding</li>
    <li>Live recording</li>
    <li>Live screencapture</li>
    <li>Porn detection</li>
    </ul></td>
</tr>
<tr>
<td>Original price</td>
<td>Total fees of the sub-feature(s) used in this month</td>
</tr>
<tr>
<td>Discount rate</td>
<td>The user’s discount rate this month:Users on the daily billing cycle do not receive discounts. Their discount rate is 1.</td>
</tr>
<tr>
<td>Total cost</td>
<td>Total cost = Original price × (1 - Discount rate)</td>
</tr>
</tbody></table>

>? Other fields are assigned by Tencent Cloud. For details, see [Bills](https://intl.cloud.tencent.com/document/product/555/7432).
<span id="detail"></span>
## Bill Details
1. Click the **Bill Details** tab.
2. Click **All products** and then select **CSS** to view the details of the CSS bills.

![](https://main.qcloudimg.com/raw/0716954d4d5a955a77acd4149961ca1b.png)

#### Bill fields

| Field     | Description                                                         |
| :--------- | :----------------------------------------------------------- |
| Component type  | CSS sub-feature used in this month                               |
| Component name  | Sub-item under this component type                                 |
| Component’s published unit price | The component’s published unit price without discounts                    |
| Component’s usage   | Usage of the component                                             |
| Discount rate    | The user’s discount this month: users on the daily billing cycle do not receive discounts. Their discount rate is 0. Users on the monthly billing cycle can contact sales to query about receiving discounts |
| Usage duration   | Total usage duration of the component    |
| Total cost    | Total cost = Component’s original price x (1 - Discount rate). Component’s original price = Component’s published unit price x Usage duration |

>?Other fields are assigned by Tencent Cloud. For details, see [Bills](https://intl.cloud.tencent.com/document/product/555/7432).
