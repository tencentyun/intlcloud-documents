本文将为您详细介绍如何修改弹性网卡所属子网。
1. 进入 [私有网络控制台](https://console.cloud.tencent.com/vpc) 。
2. 单击左侧目录中的【IP 与网卡】>【弹性网卡】，进入弹性网卡列表页。
![](https://main.qcloudimg.com/raw/011cadeb3efb542f5bc62197e28212f8.png)
3. 单击需要绑定的实例 ID，进入详情页。
4. 单击所属子网后的【更换子网】。
![](https://main.qcloudimg.com/raw/ca351583b467976fd2ba29aef1dd17fa.png)
5. 在弹出框中选择需要更换的子网，并指定新的主 IP。
![](https://main.qcloudimg.com/raw/8fbc63af36c9e65b6d4ea185f45c3b17.png)
6. 单击【确定】即可。

>
>- 仅主网卡可以修改所属子网。
>- 更改所属子网前，请先解绑所有辅助 IP。
>- 仅可以将子网修改为同可用区下的其他子网。
