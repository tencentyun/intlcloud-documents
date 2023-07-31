You can adjust the bandwidth or the billing mode of public network CLB instances as needed in real time.

## Restrictions
- IPv4 CLB instances: network configuration adjustment is only supported for bill-by-IP accounts but not for bill-by-CVM accounts.
- IPv6 CLB instances: network configuration adjustment is supported for both bill-by-IP and bill-by-CVM accounts.
- For more information on checking your account type, please refer to [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).

## Bandwidth Cap
<table>
<tbody><tr><th>Instance Billing Mode</th><th>Network Billing Mode</th><th >Bandwidth Cap Range (in Mbps)</th></tr>
<tr><td rowspan="3">Pay-as-you-go</td><td>Bill-by-bandwidth (hourly)</td><td  rowspan="3">0 - 2048 (inclusive)</td></tr>
<tr><td>Bill-by-traffic</td></tr>
<tr><td>Bandwidth package</td></tr>
</tbody></table>

>? If you need to set a higher bandwidth cap, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) or contact your Tencent Cloud sales rep.
>

## Adjusting Bandwidth
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. On the **Instance Management** page, select a region, and click **More** -> **Adjust Bandwidth** on the right of a public network CLB instance.
3. In the dialog box, set the bandwidth cap and click **Submit**.

## Changing Billing Mode
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. On the **Instance Management** page, select a region, click **More** on the right of a public network CLB instance and continue to adjust the network billing mode.
<table>
<tbody><tr><th>Instance Billing Mode</th><th>Network Billing Mode</th><th >Adjustment</th></tr>
<tr><td rowspan="3">Pay-as-you-go</td><td>Bill-by-bandwidth (hourly)</td><td>Add IP to a bandwidth package: instance billing mode remains the same; network billing mode is switched to using a bandwidth package; each instance can have its billing mode switched once only.</td></tr>
<tr><td>Bill-by-traffic</td><td><ul><li>Switch to monthly subscription: instance billing mode is switched to monthly subscription; network billing mode is switched to bill-by-bandwidth (monthly); each instance can have its billing mode switched once only.</li><li>Add IP to a bandwidth package: instance billing mode remains the same; network billing mode is switched to using a bandwidth package; each instance has unlimited chances for switching billing modes.</li></ul></td></tr>
<tr><td>Bandwidth package</td><td>Remove IP from bandwidth package: instance billing mode remains the same; network billing mode is switched to bill-by-traffic; each instance has unlimited chances for switching billing modes.</td></tr>
</tbody></table>
3. Click **Submit** in the pop-up dialog box.

