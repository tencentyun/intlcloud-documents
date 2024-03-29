安全组是腾讯云提供的防火墙，可以对云数据库进行入流量控制。您可以在购买集群时绑定安全组，也可以购买集群后在控制台绑定安全组。

本文介绍通过控制台为 TDSQL-C MySQL 版配置安全组。
>!
>- 目前 TDSQL-C MySQL 版安全组仅支持私有网络云数据库配置。
>- TDSQL-C MySQL 版支持为读写地址、只读地址配置不同安全组，互相不影响。

## 配置安全组
### 购买集群时配置安全组
1. 登录 [购买页](https://buy.cloud.tencent.com/cynosdb?regionId=8#/)。
2. 完成数据库配置和基础信息配置，在高级配置下配置安全组，完成余下购买设置，单击立即购买即可 。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/kjDU265_14.png)

### 购买集群后在控制台配置安全组
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)。
2. 在上方选择地域，在集群列表找到目标集群，单击集群 ID 或**操作**列的**管理**，进入集群管理页面。
3. 在集群管理页面，选择**安全组**页，选择需要配置安全组的读写实例或者只读实例，单击**配置安全组**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yh7N015_15.png)
4. 在配置安全组窗口下，选择安全组规则（也可以通过检索安全组ID找到您需要的安全组），单击**确定**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/CtjH139_16.png)
>?
>- 您可配置多个安全组规则，最多不超过5个。
>- 不同的访问地址可配置不同的安全组，安全组拦截仅会对通过当前地址访问的源进行控制。

## 调整安全组优先级
当 TDSQL-C MySQL 版实例绑定多个安全组时，多个安全组将按照优先级顺序（如1、2）依次匹配执行，您可以调整安全组的优先级。

1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)。
2. 在上方选择地域，在集群列表找到需要的集群，单击集群 ID 或**操作**列的**管理**，进入集群管理页面。
3. 在集群管理页面，选择**安全组**页，选择需要配置安全组的读写实例、数据库代理或者只读实例，单击已加入安全组下面的**编辑**。
4. 在安全组操作列，通过上调/下调/删除![](https://qcloudimg.tencent-cloud.cn/raw/0796ce4fc98c14bfcb924b1da3083149.png)图标调整安全组的优先级，调整后单击**保存**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9F25795_18.png)

