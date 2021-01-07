云数据库 MongoDB 支持免认证访问功能，您可以通过控制台直接开启、关闭免认证访问。
>?MongoDB 目前仅 3.6、4.0 版本支持免认证访问。


## 操作步骤
<span id = "sjnhbb"></span>
### （可选）升级内核版本
>?免认证访问功能上线之前已创建的实例使用该功能时，需要先升级内核版本。

1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，在实例列表，选择对应地域，单击实例名，进入实例详情页。
2. 在实例详情页的“免认证访问”处，单击【升级】。
![](https://main.qcloudimg.com/raw/86de5591810d175b3f894802850d334a.png)
3. 在弹出的对话框，单击【确定】。
>!升级免认证版本涉及内核升级，有秒级的连接闪断。
>
![](https://main.qcloudimg.com/raw/9abf4438b26a9f573034ae6e772bad2d.png)
4. 返回实例详情页，实例状态变为“升级数据库版本中”，待实例状态变为“运行中”，即可进行后续操作。
![](https://main.qcloudimg.com/raw/2561653b1b5c4564632df3fc4c171b29.png)

### 开启免认证访问
1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，在实例列表，选择对应地域，单击实例名，进入实例详情页。
2. 在实例详情页的“免认证访问”处，单击【开启】。
![](https://main.qcloudimg.com/raw/4ffd1f99bf0240bf2f9553168dff8cc6.png)
3. 在弹出的对话框，单击【确定】。
![](https://main.qcloudimg.com/raw/bf12dc0f3b27ae0b7bdb532a7d8c77ed.png)
4. 返回实例详情页，待实例状态变为“运行中”，即可正常使用。

### 关闭免认证访问
1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，在实例列表，选择对应地域，单击实例名，进入实例详情页。
2. 在实例详情页的“免认证访问”处，单击【关闭】。

## 相关操作
您可通过 MongoDB shell 或者各语言驱动访问 MongoDB 数据库，请参见 [连接 MongoDB 实例](https://intl.cloud.tencent.com/document/product/240/7092)。

