## 概述

访问策略可用于授予访问云监控相关的权限。访问策略使用基于 JSON 的访问策略语言。您可以通过访问策略语言授权指定委托人（principal）对指定的应用性能观测资源执行指定的操作。

## 策略语法
CAM 策略：

```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 

```

#### 元素用法
- **版本 version** 是必填项，目前仅允许值为"2.0"。
- **语句 statement** 是用来描述一条或多条权限的详细信息。该元素包括 effect、action、resource，condition 等多个其他元素的权限或权限集合。一条策略有且仅有一个 statement 元素。
 - **影响 effect** 描述声明产生的结果是“允许”还是“显式拒绝”。包括 allow (允许) 和 deny (显式拒绝) 两种情况。该元素是必填项。
 -  **操作 action** 用来描述允许或拒绝的操作。操作可以是 API （以 name 前缀描述）或者功能集（一组特定的 API，以 permid 前缀描述）。该元素是必填项。
 - **资源 resource** 描述授权的具体数据。有关如何指定资源的信息，请参阅您编写的资源声明所对应的产品文档。该元素是必填项。
 -  **生效条件 condition** 描述策略生效的约束条件。条件包括操作符、操作键和操作值组成。条件值可包括时间、IP 地址等信息。云监控目前并不支持特殊的生效条件，所以此项可不进行配置。



### 指定效力（effect）

如果没有显式授予（允许）对资源的访问权限，则隐式拒绝访问。同时，也可以显式拒绝（deny）对资源的访问，这样可确保用户无法访问该资源，即使有其他策略授予了访问权限的情况下也无法访问。下面是指定允许效力的示例：

```json
"effect" : "allow"
```

### 指定操作（action）

在 CAM 策略语句中，您可以从支持 CAM 的任何服务中指定任意的 API 操作在 CAM 策略语句中，您可以从支持 CAM 的任何服务中指定任意的 API 操作。对于云监控，请使用以 name/monitor: 为前缀的 API。例如："name/monitor:GetMonitorData"

您也可以使用通配符指定多项操作。例如，您可以指定名字以单词 "Describe" 开头的所有 API 操作，如下所示：

```
"action": [
  "name/monitor:Describe*"
]
```

如果您要指定云监控中所有操作，请使用 * 通配符，如下所示：

```
"action"：["name/monitor:*"]

```

### 指定资源（resource）

资源（resource）元素描述一个或多个操作对象，如等。所有资源均可采用下述的描述方式。

```plaintext
qcs:service_type:account:resource
```

参数说明如下：

| 参数         | 描述                                                         | 是否必选 |
| ------------ | ------------------------------------------------------------ | -------- |
| qcs          | 是 qcloud service 的简称，表示是腾讯云的云服务               | 是       |
| service_type | 产品简称，这里为 monitor                                 | 是       |
| account      | 描述资源拥有者的主账号信息，即主账号的 ID，表示为 `uin/${OwnerUin}`，如 uin/100000000001 | 是       |
| resource     | 描述具体资源详情，例如：cm-policy/policy-p1234abc     | 是       |

您可以对下列资源进行访问控制：

| 资源类型           | 授权策略中的资源描述方法                   |
| :----------------- | :----------------------------------------- |
| 告警策略/cm-policy | `qcs::monitor::uin/:cm-policy/${policyId}` |
| 通知模板/cm-notice | `qcs::monitor::uin/:cm-notice/${noticeId}` |

**指定资源示例**

例如您可以使用特定的策略 ID 指定它，如下所示：

```
"resource":["qcs::monitor:uin/1250000000:cm-policy/policy-p1234abc"]
```


若您要指定所有资源，或者特定 API 操作不支持资源级权限，请在 Resource 元素中使用 * 通配符，如下所示：

```
"resource": ["*"]
```

## 控制台示例

**授权用户拥有部分告警策略权限**

1. 根据 [创建自定义策略](https://intl.cloud.tencent.com/document/product/598/35596)，创建一个自定义策略。
该示例策略允许用户拥有对告警策略（策略 ID 为 policy-p1234abc和policy-p5678abc）的操作权限，策略内容可参考以下策略语法进行设置：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": "monitor:*",
            "resource": [
                        "qcs::monitor:uin/1250000000:cm-policy/policy-p1234abc",
                        "qcs::monitor:uin/1250000000:cm-policy/policy-p5678abc"
                        ],
            "effect": "allow"
        }
    ]
}
```

2. 找到创建的策略，在该策略行的 “操作” 列中，单击**关联用户/组**。
3. 在弹出的 “关联用户/用户组” 窗口中，选择您需要授权的用户/组，单击**确定**。







