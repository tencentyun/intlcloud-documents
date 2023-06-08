The unified organization payment mode is a financial pay-on-behalf mode including the following capabilities:

| Capability     | Description                                                                         |
| -------- | ------------------------------------------------------------ |
| Orders | Member accounts' monthly subscription and pay-as-you-go orders are automatically paid by the payer account. |
| Offers     | This capability is optional. If member accounts have the offer inheritance permission, the offer inheritance rules will apply; otherwise, member accounts will use their own offers. |
| Vouchers   | Member accounts use the admin account's vouchers by default.                                 |
| Bills     | Member accounts' bills are automatically settled to the payer account for unified management.           |
| Invoices     | Member accounts' invoiceable amounts are automatically settled to the payer account for unified invoice issuance.                 |
| Transaction details | Member accounts' transaction details are uniformly managed by the payer account.   |
| Lifecycle | Overdue payments, service suspension, and top-up under member accounts are processed based on the balance of the payer account.   |

Relevant rules are as detailed below:

### Orders

#### Purchasing/upgrading monthly subscribed resource

When a member account purchases/upgrades a monthly subscribed resource, only payment-on-behalf can be selected, and payment with balance or online payment are not supported. Then, the payer account doesn't need to process the order manually, and the system will automatically complete the payment-on-behalf based on the balance and credit of the payer account and display the pay-on-behalf result.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/ujpb115_%E8%AE%A2%E5%8D%95%E7%A1%AE%E8%AE%A4%E9%A1%B5%E9%9D%A2.png)

