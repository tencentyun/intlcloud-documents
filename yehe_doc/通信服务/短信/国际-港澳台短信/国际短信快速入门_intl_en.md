This document helps you understand how to quickly use the global SMS. We assume that an application named TEST is created by a verified enterprise user, and the application is used to send the following message to mobile phone users outside the Chinese mainland: `[Tencent Cloud]Your verification code is 1234(valid for 5 minutes). For account safety, don't forward the code to others.` For more terms about SMS, see [Glossary](https://intl.cloud.tencent.com/document/product/382/13299).

>!The SMS console has been upgraded. Users who apply for the SMS after September 18, 2019 will be redirected to the [new console](https://console.cloud.tencent.com/smsv2) by default. New features will be launched on the new console subsequently. The legacy console support ended on **March 31, 2020**.
>To ensure that you can use the console properly, we advise you to upgrade your console to the latest version before September 18, 2019.

## Step 1: Activate SMS
### Sign up for a Tencent Cloud account
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985), and complete the [organization identity verification](https://intl.cloud.tencent.com/document/product/378/10496).
- If you already have a Tencent Cloud account with identity verification completed, skip signup.

### Apply for SMS activation
>!When you log in to the SMS console for the first time, you need to apply for SMS activation.

Log in to the [SMS console](https://console.cloud.tencent.com/sms), select **I have read and agree to Tencent Cloud SMS Terms of Service**, and click **Access**.


## Step 2: Add an Application
1. On the [Application List](https://console.cloud.tencent.com/sms/smslist) page, click **Create Application**.
2. In **Application Name**, enter `TEST`. In **Application Intro**, enter `global SMS for test`, and click **Create**.


## Step 3: Configure SMS Content
 A complete SMS message consists of a SMS signature and SMS body. You can set different templates to suit your business needs, and then form a final SMS message in the format of `SMS signature + body`. After the SMS signature and template are submitted, we will complete the review in about 2 hours. If necessary, you can set a mobile number and email address to receive the review result.
Global SMS messages can be sent without signatures. The `Tencent Cloud` signature is used as an example in this document.

<span id="Sign"></span>
### Create a signature
1. On the [Application List](https://console.cloud.tencent.com/sms/smslist) page, click the target application **TEST** to go to the application details page.
2. On the left sidebar, click **Global SMS** -> **Signatures**, and click **Create Signature**.
3. Set the following parameters:
 - **Signature Type**: select **Company**.
 - **Signature Purpose**: select **For self-use (the signature is an organization name, website, product name, or something else verified under the current account)**.
 - **Signature Content**: enter `Tencent Cloud`.
 - **Certificate Type**: select **Three-in-one**.
 - **Certificate Upload**: upload a certificate image or a scanned copy.
4. Click **OK**. 
 Wait for the approval of the signature. The SMS signature will be available only after its status changes to **Approved**.

<span id="Template"></span>
### Create a body template
1. On the [Application List](https://console.cloud.tencent.com/sms/smslist) page, click the target application **TEST** to go to the application details page.
2. On the left sidebar, click **Global SMS** -> **Body Templates**, and click **Create Body Template**.
3. Set the following parameters:
 - **Template Name**: enter `verification code`.
 - **SMS Type**: select **Regular SMS**.
 - **SMS Content**: enter `Your verification code is {1}(valid for {2} minutes). For account safety, don't forward the code to others.`
4. Click **OK**. 
 Wait for the approval of the body template. The body template will be available only after its status changes to **Approved**.


## Step 4: Send an SMS Message
Before sending an SMS message, ensure that the signature and body template of the SMS message have been approved.
You can send SMS messages either through the console or through [APIs](https://intl.cloud.tencent.com/document/product/382/34689). The following describes how to send SMS messages through the console.

1. On the [Application List](https://console.cloud.tencent.com/sms/smslist) page, click the target application **TEST** to go to the application details page.
2. On the left sidebar, click **Global SMS** -> **Bulk SMS**, and click **Create Bulk SMS Delivery Task**.
3. Configure the following parameters as required:
 - **Template Name**: select the **verification code** template that you created in the [Create a body template](#Template) step.
 - **Signature Name**: select the **Tencent Cloud** signature that you added in the [Create a signature](#Sign) step.
 - **SMS Preview**: view and confirm the content, number of characters, and expected number of SMS messages to be sent.
 - **Delivery Time**: click **Send now**.
 - **Recipient**: click **Download Standard Template**, enter the recipient's mobile number and custom SMS content in the downloaded form, and click **Click here** to upload the form. The maximum size of the form that can be uploaded is 30 MB.
   >!The mobile numbers of all customers receiving the message sent at the same time must belong to regions outside the Chinese mainland.
   
4. Click **OK**.
5. Check the SMS content, number of users, and delivery time, and click **Send**. 
 You can view the status of the task in the **Bulk SMS** list. When the status is **Sent**, the message has been sent.

## Step 5: View the Delivery Results of SMS Messages
You can view the delivery results of SMS messages in either of the following ways:
- On the **Bulk SMS** page, click **Details & Receipt Analytics** in the row of the target task to view its details and receipt analysis.
- On the left sidebar, click **Business Statistics** > **Global SMS**. In the drop-down list next to “Applications,” select “TEST” to view the data records and analysis of all global SMS messages under the TEST application.

