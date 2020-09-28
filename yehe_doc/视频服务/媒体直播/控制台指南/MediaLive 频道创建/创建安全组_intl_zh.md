# 创建安全组

 输入安全组是用于对输入源 IPV4 地址进行合法性校验的手段，通过输入安全组配置，可以使 medialive 频道的输入更加安全。

将 CIDR 格式的字符串添加到新的输入安全组中，并用逗号或换行符分隔。
![](https://main.qcloudimg.com/raw/fa4a607b8f856c0733fef5d5ff1f4ea0.jpg)

>!
>- 安全组存在两种状态，idle 和 occupied 两种状态。idle 表示当前安全组没有被关联，可以编辑和删除；occupied 表示当前安全组已经被 channel-input 关联，此时的安全组只能编辑，不能被删除。
>- 控制台默认只支持5个安全组的创建，如果大量安全组创建需求，请[提工单](https://console.cloud.tencent.com/workorder/category)联系腾讯云客服人员。
