﻿默认情况下，子用户没有使用 MySQL 数据库审计的权利。因此用户就需要创建策略来允许子用户使用数据库审计。
若您不需要对子用户进行 MySQL 数据库审计相关资源的访问管理，您可以忽略此文档。

访问管理（Cloud Access Management，CAM）是腾讯云提供的一套 Web 服务，主要用于帮助用户安全管理腾讯云账号下资源的访问权限。通过 CAM，您可以创建、管理和销毁用户（组），并通过身份管理和策略管理控制指定用户可以使用的腾讯云资源。

当您使用 CAM 的时候，可以将策略与一个用户或一组用户关联起来，策略能够授权或者拒绝用户使用指定资源完成指定任务。

## 给子用户授权
1. 以主账号身份登录访问管理控制台，在用户列表选择对应子用户，单击**授权**。
2. 在弹出的对话框，选择 **QcloudCDBFullAccess云数据库（CDB）全读写访问权限**或 **QcloudCDBInnerReadOnlyAccess云数据库（CDB）只读访问权限**预设策略，单击**确定**，即可完成子用户授权。
>?MySQL 数据库审计是 MySQL 数据库的子模块，因此上述 MySQL 的两个权限预设策略即涵盖了 MySQL 数据库审计所需的权限策略。如果子用户仅需要 MySQL 数据库审计所需的权限，可参考 [自定义 MySQL 数据库审计策略](#zdymsjksjcl)。
>

## [策略语法](id:clyf)
MySQL 数据库审计的 CAM 策略描述如下：
```
{     
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"]
           } 
       ] 
} 
```

- **版本 version**：必填项，目前仅允许值为"2.0"。
- **语句 statement**：用来描述一条或多条权限的详细信息。该元素包括 effect、action、resource 等多个其他元素的权限或权限集合。一条策略有且仅有一个 statement 元素。
- **影响 effect**：必填项，描述声明产生的结果是“允许”还是“显式拒绝”。包括 allow（允许）和 deny（显式拒绝）两种情况。
- **操作 action**：必填项，用来描述允许或拒绝的操作。操作可以是 API（以 name 前缀描述）或者功能集（一组特定的 API ，以 permid 前缀描述）。
- **资源 resource**：必填项，描述授权的具体数据。


## API 操作
在 CAM 策略语句中，您可以从支持 CAM 的任何服务中指定任意的 API 操作。对于数据库审计，请使用以 name/cdb: 为前缀的 API 。如果您要在单个语句中指定多个操作，请使用逗号将它们隔开，如下所示：
```
"action":["name/cdb:action1","name/cdb:action2"]
```

您也可以使用通配符指定多项操作。例如，您可以指定名字以单词"Describe"开头的所有操作，如下所示：
```
"action":["name/cdb:Describe*"]
```


## 资源路径
资源路径的一般形式如下：
```
qcs::service_type::account:resource
```
 
- service_type：产品简称，此处为 cdb。
- account：资源拥有者的主账号信息，如 uin/326xxx46。
- resource：产品的具体资源详情，每个 MySQL 实例（instanceId）就是一个资源。

示例如下：
```
 "resource": ["qcs::cdb::uin/326xxx46:instanceId/cdb-kf291vh3"]
```
其中，cdb-kf291vh3 是 MySQL 实例资源的 ID，在这里是 CAM 策略语句中的资源 resource。

## 示例
以下示例仅为展示 CAM 用法。

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/cdb: DescribeAuditRules"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/cdb: CreateAuditPolicy"
            ],
            "resource": [
                "*"
            ]
        },
       
        {
            "effect": "allow",
            "action": [
                "name/cdb: DescribeAuditLogFiles"
            ],
            "resource": [
                "qcs::cdb::uin/326xxx46:instanceId/cdb-kf291vh3"
            ]
        }
    ]
}
```

## [自定义 MySQL 数据库审计策略](id:zdymsjksjcl)
1. 以主账号身份登录访问管理控制台，在策略列表，单击**新建自定义策略**。
2. 在弹出的对话框，选择**按策略生成器创建**。
3. 在选择服务和操作页面，选择各项配置，单击**下一步**。
 - 服务(Service)：选择**云数据库 MySQL（cdb）**。
 - 操作(Action)：选择 MySQL 数据库审计的所有 API。
 - 资源(Resource)：选择全部资源，表示可以操作所有 MySQL 实例的审计日志。
 - 条件(Condition)：选填，设置上述授权的生效条件。
4. 在**关联用户/用户组/角色**页面，按命名规范，输入“策略名称”（例如 SQLAuditFullAccess）和“描述”后，单击**完成**。
5. 返回策略列表，即可查看刚创建的自定义策略。
