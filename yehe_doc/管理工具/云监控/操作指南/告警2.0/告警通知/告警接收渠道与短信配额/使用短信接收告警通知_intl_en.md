This document describes how to receive alarm notifications through SMS.

## Configuring SMS Alarm Channel

1. Go to the [User List](https://console.cloud.tencent.com/cam) page.
2. Find the user for whom to configure the SMS alarm channel and click the username to enter the user details page.
3. Click the "Edit" icon on the right of "Mobile" as shown below, enter a mobile number, and click **OK**.
   ![](https://main.qcloudimg.com/raw/58b96f08cf334fd22e079549059bf2c3.png)
4. On the right of "Email" on the user details page, click **Send Verification Link**.
5. Then, Cloud Monitor will send a verification message to the entered mobile number, and the link should be clicked to verify the number.
   

## Enabling SMS Alarm Channel

1. Enter the [Notification Template](https://console.cloud.tencent.com/monitor/alarm2/notice) page in the Cloud Monitor Console.
2. Click **Create** to create a notification template.
3. After configuring the basic information on the notification template creation page, select "SMS" as the alarm receiving channel.
4. Enter the [Alarm Policy List](https://console.cloud.tencent.com/monitor/alarm2/policy), click the name of the policy that needs to bind alarm callbacks to enter the alarm policy management page, and bind the notification template.
   ![](https://main.qcloudimg.com/raw/6dec96e3f487ddb9ff9b81a100f17989.png)
   ![](https://main.qcloudimg.com/raw/de02c89a889239b00ae32b22e4978c46.png)

