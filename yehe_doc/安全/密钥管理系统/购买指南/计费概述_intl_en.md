## Key Management Service (KMS)


The billing of KMS is based on two factors: [CMK](https://intl.cloud.tencent.com/document/product/1030/31984) storage and API calls, as detailed below:

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

### Settlement cycle

KMS supports the pay-as-you-go billing method on a monthly basis. The fees for one month are calculated and deducted on the 3rd to 5th days of the following month. 

### CMK storage fees

This refers to the fees for storing the CMKs created in KMS. The CMK storage fees are billed daily according to the total number of CMKs under a specified.

- **Tencent Cloud managed CMKs**: free of charge. A Tencent Cloud managed CMK is automatically created for you when a Tencent Cloud product (such as COS or TDSQL) calls the KMS service.
- **Customer managed CMKs**: 0.06 USD/key/day. A customer managed CMK is actively created by you in the console or via an API call.

> !
> - Limits: each account can have up to 200 CMKs per region (excluding Tencent Cloud managed CMKs and the ones in **Scheduled deletion** status). If you need to create more CMKs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) or contact your Tencent Cloud sales rep.
> - CMK billing status: the customer managed CMKs in **Scheduled deletion** status are not billed.

### API call fees

KMS provides a free tier of 20,000 API calls. After the free tier is used up, API calls will be billed monthly, that is, the cumulative API calls under a specified account in one month will be billed monthly.

**API calls**: 0.18 USD/10,000 calls, billed monthly.

> !If there are less than 1000 API calls, fees will be billed for 1000 calls.
