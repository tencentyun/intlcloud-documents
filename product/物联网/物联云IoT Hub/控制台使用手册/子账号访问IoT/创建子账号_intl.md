[//]: # (chinagitpath:XXXXX)

1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) using the **primary account**. Find "Cloud Products" and click "Access Management" to access the Access Management Console.
![](https://mc.qcloudimg.com/static/img/4bdb983c6c29a873c706acdfe9b90e6b/camconsole_enter.png)

2. Click "User Management" , then "Create User" to access the user type selection page. Select "Collaborator" or "Sub-user". Here we use "Collaborator" as an example.
![](https://mc.qcloudimg.com/static/img/e85c28dff8a475c66362cc41ee6088c4/cam_role_create1.png)

3. Fill out "Username", "Login account", "Mobile number" and "Email" required on the collaborator creation page and click **Next**.
![](https://mc.qcloudimg.com/static/img/b45d7fa3dbd3adafc788551bae31ede5/cam_createrole2.png)

4. Select a user group for the new collaborator. If there is no existing user group, click **Create User Group**.
![](https://mc.qcloudimg.com/static/img/ed3348b2687df524bec2d88b58b5b85e/cam_createrole3.png)

5. Select "Authorize from policy list", search for "iot" in the list, select the iot-related policies as shown in the figure and click **Done**.
![](https://mc.qcloudimg.com/static/img/f29f424c7a15b7085eacbf3a4fadd2d4/cam_createrole4.png)

6. Once the collaborator is created, its information can be viewed on the user list. Click the collaborator username to enter the user information management interface and create an API key for the collaborator. This key is used by the collaborator to access the primary account's IoT resource through the RestAPI.
![](https://mc.qcloudimg.com/static/img/429d52f5bd60f8ac3f75bae4823376db/cam_createrole5.png)

