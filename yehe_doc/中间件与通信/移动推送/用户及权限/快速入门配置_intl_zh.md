
本文将指导您创建子用户并授权，如果您未接触过腾讯云访问权限管理，请参考此入门配置。

移动推送使用腾讯云访问管理模块（CAM）进行权限管理，需要先完成对应用的授权，新建子用户，并对子用户进行应用权限授权，详细请参考如下操作流程。

## 新建子用户
1. 前往 [访问管理](https://console.cloud.tencent.com/cam)，单击**新建用户**。
![](https://qcloudimg.tencent-cloud.cn/raw/f66c0500cc623b161f611bba8b1a0c4c.png)
2. 以下是自定义创建的方式，单击**自定义创建**，进入新建子用户页面。
![](https://qcloudimg.tencent-cloud.cn/raw/08e0b1bc2080def5772794dd97202a36.png)
3. 根据指引，配置子用户的登录信息，到“设置用户权限”步骤时，为用户授权应用的权限。


## 应用授权
#### 对全部应用统一授权：
1. 继续上一步骤的页面，见下图：
![](https://qcloudimg.tencent-cloud.cn/raw/01df52c8be53b93b22675e284849650d.png)
2. 在搜索框中输入“移动推送”，在搜索结果中，有两个默认预置权限，对应权限为：

| 策略名称 | 权限范围 |
| --- | --- |
| QcloudTPNSFullAccess | 可对主账号下所有应用进行所有权限 |
| QcloudTPNSReadOnlyAccess | 可对主账号下所有应用进行数据可读及进行推送权限 |

#### 对部分应用进行授权

1. 单击**新建自定义策略**。
![](https://qcloudimg.tencent-cloud.cn/raw/6741b778bc804388134b3d97d68fe433.png)
2. 打开新的页面如下，选择**按策略语法创建**。
![](https://qcloudimg.tencent-cloud.cn/raw/9f875d430a89c2270aa0cdbf63a3d020.png)
3. 选择**空白模板**。
![](https://qcloudimg.tencent-cloud.cn/raw/3b7d9e84a1a3db6b24506f659b8a77bc.png)
4. 单击**下一步**，进入语法创建页面后，见下图。
![](https://qcloudimg.tencent-cloud.cn/raw/de89a170da2bb02f20f7e2be15ae5a4a.png)
>?
>- 您可以输入易于记忆的策略名称。
>- 复制文档中的代码，替换其中的账号 ID（可在管理台右上角个人 >账号信息页面找到）和 Access_ID（可在管理台移动推送产品管理页面找到）。
>
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
 - 主账号ID替换：进入当前主账号的 [账号信息](https://console.cloud.tencent.com/developer) 页面，复制账号 ID，替换上方语法中的 1000000000。
>?如果您当前登录的账号是协作者或子账号，需要向给您分配权限的主账号拥有者获取账号 ID。
![](https://qcloudimg.tencent-cloud.cn/raw/82f946f2d0dc124a634d6398531d3f89.png)
 - 应用`Access_ID`替换：进入 [移动推送产品管理](https://console.cloud.tencent.com/tpns) 页面，复制需要授权的`Access_ID`，替换上方语法中的 1500000000，如需要同时授权多个应用，可以将 resource 改为：
`"qcs::tpns::uin/1000000000:app/{应用Access_ID1}"`,`"qcs::tpns::uin/1000000000:app/{应用Access_ID2}"`
>?其中大括弧“{“、"}"请删除，如需要更多细分操作，请仔细阅读 [进阶自定义配置](https://intl.cloud.tencent.com/document/product/1024/35288)。
5. 返回创建用户页面。
![](https://qcloudimg.tencent-cloud.cn/raw/b8806c04fccc0c79d3021c45133f22a7.png)
搜索您创建的策略名称并勾选，选择下一步后，单击完成。
6. 完成权限配置后您可以在登录界面选择使用子用户进行账号权限验证。
