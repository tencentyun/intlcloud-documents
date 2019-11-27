
If you are unsatisfied with the prepaid CDB you have purchased, you can apply for an unconditional return and refund within five days after the purchase. The 5-day unconditional return is allowed only for **one** CDB. The amount you paid is returned to the same account you used to make the payment. In addition, you can apply for an ordinary self-service return within five days after your purchase, in which case the fees for the consumed resources are deducted from the amount actually paid and the remaining amount is returned to your account in the form of coupons. All of the above operations can be performed by yourself in CDB console.

## 5-Day Unconditional Self-Service Return
If you are unsatisfied with the CDB you purchased, you can apply for an unconditional self-service return within five days after the purchase. The rules for return and refund are as follows:

1. For a single account, you can apply for an unconditional return for **one** CDB within five days (inclusive) after the purchase.
2. In case of any application for a return suspected to be abnormal/malicious, Tencent Cloud reserves the right to reject the application.


### Rules for 5-Day Unconditional Self-Service Return
For an order eligible for the 5-day unconditional return, the refund amount is **the total amount paid upon purchase**, including the amount of cash account, revenue account and complimentary account.

**Note: Rebates and coupons are not returned.**

**Refund amount** is **returned in full to the same accounts you used to make the payment**.

## Ordinary Self-Service Return
For the orders not eligible for 5-day unconditional return and refund policy, the refund policy is as follows:


If you have applied for 5-day unconditional return, you can return additional **3** prepaid CDBs in the console within 5 days (inclusive) after the purchase. For ordinary self-service return, the fees for the consumed resources are deducted from the amount paid and the remaining amount is returned to your account in the form of coupons. For more information on refund rules, please see [Rules for Ordinary Self-Service Return of CDB].


### Service Limits on Ordinary Self-service Return	
In the following scenarios, ordinary self-service return of prepaid instances is not supported:

1. Prepaid instances that have been purchased for more than 5 days are not eligible for self-service return.
2. Self-service return is not supported for some resources in promotional activities. Please refer to the information provided on official website.


## Notes about Self-service Return of Prepaid CDB Instancess
1. After a prepaid instance is returned, no fee for the instance is incurred once its status changes to "Terminating" or "Terminated".
2. The IP resource is released upon the complete termination of a prepaid CDB instance, and the instance cannot be accessed. If the instance has a read-only or disaster recovery instance:
	- The read-only instance is terminated at the same time.
	- The synchronization connection between the disaster recovery instance and the master instance is broken, and the disaster recovery instance is automatically upgraded to the master instance.
3. After a prepaid instance is returned, it is moved to the **CDB Recycle Bin to be kept for 7 days**, and cannot be accessed. If you want to resume a prepaid instance you have returned, you can go to the CDB Recycle Bin to renew and resume it.
4. In case of any application for a return suspected to be abnormal/malicious, Tencent Cloud reserves the right to reject the application.


<span id = "cdb_pt_refund"></span>
### Rules for Ordinary Self-Service Return of CDB
Refund amount=Amount of effective order + Amount of non-effective order - Value of used resources

**Amount of effective order**: The amount paid for the order in effect, excluding discounts and coupons

**Amount of non-effective order**: The amount paid for the order that will take effect in the future, excluding coupons.

**The fees for used resources** are calculated based on the following policies:

- For the consumed resources, if the application for return is submitted one month after the purchase, the monthly fees are deducted. If such application is submitted less than a month after the purchase, the fees for the actually consumed resources are deducted.
- The consumed resources are calculated with an accuracy down to seconds.
- If refund amount<=0, it is considered 0 and resources are cleaned up.

**Note: Rebates and coupons are not returned.**






