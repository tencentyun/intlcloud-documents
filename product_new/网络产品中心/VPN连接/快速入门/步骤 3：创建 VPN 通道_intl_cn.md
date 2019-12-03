在 VPN 通道创建前，需要创建对端网关：
1. 登录 [腾讯云控制台](https://console.cloud.tencent.com/)，选择【云产品】>【私有网络】进入私有网络控制台。
2. 在左侧目录中单击【VPN 连接】>【VPN 通道】，进入管理页。
3. 选择私有网络所在的地域和私有网络，单击【新建】。
4. 输入通道名称（如：TomVPNConn），选择 VPN 网关`TomVPNGw`与对端网关`TomVPNUserGw`，并输入预共享密钥（如：`123456`），单击【下一步】。
 ![](https://main.qcloudimg.com/raw/16563ad3fdf63ce147bd2ffa35e5d014.png)
5. 输入 SPD 策略来限制本段哪些网段和对端哪些网段通信，在本例中本端网段即为子网 A 的网段`192.168.1.0/24`，对端网段为`10.0.1.0/24`，单击【下一步】。
 ![](https://main.qcloudimg.com/raw/ee39d49c99ab4cd5883af7d2adb71788.png)
6. （可选）配置 IKE 参数，如果不需要高级配置，可直接单击【下一步】。
 ![](https://main.qcloudimg.com/raw/4c003c6438a4c8e47e8057113edb1371.png)
7. （可选）配置 IPsec 参数，如果不需要配置，可直接单击【完成】。
 ![](https://main.qcloudimg.com/raw/3fe3a316218c475f6b5bfcf7a871167a.png)
8. 创建成功后，返回 VPN 通道列表页，单击【下载配置文件】并完成下载。
 ![](https://main.qcloudimg.com/raw/00575f0bbbfb9aae0442731db89d042c.png)
