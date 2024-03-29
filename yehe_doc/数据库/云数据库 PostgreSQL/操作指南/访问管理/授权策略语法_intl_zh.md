<span id = "clyf"></span>
### 策略语法
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

- **版本 version**：必填项，目前仅允许值为"2.0"。
- **语句 statement**：用来描述一条或多条权限的详细信息。该元素包括 effect、action、resource、condition 等多个其他元素的权限或权限集合。一条策略有且仅有一个 statement 元素。
 - **影响 effect**：必填项，描述声明产生的结果是“允许”还是“显式拒绝”。包括 allow（允许）和 deny（显式拒绝）两种情况。
 - **操作 action**：必填项，用来描述允许或拒绝的操作。操作可以是 API 或者功能集（一组特定的 API ，以 permid 前缀描述）。
 - **资源 resource**：必填项，描述授权的具体数据。资源是用六段式描述，每款产品的资源定义详情会有所区别。
 - **生效条件 condition**：描述策略生效的约束条件。条件包括操作符、操作键和操作值组成。PostgreSQL 目前并不支持特殊的生效条件，所以此项可不进行配置。

<span id = "cz"></span>
### PostgreSQL 的操作
在 CAM 策略语句中，您可以从支持 CAM 的任何服务中指定任意的 API 操作。对于 PostgreSQL，请使用以 postgres: 为前缀的 API。例如 postgres:DescribeDBInstances 或者 postgres:DescribeDBInstanceAttribute。
如果您要在单个语句中指定多个操作的时候，请使用逗号将它们隔开，如下所示：
```
"action":["postgres:action1","postgres:action2"]
```

您也可以使用通配符指定多项操作。例如，您可以指定名字以单词 "Describe" 开头的所有操作，如下所示：
```
"action":["postgres:Describe*"]
```

如果您要指定 PostgreSQL 中所有操作，请使用 * 通配符，如下所示：
```
"action"：["postgres:*"]
```

<span id = "zylj"></span> 
### PostgreSQL 的资源路径
每个 PostgreSQL 策略语句都有适用于自己的资源。
资源路径的一般形式如下：
```
qcs:project_id:service_type:region:account:resource
```
**project_id**：描述项目信息，仅为了兼容 CAM 早期逻辑，无需填写。
**service_type**：产品简称 postgres。
**region**：[地域信息](https://intl.cloud.tencent.com/document/product/213/6091)，如 ap-shanghai。
**account**：资源拥有者的主帐号信息（即 [账号信息](https://console.cloud.tencent.com/developer) 页的“账号ID”），如164xxx472。
**resource**：各产品的具体资源详情，如实例为 DBInstanceId/postgres-0xssvm8e 或者 DBInstanceId/\*，下表描述了 PostgreSQL 能够使用的资源和对应的资源描述方法。

| 资源 | 授权策略中的资源描述方法                                |
| ---- | ------------------------------------------------------- |
| 实例 | qcs::postgres:$region:$account:DBInstanceId/$DBInstanceId |

例如，您可以使用特定实例（实例 ID 为 postgres-0xssvm8e）语句中指定它，如下所示：
```
"resource":[ "qcs::postgres:ap-shanghai:164xxx472:DBInstanceId/postgres-0xssvm8e"]
```

您还可以使用 * 通配符指定属于特定账户上海地域的所有实例，如下所示：
```
"resource":[ "qcs::postgres:ap-shanghai:164xxx472:DBInstanceId/*"]
```

您要指定所有资源，或者如果特定 API 操作不支持资源级权限，请在 Resource 元素中使用 * 通配符，如下所示：
```
"resource": ["*"]
```

如果您想要在一条指令中同时指定多个资源，请使用逗号将它们隔开，如下所示为指定两个实例的例子：
```
"resource":["qcs::postgres::164xxx472:DBInstanceId/postgres-0xf1f41e","qcs::postgres::164xxx472:DBInstanceId/postgres-0xssvm8e"]
```
