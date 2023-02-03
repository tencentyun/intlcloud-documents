You can view your CSS bills and payment details in **Billing Center** > **Bills** > [Bill Details](https://console.cloud.tencent.com/expense/bill/summary).
The Bill Details page includes the **Bill by Instance** and **Bill Details** tabs:
- Bill by Instance: Displays bills aggregated by instance.
- Bill Details: Displays each deduction without performing aggregation.

[](id:resources_id)
## Bill by Instance
1. Click the **Bill by Instance** tab.
2. Click **All products** and select **Cloud Streaming Services**.
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
    <li>Daily settlement: Fees are deducted daily.</li>
    <li>Monthly settlement: Fees are deducted monthly</li>
    <li>New monthly subscription: CSS packages</li></ul>
    </td>
</tr>
<tr>
<td>Configuration description</td>
<td>The CSS features used in the current month and their usage.<ul style="margin:0;">
    <li>Live transcoding</li>
    <li>Live recording</li>
    <li>Live screencapturing</li>
    <li>Intelligent porn detection</li>
    </ul></td>
</tr>
<tr>
<td>Original cost</td>
<td>The total cost of using a CSS feature in the current month.</td>
</tr>
<tr>
<td>Discount multiplier</td>
<td>The discount multiplier for the month (1 indicates that no discounts were applied).</td>
</tr>
<tr>
<td>Total amount after discount</td>
<td>Total amount after discount = Original cost x Discount multiplier</td>
</tr>
</tbody></table>

>? Other fields are assigned by Tencent Cloud. For details, see [Bills](https://intl.cloud.tencent.com/document/product/555).

[](id:detail)
## Bill Details
1. Click the **Bill Details** tab.
2. Click **All products** and select **Cloud Streaming Services**.

![](https://main.qcloudimg.com/raw/0716954d4d5a955a77acd4149961ca1b.png)

#### Bill fields

| Field       | Description                                                         |
| :--------- | :----------------------------------------------------------- |
| Component type  | The CSS feature used in the current month.                               |
| Component name  | The sub-item of the feature used.                                 |
| Component price | The component’s list price without discounts.                    |
| Component usage   | The component usage.                                             |
| Discount multiplier    | The discount multiplier for the month (1 indicates that no discounts were applied). Monthly billed users are offered discounts. For details, please contact sales. |
| Usage duration   | The total usage of the component in the current month.   |
| Total amount after discount    | Total amount after discount = Original cost x Discount multiplier. Original cost = Component price x Usage duration. |

>?Other fields are assigned by Tencent Cloud. For details, see [Bills](https://intl.cloud.tencent.com/document/product/555).
