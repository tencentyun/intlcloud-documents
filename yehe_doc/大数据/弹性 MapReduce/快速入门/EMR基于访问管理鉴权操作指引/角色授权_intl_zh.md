使用弹性 MapReduce 服务时，用户需要为服务账号授予系统默认角色 EMR_QCSRole。当该角色授予成功后，弹性 MapReduce 才能调用相关服务（CVM、COS 等）创建集群和保存日志等。
>!首次开通弹性 MapReduce 服务时，必须使用主账号完成角色授权流程，否则子账号和主账号均不能使用弹性 MapReduce。

## 角色授权流程
1. 当用户创建集群或创建按需执行计划时，若为服务账号授予 EMR_QCSRole 角色失败，会有如下提示。然后单击**前往访问管理**，进行角色授权。
![](https://main.qcloudimg.com/raw/fec28f413d0423a4e42f57ee838299a2.png)
2. 单击**同意授权**，将默认角色 EMR_QCSRole 授予弹性 MapReduce 的服务账号。
 ![](https://main.qcloudimg.com/raw/d8ad5786438aba4f5233f6117155e5bc.png)
3. 授权完成后，用户需刷新弹性 MapReduce 的控制台或购买页，刷新后即可正常操作。更多 EMR_QCSRole 相关的详细策略信息，可登录 [访问管理控制台](https://console.cloud.tencent.com/cam/policy) 查看。EMR_QCSRole 包含的权限信息详见 [协作者/子账号权限](https://intl.cloud.tencent.com/document/product/1026/31100)。

## EMR 容器版角色授权特别说明
1. 当您创建 EMR 容器版集群之前，需要检查是否存在 CVM_QCSRole 角色。
![](https://qcloudimg.tencent-cloud.cn/raw/d85d2817e5aba173cbf28d5a53882eec.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/fa4d943dd9d035c7649fe878516e62b7.jpg)
2. 如果不存在 CVM_QCSRole 角色则需要提前创建。在 [访问管理](https://console.cloud.tencent.com/cam/role/detail?roleId=4611686018428056826)中新建角色，选择腾讯云产品服务。
![](https://qcloudimg.tencent-cloud.cn/raw/fdb3f045b5bceec298975d4d99c1cfeb.jpg)
3. 选择云服务器 CVM，输入角色名称，即可完成 CVM_QCSRole 角色创建。
![](https://qcloudimg.tencent-cloud.cn/raw/5c092e9bddf48af31c5e2fd6445aa59a.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/a6802504d5cea34f8327d259b3b1e217.jpg)
