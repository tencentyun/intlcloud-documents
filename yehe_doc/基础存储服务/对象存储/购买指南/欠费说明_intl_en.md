>!If you are a customer of a Tencent Cloud partner, the rules regarding resources when there are overdue payments are subject to the agreement between you and the partner.

If your account has overdue payment, a notification will be sent to you. Once receiving it, please go to the [Billing Center](https://console.cloud.tencent.com/account/recharge) in the console and pay the past due charges in time to prevent your business from being affected. This document will provide detailed information on overdue payment.

## Causes

You can learn about why overdue payment happens by browsing FAQs as below:

- [Why is my account overdue or charged even if I am on the free tier?](https://www.tencentcloud.com/document/product/436/10373)
- [Why is my account overdue or charged even if I have purchased a resource pack?](https://intl.cloud.tencent.com/document/product/436/10373)


>?
>- If you have any question, please check [Bill Overview](https://console.cloud.tencent.com/expense/bill/overview) on the console. For more information, please see [Viewing Billing Details](https://www.tencentcloud.com/document/product/436/31631).
>- See [Billable Items](https://www.tencentcloud.com/document/product/436/33776) for the description of each billing item and billing rules.
>- For information on the billing cycle of each billing item, see [Billing Cycle](https://www.tencentcloud.com/document/product/436/16871).


## Service status in the case of overdue payment


1. COS service is still available within 24 hours after your account has overdue payment, with a service suspension notification sent to you on the console. In this case, please pay charges so that your account balance is not less than 0 in order to avoid affecting your business.
2. COS service will be automatically suspended after 24 hours with overdue payment. You cannot read or write any data in COS, while charges will still accrue for the **storage usage of your data** until it is destroyed. Before the destruction, COS will retain your data for 120 days considering its potential importance. During this period, all you can do using the console is pay charges. Ensure that your account balance is not less than 0 so that the service can be activated again.
3. After 120 days on end with overdue payment, you will be deemed to have waived the COS service. With no promise to further retain your data, it will be destroyed and cannot be recovered.


## How do I avoid or process overdue payment?


1. If you no longer use the data stored in COS, delete it to avoid incurring further fees.
2. You can enable the **cost alert** feature in the **Console** > **Billing Center**. An alert notification will be sent to you when your available balance drops below the alert threshold. For more information, see [Balance Alerts](https://www.tencentcloud.com/document/product/555/9942).
3. When your account has an overdue payment, top up your account to a positive balance promptly. You can check your [bills](https://console.cloud.tencent.com/expense/bill/overview) in the Billing Center and perform an analysis based on your actual needs. If the amount of resources required for your business scenario is relatively stable, you can purchase a resource pack for deduction of your resource usage to save your costs. For more information, see [Resource Pack (Prepaid)](https://www.tencentcloud.com/document/product/436/54353).



## How do I deactivate the COS service and stop being charged?

You can deactivate COS or stop its billing as follows:

1. If you decide to stop using COS, you can avoid any further billing by permanently deleting all of your COS data (including incomplete multipart uploads and object versions) as instructed in [Directions](#close). There is no need to remove your account, and if you use other Tencent Cloud products, please avoid doing so as it will affect your other services.
2. If you don't use COS for more than one month, you can set lifecycle rules to transition data in STANDARD storage class in the bucket to a colder class such as STANDARD_IA, ARCHIVE, or DEEP ARCHIVE to reduce storage fees. For more information, see [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605). The transition will generate read requests in the original storage class and write requests in the target storage class, so transition by lifecycle will incur read/write [request fees](https://intl.cloud.tencent.com/document/product/436/40100).


**Notes**

- Data, once deleted from the bucket, cannot be recovered, so make backups accordingly.
- If versioning is enabled for the bucket, disable it before deleting data.
- Check your billing cycle to avoid overdue payments. If all your billable items are settled daily, the bill for the day of data deletion will be generated on the next day. After the data is completely cleared, the system will stop billing. For more information, see [Billing Cycle](https://intl.cloud.tencent.com/document/product/436/16871).
- If your account has overdue payment (i.e., your account balance is below 0), COS services will be suspended after 24 hours, regardless of whether your resource pack is within the validity period.
- If your account has overdue payment and COS services are suspended, the free tier for which your account is eligible won't be available.
- If data in your bucket is blocked for the second time due to non-compliance, it cannot be deleted. [Contact us](https://intl.cloud.tencent.com/contact-sales) if you have any questions. 



[](id:guide)

**Directions**


Step 1. Empty a bucket

- Empty a bucket by [setting lifecycle configuration](https://intl.cloud.tencent.com/document/product/436/14605): This applies to a bucket containing 10,000 or more objects. A deletion task will be executed when the trigger conditions are met for a lifecycle policy. For details about the task start time and completion time, see the instructions for setting a lifecycle policy in the console.
- [Empty a bucket](https://intl.cloud.tencent.com/document/product/436/30926) using the console: This applies to a bucket containing less than 10,000 objects. A bucket is emptied immediately after the emptying task is completed.

>? If you have a large amount of data in your bucket, clearing the bucket using the console may be slow or even fail due to network reasons. In this case, we recommend you clear the bucket by setting lifecycle configuration.
>

Step 2. Delete a bucket

- [Delete a bucket](https://intl.cloud.tencent.com/document/product/436/30361) using the console.
- Delete a bucket using the [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) API.
- You can also delete a bucket using the SDKs or tools as instructed in [Deleting a Bucket](https://intl.cloud.tencent.com/document/product/436/14105).

Step 3. Confirm deletion

After completing steps 1 and 2, log in to the console again to confirm that the data has been cleared and the bucket has been deleted. If the bucket list is empty, there is no bucket under your current account.

Step 4. Confirm fees

As storage usage is billed daily, your storage usage generated on a day will be billed the next day. Therefore, after you clear the data in your bucket, check the bills for the last three days to make sure that no additional fees have been incurred.

