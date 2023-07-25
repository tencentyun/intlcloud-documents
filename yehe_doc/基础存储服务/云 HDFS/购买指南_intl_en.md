
## Billing Overview


CHDFS is billed at pay-as-you-go rates according to the actual storage usage and bandwidth. The billing cycle of each item may be different.

## Billable Items

CHDFS billable items are described as follows:

<table>
   <tr>
      <th>Billable Item</th>
      <th>Description</th>
      <th>Calculation Formula</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>Storage usage</td>
      <td>Calculated based on the STANDARD storage usage</td>
      <td nowrap>STANDARD storage usage fees = Unit price of STANDARD storage x Monthly accumulated STANDARD storage usage</td>
      <td nowrap>Monthly STANDARD storage usage = Sum of "daily STANDARD storage usage" in the month/Number of days in the month<br>Daily STANDARD storage usage = Sum of "5-minute STANDARD storage usage"/288 (number of statistical points)
			</td>
   </tr>
   <tr>
      <td>Bandwidth</td>
      <td>Calculated based on the bandwidth</td>
      <td nowrap>Bandwidth fees = Bandwidth unit price x Monthly bandwidth</td>
      <td >Monthly bandwidth = Peak bandwidth of the month x Number of valid days/Number of days in the month<br>Peak bandwidth of the month: The peak bandwidths of every 5 minutes in the month are sorted in descending order, and the top 5% of data is thrown away. The next highest measurement becomes the billable peak bandwidth for the month. </td>
   </tr>
</table>



## Pricing


<table>
   <tr>
      <th>Billable Item</th>
      <th>Billing Cycle</th>
      <th>Billing Plan</th>
      <th>Chinese Mainland</th>
      <th>Outside Chinese Mainland</th>
   </tr>
   <tr>
      <td>Storage usage</td>
      <td>Monthly</td>
      <td>Pay-as-you-go</td>
      <td>0.03375 USD/GB/month</td>
      <td>0.0484 USD/GB/month</td>
   </tr>
   <tr>
      <td>Bandwidth</td>
      <td>Monthly</td>
      <td>Pay-as-you-go</td>
      <td>0.0766 USD/Mbps</td>
      <td>0.116 USD/Mbps</td>
   </tr>
</table>


## Viewing Billing Details

1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com).
2. Click **Billing Center** in the top-right corner to enter the Billing Center overview page.
3. Click **Bills** on the left sidebar.
4. Click **Bill Details** in the drop-down list and then select CHDFS to view CHDFS's bills by instance and the bill details.


## Service Suspension Due to Overdue Payments


If your account has overdue payments, we will suspend the CHDFS service after 24 hours. Your data will be preserved for 120 days. If you don’t pay the past due charges during these 120 days, your data will be destroyed. To avoid business interruption, please make the payment in time at [Billing Center](https://console.cloud.tencent.com/expense/recharge) after you receive a payment overdue notification.

You can also configure alarms for overdue payments using the balance alarm feature of the Billing Center.

>!If you are a customer of a Tencent Cloud partner, the rules regarding resources when there are overdue payments are subject to the agreement between you and the partner.