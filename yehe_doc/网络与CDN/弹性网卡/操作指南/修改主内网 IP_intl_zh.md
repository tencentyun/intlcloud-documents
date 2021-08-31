本文介绍如何在弹性网卡控制台修改云服务器主内网IP。
>!
>+ 仅支持修改云服务器主网卡的主内网 IP，不支持修改辅助网卡的主内网 IP。
>+ 修改主网卡的主内网 IP 会导致关联的实例自动重启约30s，重启过程中会存在短暂的业务中断，重启后业务即可恢复，请您根据实际情况谨慎操作。
>+ 修改主内网 IP 也可以在云服务器控制台执行，如有需要，请参考 [修改内网 IP 地址](https://intl.cloud.tencent.com/document/product/213/16561)。

## 前提条件
请先登录云服务器控制台，获取云服务器的主网卡 ID，具体请参考 [查看实例信息](https://intl.cloud.tencent.com/document/product/213/16533)。

## 操作步骤
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc) 。
2. 单击左侧目录中的【IP 与网卡】>【弹性网卡】，进入弹性网卡列表页。
3. 单击需要修改的实例 ID，进入详情页。
4. 单击选项卡中的【IPv4 地址管理】，查看已绑定的主内网 IP。
![](https://main.qcloudimg.com/raw/9ac36c5a428ae63f03b4a9d52e267152.png)
5. 单击需要修改的主内网 IP 所在行的【修改主 IP】。
![](https://main.qcloudimg.com/raw/519cc573d98fe4d30948a5ae89033782.png)
6. 在弹窗内输入新的主内网 IP，单击【确定】即可。
![](https://main.qcloudimg.com/raw/495555a2c35cf0442c670a5a7c4b1fb9.png)
