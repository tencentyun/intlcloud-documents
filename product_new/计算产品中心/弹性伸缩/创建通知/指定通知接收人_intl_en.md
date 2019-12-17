If you have created a notification and specified the recipients, AS will send the notification to the specified person(s) when a scaling activity occurs.

### Step 1: Specify notification recipients

Go to [Cloud Access Management Console](https://console.cloud.tencent.com/cam) and you will see the contact information of the account registrant.

To send the notification to more people, you can click **New** to create more.

> If you are the only user of your Tencent Cloud account, you can skip this step, because the system has a **Developer** account created by default.

### Step 2: Specify a user group (recipient classification)

AS sends notifications on a **User Group** basis, rather than **Recipient**.

**Scenarios:**

- If you want to send the notification only to yourself, you can create a user group with your contact info only.

- You have defined a number of notification recipients, who may be in the same or different departments. You may want to have a certain type of notifications sent to the recipients of department A, and another type to the recipients of department B. To do so, you can define a user group and add the different notification recipients to the corresponding user groups.

**Setup:**
1. Go to [User Group Management](https://console.cloud.tencent.com/cam/groups), and click **Create User Group**. Enter the user name and click **Confirm**.
2. Click **Add User** to add the relevant notification recipient(s).

### Step 3: Apply the user group

When you define the alarm triggering policy and notification policy of the AS, you can see the user groups you have defined in the list of recipients. You can set specific user groups to be notified as needed.







