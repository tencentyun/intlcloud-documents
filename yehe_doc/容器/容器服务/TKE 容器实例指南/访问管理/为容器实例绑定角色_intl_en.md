## Overview

EKSCI supports binding a role to the instance to authorize corresponding permissions to the instance. It is applicable to be used in the scenarios where you need to access other Tencent Cloud services through containers, such as uploading logs to CLS and modifying CLS topic permissions. This document describes how to bind a role to a container instance to authorize permissions.

In the following, we take uploading logs to CLS as an example. The steps are as follows:


## Directions

You need to bind a role when creating the container instance. The steps are as follows:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/eksci).
2. On the list page of container instances, select the region where the instance is located.
3. Click **Create Instance** at the top of the instance list.
4. Configure the parameters of the container instance based on actual needs. Click **Next**.
5. Select the role you have created in advance to complete the binding process.
    It there is no appropriate role, click **Create CAM Role**. For directions, see the following:

#### Creating a policy

You need to create a policy before creating a role. This policy determines what permissions your role has.
1. Log in to the CAM console and select **[Policies](https://console.cloud.tencent.com/cam/policy)** in the left sidebar.
2. On the **Polices** page, click **Create Custom Policy**.
3. Select **Create by Policy Generator** in **Select Policy Creation Method** pop-up.
4. Select the permissions that need to be authorized to the instance. For example, select write operation of "cls:pushLog". Click **Next**.
5. Confirm the policy name and click **Done**.

#### Creating a role

You need to bind the policy to a role after creating the policy, so as to make the role have the permissions corresponding to the policy. You can bind multiple policies to one role based on your needs and unbind them at any time.

1. Log in to the CAM console, and select **[Roles]**(https://console.cloud.tencent.com/cam/role) in the left sidebar.
2. On the **Roles** page, click **Create Role**.
3. In the **Select role entity** window that appears, select **Tencent Cloud Product Service** to go to the **Create Custom Role** page.
4. On the **Enter role entity info** tab, select **Cloud Virtual Machine (cvm)** and click **Next**.
5. On the **Configure role policy** tab, select the name of the policy created in the previous step and click **Next**.
6. On the **Review** tab, enter the role name to review the role information, and then click **Done**. For more information, see [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381).
<dx-alert infotype="notice" title="">
You must select **Cloud Virtual Machine (cvm)** as the role entity. Authorization cannot be completed if you select any other entity.
</dx-alert>
7. After creating an appropriate role, select it in step 4.
8. Click **Next** to confirm the configuration and complete instance creation. You can verify if the role has been bound properly by performing the actions corresponding to the permissions.
