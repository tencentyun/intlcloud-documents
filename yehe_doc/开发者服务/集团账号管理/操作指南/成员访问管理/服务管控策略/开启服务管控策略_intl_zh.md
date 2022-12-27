管控策略功能默认关闭，您需要开启后才能使用。

## 背景信息

开启管控策略功能后，集团账号的变化如下：

集团账号内的部门和成员会默认绑定系统策略  FullQcloudAccess  ，该策略允许对您在腾讯云上的所有资源进行任何操作。

当创建部门或成员时，系统会自动为其绑定系统策略  FullQcloudAccess  。

当邀请的腾讯云账号加入集团账号后，系统会自动为其绑定系统策略  FullQcloudAccess  。

当移除成员时，该成员绑定的所有管控策略将会自动解绑。

## 操作步骤

1、登录[集团账号控制台](https://console.intl.cloud.tencent.com/organization)。

2、在左侧导航栏，选择 **集团账号**> **服务管控策略** 。

3、单击开启 **服务管控策略**。

## 后续步骤

您可以创建自定义管控策略（例如：禁止对某资源的某个操作），然后绑定到集团账号的部门或成员，限制成员对资源的操作权限。操作方法请参见：

- [创建自定义管控策略](https://www.tencentcloud.com/document/product/1031/51871)
- [绑定自定义管控策略](https://www.tencentcloud.com/document/product/1031/51875)