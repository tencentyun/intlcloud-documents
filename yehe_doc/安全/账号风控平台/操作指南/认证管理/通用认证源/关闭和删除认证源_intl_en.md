## Scenarios
This topic describes how to disable and delete an authentication source in the Customer Identity and Access Management (CIAM) console.

>!
>- Disabling an authentication source will affect the use of the authentication source by applications. Please proceed with caution.
>- All the data of a deleted authentication source cannot be recovered. Please proceed with caution.

## Disabling an authentication source
1. Log in to the [CIAM console](https://console.cloud.tencent.com/ciam) and select **Authentication management** -> **General authentication source** in the left navigation pane.
2. On the **General authentication source** page, select the authentication source to disable and click ![](https://main.qcloudimg.com/raw/6d46521bb97025243466844d6dec632b.png).
![img](https://qcloudimg.tencent-cloud.cn/raw/ffe45a40738e5309b23c026677f94a27.png)
3. In the confirmation window displayed, click **OK** to disable the authentication source.
>?
>- If the authentication source is configured as the preferred authentication source in the login process of an application, the system will prompt that this source cannot be disabled. If you still need to disable it, unbind this source in the login process first.
>- If the authentication source is configured as the associated authentication source in the login process of an application, after this source is disabled, the system will prompt that the use of this source by the application will be affected.

![img](https://qcloudimg.tencent-cloud.cn/raw/976e42a554dfeaa8c45cc3d0d4068b1a.png)

## Deleting an authentication source
1. Log in to the [CIAM console](https://console.cloud.tencent.com/ciam) and select **Authentication management** -> **General authentication source** in the left navigation pane.
2. On the **General authentication source** page, select the authentication source to delete and click **Delete**.
>?
If the authentication source is configured as the preferred authentication source in the login process of an application, the system will prompt that this source cannot be deleted. If you still need to delete it, unbind it in the login process first.

![img](https://qcloudimg.tencent-cloud.cn/raw/f4c962732bbfaee162023c0d37d27036.png)

3. In the confirmation window displayed, click **OK** to delete the authentication source.
![img](https://qcloudimg.tencent-cloud.cn/raw/dc9e54ffdd5b6ea7e81da20acee21fdf.png)