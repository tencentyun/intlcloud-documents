
本文将指导您创建子用户并授权，如果您未接触过腾讯云访问权限管理，请参考此入门配置。

TPNS 使用腾讯云访问管理模块（CAM）进行权限管理，需要先完成对应用的授权，新建子用户，并对子用户进行应用权限授权，详细请参考如下操作流程。

## 新建子用户
1. 进入[访问管理](https://console.cloud.tencent.com/cam)，单击新建用户。

2. 根据指引，配置子用户的登录信息，到“设置用户权限”步骤时，为用户授权应用的权限。


## 应用授权
#### 对全部应用统一授权：
1.继续上一步骤的页面。
2.在搜索框中输入“TPNS”，在搜索结果中，有两个默认预置权限，对应权限为：

| 策略名称 | 权限范围 |
| --- | --- |
| QcloudTPNSFullAccess | 可对主账号下所有应用进行所有权限 |
| QcloudTPNSReadOnlyAccess | 可对主账号下所有应用进行数据可读及进行推送权限 |

#### 对部分应用进行授权
1.单击“新建自定义策略”。

2.打开新的页面如下，选择“按策略语法创建”。

3.选择空白模板。


4.单击下一步，进入语法创建页面。


复制下方的语法代码：
```
{
    "version": "2.0",
    "statement": [
        { 
            "action": [
                "tpns:Describe*",
                "tpns:CancelPush",
                "tpns:DownloadPushPackage",
                "tpns:CreatePush",
                "tpns:UploadPushPackage"
            ],
            "resource": [
                "qcs::tpns::uin/1000000000:app/1500000000"
            ],
            "effect": "allow"
        },
        {
            "action": [
                "tpns:Describe*"
            ],
            "resource": [
                "qcs::tpns::uin/1000000000:/*"
            ],
            "effect": "allow"
        }

     ]
}
```

替换语法代码中的参数：
- 主账号ID替换：进入当前主账号的 [账号信息](https://console.cloud.tencent.com/developer) 页面，复制账号ID，替换上方语法中的 1000000000。
>如果您当前登录的账号是协作者或子账号，需要向给您分配权限的主账号拥有者获取账号 ID。

- 应用`Access_ID`替换：进入 [TPNS产品管理](https://console.cloud.tencent.com/tpns) 页面，复制需要授权的`Access_ID`，替换上方语法中的 1500000000，如需要同时授权多个应用，可以将 resource 改为：
`"qcs::tpns::uin/1000000000:app/{应用Access_ID1}"`,`"qcs::tpns::uin/1000000000:app/{应用Access_ID2}"`

>其中大括弧“{“、"}"请删除。

5.返回创建用户页面。
搜索您创建的策略名称并勾选，选择下一步后，单击完成。

6.完成权限配置后您可以在登录界面选择使用子用户进行账号权限验证。
