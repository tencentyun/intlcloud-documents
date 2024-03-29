拥有 GAAP 权限的主账号或其他账号（AdministratorAccess 权限账号），可通过配置访问管理权限，使协作者账号拥有 GAAP 全读写或只读访问权限。

用户可通过策略关联用户、用户关联策略两种方式为协作者账号进行授权。更多信息，请参见 [访问管理 CAM](https://intl.cloud.tencent.com/document/product/597/17989)。

## 准备步骤
1. 使用拥有 GAAP 权限的主账号或其他账号（AdministratorAccess 权限账号），登录 [腾讯云控制台](https://console.cloud.tencent.com/)。
2. 在顶部导航中，选择**云产品** > **管理与审计** > **[访问管理](https://console.cloud.tencent.com/cam/policy)**，进入访问管理控制台。
>?您也可以在腾讯云控制台右上角，选择**您的账户名称** > **访问管理**，进入访问管理控制台。

## 操作步骤
### 策略关联用户
1. 在左侧菜单中，单击**策略**，进入管理页面。
2. 在搜索栏中，检索“GAAP”，找到2条结果。选择策略权限，单击**关联用户/组**。
![1](https://main.qcloudimg.com/raw/06fc88f33dbc935ca2b65948fb3343e3.png)
3. 勾选需要授权的用户，单击**确定**，即授权成功。
![](https://main.qcloudimg.com/raw/61df6a1fd920c302c0f2b2f68c79f4a2.png)

### 用户关联策略
1. 在左侧菜单中，选择**用户** > **用户列表**，进入管理页面。
2. 在列表中，找到需要授权的用户所在行，单击操作栏中的**授权**。
![](https://main.qcloudimg.com/raw/740bfd484b9df92eb13bb9517c6238e1.png)
3. 在关联列表中，检索“GAAP”，勾选策略权限，单击**确定**，即授权成功。
![](https://main.qcloudimg.com/raw/7a602d2eefa9ed3ba69ca72df39616a7.png)


### 查看和解除权限
授权成功的用户，可在 [用户列表](https://console.cloud.tencent.com/cam) 中，单击用户名称，查看权限、解除权限。
![](https://main.qcloudimg.com/raw/da41405cfc21806881e2c86d9bc2823e.png)
