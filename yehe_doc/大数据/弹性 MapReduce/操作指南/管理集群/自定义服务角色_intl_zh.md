自定义服务角色是指用户可以添加一个 CAM 服务角色用于访问云上对象存储（COS）资源权限，选择的服务类型为“腾讯云产品服务”，支持角色选择“弹性 MapReduce”。若未配置自定义服务角色系统默认使用 EMRCosRole 角色，用于访问对象存储（COS）资源。

## 步骤1：自定义权限策略
登录 [访问管理控制台](https://console.cloud.tencent.com/cam/policy)，单击**新建自定义策略**，在弹出的“选择创建策略方式”页面中选择**按策略语法创建**。
![](https://main.qcloudimg.com/raw/32521aa3647055cf2118e225a5edf56c.png)![](https://main.qcloudimg.com/raw/52d362b87d23e9c66acb18a1dfe53898.png)
在“按策略语法创建”页面，选择**选择模板类型**为**空白模板**。
![](https://main.qcloudimg.com/raw/8db8e6ca59519ea7aeea451974d494b5.png)
设置语法策略如下：
```
{
		"version": "2.0",
		"statement": [
			{
					"action": "cos:*",
					"effect": "allow",
					"resource": "qcs::cos::uid/$appId:$bucketName/*"
			}
		]
}
```
其中 appId 为主账号 AppID，bucketName 为想要授权的 bucket 名称。生成一个名为 TestPolicy 的策略，客户可自定义该名称。

## 步骤2：创建自定义角色
在 [访问管理控制台](https://console.cloud.tencent.com/cam/role)，单击**新建角色**，在弹出的“选择角色载体”页面中选择**腾讯云产品服务**，进入“新建自定义角色”页面，选择**支持角色的服务**为“弹性 MapReduce (emr)”。
 ![](https://main.qcloudimg.com/raw/912520936e5ab438a0a29465df509c9a.png)
绑定步骤1中生成的策略，此处为 TestPolicy，客户可根据想要授权的策略自定绑定。
![](https://main.qcloudimg.com/raw/e86f82c78c25462946822b3595e8fef9.png)
生成名为 EMRCosRole 的自定义角色，客户可自定义该名称。
![](https://main.qcloudimg.com/raw/14ed1ae36b382cb48b3f54a1bea9d8fa.png)

## 步骤3：绑定角色到 EMR 集群
在 [EMR 控制台](https://console.cloud.tencent.com/emr) 中选中对应的集群，进入实例详情，在**基本信息**>**实例信息**>**基础配置**>**自定义服务角色**中，单击**设置**。设置“自定义服务角色为”步骤2中生成的自定义角色，此处为 EMRCosRole，用户可自定义该名称。
![](https://main.qcloudimg.com/raw/af3721b9b7e6b4027c3df166ad16ec58.png)
