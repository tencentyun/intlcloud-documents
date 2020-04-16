

KMS fees are charged based on two billable items: [CMK](https://intl.cloud.tencent.com/document/product/1030/31984) storage and API calls as detailed below:

<table>
   <tr>
      <th>Item</th>
      <th colspan="2">Price</th>
   </tr>
   <tr>
      <td rowspan="2">CMK storage (USD/key/day)</td>
      <td>Tencent Cloud managed CMKs</td>
      <td>Free</td>
   </tr>
   <tr>
      <td>Customer managed CMKs</td>
      <td>0.06 USD/key/day</td>
   </tr>
   <tr>
      <td rowspan="2">API calls (USD/10,000 calls)</td>
      <td>First 20,000 calls</td>
      <td>Free</td>
   </tr>
   <tr>
      <td>API calls</td>
      <td>0.18 USD/10,000 calls</td>
   </tr>
</table>

## Settlement Cycle

KMS is monthly pay-as-you-go. The fees for one month are calculated, billed, and charged on the 3rd to 5th days of the following month. 

### CMK storage fees
This refers to the fees for storing the CMKs created in KMS. The CMK storage fees are billed daily, that is, the cumulative CMKs under a specified account will be billed on a daily basis.
- **Tencent Cloud managed CMKs**: free of charge.
A Tencent Cloud managed CMK is automatically created for you when a Tencent Cloud product (such as COS or TDSQL) calls the KMS service.
- **Customer managed CMKs**: 0.06 USD/key/day.
A customer managed CMK is created by you actively in the console or through APIs.

>
> - Limit on the total number of CMKs: up to 200 CMKs can be created under each account in each region, excluding the CMKs scheduled for deletion and Tencent Cloud managed CMKs. If you need to create more CMKs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) or contact your Tencent Cloud rep.
> - CMK billing status: only the customer managed CMKs scheduled for deletion are free of charge.

### API call fees
KMS provides a free tier of 20,000 API calls. After the free tier is used up, API calls will be billed monthly, that is, the cumulative API calls under a specified account in one month will be billed on a monthly basis.

**API calls**: 0.18 USD/10,000 calls, billed monthly.

>If there are less than 1000 API calls, fees will be billed for 1000 calls.


