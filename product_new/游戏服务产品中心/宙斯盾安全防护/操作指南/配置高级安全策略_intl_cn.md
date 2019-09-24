
宙斯盾安全防护（Aegis Anti-DDoS）提供 DDoS 高级安全防护策略。用户可针对业务平台的自身需求配置，绑定到高防 IP、高防包防护的 IP 上，通过禁用协议、禁用端口、IP 黑白名单、报文特征过滤策略、空连接防护等操作，为业务平台提供针对性防护。更详细的配置说明，详情请参见 [**自定义高级安全策略**](https://intl.cloud.tencent.com/zh/document/product/685/18800#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AE.89.E5.85.A8.E7.AD.96.E7.95.A5)。

## 添加高级安全策略
1. 用户进入 [宙斯盾高防控制台](https://console.cloud.tencent.com/gamesec)，在左侧目录中，单击【DDoS 防护高级策略】，在 “DDos 防护高级策略下”，单击【添加新策略】。添加成功后，在 “操作” 列下单击【配置】进入策略配置页面。
![1](https://main.qcloudimg.com/raw/8bc3064b064d047b0b20a93ef62aa964.jpg)
2. 选择需要配置的禁用协议跟端口，设置 IP 黑白名单，报文特征过滤，可选择性开启拒绝境外流量、空连接防护。单击保存即添加策略成功。
![2](https://main.qcloudimg.com/raw/179047876b22d537f8e1f0c9d1e6af0b.jpg)

## 高级安全策略直接绑定防护 IP
1. 单击【DDoS 防护高级策略】，在 “DDos 防护高级策略下”，单击 “策略 ID”。
![3](https://main.qcloudimg.com/raw/85a7391836c228c105334c21ed039559.jpg)
2. 在 “DDos 防护高级策略下”，单击【绑定IP列表】，单击【添加IP】。
![4](https://main.qcloudimg.com/raw/44bf9b96f9363ed40344e374aca8fcb3.jpg)

## DDoS 高防 IP 绑定高级安全策略
1. 单击【DDoS 高防 IP】，在 “DDos 高防 IP”下，单击 “高防 IP”。
![5](https://main.qcloudimg.com/raw/096dee55ad15263fffe2f5d6b292d4d6.jpg)
2.在 “DDos 高防 IP 详情” 页下单击【高级配置】。单击【绑定】，在 “配置 DDoS 防护高级策略” 弹窗中，选择好 “DDoS 防护高级安全策略” ，单击【确认】。
![6](https://main.qcloudimg.com/raw/b916e13157343663c011aecc37fe1db3.jpg)

## 给 DDoS 高防包下的防护 IP 配置高级安全策略
1. 单击【DDoS 高防包】，在 “DDos 高防包”下，单击高防包 ID。
![7](https://main.qcloudimg.com/raw/85c1f0a66ccc803dc88f64239a4079d7.jpg)
2. 在 “DDos 高防包详情” 页下单击【防护 IP 列表】，勾选需要配置的 IP，单击 “配置高级安全策略”。
![8](https://main.qcloudimg.com/raw/1d59efb8aa114045a934cc0c6bc116a6.jpg)
