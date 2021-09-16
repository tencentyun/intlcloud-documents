## 操作场景
若您需使用账号 A 绑定账号 B 的 VPC 资源，您需要先对账号 A 进行角色授权。本文将指导您如何跨账号关联 VPC。

## 前提条件
在账号 A 中已创建私有域，如未创建，请参考 [创建私有域](https://intl.cloud.tencent.com/document/product/1097/40558)。

## 操作指南
### 步骤1：B 账号给 A 账号进行角色授权
1. 使用 B 账号登录腾讯云 [访问管理控制台](https://console.cloud.tencent.com/cam/role)，进行 “角色” 管理页面，并单击**新建角色**。如下图所示：
![](https://main.qcloudimg.com/raw/5f92e4c1644678db177390e2ea5c9cb9.png)
2. 在弹出的 “选择角色载体 ”窗口中，单击**腾讯云账户**。如下图所示：
![](https://main.qcloudimg.com/raw/ae6bcf82f5d325cacb93536c46a793bf.png)
3. 在 “新建自定义角色” 页面，填写相关信息并单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/ae5ef1635cb621be9e99210bcbee0f10.png)
 - **云账号类型**：勾选**其他主账号**。
 - **账号 ID**：请输入 A 账号的账号 ID。
 - **外部 ID**：默认不勾选。
 - **控制台访问**：默认不勾选。
4. 进入 “配置角色策略” 步骤，查找并勾选 `QcloudVPCReadOnlyAccess` 策略，单击**下一步**。如下图所示：
![](https://main.qcloudimg.com/raw/3537e3e273ddd959b3ff1e4449686363.png)
5. 进入 “审阅” 步骤，填写相关信息。如下图所示：
![](https://main.qcloudimg.com/raw/8cef5af71822760442df867449b12517.png)
 - **角色名称**：请输入 `PRIVATEDNS_ACCOUNT_被授权 UIN`。例如 `PRIVATEDNS_ACCOUNT_88888888`。
 - **角色描述**：请输入相关描述。
6. 单击**完成**，即可完成角色授权操作。

### 步骤2：A 账号添加 B 账号为关联账号
1. 使用 A 账号登录 [私有域解析 Private DNS 控制台](https://console.cloud.tencent.com/privatedns/domains)，进入 “私有域列表” 管理页面。
2. 在 “私有域列表” 管理页面，选择需要授权的私有域，单击**关联 VPC**。如下图所示：
![](https://main.qcloudimg.com/raw/7f87e7e49767e1c7e350c076e6c94dc2.png)
3. 在弹出的 “修改关联 VPC” 窗口中，单击**添加账号**。如下图所示：
![](https://main.qcloudimg.com/raw/ac9d6db1f41e9b7ee93143174f716bb7.png)
4. 在弹出的 “添加账号” 窗口中，输入 B 账号的账号 ID 并单击**确定**。如下图所示：


![](https://main.qcloudimg.com/raw/da1d5245a519e5d400e06e3bdad0a0ec.png)

5. 关联成功后，即可对本账号 VPC 或关联账号的 VPC 进行关联或修改等操作。




