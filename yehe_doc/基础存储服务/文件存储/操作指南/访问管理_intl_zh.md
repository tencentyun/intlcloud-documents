## 操作场景

文件存储（Cloud File Storage，CFS）已支持资源级别的访问权限管理，即主账户可对指定的用户及用户组授予指定资源的指定操作权限。完成授权后， CFS 控制台及 API 将均按照该用户被授权情况，允许或禁止用户操作。
本指引将介绍如何为用户授权 CFS 的只读、读写以及自定义策略。更多关于腾讯云访问管理的原理及指引，请参见 [访问管理](https://intl.cloud.tencent.com/document/product/598/10583)。



## 创建访问控制策略

登录 [访问管理控制台](https://console.cloud.tencent.com/cam/policy) 策略管理页面。

- 如果需要快捷地授予用户权限 ，则可以在策略管理界面右侧的搜索框中搜索 CFS ，选择预设的 CFS 只读或读写权限并关联用户组以完成授权。
- 如果您需要给用户授予特定操作的权限 ，则可以新建一个自定义策略，并关联用户组以完成授权。

#### CFS 全读写策略

如果您想让用户拥有查询、创建、修改、删除等所有操作的权限，则可以授予用户 QcloudCFSFullAccess 权限。使用预设 QcloudCFSFullAccess 授予协作者或子用户所有 CFS 资源的读写以及 VPC 及子网的查询权限策略语法如下：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cfs:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:DescribeVpcEx",
                "vpc:DescribeSubnetEx"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

#### CFS 只读策略

如果您想让用户拥有查询权限 ，但是不具有创建、修改、删除的权限，则可以授予用户 QcloudCFSReadOnlyAccess 权限。使用预设 QcloudCFSReadOnlyAccess 授予协作者或子用户所有 CFS 资源的只读以及 VPC 及子网的查询权限策略语法如下：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cfs:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:DescribeVpcEx",
                "vpc:DescribeSubnetEx"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

#### 自定义策略

自定义策略是更加灵活的为用户授权的方式，访问管理控制台提供了多种生成策略的方式。本案例以使用 "按策略生成器创建" 的方式介绍如何新建一个自定义策略（其他方式请参见 [策略](https://intl.cloud.tencent.com/document/product/598/10601) 文档）。

策略生成器页面提供了可视化的策略配置，您只需通过参数的选择，便可自动生成策略代码，适合初次接触 CAM 授权的用户。

在 [策略管理控制台](https://console.cloud.tencent.com/cam/policy) 策略页面，选择**新建自定义策略 > 按策略生成器创建**，在新建策略页面，使用策略生成器，可以在一个自定义策略中添加多条声明，配置说明如下：

| 参数 | 对应策略参数 | 选项及效果                                                   |
| ---- | ------------ | ------------------------------------------------------------ |
| 效果 | Effect       | 允许或禁止                                                   |
| 服务 | Service      | 此处选择文件存储                                             |
| 操作 | Action       | 文件存储支持的所有接操作类型                                 |
| 资源 | Resource     | 可被操作的资源： <br><li>文件存储的所有资源写法为`*` <br><li>指定地区的所有资源写法为`qcs::cfs:ap-guangzhou::*`  <br><li>指定用户下所有地区所有资源写法为`qcs::cfs::uin/27700000:*` <br><li>指定用户下指定地区所有文件系统写法为`qcs::cfs:ap-guangzhou:uin/27700000:filesystem/*` <br><li>指定用户下指定用户组系统写法为`qcs::cfs::uin/27700000:pgroup/pgroup-doxpcqh`  <br><li>注意：策略中的 UIN 必须为主账号 UIN（后面的文件系统或权限组资源必须属于该主账号）</li> |
| 条件 | Condition    | 在何种条件下，该策略生效，设置方法请参见 [生效条件](https://intl.cloud.tencent.com/document/product/598/10608) |

其中，CFS 各个接口、接口功能及授权时注意事项在如下列出，可以根据下列说明，配置资源选项。

<table>
   <tr>
      <th>接口类别</th>
      <th>接口名称</th>
      <th>接口描述</th>
      <th>权限类型</th>
      <th>注意事项</th>
   </tr>
   <tr>
      <td rowspan="2">服务接口</td>
      <td>SignUpCfsService</td>
      <td>开通 CFS 服务</td>
      <td>写权限</td>
      <td>授权该接口无需指定资源</td>
   </tr>
   <tr>
      <td>DescribeCfsServiceStatus</td>
      <td>查询 CFS 服务开通状态</td>
      <td>读权限</td>
      <td>授权该接口无需指定资源</td>
   </tr>
   <tr>
      <td rowspan="9">文件系统接口</td>
      <td>DescribeCfsFileSystems</td>
      <td>列出文件系统</td>
      <td>读权限</td>
      <td>授权该接口需指定资源为<code>*</code></td>
   </tr>
   <tr>
      <td>CreateCfsFileSystem</td>
      <td>创建文件系统</td>
      <td>写权限</td>
      <td>授权该接口无需指定文件系统资源</td>
   </tr>
   <tr>
      <td>UpdateCfsFileSystemName</td>
      <td>更新文件系统名称</td>
      <td>写权限</td>
      <td>授权该接口需要指定文件系统资源</td>
   </tr>
   <tr>
      <td>UpdateCfsFileSystemPGroup</td>
      <td>更新文件系统的权限组</td>
      <td>写权限</td>
      <td>授权该接口需要指定文件系统资源</td>
   </tr>
   <tr>
      <td>UpdateCfsFileSystemSizeLimit</td>
      <td>更新文件系统配额</td>
      <td>写权限</td>
      <td>授权该接口需要指定文件系统资源</td>
   </tr>
   <tr>
      <td>DeleteCfsFileSystem</td>
      <td>删除文件系统</td>
      <td>写权限</td>
      <td>授权该接口需要指定文件系统资源</td>
   </tr>
   <tr>
      <td>DescribeMountTargets</td>
      <td>查询挂载点</td>
      <td>读权限</td>
      <td>授权该接口需要指定文件系统资源</td>
   </tr>
   <tr>
      <td>AddMountTarget</td>
      <td>创建挂载点</td>
      <td>写权限</td>
      <td>授权该接口需要指定文件系统资源</td>
   </tr>
   <tr>
      <td>DeleteMountTarget</td>
      <td>删除挂载点</td>
      <td>写权限</td>
      <td>授权该接口需要指定文件系统资源</td>
   </tr>
   <tr>
      <td rowspan="8">权限组接口</td>
      <td>DescribeCfsPGroups</td>
      <td>列出权限组</td>
      <td>读权限</td>
      <td>授权该接口需指定资源为<code>*</code></td>
   </tr>
   <tr>
      <td>CreateCfsPGroup</td>
      <td>创建权限组</td>
      <td>写权限</td>
      <td>授权该接口无需指定资源</td>
   </tr>
   <tr>
      <td>UpdateCfsPGroup</td>
      <td>更新权限组信息</td>
      <td>写权限</td>
      <td>授权该接口需要指定权限组资源</td>
   </tr>
   <tr>
      <td>DeleteCfsPGroup</td>
      <td>删除权限组</td>
      <td>写权限</td>
      <td>授权该接口需要指定权限组资源</td>
   </tr>
   <tr>
      <td>DescribeCfsRules</td>
      <td>列出权限组规则</td>
      <td>读权限</td>
      <td>授权该接口需要指定权限组资源</td>
   </tr>
   <tr>
      <td>CreateCfsRule</td>
      <td>创建权限组规则</td>
      <td>写权限</td>
      <td>授权该接口需要指定权限组资源</td>
   </tr>
   <tr>
      <td>UpdateCfsRule</td>
      <td>更新权限组规则信息</td>
      <td>写权限</td>
      <td>授权该接口需要指定权限组资源</td>
   </tr>
   <tr>
      <td>DeleteCfsRule</td>
      <td>删除权限组规则</td>
      <td>写权限</td>
      <td>授权该接口需要指定权限组资源</td>
   </tr>
   <tr>
      <td>密钥相关接口</td>
      <td>DescribeKmsKeys</td>
      <td>查询KMS密钥</td>
      <td>读权限</td>
			<td>授权该接口需指定资源为<code>*</code></td>
   </tr>
</table>

>! 另外，由于 CFS 文件系统使用 VPC 的 IP，因此创建文件系统、列出 CFS 文件系统列表、查询文件系统详情等页面中需要获取 "vpc:DescribeVpcEx" 及 "vpc:DescribeSubnetEx" 接口的权限（如果不授予则无法查询和创建）。强烈建议您对所有授权 CFS 的策略中增加这两个接口对 VPC 所有资源的授权。 详细策略写法可以参考  QcloudCFSReadOnlyAccess 策略申明。

上述参数设置完成后，单击**添加声明**，则为该自定义策略添加了一条声明。您可以重复上述操作，添加多条声明。若有重复或冲突的策略，他们之间的关系及生效结果请参见 [语法结构](https://intl.cloud.tencent.com/document/product/598/10604)。

策略的写法格式如下，每个策略中可以有多条声明（statement）。

```
{
    "version": "2.0",
    "statement": [{
        "effect": "Effect",
        "action": [
            "Action"
        ],
        "resource": "Resource"

    }]
}
```

例如，禁止用户对某几个文件系统执行删除及更新配额操作的权限策略语法。

```
{
    "version": "2.0",
    "statement": [{
        "effect": "deny",
        "action": [
            "name/cfs:DeleteCfsFileSystem",
            "name/cfs:UpdateCfsFileSystemSizeLimit"
        ],
        "resource": [
            "qcs::cfs::uin/2779643970:filesystem/cfs-11111111",
            "qcs::cfs::uin/2779643970:filesystem/cfs-22222222",
            "qcs::cfs::uin/2779643970:filesystem/cfs-33333333"
        ]
    }]
}
```

## 为用户/用户组授权

如果是选择系统提供的权限，则可以直接在策略详列表搜索到 QcloudCFSFullAccess 或 QcloudCFSReadOnlyAccess 或者是其他自定义策略后，在列表右侧的操作栏里单击**关联用户/组**，在弹出的窗口中查找并勾选需要被授权的用户或用户组，最后单击**确定**完成授权。

## 取消用户/用户组授权

如需取消已授权用户的权限，可在对应策略详情页的**关联用户/组**列表中，勾选需要取消授权的用户/用户组，然后单击**解除用户/用户组**，确认解除授权后，该用户/用户组将失去操作 CFS 资源的权限。
