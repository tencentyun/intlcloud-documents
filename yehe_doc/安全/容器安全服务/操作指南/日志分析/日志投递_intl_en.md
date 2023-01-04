You can ship logs to [CKafka](https://intl.cloud.tencent.com/document/product/597) or [CLS](https://intl.cloud.tencent.com/document/product/614).

## Shipping to CKafka
1. On the [**Log Analysis**](https://console.cloud.tencent.com/tcss/report/logAnalysis) page, click **Log shipping** > **KAFKA** at the top.
2. On the **KAFKA** tab, click **Configure now**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b11621eaa55daace1c85b71624897576.png" style="zoom:50%;" />
3. On the **Shipping to CKafka** page, grant the access, configure the message queue instance, public domain name, username, and password, and click **OK**.
>!
>- **Network access** is set to **Public domain name** by default.
>- You can select **Ship to the current Tencent Cloud account** or [**Ship to another Tencent Cloud account**](#gw) for **Ship to**.

<img src="https://qcloudimg.tencent-cloud.cn/raw/fc1a83b1f4cc78f6925ce4c783ae9664.png" style="zoom:50%;" />

4. After the configuration, check whether shipping is enabled for each log type and the topic ID/name.

## Cross-Account Log Shipping Through the Public Domain Name[](id:gw)
### Step 1. Select the shipping method[](id:stpe1)
1. On the [**Log Analysis**](https://console.cloud.tencent.com/tcss/report/logAnalysis) page, click **Log shipping** > **KAFKA**/**CLS** at the top.
2. On the **KAFKA** tab, select **Ship to another Tencent Cloud account** and enter the UIN of the recipient account.
>!
>- **When configuring the message instance for the recipient account in the [CKafka console](https://console.cloud.tencent.com/ckafka/index?rid=1), you need to select **Public domain name** and create three topics that can receive TCSS audit logs.
>- Back up the ID and public domain name of the message instance, as well as the ID and name of the topics for receiving the three types of logs. Remember the username and password. After cross-account authorization, you need to enter the above information for the shipping account.

<img src="https://qcloudimg.tencent-cloud.cn/raw/dbec9984378afd041736559b7ecb93f3.png" style="zoom:50%;" />

### Step 2. Authorize cross-account log shipping
To ship TCSS logs across accounts, you need to perform authorization for the recipient account and allow the shipping account to verify the CKafka instance of the recipient account and pull the topic ID and name.

#### If a TCSS role already exists
1. Log in to [CAM console](https://console.cloud.tencent.com/cam/role) and click **Role** on the left sidebar.
2. On the **Role** page, enter **TCSS** in the search box. If the following content is found: role name: `TCSS_QCSRole`; role entity: `Product Service - tcss`, a TCSS role has been bound to the account, and you only need to add the CAM and CKafka policy permissions in **Associate Policy**.
>! The UIN of the recipient account should be the same as that entered in [step 1](#stpe1).

![](https://qcloudimg.tencent-cloud.cn/raw/f29ea25323cd77fc013a0fa83e4aa05f.png)
3. Click **TCSS_QCSRole** to enter the **Permission** tab.
4. On the **Permission** tab, search for `QcloudCamSubaccountsAuthorizeRoleFullAccess` and `QcloudAccessForTCSSRoleInCkafka` policies.
 - **If the policies already exist:**
    Go back to the [TCSS console](https://console.cloud.tencent.com/tcss), log in to the shipping account, and check whether the authorization is successful as prompted on the page, and if so, configure the public domain name, message queue, and topic information for log shipping to CKafka.
![](https://qcloudimg.tencent-cloud.cn/raw/af6fb4999ac41cf966e59145e197e0b8.png)
 - **If the policies do not exist:**
    1. Click **Associate Policy** and confirm the information to pop up the **Associate Policy** window.
>! The role is authorized by you and changes to the role content (such as the associated policy and role entity) may lead to the consequence that the service you authorize the role to cannot use the role normally.

<img src="https://qcloudimg.tencent-cloud.cn/raw/aab03db87b7ac08b2f5650d8c71fd78b.png" style="zoom:67%;" />
    2. In the **Associate Policy** pop-up window, search for `QcloudCamSubaccountsAuthorizeRoleFullAccess` and `QcloudAccessForTCSSRoleInCkafka` policies, select the policies, and click **OK**. Then, you can view the policies in the details of the `TCSS_QCSRole` role.
![](https://qcloudimg.tencent-cloud.cn/raw/79df9c3c28b7f511523f6171b831c074.png)
        3. After the configuration, go back to the [TCSS console](https://console.cloud.tencent.com/tcss), log in to the shipping account, and check whether the authorization is successful as prompted on the page, and if so, configure the public domain name, message queue, and topic information for log shipping to CKafka.


#### If no TCSS roles exist
1. On the [**Role**](https://console.cloud.tencent.com/cam/role) page, enter **TCSS** in the search box. If the following content cannot be found: role name: `TCSS_QCSRole`; role entity: `Product Service - tcss`, no TCSS roles have been bound to the account, and you need to create a role in the list.
![](https://qcloudimg.tencent-cloud.cn/raw/a1f737e34bd0a4aee562f7700f024889.png)
2. On the **Role** page, click **Create Role** and select **Tencent Cloud Product Service**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/cdda9b97471f7f3d6a222443fe7ffdcd.png" style="zoom:67%;" />
3. In the **Enter Role Entity Info** step, select **Tencent Container Security Service (tcss)** and click **Next**.
4. In the **Configure Role Policy** step, search for and select `QcloudCamSubaccountsAuthorizeRoleFullAccess` and `QcloudAccessForTCSSRoleInCkafka` and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/9da23a47f14362b43972b5dbf10c3d52.png)
5. In the **Set Role Tag** step, customize the role tag or leave it empty and click **Next**.
6. In the **Review** step, configure **Role Name** as **TCSS_QCSRole** (as TCSS pulls the configured permission based on the role name) and customize **Description** or leave it empty. After the configuration, click **Complete**. Then, you can view the role and associated policy on the **Role** page after authentication.
![](https://qcloudimg.tencent-cloud.cn/raw/4d4e66c773606866399f89d40731f1ae.png)
7. After the configuration, go back to the [TCSS console](https://console.cloud.tencent.com/tcss), log in to the shipping account, and check whether the authorization is successful as prompted on the page, and if so, configure the public domain name, message queue, and topic information for log shipping to CKafka.

## Shipping to CLS
Shipping to CLS requires authorization for access. After the authorization, check whether shipping is enabled for each log type and the logset and log topic information.
1. On the [**Log Analysis**](https://console.cloud.tencent.com/tcss/report/logAnalysis) page, click **Log shipping** > **CLS** at the top.
2. On the **CLS** tab, select the target log type and click **Configure now**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5a3c95f0d449af24dc0046e4b735c75f.png" style="zoom:50%;" />
3. On the shipping settings page, configure parameters and click **OK**.
>? After CLS access is authorized and shipping to CLS is enabled under your account, pay-as-you-go storage space will be automatically created in CLS, along with pay-as-you-go bills. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509).

<img src="https://qcloudimg.tencent-cloud.cn/raw/4ac92654ed78dd3cba0d0d7b22fb3f73.png" style="zoom:67%;" />

