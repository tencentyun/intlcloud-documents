The organization creator can add a member to an organization through invitation or creation.

## Directions[](id:addMembers)
Choose a method of adding a member as needed:
<dx-tabs>
::: Inviting a member[](id:inviteMembers)

1. Log in to the TCO console and click **[Member account management](https://console.cloud.tencent.com/organization/member)** on the left sidebar.
2. On the **Member list** page, click **Add member**.
3. On the **Add member** page, select **Invite member**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NTDk417_1_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.jpg)
4. Set the account ID, member name, finance permission, payment mode, department, and whether to allow the member to actively quit the organization. You can obtain the account ID on the [Account information](https://console.cloud.tencent.com/developer) page.
5. Click **OK**, and the information of the invited member will be verified. The account you invite must have completed enterprise identity verification and cannot have joined any other organization before. The verified entity of the invited account needs to be either the same as or associated with that of the admin account. If the association is not completed, contact your sales rep.
6. After the member is successfully invited, the invitation information will be retained for 15 days. You can check the invitation records by selecting **[Organization change record](https://console.cloud.tencent.com/organization/invitations)** on the left sidebar and selecting the **Member invitation record** tab. ![](https://staticintl.cloudcachetci.com/yehe/backend-news/aTy8515_3_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.jpg)
   :::

::: Creating a member[](id:newMember)
The organization creator can create members under the current entity (which is the admin account's entity) or other entities.

**Creating a member under the current entity**

1. Log in to the TCO console and click **[Member account management](https://console.cloud.tencent.com/organization/member)** on the left sidebar.
2. On the **Member list** page, click **Add member**.
    ![](https://staticintl.cloudcachetci.com/yehe/backend-news/ItNX867_1_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.jpg)
3. Set the name, entity, finance permission, payment mode, and department.
 - For the entity, select **Current entity**.
 - You can create a department as instructed in [Creating Department](https://www.tencentcloud.com/document/product/1031/51858).
4. Click **OK**, and the member account will be created automatically and inherit the identity information of the creator.
You can select **[Organization change record](https://console.cloud.tencent.com/organization/invitations)** on the left sidebar and click **Member change record** > **Member creation record** to view the creation record and result.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9pYd010_2_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.jpg)

**Creating a member under other entities**

1. Contact your sales rep to apply to associate with other entities.
2. After the entity is successfully associated, log in to the [TCO console](https://console.tencentcloud.com/organization) and select **Verified entity management** on the left sidebar. In the entity list, click **Invite member** in the **Operation** column to invite the member under the target entity to join the organization. For details, see the **Inviting a member** tab in [this document](https://www.tencentcloud.com/document/product/1031/51865). ![](https://staticintl.cloudcachetci.com/yehe/backend-news/FSiR364_3_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.jpg)
3. Return to the [Verified entity management]](https://console.cloud.tencent.com/organization/group-subject) page and click **Edit entity admin account** to set the entity admin. ![](https://staticintl.cloudcachetci.com/yehe/backend-news/R7Kr120_4_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.jpg)
4. Under the **Entity list** tab on the **Verified entity management** page, click **Create member** to enter the **Add member** page and select **Create member** as the adding method.
5. Complete all the other required information, select **Other entities** as the entity, and select an entity in the drop-down list. ![](https://staticintl.cloudcachetci.com/yehe/backend-news/fyDd242_5_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.jpg)
6. The entity admin account will review the member creation application, and the member can be successfully created after the application is approved. The created member account will inherit the enterprise identity information of the entity admin account. You can select [Organization change record](https://console.cloud.tencent.com/organization/invitations) on the left sidebar and click **Member change record** > **Member creation record** to view the creation record and result. ![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ufnm109_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_a88f4eb3-03ec-425f-a98e-b092af36560a.png)

:::
</dx-tabs>