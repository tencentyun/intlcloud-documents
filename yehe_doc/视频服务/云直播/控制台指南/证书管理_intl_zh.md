直播域名使用简单的 HTTP 协议，将 HTTP 用 SSL/TLS 协议进行封装成为 HTTPS，实现数据加密传输。若需批量管理多个域名，为其配置 SSL 证书，可通过【证书管理】来实现批量查询和配置 SSL 证书。

## 配置原理
域名配置 SSL 证书，目的是传输过程中对用户的关键信息进行加密，基于 SSL 证书，可将站点由 HTTP（Hypertext Transfer Protocol）切换到 HTTPS（Hyper Text Transfer Protocol over Secure Socket Layer），即基于安全套接字层（SSL）进行安全数据传输的加密版 HTTP 协议。 

[](id:c_ssl)
## 配置证书
1. 进入云直播控制台的【[域名管理](https://console.cloud.tencent.com/live/domainmanage)】，单击【证书管理】进入证书管理配置页。
![](https://main.qcloudimg.com/raw/e39413b101a445ed747d78c8c9e7c8ac.png)
2. 单击【配置证书】，创建新的证书配置。
![](https://main.qcloudimg.com/raw/5aeee06ba8b978b823be16e9191bf705.png)
3. 在证书配置弹窗中选择证书上传方式，其中腾讯云支持两种证书来源：
  - **自有证书**：需要填写证书备注后输入证书内容和证书密钥，该证书保存成功后会同步至 [SSL 证书管理](https://console.cloud.tencent.com/ssl)，可以在此查看证书。证书内容和证书密钥输入操作可参见 [HTTPS 配置](https://intl.cloud.tencent.com/document/product/267/31066)。
![](https://main.qcloudimg.com/raw/998de2fdadf6ed9ab52e7fdcef288f51.png)
  - **腾讯云托管证书**：选择已在腾讯云 SSL 证书管理购买的证书，可以通过证书列表选择证书适配加速域名。
![](https://main.qcloudimg.com/raw/4f36c491c7392798bc81410ecc65ae6e.png)
4. 证书校验正确后，单击【下一步】，进入选择域名配置页。
5. 在“关联域名”栏中选择按证书域名筛选出匹配的播放域名，可多选。若当前域名已绑定过其他证书，则覆盖更新证书。
6. 完成选择后右侧的“已选择”栏中会显示已选中的域名和绑定后的状态效果。
![](https://main.qcloudimg.com/raw/bc1a0c51023d295120b8c94420b7b628.png)
7. 选择是否为所选域名同时开启 HTTPS 配置：
  >? 
  >- 【同时开启HTTPS配置】按钮，支持选择开启 HTTPS 配置。开启后，同时支持 HTTP 和 HTTPS；关闭时，只能支持 HTTP。
  >- 【同时开启HTTPS配置】按钮默认开启，保存后更新的域名均开启 HTTPS 配置，若关闭则仅更新证书，不修改 HTTPS 的开/关。
6. 单击【确定】，完成证书配置。


[](id:check)
## 查看证书配置
[配置证书](#c_ssl) 完成后，您可在【[证书管理](https://console.cloud.tencent.com/live/common/certificate)】的配置列表中查看您已创建成功的配置信息。展示数据包括您已配置证书的域名、证书备注、证书来源、HTTPS 配置以及到期时间。
![](https://main.qcloudimg.com/raw/e4012e075b695afc912840462e0c5694.png)

[](id:update)
## 更新证书配置
1. 在【[证书管理](https://console.cloud.tencent.com/live/common/certificate)】的配置列表中，单击需要**更新**的配置列右侧的【更新】。
![](https://main.qcloudimg.com/raw/bfad71179c2ab41cd3c35e23e47e0224.png)
2. 进入证书配置页，重新 [配置证书](#c_ssl) 信息。
3. 单击【确定】，重新提交后即可更新证书。

[](id:delete)
## 删除证书绑定
1. 在【[证书管理](https://console.cloud.tencent.com/live/common/certificate)】的配置列表中，单击需要**删除**的配置信息右侧的【删除】。
![](https://main.qcloudimg.com/raw/a5d8f92c8aa7f2264c56e5ef6bf1f15b.png)
2. 确定是否删除证书绑定，单击【确定】即可成功删除。
![](https://main.qcloudimg.com/raw/10305e0609cfcda523505cbcf8a099c8.png)
>! 删除后该域名将无法使用 HTTPS 配置。


