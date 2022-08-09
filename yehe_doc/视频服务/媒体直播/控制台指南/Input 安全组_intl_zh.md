Input安全组是一种有状态的包含过滤功能的虚拟防火墙。主要针对推流类型input，在用户推流时做安全校验，目前支持IP(段)白名单方式，是腾讯云提供的重要的网络安全隔离手段。



## 前提条件
- 已开通 [StreamLive](https://intl.cloud.tencent.com/products/mdl)。 
- 已登录 [StreamLive控制台](https://console.intl.cloud.tencent.com/mdl/security)。

## Input安全组管理
单击左侧导航栏**Security Group Management**，可以查看已创建的input安全组名称、使用状态、ID。并且可以进行创建、编辑、删除操作。目前腾讯云StreamLive已提供印度孟买、泰国曼谷、韩国首尔、日本东京、德国法兰克福五个可用区，您可在此选择您所在的地域。如果您有其余可用区的部署诉求请[联系我们](https://intl.cloud.tencent.com/contact-us)。

![](https://qcloudimg.tencent-cloud.cn/raw/fc7c32157eccae3591533e14c511fa8f.png)


### 创建Input安全组
安全组是用于对输入源IPV4地址进行合法性校验的手段，通过输入安全组配置，可以使StreamLive频道的输入更加安全。若您需要创建input安全组，单击页面左上角**Create Security Group**按钮，在弹窗中进行配置：
1）**Name**：安全组名称，可由用户自定义。可支持1-32位数字、字母、下划线“_”。
2）**IP Allowlist**：IP白名单，使用CIDR格式，并用逗号或换行符分隔，如果不需要限制来源IP，填0.0.0.0/0即可。
输入后点击**Confirm**按钮完成创建。

![](https://qcloudimg.tencent-cloud.cn/raw/4fd4169c10d7b6f968f323822c37301a.png)

### 修改Input安全组
若您需要修改Input安全组，单击需要修改的**input security group**右侧**Edit**，在弹窗中进行修改，修改完成后点击**Confirm**完成修改。

![](https://qcloudimg.tencent-cloud.cn/raw/6fbf87ce94c7c1cc8e9914c5fb9425ef.png)

### 删除Input安全组
若您需要删除Input安全组，单击需要删除的**input security group**右侧**Delete**，在弹窗中点击**Confirm**完成删除。

![](https://qcloudimg.tencent-cloud.cn/raw/b0f08d28e5b0658c04756a179100dad9.png)

>?
>- 安全组存在两种状态，idle和occupied两种状态。
>- idle表示当前安全组没有被关联，可以编辑和删除。
>- occupied表示当前安全组已经被channel-input关联，此时的安全组只能编辑，不能被删除。
>- 控制台默认只支持5个安全组的创建，如有更多的安全组创建需求，请 [提交工单](https://console.cloud.tencent.com/workorder)联系腾讯云客服人员。

