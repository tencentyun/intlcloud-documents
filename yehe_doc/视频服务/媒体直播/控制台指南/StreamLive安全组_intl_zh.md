安全组是一种有状态的包含过滤功能的虚拟防火墙，主要对输入源的安全校验进行管理，是腾讯云提供的重要的网络安全隔离手段。

### 安全组区域选择

目前腾讯云StreamLive已提供印度孟买、泰国曼谷、韩国首尔、日本东京四个可用区，您可在此选择您所在的地域。如果您有其余可用区的部署诉求请[联系我们](https://intl.cloud.tencent.com/contact-sales)。
![](https://qcloudimg.tencent-cloud.cn/raw/c099c3984d22fca6227e14123d9e2c17.jpg)

### 创建安全组

安全组是用于对输入源IPV4地址进行合法性校验的手段，通过输入安全组配置，可以使StreamLive频道的输入更加安全。

选择【Security Group Management】菜单，点击【Create Security Group】创建安全组。输入Name后，将CIDR格式的字符串添加到新的输入安全组中，并用逗号或换行符分隔。输入完毕后点击【Confirm】完成创建。

![img](https://main.qcloudimg.com/raw/e5c7365ba3724802b2013b3c25cdc07b.png)

>?
> - 安全组存在两种状态，idle和occupied两种状态。
> - idle表示当前安全组没有被关联，可以编辑和删除；
> - occupied表示当前安全组已经被channel-input关联，此时的安全组只能编辑，不能被删除。
> - 控制台默认只支持5个安全组的创建，如有更多的安全组创建需求，请[提交工单](https://console.cloud.tencent.com/workorder)联系腾讯云客服人员。
