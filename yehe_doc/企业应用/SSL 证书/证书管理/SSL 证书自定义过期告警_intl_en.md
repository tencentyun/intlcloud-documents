## Overview

This document describes how to configure alarms for the `e79vbLDZ` SSL certificate instance to have alarms sent to specified recipients via SMS and email when it will expire within 30 calendar days.

> **Notes**
> 
> You can set the number of days, interval, and recipients to receive alarm messages for the expiration of the SSL certificate.
> 


## Prerequisites
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/).

2. On the left sidebar, click **Alarm Configuration** > **Alarm Policy**.

3. Click **Add** to enter the **Create Policy** page and configure relevant information.


## Directions

### Step 1. Configure the basic information

In the **Basic Info** module, enter the relevant information.
- **Policy Name**: Enter a custom policy name.

- **Remarks**: Enter the remarks.

- **Monitoring Type**: It is **Cloud Product Monitoring** by default.

- **Policy Type**: Select **SSL Certificate/Expiration Time**.

- **Project**: You can select **Default Project** or another as needed.


### Step 2. Configure the alarm policy
1. In the **Alarm Policy** module, configure the **Alarm Object**, select **Instance ID**, and select the target SSL certificate instance.

2. Set **Trigger Condition** to **Configure manually** and configure the following conditions.

  - **Condition**: Select **any**.

  - **Threshold**: Select **Static**.

  - **"Metric alarm" condition**: Set the condition to receive only one alarm message if the expiration time is within 30 days under the statistical period of 1 minute.
    

      > **Notes**
      > 
      > You can set the alarm trigger condition as needed.
      > 


### Step 3. Configure alarm notifications

In the **Configuring Alarm Notification** module, preferably set **Notification Template** to **Select template** and add [Recipient]/[Recipient Group] of the alarm. The figure takes the preset notification template as an example:

> **Notes**
> 
> If no templates are created, click **Create template** to create one. Then, you can specify the recipient to receive the expiration alarm.
> 



### Step 4. Configure advanced settings
1. In the **Advanced Settings** module, set whether to trigger the auto scaling policy after the alarm conditions are met.

2. Click **Complete**.

3. After the configuration, if the `e79vbLDZ` SSL certificate instance will expire within 30 calendar days, the specified recipient will be notified via SMS and email.
   

   > **Notes**
   > 
   >  For more information, see [Cloud Monitor](https://www.tencentcloud.com/document/product/248) documentation.
   > 
