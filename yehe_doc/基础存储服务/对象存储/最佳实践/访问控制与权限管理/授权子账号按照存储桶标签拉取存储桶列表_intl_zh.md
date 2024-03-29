## 简介

对象存储（Cloud Object Storage，COS）控制台、API 提供了按存储桶标签筛选存储桶列表的功能，该功能通过标签授权实现。

## 授权步骤


1. 使用主账号 Owner 登录到 [访问管理](https://console.cloud.tencent.com/cam/policy) 控制台，进入到策略配置页面。
2. 根据以下步骤，授权子账号 SubUser 子账号访问具有指定标签的存储桶，可通过**策略生成器**或**策略语法**实现。
<dx-tabs>
::: 通过策略生成器
1. 进入 [访问管理](https://console.cloud.tencent.com/cam/policy) 策略配置页面。
2. 单击**新建自定义策略 > 按策略生成器创建**。
3. 进入授权配置页面，配置信息如下：
	- **效果**：选择为允许，默认不变。
	- **服务**：选择对象存储。
	- **操作**：选择**读操作 > GetService(拉取存储桶列表)**。
	- **资源**：选择**全部资源**。
	- **条件**：单击**添加其他条件**。进入侧窗配置，配置信息如下：
		- **条件键**：选择 `qcs:resource_tag`。
		- **运算符**：选择 `string_equal`。
		- **条件值**：按照 `key&val` 格式输入标签，将 key 替换为标签键，value 替换为标签值。
4. 单击**下一步**，输入策略名称。
5. 单击**完成**，即可完成创建。
:::
::: 通过策略语法
1. 进入 [访问管理](https://console.cloud.tencent.com/cam/policy) 策略配置页面。
2. 单击**新建自定义策略 > 按策略语法创建**。
3. 选择空白模板创建，单击**下一步**。
4. 按照如下策略格式进行输入。其中，需要将 key 和 value 分别替换为指定的标签键和标签值。
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/cos:GetService"
            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        }
    ]
}
```
5. 单击**完成**，即可完成创建。
:::
</dx-tabs>
3. 将策略关联子账号 SubUser。在策略页面，找到步骤2创建的策略，在其右侧单击**关联用户/组/角色**。
4. 在弹窗中，勾选子账号 SubUser，并单击**确定**，即可将子账号 SubUser 关联至该策略。


## 控制台查看


1. 通过子账号 SubUser 登录 [COS 控制台](https://console.cloud.tencent.com/cos5)。
2. 在存储桶列表页面，将**自动展示该子账号有权限访问的存储桶列表**。

经过上述步骤，即完成了子账号授权访问包含指定标签（key，value）的存储桶。


## 接口调用


>!
> - 与控制台不同，调用 GetService API 接口不支持自动展示子账号有权限访问的存储桶列表，必须传入标签参数。
> - GetService 接口当前仅支持传入一个标签。


1. 使用子账号 SubUser 的密钥发起请求。
2. 调用 GetService 接口，传入标签过滤参数，例如(key,value)。请求示例如下，详情可参见 [GET Service（List Buckets）](https://intl.cloud.tencent.com/document/product/436/8291)。

```
GET /?tagkey=key1&tagvalue=value1 HTTP/1.1
Date: Fri, 24 May 2019 11:59:51 GMT
Authorization: Auth String
```


