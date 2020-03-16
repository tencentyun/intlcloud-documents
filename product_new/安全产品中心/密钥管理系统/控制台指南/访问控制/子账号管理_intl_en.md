

## Overview
This document describes how to create a sub-account and grant it permission to manage KMS.





## Directions
#### Step 1. Create a sub-account 
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) with your root account.
2. On the **User List** page, click **Create User** to create a sub-account.

#### Step 2. Create an API key 
1. Click the sub-account name to enter the details page.
2. Select **API Key** > **Create Key** to create `SecretId` and `SecretKey`. The API key is used to access KMS.
![](https://main.qcloudimg.com/raw/b86373cfc243c4a60c337ec767cbcb73.png)

#### Step 3. Authorize the sub-account
The newly created sub-account can be granted with the access to KMS by associating a KMS policy.
1. Go to **Permissions** > **Associate Policies** > **Select Policies from the Policy List to Associate** and select the appropriate KMS policy.
<img src="https://main.qcloudimg.com/raw/b95ea21c77d4f45752e73443a8fc2739.png" width="80%">
2. Click **Next** > **OK** to grant KMS permission to the sub-account.
