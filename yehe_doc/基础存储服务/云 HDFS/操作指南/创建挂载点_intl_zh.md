CVM、CPM 2.0或者容器通过挂载点来访问 CHDFS 中数据，挂载点是 CHDFS 在 VPC 内访问的目标地址，同时每个挂载点对应一个域名，本文为您详细介绍如何创建挂载点。

## 操作步骤
1. 登录 [CHDFS 控制台](https://console.cloud.tencent.com/chdfs)，在左侧导航栏中单击【文件系统】，选择所需地域，例如广州。
2. 找到需要操作的 CHDFS，单击其【配置】，可查看其基础配置和挂载信息。
3. 选择【挂载点】>【添加挂载点】，在添加挂载点页面，输入名称，指定 VPC 网络和权限组。
 - 名称：挂载点名称，仅支持大小写字母、数字和 - 或 _ 的组合，长度为4 - 64的字符。
 - VPC 网络名称/ID：选择 VPC 网络。
 - 权限组：选择权限组，若未新建，请先 [创建权限组](https://intl.cloud.tencent.com/document/product/1106/41962)。
![](https://main.qcloudimg.com/raw/71dd4afeeaf75de0ca946951bd6fd1f7.png)
3. 单击【保存】，即可新建挂载点。

