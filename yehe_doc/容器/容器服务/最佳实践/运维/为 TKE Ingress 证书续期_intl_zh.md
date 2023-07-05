## 操作场景
使用容器服务 TKE 控制台创建的 Ingress 配置的证书，会引用 [SSL 证书](https://console.cloud.tencent.com/ssl) 中托管的证书，若 Ingress 使用时间较长，证书存在过期的风险。证书过期会对线上业务造成巨大影响，因此需要在证书过期前进行续期，您可参考本文为 Ingress 证书续期。 

## 操作步骤
### 查询证书到期时间

1. 登录 [SSL 证书控制台](https://console.cloud.tencent.com/ssl)，选择左侧导航栏中的**证书管理**。 
2. 在证书列表项的“到期时间”中，查看即将过期的证书。 

### 新增证书
在“证书管理”页面中，为旧证书续期生成新证书。您可根据自身情况选择**购买证书**、**申请免费证书**或**上传证书**中的任意一种方式来添加新证书。 

### 查看引用旧证书的 Ingress [](id:ingress)
1. 登录 [SSL 证书控制台](https://console.cloud.tencent.com/ssl)，选择旧证书右侧的**关联资源**即可查看引用此证书的负载均衡器。
2. 点击负载均衡器的 ID 跳转到**负载均衡**详情页面。如果是 TKE Ingress 的负载均衡器，在标签栏会出现 `tke-clusterId` 和 `tke-lb-ingress-uuid` 的标签，分别表示集群 ID 和 Ingress 资源的 UID。
3. 在负载均衡器的“基本信息”页面，点击标签行右侧的编辑按钮，即可进入“编辑标签”页面。
4. 使用 Kubectl 可以查询集群 ID 对应集群的 Ingress，过滤 uid 为 `tke-lb-ingress.uuid` 对应值的 Ingress 资源。参考代码示例如下：
```
$ kubectl get ingress --all-namespaces -o=custom-columns=NAMESPACE:.metadata.namespace,INGRESS:.metadata.name,UID:.metadata.uid | grep 1a******-****-****-a329-eec697a28b35
api-prod    gateway      1a******-****-****-a329-eec697a28b35
```
由查询结果可知，该集群中 `api-prod/gateway` 引用了此证书，因此需要更新此 Ingress。 

### 更新 Ingress

1. 在 [容器服务控制台](https://console.cloud.tencent.com/tke2) 找到 [引用旧证书的 Ingress](#ingress) 中对应的 Ingress 资源，单击**更新转发配置**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/44ba860bacb644d1c1f3a3e15f7568d9.png)
2. 在“更新转发配置”页面，为新证书**新建密钥**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/931646bb90883beb0ff28ed141ce1b8f.png)
 在“新建密钥”页面，选择新添加的证书，然后单击**创建Secret**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/3b40a3fed01728f31c3abb829d210737.png)
返回至“更新转发配置”页面，修改 Ingress 的 TLS 配置，添加新创建的证书 Secret。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/78c26a7a003152874d237fcb2f7d516f.png)
单击**更新转发配置**即可完成 Ingress 证书的续期。 
