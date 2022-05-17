## Overview
EMR provides a software WebUI entry to access the WebUIs of components. It is required to authenticate access requests. The username is "root", and the default password is the one you entered when creating the cluster. You can reset the WebUI password in the EMR console if you forgot it. This document describes how to do so.
## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. Click **Cluster Service** on the cluster details page and click **Reset WebUI Password** in the top-left corner to reset the password.
>!
>- The password must contain 8 to 16 characters with at least three of the following character types: uppercase letters, lowercase letters, digits, and special symbols (! @ # % ^ *). The first character cannot be a special symbol.
>- If OpenLDAP is installed in the cluster (EMR v2.6.0 and EMR v3.2.1 or later), you can change the password only on the **User Management** page. To reset the WebUI password, go to **User Management** and create a user.

![](https://main.qcloudimg.com/raw/6e997c19d214702284e9ac4ad347a44e.png)
