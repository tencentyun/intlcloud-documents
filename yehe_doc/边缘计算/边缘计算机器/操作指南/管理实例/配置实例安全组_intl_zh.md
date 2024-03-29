
## 操作场景

安全组是一种虚拟防火墙，具备有状态的数据包过滤功能，用于设置单台或多台边缘实例的网络访问控制，是腾讯云提供的重要的网络安全隔离手段。
创建边缘实例时必须要为实例配置安全组，如果您已创建的实例默认使用的模块安全组或自定义配置的安全组无法满足您的业务场景时，可参考本文更换实例所属的安全组。



## 操作步骤
1. 登录 [边缘计算机器控制台](https://console.cloud.tencent.com/ecm/overview)。
2. 选择左侧导航栏中的【[实例列表](https://console.cloud.tencent.com/ecm/instance)】，进入“实例列表”页面。
3. 在“实例列表”页面中，选择需重新配置安全组边缘实例所在行右侧的【更多】>【配置安全组】。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/3cfceaf09f76d40714817500f28590e1.png)
即可跳转至实例管理页【安全组】页签，进行安全组绑定。
4. 在【安全组】页签的“已绑定安全组”，单击【绑定】。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/e1315a21532dca1d02b5a4444e07eb35.png)
5. 在弹出的“配置安全组”窗口中，根据实际需求勾选需要绑定的安全组，单击【确定】即可完成绑定。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/cf0f907e1b576eb474d8985c2eb4738f.png)

