Promo vouchers can be used to deduct certain amounts from the fees you incur with Tencent Cloud. You can view your promo vouchers in **Billing Center** > [Vouchers](https://console.tencentcloud.com/expense/voucher). You cannot transfer promo vouchers to other accounts, exchange them for cash, or request invoices for them.
If you have questions, see [FAQs > Promo Vouchers](https://intl.cloud.tencent.com/document/product/555/10870).

## Use Limits
### Use limits for promo vouchers
#### 1. Status
A promo voucher may be in one of three statuses: "Unused", "Used", or "Expired".
- Unused: The voucher is valid and has not been fully exhausted. Unused vouchers can be applied to your payments, but they cannot be used as frozen funds when you enable the pay-as-you-go billing mode.
- Used: The voucher has already been fully exhausted. Used vouchers cannot be used to deduct any amount from your payments.
- Expired: The voucher has expired. Expired vouchers cannot be used to deduct any amount from your payments.

#### 2. Applicable products
Depending on their applicable products, promo vouchers are classified as product vouchers or general vouchers.

**A. Product vouchers:**
Product vouchers can only be used to pay for specific products or groups of products.

**B. General vouchers:**
General vouchers can be used to pay for any products (excluding some products that cannot be paid for with general vouchers).

#### 3. Payment scenarios
A. Depending on the payment scenario, vouchers are classified into the following types:
- Prepaid: The voucher is only applicable to monthly subscriptions.
- Pay-as-you-go: The voucher is only applicable to pay-as-you-go payments.

B. The application scenarios of prepaid and pay-as-you-go vouchers are also different.
- Prepaid: Vouchers can be used for purchase, renewal, or upgrade.
- Pay-as-you-go: Vouchers can be used for pay-as-you-go payments.

#### 4. Time limits
For a voucher to be applied to a monthly subscription order, the duration of the subscription cannot be longer than the time limit of the voucher.
For example, suppose the time limit of a promo voucher is 0-3 months. If you want to use the voucher to pay for a monthly subscription order, the duration of the subscription must also be within 0-3 months.

#### 5. Minimum spend
To use a minimum-spend voucher, your payment amount must exceed a certain threshold.
Based on their minimum spend requirements, vouchers are classified into the following types:
- No minimum spend: The voucher can be used for orders that contain the applicable products regardless of the payment amount.
  For example, if a voucher has a face value of 100 USD and is applicable to CVM and TencentDB for MySQL, then it can deduct at most 100 USD from a payment that contains orders for CVM and/or TencentDB for MySQL.
- Minimum-spend voucher: The voucher can only be used if the total amount for the payment exceeds a certain threshold.
  For example, suppose you have a 50-USD voucher whose minimum spending requirement is 100 USD, and the applicable products are CVM and TencentDB for MySQL. You can use the voucher only if your order is for CVM or/and TencentDB and the total payment amount exceeds 100 USD.

#### 6. Validity period
A voucher can be used only within its validity period, which cannot be extended.

#### 7. Number of uses
- One-time: A one-time voucher can be used only once (after which its status will become **Used**), regardless of whether its balance has been fully exhausted.
- Reusable: A reusable voucher can be used multiple times until it expires or until its balance becomes zero.

#### 8. Other limits
- Only the account creator and collaborators/sub-users with finance management permissions can use and manage vouchers.
- Vouchers whose status is "used" or "expired" cannot be used.
- Vouchers cannot be used to offset overdue payments.
- You cannot use vouchers to take the place of frozen funds when enabling the pay-as-you-go billing mode.
- You may not be able to use vouchers for orders that were purchased through a promotional campaign. Please check the rules of the specific promotion for details.
- Orders paid on behalf of other users cannot be paid with vouchers.

### Examples

Take the promo voucher in the screenshot below as an example. It has the following use limits.
![](https://qcloudimg.tencent-cloud.cn/raw/c1226e6e611183dfd820d32fd24314cb.png)
- Unused: The voucher is unused (has a positive balance remaining).
- Applicable products: The voucher can only be used to pay for CVM, TencentDB for MySQL, or CBS.
- Scenario: The voucher can be applied to both prepaid and pay-as-you-go payments.
- Minimum spend: The voucher does not have a minimum spend requirement.
- Validity period: The voucher is valid from 2022-06-23 00:00:00 to 2022-08-22 23:59:59.
- Number of uses: The voucher is reusable and can be used multiple times until it expires or its balance becomes zero.

## Using Promo Vouchers

Vouchers are applied differently to prepaid and pay-as-you-go payments.

### Prepaid payments
When purchasing, manually renewing, or upgrading a subscription plan, you can apply a promo voucher on the **payment page**.
![](https://qcloudimg.tencent-cloud.cn/raw/0fd360129824ba47070356617d9255d9.png)
>?
>- The system will match promo vouchers with the order, taking into account the applicable products, billing mode, order amount, and other use limits. Only vouchers that meet all the conditions can be applied to the order.
>- For auto-renewal, the system will apply a promo voucher first before deducting the remaining amount from your account balance. For details, see [Auto-application](#Auto application). To learn about how to enable auto-renewal, see [Renewal Management](https://intl.cloud.tencent.com/document/product/555/7454).
>- **You can use only one promo voucher for each payment**. If there are multiple applicable vouchers for an order, you need to choose one to use. If you do not want to use a voucher, unselect **Use promo voucher**.
>- You can pay for multiple orders together on the **Order Management** page (select the orders you want to pay and click **Consolidated Payment**) and apply a promo voucher to the payment.
>- If you refund a prepaid order, the promo voucher applied will not be returned.

### Pay-as-you-go payments
The system will automatically apply vouchers when deducting fees (hourly/daily/monthly) under the pay-as-you-go mode.
- **Only one promo voucher can be used for each payment**. The system will apply a promo voucher first before deducting the remaining amount from your account balance. For details, see [Auto-application](#Auto-application).
- You cannot use vouchers to take the place of frozen funds when enabling the pay-as-you-go billing mode.
- You can view the usage of automatically applied promo vouchers on the [Bill Details](https://console.intl.cloud.tencent.com/expense/bill/summary) page.

## Enabling Auto-Deduction
You can enable auto-deduction for each of your promo vouchers so that they will be automatically applied to auto-renewal, pay-as-you-go, or other applicable payments. To enable it, go to [Billing Center](https://console.cloud.tencent.com/expense) > [Promo voucher](https://console.tencentcloud.com/expense/voucher).
By default, auto-deduction is enabled for each voucher (i.e., promo vouchers will be automatically applied). To disable it, click the toggle and confirm in the pop-up window. To enable auto-deduction again, click the toggle again.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9yVX405_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16770487932568.png)

>?
> After your promo vouchers are used up or expire, the toggle status will not be changed.

## Voucher Application Rules
<span id="Auto-application"></span>
### Auto-application
The system matches promo vouchers with a payment (taking into account the applicable products, billing modes, scenarios, and other use limits) and **sorts the applicable vouchers by expiration time from the soonest to the latest. If multiple vouchers have the same expiration time, they will be sorted by deductible amount from the highest to the lowest. If multiple vouchers have the same expiration time and deductible amount, they will be sorted by remaining balance from the lowest to the highest.**
- The highest priority is given to the one that expires the soonest among vouchers that can cover the whole payment amount.
- If no voucher can cover the whole payment amount, the promo voucher that expires the soonest will be applied.
- If there are multiple vouchers that expire at the same time, the voucher that can deduct the highest amount from the payment will be used. If the deductible amount is the same, the voucher with the lowest balance will be used.

**Example 1:**
On March 1, 2019, a customer was billed for CVM in the hourly pay-as-you-go mode. The fee incurred was 10 USD. Four promo vouchers were eligible:
Voucher A: Face value: 10 USD; balance: 5 USD; expiration time: March 9, 2019; deductible amount: 5 USD.
Voucher B: Face value: 10 USD; balance: 8 USD; expiration time: March 9, 2019; deductible amount: 8 USD.
Voucher C: Face value: 20 USD; balance: 10 USD; expiration time: March 10, 2019; deductible amount: 10 USD.
Voucher D: Face value: 20 USD; balance: 12 USD; expiration time: March 11, 2019; deductible amount: 10 USD.
The system would automatically apply voucher C because it expires the soonest among the vouchers that can cover the whole payment amount.

**Example 2:**
On March 1, 2019, a customer was billed for CVM in the hourly pay-as-you-go mode. The fee incurred was 20 USD. Four vouchers were eligible.
Voucher A: Face value: 10 USD; balance: 5 USD; expiration time: March 9, 2019; deductible amount: 5 USD.
Voucher B: Face value: 10 USD; balance: 8 USD; expiration time: March 9, 2019; deductible amount: 8 USD.
Voucher C: Face value: 20 USD; balance: 10 USD; expiration time: March 10, 2019; deductible amount: 10 USD.
Voucher D: Face value: 20 USD; balance: 12 USD; expiration time: March 11, 2019; deductible amount: 12 USD.
None of the four vouchers can cover the whole payment amount. Therefore, among vouchers that expire the soonest, the one with the highest deductible amount would be used, which is voucher B.

**Example 3:**
On March 1, 2019, a customer was billed for CVM in the hourly pay-as-you-go mode. The fee incurred was 4 USD. Four vouchers were eligible.
Voucher A: Face value: 10 USD; balance: 5 USD; expiration time: March 9, 2019; deductible amount: 4 USD.
Voucher B: Face value: 10 USD; balance: 8 USD; expiration time: March 9, 2019; deductible amount: 4 USD.
Voucher C: Face value: 20 USD; balance: 10 USD; expiration time: March 10, 2019; deductible amount: 4 USD.
Voucher D: Face value: 20 USD; balance: 12 USD; expiration time: March 11, 2019; deductible amount: 4 USD.
All four vouchers have the same deductible amount. Therefore, among the vouchers that expire the soonest, the one with the lowest balance will be used, which is voucher A.

### Spread over multiple orders

If a voucher is applied to a payment that contains multiple orders, and it cannot cover the whole payment amount, the deduction will be spread over the orders as follows:

- **Prepaid**
When you renew multiple subscription plans together, the system will spread the deduction amount of a voucher according to the renewal fee of each plan.
**Example**: A customer renewed two plans together. The renewal fee of plan 1 was 100 USD and that of plan 2 was 200 USD. Suppose the customer had a promo voucher with a balance of 90 USD. 30 USD would be deducted from the renewal fee of plan 1 and 60 USD would be deducted from the renewal fee of plan 2. The remainder would be paid out of the customer’s account balance.

- **Pay-as-you-go**
If there are multiple pay-as-you-go orders for a billing period, the deduction amount of a voucher will be spread over the orders according to the amount of each order.
**Example**: A customer had two pay-as-you-go orders for a billing period. The amount of order 1 was 100 USD and that of order 2 was 200 USD. Suppose the customer had a promo voucher with a balance of 90 USD. 30 USD would be deducted from the fee of order 1 and 60 USD would be deducted from the fee of order 2. The remainder would be paid out of the customer’s account balance.

