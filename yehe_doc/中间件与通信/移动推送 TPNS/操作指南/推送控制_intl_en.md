## Overview

Proper message push can quickly improve user activity, increase conversion rate, and bring other benefits at a very low cost. However, improper message push will adversely affect product reputation, and even sharply increase the application uninstalls.
TPNS provides the following capabilities for you to implement proper push in a secure and efficient manner:
- Frequency capping: limits the pushes to avoid annoying users
- Message deduplication: blocks identical pushes caused by misoperation at the system level
- Specified time range: sets a time range that allows pushes to avoid disturbing users late at night.

## Use Instructions

### Frequency Capping

#### Background

Ecommerce applications often need to push promotion and marketing messages to targeted groups that are selected according to their browsing habits, shopping frequency, and other information. As a result, the same user may receive multiple push notifications in a short period of time, which seriously affects user experience and even causes the user to turn off notifications or uninstall the application.

 #### Directions
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Select **Message Management** > **Push Settings** on the left sidebar.
3. Click **Enable** in the **Frequency Capping** section.

4. Enter an integer within 1-100 or keep the default value 3 in the text box of **Max Pushes to a Device per Day**. Select a [push plan](https://intl.cloud.tencent.com/document/product/1024/37452) to which the setting applies, and click **Save** to complete the configuration.



### Message Deduplication
#### Background
News and video applications usually need to preemptively reach out to users with breaking news or hot issues for users to quickly get the latest and most concerned information. However, receiving repeated pushes in a short period may irritate users. This feature avoids duplicate pushes to users.
#### Directions
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Select **Message Management** > **Push Settings** on the left sidebar.
3. Click **Enable** in the **Message Deduplication** section.


After this feature is enabled, the system will block identical pushes to the same recipients within 1 hour to prevent users from receiving repeated pushes in a short period.

>? This applies only to pushes to all devices, to multiple accounts, by tag combination, or by user group.
>


### Specified Time Range
#### Background
Tools or applications with system notification requirements usually need to notify users when the user or system function status changes. However, pushing notifications late at night will disturb users, thus damaging the reputation of the applications and even causing uninstallation. This feature sets a time range that allows pushes to avoid disturbing users late at night.

#### Directions
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Select **Message Management** > **Push Settings** on the left sidebar.
3. Click **Enable** in the **Specified Time Range** section to set a time range that allows pushes, and click **Save**. The pushes outside the specified time range will not be delivered.
>? The **Specified Time Range** is a period that allows pushes to deliver rather than to reach devices. For example, if the time range is set to 15:00-16:00, only push tasks created within this period will be delivered, and other push tasks will be blocked.
>






