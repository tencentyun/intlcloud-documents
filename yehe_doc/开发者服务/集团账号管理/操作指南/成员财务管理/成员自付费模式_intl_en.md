The member self-pay mode involves the following finance permissions:

| Finance Permission         | Description                                  |
| ---------------- | -------------------------------------- |
| View member account information | The admin account can view the balance information of member accounts.   |
| View member account bills     | The admin account can view the bill details of member accounts.   |
| Issue invoices to member accounts   | The admin account can issue invoices to member accounts.           |
| Consolidate bills         | The admin account can consolidate the bills of multiple member accounts for download. |
| Inherit offers         | Member accounts can inherit the admin account’s offers specified in the contract.     |



### **Viewing Member Account Balance**

This section describes how the admin account views the balance information of its member accounts.

#### **Directions**

1. Log in to the **Billing Center** console with the admin account and select [Account Info](https://console.tencentcloud.com/expense) on the left sidebar.

2. In the drop-down list in the top-right corner, select a member account to view its balance information.

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/H2cG398_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324110731.png)



### **Viewing Member Account Bills**

This section describes how the admin account views the bill details of member accounts.

#### **Directions**

1. Log in to the **Billing Center** console with the admin account and select [Bills](https://console.tencentcloud.com/expense/bill/overview) on the left sidebar.

2. On the **Bill Overview** page, select a member account in the drop-down list in the top-right corner to view its bill overview.

3. On the **Bill Details** page, select a member account in the drop-down list in the top-right corner to view its bill details. You can also click **Confirm Bill** to confirm the bill for the member account for the selected month.

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/3wc5340_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324110752.png)  

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/ZNsJ175_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324110811.png)

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/CuzK230_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324110821.png)


### **Consolidating Member Account Bills**

This section describes how the admin account consolidates the bills of multiple member accounts.

#### **Directions**

1. Log in to the **Billing Center** console with the admin account and select [Bill Details](https://console.tencentcloud.com/expense/bill) on the left sidebar.

2. Select the **Consolidated Bill** tab, select the member accounts for which you want to consolidate bills, and click **Download Consolidated Bill**. You can also go to the [Download Records](https://console.tencentcloud.com/expense/download) page and click **Download** to download the consolidated bills. 

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/WHbI289_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324110851.png)


### **Issuing Invoices to Member Accounts**

This section describes how the admin account issues invoices to member accounts.

#### **Directions**

1. Log in to the **Billing Center** console with the admin account and select [Invoicing](https://console.tencentcloud.com/expense/invoicing) on the left sidebar.

2. In the drop-down list in the top-right corner, select a member account to issue the invoice. The issued invoice belongs to the member account.

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/FkNv495_image%20%281%29.png)


### **Inheriting Offers**

This section describes how a member account inherits the admin account’s offers specified in the contract.

#### **Inheritable offers**

Member accounts can inherit the contract offers applied for by the sales rep, but not the official discount or promotional discount.

Contract offers include **billing-level offers**, **finance-level offers**, and **rebates**, as detailed in the table below:

| Offer Type             | Billing-Level Offer                                            | Finance-Level Offer                                                   | Rebate                                                         |
| ---------------------------- | ----------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Offer description                     | It is applied to a single prepaid or pay-as-you-go order and takes effect in real time. | It is applied to consolidated bills on a monthly basis and takes effect on the first day of the next month. | It is a rebate (in the form of voucher or free credit) calculated based on a certain proportion of the bill amount in the current month. It takes effect on the third day of the next month. |
| Discount                 | ✔                                                     | ×                                                            | ×                                                            |
| Contract price (linear, tiered, or fixed pricing) | ✔                                                     | ×                                                            | ×                                                            |
| Minimum spend (fixed or fluctuated monthly)   | ×                                                     | ×                                                            | ×                                                            |

<dx-alert infotype="explain" title="">
“✔” means the offer is inheritable, and “×” means uninheritable.
</dx-alert>

<dx-alert infotype="notice" title="">
1.Make sure all offers of member accounts are covered by the ones the admin account has applied for, so that they can still enjoy those offers after inheriting from the admin. Member accounts can choose to use their own applied offers without inheriting the admin account's offers, but once they inherit, only the inherited offers will apply.
2. Inherited offers cannot be applied to products in the blocklist which don’t support offer inheritance.
3. Only when the member accounts and the admin account use the same settlement cycle (such as daily or monthly) can the former inherit the latter’s offers. You can adjust the settlement cycle of products such as Cloud Streaming Services, Video on Demand, and Short Message Service for member accounts through CPQ.
4. Rebates and finance-level offers cannot be inherited.
</dx-alert>

You can go to the TCO console to allow **member accounts under the same verified entity as yours** to inherit your offers. To implement offer inheritance for **member accounts under a different verified entity**, contact your sales rep. Once the inheritance relationship is established, you can view the inheritance details of your member accounts.

In the organization fund allocation or member self-pay mode, the inherited offers will remain effective when the admin deletes the organization or removes organization members, or when members actively quit the organization. To cancel these offers, contact your sales rep.


#### **Directions**

Setting offer inheritance

When adding a member, you can set offer inheritance for the member account as follows:

1. Log in to the TCO console and click [Member account management](https://console.tencentcloud.com/organization/member) on the left sidebar.

2. On the **Member account management** page, click **Add member**.

3. On the **Add member** page, set offer inheritance in different ways based on different member adding methods.

**Create member**: The created member account and the admin account are under the same verified entity by default. Select **Self-pay** for the **Payment mode** option, select **Inherit offer**, and fill in other required information to create the member.

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/KwxJ366_image%20%282%29.png)

**Invite member**:

If the member account and the admin account are under the same verified entity, select **Self-pay** for the **Payment mode** option, select **Inherit offer**, and fill in other required information to invite the member.

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/Y9aR987_image%20%283%29.png)

If the member account and the admin account are under different verified entities, contact your sales rep if you want to set offer inheritance after selecting **Self-pay** for the **Payment mode** option.


#### **Canceling inherited offers**

To cancel the inherited offers of member accounts, contact your sales rep.