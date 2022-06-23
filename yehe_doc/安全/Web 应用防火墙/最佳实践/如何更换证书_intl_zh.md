## 操作场景
如果证书已过期，用户在浏览网站的时候会显示证书不可信；如果客户该域名有使用 API 调用，在调用过程中将会报错。为了避免证书过期对业务造成影响，请在腾讯云控制台上及时更新证书。

## 操作步骤
### 示例1：更换自有证书
1. 登录 [Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/tea-domain)，在左侧导航中，选择选择**资产中心** > **域名列表**。
2. 在域名列表页面，选中所需域名，单击**编辑**，进入编辑域名页面。
![](https://qcloudimg.tencent-cloud.cn/raw/321d2ebd5d8301be5e2a2698495e51a2.png)
3. 在编辑域名页面，单击服务器配置中的**重新关联**，弹窗证书配置窗口。
![](https://qcloudimg.tencent-cloud.cn/raw/02f1a44a64e457c71de866b3ad92c032.png)
4. 在证书配置窗口，证书来源选择自有证书，并输入相关的证书和私钥，单击**确认**，即可更换自有证书。
![](https://qcloudimg.tencent-cloud.cn/raw/9ed50f530b4cc479a24fadfbc19016c2.png)

### 示例2：腾讯云托管证书
1. 在 [域名列表](https://console.cloud.tencent.com/guanjia/tea-domain) 页面，选中所需域名，单击**编辑**，进入编辑域名页面。
![](https://qcloudimg.tencent-cloud.cn/raw/60a5a32c4630229970a9a9ae9a917b07.png)
2. 在编辑域名页面，单击服务器配置中的**重新关联**，弹窗证书配置窗口。
![](https://qcloudimg.tencent-cloud.cn/raw/b91f8519e2a4953ca0f1c7c6463bc27e.png)
3. 在证书配置窗口，证书来源选择腾讯云托管证书，并选择新证书，单击**确定**，即可更换 SSL 证书。
>? 此方法只适用于证书已经上传到 SSL 证书管理。

![](https://qcloudimg.tencent-cloud.cn/raw/29ea07010ec8bef8b392e4a02a672fe9.png)

## 检验是否生效
通过浏览器访问相关域名，可以查看证书的生效时间和到期时间。如果更换证书始终不生效，请 [联系我们](https://intl.cloud.tencent.com/contact-us) 获得帮助。
