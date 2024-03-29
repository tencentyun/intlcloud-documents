您可以通过如下步骤快速使用全站加速网络（Enterprise Content Delivery Network，ECDN）服务。  
![](https://main.qcloudimg.com/raw/efc38b1772f7b12fa21e6388de73e88e.png)

## 开通 ECDN 服务
全站加速服务已经全量开放服务，您可以通过 [ECDN 控制台](https://console.cloud.tencent.com/dsa) 申请开通全站加速服务。若您的账号已经开通了 ECDN 服务，请直接跳到第二步 [添加域名配置](#yuming)。
开通 ECDN 服务流程如下：

1. 根据国家政策法规规定，新用户必须完成实名认证才可以使用全站加速服务，您可以通过 [账号中心](https://console.cloud.tencent.com/developer) ，在认证信息一栏中，单击 【提交认证】进行认证。
 ![rec](https://main.qcloudimg.com/raw/f4f9c571ccbc82912aab084315d36dff.png)
 >
>- 实名认证详细流程可参见 [实名认证指引](https://intl.cloud.tencent.com/document/product/378/3629) 。
>- 个人认证会在提交审核后立即完成，企业认证约一个工作日完成，且认证成功后您将收到短信通知。您可以通过 [工单](https://console.cloud.tencent.com/workorder/category/create?level1_id=1&level2_id=41&level1_name=%E5%85%AC%E5%85%B1%E5%9F%BA%E7%A1%80%E7%B1%BB%E9%97%AE%E9%A2%98&level2_name=%E8%B4%A6%E5%8F%B7%E7%B1%BB) 咨询实名认证进度。
2. 已完成实名认证的用户，可直接进入 [ECDN 控制台](https://console.cloud.tencent.com/dsa) 页面，单击【产品计费说明】可以前往查看产品资费说明，单击【激活】可以自助开通服务。
 ![](https://main.qcloudimg.com/raw/df8fead92c1b97f550b83fe94c35b4e5.png)

<span id="yuming"></span>
## 添加域名配置
1. 登录 [ECDN 控制台](https://console.cloud.tencent.com/dsa)，在左侧菜单中，单击【域名管理】，进入管理页面。
2. 单击【添加域名】。
![](https://main.qcloudimg.com/raw/36265ae189909f1b34e1b393c1af607c.png)
3. 在**加速域名**处，填写需要加速的域名。
4. 选择**源站类型**并填写源站信息。**源站类型只能是【源站 IP】或【源站域名】**。
 - **源站类型为源站 IP：**
    - 默认回源配置：默认使用择优回源策略，该模式下您可以在 “IP 地址”处填写源站 IP 信息，每行填写一个（最多支持32个），支持端口设置，设置格式为 `IP:Port`，端口号需 ＞ 0 且 ＜ 65536。
    - 高级回源配置：源站类型为源站 IP 时，还支持分权重回源和分主备回源策略，详细配置说明请参见 [高级回源策略配置说明](https://intl.cloud.tencent.com/document/product/570/35821)。
 -  **源站类型为源站域名：**
 只能填入一个源站域名，且不能与加速域名相同，支持端口设置，设置格式为 `Host:Port`，端口号需 ＞ 0 且 ＜ 65536。
5. 选择回源协议，即配置边缘节点与源站之间通信所采用的传输协议。
6. 配置缓存规则，可默认使用推荐配置，或在此基础上自主编辑。
7. 域名配置完成后，单击【提交】，即可添加域名。成功添加的域名，系统将在后台为您部署相关配置，生效时间大约为5分钟。
![](https://main.qcloudimg.com/raw/c2414b82d62ca3644822ca4b7daa4e99.png) 

## 添加 CNAME 记录
1. 接入域名后，系统会为您分配对应的 **CNAME** ，以 `.dsa.dnsv1.com` 为后缀。您可以在域名管理页查看。
![](https://main.qcloudimg.com/raw/2c23e8238a172a6961ab55f1b9725ab0.png)
2. 您需要到接入域名的 DNS 服务商处完成 CNAME 配置，配置方法请参见 [CNAME 配置](https://intl.cloud.tencent.com/document/product/570/11134)。
3. 验证域名 CNAME 是否已经生效：不同的 DNS 服务商，CNAME 生效的时间略有不同，一般会在半个小时之内生效。您也可以通过 PING 的方式来查询 CNAME 是否生效，如果 PING 到后缀为 `.dsa.sp.spcdntip.com` 或 `.dsa.p23.tc.cdntip.com` 的域名，表示域名 CNAME 已生效。