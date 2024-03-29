腾讯云账号（主账号）和子账号进行权限分割，按需为子账号赋予不同的权限，可以避免因暴露腾讯云账号密钥而造成的安全风险。 

## 给子账号授权权限策略
### 背景信息
企业 A 开通了腾讯云数据库 MongoDB 服务，需要自己的团队成员操作云数据库 MongoDB 服务所涉及的云上资源。出于安全或信任的考虑，企业 A 不希望将云账号密钥直接透露给团队成员，而希望能给团队成员创建相应的子账号。而子账号只能在主账号授权的前提下操作云上资源，且不需要对子账号进行独立的计量计费，所有开销都计入企业腾讯云账号下，随时也可以撤销或者删除子账号的操作权限。

###  操作步骤
#### 步骤1：创建子账号用户
您可以通过控制台或者 API 接口进行创建。
- 登录腾讯云访问管理（CAM）控制台，进入 [用户列表](https://console.cloud.tencent.com/cam) 页面创建。具体操作，请参见 [新建子用户](https://intl.cloud.tencent.com/document/product/598/13674)。
- 通过访问密钥调用 AddUser 接口添加子用户并设定权限。具体信息，请参见 [添加子用户](https://intl.cloud.tencent.com/document/product/598/32265)。

#### （可选）步骤2：创建自定义权限策略
1. 在访问管理（CAM）控制台的 [策略](https://console.cloud.tencent.com/cam/policy) 页面，在右上角搜索框根据策略名称搜索策略。
2. 如果策略不存在，您需要自定义权限策略。具体操作，请参见 [创建自定义策略](https://intl.cloud.tencent.com/document/product/598/35596)。

#### 步骤3：给子账号用户授予权限策略
- 在访问管理（CAM）控制台的 [策略](https://console.cloud.tencent.com/cam/policy) 页面，找到需关联的权限策略与子账户用户进行关联。具体操作，请参见 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。
- 在访问管理（CAM）控制台的 [用户列表](https://console.cloud.tencent.com/cam) 页面，找到需授权的子账户用户，给用户关联策略。具体操作，请参见 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。

### 更多参考
#### 登录控制台
您可以请团队成员使用子账号登录腾讯云控制台，访问云数据库 MongoDB。具体操作，请参见 [子账号登录控制台](https://intl.cloud.tencent.com/document/product/598/38248)。

#### 修改子账号用户信息
如果您需要查看并修改子账号的用户信息，请参见 [用户信息](https://intl.cloud.tencent.com/document/product/598/34005)。

#### 删除子账号
如果您想撤销或者删除子账号的操作权限，请参见 [删除子用户](https://intl.cloud.tencent.com/document/product/598/32653)。

## 跨云账号授权权限策略
### 背景信息
企业 A 开通了云数据库 MongoDB 的服务，希望企业 B 拥有其云数据库 MongoDB 的部分业务权限，例如，云监控、实例的读写权限、慢查询操作等。而企业 B 希望有一个子账号负责这部分业务。企业 A 可以授权企业 B 的主账号通过角色访问云数据库 MongoDB 的资源。角色的具体概念以及应用场景，请参见 [角色概述](https://intl.cloud.tencent.com/document/product/598/19420)。

### 操作步骤
#### 步骤1：企业A为企业B创建角色
1. 登录腾讯云访问管理（CAM）控制台，进入 [角色](https://console.cloud.tencent.com/cam/role) 页面。
2. 单击**新建角色**，在**选择角色载体**对话框中，选择**腾讯云账户**。
3. 在**新建自定义角色**配置向导页面，创建角色。
   a. 在**输入角色载体信息**页面，选择**云账号类型**为**其他主账号**，在**账号ID**输入企业B的主账号，其他参数可根据提示设置，单击**下一步**。
   b. 在**配置角色策略**页面，选择需要授权该角色的策略，单击**下一步**。
   c. 在**审阅**页面的**角色名称**输入框，设置角色名称，例如 DevOpsRole。并审阅所选择的策略，单击**完成**。

#### 步骤2：企业B为子账号赋予扮演角色的权限
1. 在访问管理（CAM）控制台的 [策略](https://console.cloud.tencent.com/cam/policy) 页面，单击**新建自定义策略**。
2. 在**选择创建策略方式**对话框，选择**按策略语法创建**。
3. 在**按策略语法创建**的配置向导中，创建策略。
   a. 在**选择模板类型**区域，选择**空白模板**，单击**下一步**。
   b. 在**编辑策略**页面，在**策略名称**输入框设置策略的名称。例如 sts:AssumeRole。
   c. 在**策略内容**中，根据策略语法设置策略内容，单击**完成**。示例如下：
```
{
    "version": "2.0",
    "statement": [
    {
        "effect": "allow",
        "action": ["name/sts:AssumeRole"],
        "resource": ["qcs::cam::uin/12345:RoleName/DevOpsRole"]
    }
    ]
}
```
4. 返回 [**策略**](https://console.cloud.tencent.com/cam/policy) 页面，找到创建的自定义策略，单击**操作**列的**关联用户/组**。
5. 给自定义策略关联企业B的子账户，单击**确定**。

#### 步骤3：企业B使用子账号通过角色访问云资源
1. 通过公司 B 的子账号登录控制台，在控制台头像下拉菜单中，选择**切换角色**。
2. 在切换角色页面，输入公司 A 的主账号，以及角色名称。即可切换为公司 A 的角色身份。 

### 更多参考
- 如果您需要对角色进行修改，请参见 [修改角色](https://intl.cloud.tencent.com/document/product/598/19389)。
- 如果您需要删除角色，请参见 [删除角色](https://intl.cloud.tencent.com/document/product/598/19388)。
- 更多访问管理（CAM）的使用操作，请参见 [用户指南](https://intl.cloud.tencent.com/document/product/598/17848)。

