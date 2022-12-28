## 操作场景
集团管理账号可以通过创建集团管理策略，授权子用户登录管理成员账号的权限。本文介绍如何通过为集团管理账号的子用户授予集团管理策略，使其可以登录集团组织创建的成员账号。

## 前提条件
已参考 [新建成员](https://www.tencentcloud.com/document/product/1031/51865) 成功创建组织成员。

## 操作步骤

### 添加授权
1. 登录集团账号管理控制台，选择左侧导航栏中的 **[成员账号管理](https://console.cloud.tencent.com/organization/member)** 。
2. 在“成员账号管理”页面，单击成员所在行右侧的**登录账号**。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/DFiY033_%E6%8E%88%E6%9D%83%E8%AE%BF%E9%97%AE%E6%88%90%E5%91%98%E8%B4%A6%E5%8F%B7-%E6%B7%BB%E5%8A%A0%E6%8E%88%E6%9D%83.png)
3. 在弹出的“登录账号”窗口中，单击**新建授权策略**。
<dx-alert infotype="explain" title="">
本步骤中新建的策略即为集团管理策略。
</dx-alert>
4. 在“新建授权策略”窗口中，参考以下信息进行配置。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cz24304_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226180956.png)
   - **授权策略名称**：自定义授权策略名称。
   - **访问权限**：授予具体权限。
   - **关联子账号**：勾选所需子账号，即表示为子账号授予成员管理权限。
5. 单击**确定**即可完成授权。


### 使用子账号登录成员控制台[](id:membersLogConsole)
完成授权后，您可参考以下步骤，使用子账号登录成员控制台并进行管理操作。
1. 使用授权子账号登录集团账号管理控制台，选择左侧导航栏中的 **[成员账号管理](https://console.cloud.tencent.com/organization/member)** 。
2. 在“成员账号管理”页面中，单击需管理的成员账号所在行右侧的**登录账号**。
即可在弹出的“登录账号”窗口中进行相关管理操作。
