
## Prerequisites

- The SMS body template has been approved.
- The signature has been approved if you want to add a signature to a SMS message.

## Directions
1. Log in to the [SMS console](https://console.cloud.tencent.com/sms).
2. In the left sidebar, click **Global SMS** -> **Bulk SMS**.
3. Click **Create Bulk SMS Delivery Task**.
4. Configure the following parameters as required:
 - **Template Name**: select an approved body template (different templates are distinguished by template name).
 - **Signature Name**: optional. Select an approved SMS signature (different signatures are distinguished by signature name).
 - **SMS Preview**: view and confirm the content, number of characters, and expected number of SMS messages to be sent.
 - **Delivery Time**: select **Send now** or **Send by schedule**.
 - **Recipient**: click **Download Standard Template**, enter the recipient's mobile number and custom SMS content in the downloaded form, and click **Click here** to upload the form. The maximum size of the form that can be uploaded is 30 MB.
   >!Each Tencent Cloud account has a daily quota of 1,000 global text messages. The mobile numbers of all customers receiving the message sent at the same time must belong to regions outside the Chinese mainland.
   >
4. Click **OK**.
5. Check the SMS content, number of users, and delivery time, and click **Send**. 
 You can view the status of the task in the **Bulk SMS** list. When the status is **Sent**, the message has been sent.

## Subsequent Operations

You can query the SMS delivery result in the following ways:
- On the **Bulk SMS** page, click **Details & Receipt Analytics** in the row of the target task to view its details and receipt analysis.
- On the left sidebar, click **Business Statistics** > **Global SMS**. In the drop-down list next to “Applications,” select the name of the target application to view the data records and analysis of all global SMS messages under the current application.

## Related Documentation
You can also send SMS messages through APIs. For details, see [API Categories](https://intl.cloud.tencent.com/document/product/382/34689#.E7.9F.AD.E4.BF.A1-api).

