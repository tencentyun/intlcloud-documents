This document helps you quickly get start with Serverless Cloud Function (SCF).

## 1. SCF Overview

Tencent Cloud Serverless Cloud Function (SCF) is a serverless execution environment that enables you to build and run applications without having to purchase and manage servers. Simply code in a supported language and set the execution conditions, and your code can be run on the Tencent Cloud infrastructure elastically and securely.

SCF allows you to develop, deploy, and test functions through the [SCF console](https://console.cloud.tencent.com/scf), [Serverless Cloud Framework](https://intl.cloud.tencent.com/document/product/583/36267), or [TencentCloud API](https://intl.cloud.tencent.com/document/product/583/17234).


## 2. SCF Billing

New SCF users are entitled to a certain monthly free tier within three months of activation. SCF can be billed in a prepaid (subscription package) or postpaid (pay-as-you-go) manner in USD. To learn more about the resource fees incurred during use of SCF, see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).

## 3. Using SCF

#### 3.1 Register on Tencent Cloud

Before using SCF, you need to sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/account/register) and complete the [identity verification](https://www.tencentcloud.com/document/product/378/3629) first.

#### 3.2 Role authorization

You need to authorize the current service role and grant operation permissions for SCF before accessing your other Tencent Cloud service resources.
Log in to the Tencent Cloud console, select **Products** > **Serverless Cloud Function** to enter the [SCF console](https://console.cloud.tencent.com/scf), and follow the prompts to authorize SCF. After completing service authorization to get the relevant resource operation permissions, you can start creating functions.


#### 3.3 Creating function

- SCF provides two function types: Event-triggered function and HTTP-triggered function. For more information, see [Creating and Updating Function](https://intl.cloud.tencent.com/document/product/583/19806) and [Creating and Testing Function](https://intl.cloud.tencent.com/document/product/583/40689).
- SCF provides two function creation methods. You can quickly create a function in the console as instructed in [Creating Event-Triggered Function in Console](https://intl.cloud.tencent.com/document/product/583/32742). You can also create a function through Serverless Cloud Framework as instructed in [Creating Function on CLI](https://intl.cloud.tencent.com/document/product/583/32743).

#### 3.4 Deploying function

After editing the function code online, click **Save**, and the function will be deployed. After the code is deployed in the cloud, SCF can execute the function after a trigger condition is configured. An execution condition of a function is called a trigger. You can configure various types of triggers, such as timer, API Gateway, and COS triggers. For detailed directions on how to configure a trigger, see [Trigger Management](https://www.tencentcloud.com/document/product/583/31440). SCF currently supports two trigger modes: event-triggered and HTTP-triggered. For more information, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).

#### 3.5 Invoking and testing function

You can directly invoke a function and simulate the triggering event sent by the trigger in the SCF console, and the test result will display the function execution conditions, returned content, and execution log. For more information, see [Testing Function](https://intl.cloud.tencent.com/document/product/583/14572).

#### 3.6 Managing function

- View logs: SCF supports displaying historical or real-time function logs in various ways. For more information, see [Log Management](https://www.tencentcloud.com/document/product/583/39776).
- View monitoring data and configure alarms: You can stay on top of the function running status by viewing monitoring metrics. You can also configure alarms for functions to promptly receive alarm messages when your business is abnormal. For more information, see [Managing Monitors and Alarms](https://www.tencentcloud.com/document/product/583/32737).


## 4. Beginner's Guide

#### What are the differences between HTTP-triggered function and event-triggered function?

As a new function type, HTTP-triggered can be directly triggered by HTTP requests, breaking through the limit of JSON event format required by the current event-triggered function type. It has more flexible application scenarios and delivers a development experience much similar to that of native web services.

#### A function can run normally in the local system, but I am prompted that some dependencies cannot be found when I try to run it online. What should I do?

A common reason is that third-party dependencies have not been packaged and uploaded to the online environment. You can [install the dependencies](https://intl.cloud.tencent.com/document/product/583/34879) and run the function again for test.


#### Can I use a local code base?

Yes. You can add your own code repository to the function code and upload it to the platform as a zip package.

#### Can SCF interconnect with other Tencent Cloud services such as CVM or TencentDB?

Yes. When you create or modify a function, select [VPC configuration](https://intl.cloud.tencent.com/document/product/583/19703) and deploy the function in the same VPC as the CVM or TencentDB instance.

#### How can I use a custom domain name?

You can bind your independent domain name to the SCF service, so that the service can be accessed at it. For more information, see [Configuring a Custom Domain Name](https://intl.cloud.tencent.com/document/product/628/11791). Then you can select **Use Existing API Service** to create an API Gateway trigger for a function that requires a custom domain name.



## 5. Feedback and Suggestion	

If you have any questions or suggestions about SCF, you can send your feedback through the following channels, and we will get back to you accordingly:

- For questions about the product documentation, such as links, content, or APIs, click **Send Feedback** on the right of the document page.
- If you encounter any problems while using the product, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.


