This document answers frequently asked questions about promo vouchers. To learn more about promo vouchers, see [Promo vouchers](https://intl.cloud.tencent.com/document/product/555/7428).

### How do I view my promo vouchers?
Log in to the Tencent Cloud console and go to **Billing Center** > [Vouchers](https://console.cloud.tencent.com/account/voucher) to view your promo vouchers.

### What can I do if a promo voucher is claimed by the wrong account?
A promo voucher can only be used by the account that claimed it and cannot be transferred between accounts.

### In what cases are promo vouchers not applicable?
- Promo vouchers have use limits. Payments that do not meet the requirements (applicable products, billing modes, scenarios, etc.) cannot use promo vouchers.
- Only the account creator and collaborators/sub-users with finance management permissions can use and manage vouchers.
- Promo vouchers whose status is "used" or "expired" cannot be used.
- Promo vouchers cannot be used to offset overdue payments.
- You cannot use promo vouchers as frozen funds when enabling the pay-as-you-go billing mode.
- Some promotional campaigns may not support promo vouchers.
- Resellers’ vouchers cannot be used on orders paid on behalf of customers.

### What are the use limits of a promo voucher?
Promo vouchers have use limits. If a promo voucher is not applicable, check if your payment meets all the requirements of the voucher.

1. **Applicable products**
	Depending on their applicable products, promo vouchers are classified into product vouchers and general vouchers.
	1. Product voucher: Applicable to specific products
	   - A product voucher can be applied to payments for multiple specific products. For example, if a voucher has a face value of 100 USD and is applicable to CVM and TencentDB for MySQL, then it can deduct at most 100 USD from a payment that contains orders for CVM and/or TencentDB for MySQL.
	   - Minimum-spend vouchers can be used only if the amount of a payment exceeds a certain threshold. For example, suppose you have a 50-USD promo voucher whose minimum spending requirement is 100 USD and applicable products are CVM and TencentDB for MySQL. You can use the voucher only if your order is for CVM or/and TencentDB and the amount exceeds 100 USD.
	2. General vouchers
		There are three types of general promo vouchers:
		- Prepaid general vouchers (applicable to all prepaid payments)
		- Pay-as-you-go general vouchers (applicable to all pay-as-you-go payments)
		- All-product general vouchers (applicable to all Tencent Cloud payments)

>! We have adjusted our policy for general promo vouchers. Starting from December 10, 2020, we will specify the applicable or non-applicable products for pay-as-you go general vouchers, prepaid general vouchers, and all-product general vouchers.

2. **Payment scenarios**
	1. Billing mode
            Prepaid vouchers are only applicable to monthly subscriptions.
            Pay-as-you-go vouchers are only applicable to pay-as-you-go payments.
	2. Application scenario
            Prepaid: Purchase, renewal, or upgrade
            Pay-as-you-go: Pay-as-you-go payments

3. **Voucher status**
A promo voucher may be in one of three statuses: "Unused", "Used", or "Expired".
 - Unused: Promo vouchers that are valid and not (fully) used. Unused vouchers can be applied to your payments, but they cannot be used as frozen funds when you enable the pay-as-you-go billing mode.
 - Used: Promo vouchers that are (fully) used. Used vouchers cannot be used to deduct any amount from your payments.
 - Expired: Promo vouchers that have expired. Expired vouchers cannot be used to deduct any amount from your payments.

4. **Time limits**
For a promo voucher to be applied to a monthly subscription order, the duration purchased cannot be longer than the time limit of the voucher. For example, suppose the time limit of a promo voucher is 0-3 months. If you want to use the voucher with a monthly subscription order, the duration purchased must be 0-3 months.

5. **Minimum spend**
To use a minimum-spend voucher, your payment amount must exceed a certain threshold.

6. **Validity period**
A promo voucher can be used only within its validity period, which cannot be extended.

7. **Number of uses**
   1. One-time: A one-time voucher can be used only once (after which its status will become **Used**), regardless of whether its balance has been used up.
   2. Reusable: A reusable voucher can be used multiple times until it expires or its balance becomes zero.

### What is the time limit of a promo voucher?
A promo voucher has a time limit only when it is applied to prepaid payments. The duration purchased cannot be longer than the time limit.
For example, suppose the time limit of a promo voucher is 0-3 months. If you want to use the voucher when purchasing or renewing a monthly subscription, the duration purchased or renewed must be 0-3 months.

### Why can’t I use a promo voucher with my order?
Promo vouchers have use limits. To use a voucher, your order must meet the voucher’s application requirements (see the highlighted parts in the figure below).
![](https://qcloudimg.tencent-cloud.cn/raw/05445f5758a1e68fc5c014ef2c682bd3.png)

### How do I pay multiple orders together and apply a promo voucher to the payment?
Go to [Order Management](https://console.intl.cloud.tencent.com/expense/deal), select the orders you want to pay, and click **Consolidated Payment**. On the payment page, select **Use promo voucher**.
![](https://qcloudimg.tencent-cloud.cn/raw/4bc25d502a3dda62fdfd8c0cb0fb69b8.png)

### Can I use promo vouchers on orders that are part of a promotional campaign?
In most cases, orders that are already part of a promotional campaign cannot be paid for using promo vouchers.

### After I refund an order, will the promo voucher be returned to my account?
No, the used portion of a promo voucher is non-refundable.

### Can I use promo vouchers as frozen funds when enabling the pay-as-you-go billing mode?
No. Promo vouchers can be applied to pay-as-you-go payments, but cannot be used as frozen funds.

### Can I extend the validity period of a promo voucher?
A promo voucher can be used only within its validity period. The validity period cannot be extended.

### Can I transfer a promo voucher to another account, exchange it for cash, or reload it?
No, a promo voucher can only be used by the account which claimed it, and the voucher amount can’t be topped-up or exchanged for cash.

### Can orders paid on behalf of other users be paid for using promo vouchers?
No, promo vouchers cannot be applied to a payment made on another user’s behalf.

### Can I use promo vouchers when my account has overdue payments?
You cannot use promo vouchers to purchase new resources if your account has overdue payments. Promo vouchers cannot be used to offset overdue payments.