![](https://staticintl.cloudcachetci.com/yehe/backend-news/C2Sk845_%E6%94%AF%E4%BB%98%E7%BB%93%E6%9E%9C%E9%A1%B5%E9%9D%A2.png)

#### Downgrading/unsubscribing monthly subscribed resource

When a member account downgrades or unsubscribes from a monthly subscribed resource, the amount will be refunded to the payer account based on the UIN and payment ratio.

You can learn about the rules by referring to the following scenario:

Below are the member account details:

![](https://staticintl.cloudcachetci.com/yehe/backend-news/zbau979_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221227155435.png)

<table>
  <tr>
  <th><b>Order</b></th>
  <th><b>Pay-on-Behalf</b></th>
  <th><b>Account to Refund to</b></th>
    </tr>
   <tr>
      <td rowspan=2>The order is placed in region A and refunded in region B.</td>
    <td>No</td>
   <td>The amount is refunded to the member account based on the payer UIN.</td> 
	  </tr>
	<td>Yes (the resource may be upgraded in region B)</td>
	<td>The amount is refunded to the member and admin accounts based on the payer UIN.</td>
	</tr>
	<tr>
	   <td>The order is placed in region B.</td>
	<td>Yes</td>
	<td>The amount is refunded to the admin account based on the payer UIN.</td>
	</tr>
	<tr>
	    <td rowspan=2>The order is placed in region A and refunded in region C.</td>
	<td>No</td>
	<td>The amount is refunded to the member account based on the payer UIN.</td>
	  </tr>
	<td>Yes (the resource may be upgraded in region B)</td>
	<td>The amount is refunded to the member and admin accounts based on the payer UIN.</td>
	</tr>
	<tr>
</table>

#### Amount freezing upon pay-as-you-go resource activation

When a member account joins an organization, the frozen amount of the member account's pay-as-you-go resources will be unfrozen.

When the member account quits the organization, the member account's order corresponding to the admin account's frozen amount of pay-as-you-go resources will be unfrozen.

Below is an example:

![](https://staticintl.cloudcachetci.com/yehe/backend-news/p3QT475_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221227155734.png)

#### Pay-as-you-go resource settlement

The fees incurred within the current or next cycle will be deducted from the payer account.

The fees incurred within the last cycle will be deducted from the member account.

>! The rules also apply to the extended cycle of pay-as-you-go resources.

Vouchers: Member accounts can use the payer account's vouchers.

Resource pack: The rules for product purchase, upgrade/downgrade, unsubscription are the same as those for monthly subscribed products. Currently, fees incurred by pay-as-you-go resources cannot be paid on behalf; instead, they will be deducted from the member account's own resource pack.

Below is an example:

![](https://staticintl.cloudcachetci.com/yehe/backend-news/whxX224_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221227155800.png)

<table>
  <tr>
  <th><b>Settlement Cycle</b></th>
  <th><b>Example</b></th>
  <th><b>Settlement Rule</b></th>
  <th><b>Resource Pack Deduction</b></th>
    </tr>
   <tr>
      <td rowspan=2>Hourly</td>
    <td>2021-09-09   <br/>12:00:00–13:00:00</td>
   <td>The fees and vouchers are deducted from the payer account.</td> 
   <td>The fees are deducted from the member account's own resource pack.</td> 
	  </tr>
	<td>2021-10-30  <br/>11:00:00–12:00:00</td>
	<td>The fees are deducted from the member account, and vouchers can be used.</td>
	<td>The fees are deducted from the member account's own resource pack.</td>
	</tr>
	<tr>
	   <td rowspan=2>Daily</td>
	<td>2021-09-09</td>
	<td>The fees and vouchers are deducted from the payer account.</td>
	<td>The fees are deducted from the member account's own resource pack.</td>
	   </tr>
	<td>2021-10-30</td>
	<td>The fees are deducted from the member account, and vouchers can be used.</td>
	<td>The fees are deducted from the member account's own resource pack.</td>   
	</tr>
	<tr>
	    <td rowspan=2>Monthly</td>
	<td>2021-09</td>
	<td>The fees and vouchers are deducted from the payer account.</td>
	<td>The fees are deducted from the member account's own resource pack.</td>
	  </tr>
	<td>2021-10</td>
	<td>The fees are deducted from the member account, and vouchers can be used.</td>
	<td>The fees are deducted from the member account's own resource pack.</td>
	</tr>
	<tr>
</table>



#### Viewing pay-on-behalf orders

After a payment-on-behalf is completed, you can log in to the [TCO console](https://console.cloud.tencent.com/organization) and select **Pay-on-behalf order management** on the left sidebar to view the pay-on-behalf order and perform relevant operations based on your role.

##### Admin account

The admin account can view the pay-on-behalf orders of member accounts. For orders to be paid, the admin account can also pay on behalf or cancel them.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/iXr5683_%E9%9B%86%E5%9B%A2%E8%B4%A6%E5%8F%B7%E9%A2%84%E4%BB%98%E8%B4%B9%E4%BB%A3%E4%BB%98%E8%AE%A2%E5%8D%95%E6%9F%A5%E7%9C%8B.png)

##### Member account

A member account can view all orders paid by the payer account and apply for payment-on-behalf on the page.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/EHVJ136_%E6%88%90%E5%91%98%E8%B4%A6%E5%8F%B7%E9%A2%84%E4%BB%98%E8%B4%B9%E4%BB%A3%E4%BB%98%E8%AE%A2%E5%8D%95%E6%9F%A5%E7%9C%8B.png)

#### Offers

In financial pay-on-behalf mode, the admin account can set whether to enable “offer inheritance” for member accounts. If it is enabled, the offer inheritance rules will apply; otherwise, member accounts will use their own offers.

<dx-alert infotype="notice" title="">
- Offers cannot be inherited for products in the blocklist, for which the member accounts' own offers will apply. For more information on the blocklist, contact your channel manager or submit a ticket for assistance.
- Rebates of the payer account are not inherited by member accounts.
- The admin account can set whether to enable “offer inheritance” for member accounts. If “offer inheritance” is enabled, the existing offer inheritance relationship will be verified. If a member chooses another member as its payer, they can’t establish a new inheritance relationship if any of them is already involved in one.
If you want to cancel the existing offer inheritance relationship and establish a new one, contact your sales rep to confirm that the payer account has successfully applied for contract offers and to help cancel the existing offer inheritance relationship. If you have any questions, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
</dx-alert>

#### Vouchers

Member accounts can use the admin account's vouchers but not their own vouchers.

#### Bills

Member accounts' bills are automatically settled to the payer account for unified management. The payer account can view the bills of all associated member accounts, and a member account can only view its own bills paid by the payer account but not the bills of other member accounts.

Paid-on-behalf bills can be viewed in the [TCO console](https://console.cloud.tencent.com/organization/bill/overview), while self-paid bills can be viewed in the [Billing Center](https://console.cloud.tencent.com/expense/bill/overview). For more information on the bill fields, see [Fields in Bills](https://www.tencentcloud.com/document/product/555/37506).

Below are the bills from the perspectives of the admin account and member account respectively:
<dx-tabs>
::: Admin account
After logging in to the Tencent Cloud console, the admin account can go to [Billing Center -> Bills](https://console.cloud.tencent.com/expense/bill/summary) to view pay-on-behalf bills.![](https://staticintl.cloudcachetci.com/yehe/backend-news/M4w9052_%E9%9B%86%E5%9B%A2%E8%B4%A6%E5%8F%B7%E8%B4%A6%E5%8D%95%E8%AF%A6%E6%83%851.png)



![](https://staticintl.cloudcachetci.com/yehe/backend-news/rIAQ772_%E9%9B%86%E5%9B%A2%E8%B4%A6%E5%8F%B7%E8%B4%A6%E5%8D%95%E8%AF%A6%E6%83%852.png)
:::
::: Member account
After logging in to the Tencent Cloud console, the member account can go to [Tencent Cloud Organization -> Pay-on-behalf bill management](https://console.cloud.tencent.com/organization/agentdeal) to view pay-on-behalf bills.![](https://staticintl.cloudcachetci.com/yehe/backend-news/gbvZ135_%E8%B4%A6%E5%8D%95%E8%AF%A6%E6%83%851.png)
:::
</dx-tabs>

#### Invoices

Member accounts are verified with the same enterprise identity as the payer account, and invoices are issued by the payer account uniformly.

#### Transaction details

Member accounts' transaction details are uniformly managed by the payer account.

#### Lifecycle

The payer account should guarantee a sufficient balance to ensure that the member accounts' resources can be used normally. For resources that need to be renewed manually, the payer account should renew them timely. Below are the rules for overdue payment, service suspension, and resource termination events:

##### Message events

- Messages about monthly subscribed resources such as notifications for resource expiration/termination and service suspension/recovery will be sent to the payer account.
- Messages about pay-as-you-go resources will be sent to the member account.

##### Action events

- Service suspension and termination events under member accounts are processed based on the balance of the payer account. If the payer account has an overdue payment, the service will be suspended for all associated member accounts.
- After the payer account is topped up to a positive balance, the service will be recovered for all associated member accounts.

##### Status processing

- After a member account joins an organization, service suspension and recovery will be subject to the balance, credit, or privileges of the payer account.
- After a member account quits an organization, service suspension and recovery will be subject to its own balance, credit, or privileges.

#### Miscellaneous

If you and Tencent Cloud have entered into a contract for private cloud businesses, the billing rules stipulated in the contract shall prevail.
