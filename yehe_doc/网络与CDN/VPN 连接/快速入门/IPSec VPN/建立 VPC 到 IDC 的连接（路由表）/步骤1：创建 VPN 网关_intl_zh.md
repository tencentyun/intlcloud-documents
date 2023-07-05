1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧目录中单击 **VPN 连接** > **VPN 网关**，进入管理页。
3. 选择地域，如示例中的**东京**，单击<b>+新建</b>。
>? 若<b>+新建</b>显示灰色，且鼠标移至上方时显示“无可用私有网络”，请 [创建私有网络](https://intl.cloud.tencent.com/document/product/215/31805) 后再进行新建 VPN 网关。 
>
![](https://qcloudimg.tencent-cloud.cn/raw/e2a11579b443c9e5affdb0c842da5103.png)
4. 在弹出的创建对话框中填写 VPN 网关名称（如 VPN1），选择关联网络为私有网络、所属网络选择 VPC1，设置带宽上限及计费方式等。
>?
>- 如果 VPN 网关使用200Mbps、500Mbps、1000Mbps和3000Mbps规格的带宽，VPN 通道加密协议建议使用 AES128+MD5。
>
![](https://qcloudimg.tencent-cloud.cn/raw/de9c596b396c72604f643b4dc88fc47c.png)
5. 单击**创建**。VPN 网关创建完成后，系统随机分配公网 IP，如：`119.29.147.109`。
    ![](https://qcloudimg.tencent-cloud.cn/raw/10ddbbb6350f585850445fcf73a86ec2.png)
