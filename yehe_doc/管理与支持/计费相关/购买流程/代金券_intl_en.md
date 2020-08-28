International Console Voucher

A voucher is a coupon for fee deduction. You can log in to the Tencent Cloud console and go to **Billing Center** > **Voucher** to view the vouchers under your account. Vouchers cannot be withdrawn, transferred, or invoiced.

## Voucher Use Limits

1. Voucher status

A voucher can be "Unused", "Used", or "Expired".

- Unused: the voucher has not been used up. It can be used for fee deduction (excluding frozen fees for pay-as-you-go services). 

- Used: the voucher has been used up and cannot be used. 

- Expired: the voucher has expired and cannot be used.

2. Applicable services
All pay-as-you-go Tencent Cloud services.
3. Payment scenarios
Postpaid: postpaid vouchers can be used for fee deduction only for pay-as-you-go services.
4. Validity period
A voucher can be used only within its validity period, which cannot be extended.
5. Number of uses
A voucher can be used repeatedly until it expires or its balance is used up.
6. Other limits 
Only the account creator and collaborators or sub-users with finance management permissions can use and manage vouchers. Once a voucher expires or its balance is used up, it cannot be used anymore.
Vouchers cannot be used in the following cases: account arrears, frozen fees for pay-as-you-go service activation, certain promotional campaigns (subject to specific campaign rules), and pay-on-behalf orders.

An unused voucher is used as an example below to demonstrate use limits. It can be used only if your order meets the following conditions:
![](https://main.qcloudimg.com/raw/4b722364f2ec226ae87107d56abdfa77.png)

![](https://main.qcloudimg.com/raw/0094d41e669546a8a63c89b0efd051db.png)

Unused: the voucher is unused or has a positive balance.
Payment scenarios: the voucher can be used for fee deduction only for pay-as-you-go services.

Validity period: the voucher is valid from August 21, 2020 00:00:00 to September 20, 2020 23:59:59.

## Using Vouchers 

Currently, only postpaid vouchers are supported, and the instructions on how to use the vouchers are described as follows:

Using voucher for pay-as-you-go services

The system will automatically use vouchers when billing and deducting fees for (hourly/daily/monthly) pay-as-you-go services.
Multiple vouchers can be used in one single payment. When deducting fees, the system will automatically use applicable vouchers first before deducting from the account balance.
When a pay-as-you-go service is activated, the frozen fees cannot be deducted with vouchers.
After the system automatically selects a voucher for fee deduction, the deducted amount can be viewed in **Bill Details**.

## Voucher Rules

System voucher selection 

The system will sort unused vouchers matching the service, payment mode, scenario, and conditions first by expiration date in ascending order, then by deductible amount in descending order, and finally by voucher balance in ascending order. Vouchers that will expire sooner will be used first. If multiple vouchers have the same expiration date, then the voucher with the smallest deductible amount will be used first.

Example 1:
Tom uses an hourly pay-as-you-go service XXX for one hour on March 1, 2019, which incurs fees of 10 USD. There are four vouchers that meet the conditions and can be used for fee deduction: 

Voucher A (face value: 10 USD; balance: 5 USD; expiration date: March 9, 2019; deductible amount: 5 USD).

Voucher B (face value: 10 USD; balance: 8 USD; expiration date: March 9, 2019; deductible amount: 8 USD).

Voucher C (face value: 20 USD; balance: 10 USD; expiration date: March 10, 2019; deductible amount: 10 USD).

Voucher D (face value: 20 USD; balance: 12 USD; expiration date: March 11, 2019; deductible amount: 12 USD). 

The system will use voucher A first to deduct 5 USD, then use voucher B to deduct the remaining 5 USD. Both has the same expiration date so the voucher with the smaller deductible amount is used first.

Example 2:
Tom uses an hourly pay-as-you-go service XXX for one hour on March 1, 2019, which incurs fees of 20 USD. There are four vouchers that meet the conditions and can be used for fee deduction: 

Voucher A (face value: 10 USD; balance: 5 USD; expiration date: March 9, 2019; deductible amount: 5 USD).

Voucher B (face value: 10 USD; balance: 8 USD; expiration date: March 9, 2019; deductible amount: 8 USD).

Voucher C (face value: 20 USD; balance: 10 USD; expiration date: March 10, 2019; deductible amount: 10 USD).

Voucher D (face value: 20 USD; balance: 12 USD; expiration date: March 11, 2019; deductible amount: 12 USD).

The system will use voucher A to deduct 5 USD first, then it will use voucher B to deduct 8 USD and finally voucher C to deduct 7 USD. Vouchers that expire sooner and has a smaller deductible amount are used first. 

Example 3:
Tom uses an hourly pay-as-you-go service XXX for one hour on March 1, 2019, which incurs fees of 4 USD. There are four vouchers that meet the conditions and can be used for fee deduction: 

Voucher A (face value: 10 USD; balance: 5 USD; expiration date: March 9, 2019; deductible amount: 4 USD).

Voucher B (face value: 10 USD; balance: 8 USD; expiration date: March 9, 2019; deductible amount: 4 USD).

Voucher C (face value: 20 USD; balance: 10 USD; expiration date: March 10, 2019; deductible amount: 4 USD).

Voucher D (face value: 20 USD; balance: 12 USD; expiration date: March 11, 2019; deductible amount: 4 USD).

The system will use voucher A for deduction first, as it has the smallest balance among the vouchers with the same expiration date and deductible amount.

