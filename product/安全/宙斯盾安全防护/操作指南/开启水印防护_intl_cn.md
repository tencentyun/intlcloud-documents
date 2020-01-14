
客户可以通过接入水印防护，高效全面防护 4 层 CC 攻击，如模拟业务报文攻击和重放攻击等。水印防护通过在业务端和宙斯盾防护系统端共享水印算法和密钥，使客户端每个发出的报文都嵌入了水印特征。而攻击报文却无水印特征，防护系统将甄别出攻击报文并将其丢弃。更详细的配置说明，详情请参见 [自定义高级安全策略](https://cloud.tencent.com/document/product/685/18800#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AE.89.E5.85.A8.E7.AD.96.E7.95.A5)。
## 流程图
![](https://main.qcloudimg.com/raw/782b52f9c58007e6c7f4d2936aa2929d.png)

## 开启流程
1. ** 进入 “业务列表” 开启水印**
用户进入 [宙斯盾高防控制台](https://console.cloud.tencent.com/gamesec)，在左侧目录中单击 【业务域名列表】，在已经创建的对应项目列，单击【开启水印】。
![1](https://main.qcloudimg.com/raw/6c53776a2a1f72da1aab2e4cbeb7b67e.png)
2. **复制密钥**
a. 开启水印成功后，在 “水印功能开启成功” 的弹窗中选择 “复制密钥”，单击【添加防护策略】。
![2](https://i.imgur.com/YqQ6cKQ.png)
b. 进入 “添加防护策略” 页面，选择 “防护 IP”。
![3](https://main.qcloudimg.com/raw/c15bc6e8aefa1b7a711bb4b187a9f2cf.png)
c. 添加好 TCP 协议防护端口、UDP 协议防护端口、白名单，单击【确认添加】。
![4](https://main.qcloudimg.com/raw/bb5b8a2c9394a19720ba92aa5c2b5682.png)
3. **线下配置**
在 “水印功能开启成功” 弹窗中，单击【客户端接入文件】下载，完成客户端和服务端的接入。
4. **开启策略**
a. 用户创建策略成功后，在【水印防护】下，单击【增加策略】进行修改，单击【启用】策略。
![](https://main.qcloudimg.com/raw/8fe6f6bd3b004821f8e2c4e06515bebd.png)
b. 等待几秒钟，防护状态显示为“防护生效”，水印开启成功。
![](https://i.imgur.com/Qnh0UC9.png)
