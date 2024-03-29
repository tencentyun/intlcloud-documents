
为简化客户权限的配置操作，腾讯云的产品在接入访问管理时，会提供默认的授权策略，客户可以直接使用这些策略来关联 CAM 子账号或用户组，实现控制对应产品服务访问权限的目的。这类策略属于 CAM 预设策略，每类产品服务通常至少提供管理策略和只读策略。

步骤1：
进入**访问管理** > [**策略**](https://console.cloud.tencent.com/cam/policy) 控制台，在搜索框中输入产品名称（如云服务器），即可查看对应产品的预设策略列表。
![](https://qcloudimg.tencent-cloud.cn/raw/14537fb157c22fa3105756026d309519.png)
其中，QcloudCVMFullAccess为管理策略，QcloudCVMInnerReadOnlyAccess为 只读策略。

>!部分产品的管理策略是不包含支付权限的，您可以同步为需要授权的 CAM 子用户/用户组管理支付所需的默认策略，如 CVM 的 QcloudCVMFullAccess。

步骤2：
将上述策略授权给 CAM 子账号/用户组。授权方式请参考 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。

- 如果您需要为子用户授予腾讯云账号的全部管理权限，您可以使用预设策略 AdministratorAccess。
AdministratorAccess ：该策略允许您管理账户内所有用户及其权限、财务相关的信息、云服务资产。
- 如果您需要为子用户授予腾讯云账号的只读权限，您可以使用预设策略 ReadOnlyAccess。
ReadOnlyAccess：该策略允许您只读访问账户内所有支持接口级鉴权或资源级鉴权的云服务资产。

