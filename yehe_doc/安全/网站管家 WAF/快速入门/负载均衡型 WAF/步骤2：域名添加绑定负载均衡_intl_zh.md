本文档将指导您如何在 Web 应用防火墙控制台中，进行域名添加绑定负载均衡。
## 操作步骤

1. 登录 [Web 应用防火墙控制台](https://console.intl.cloud.tencent.com/guanjia)，在左侧导航栏中，选择【实例管理】>【实例列表】>【负载均衡型】，进入负载均衡型防护设置页面。
2. 在负载均衡型防护设置页面，选择需要添加域名的实例，单击【域名接入】，进入域名接入页面。
![](https://main.qcloudimg.com/raw/bb237d6a08bb25c4b25c1cde17145598.png)
3. 在域名接入页面左侧，单击【添加域名】，填写需要防护域名，填写完成后，单击【下一步】，进入选择监听器页面。
>填写的域名需要和负载均衡监听器中添加的域名保持一致。
>
![](https://main.qcloudimg.com/raw/868d3f6f9cdae3f08147cf88c7f2b0fa.png)
4. 在选择监听器页面，选择 [步骤1：确认负载均衡配置](https://intl.cloud.tencent.com/zh/document/product/627/34719) 中确认配置的地域和负载均衡监听器，完成绑定。
![](https://main.qcloudimg.com/raw/27b2fe447eee3f72f0fbd2ade23726ca.png)
5. 绑定完成后，在页面下方，单击【完成】即可返回域名列表。在域名列表可以查看到防护域名`wow.qcloudwaf.com`和负载均衡的负载均衡 ID、名称、VIP 和监听器信息等。
![](https://main.qcloudimg.com/raw/a6d7c75770afc3e66667e2de7c7cb2c2.png)
## 后续步骤
当您完成域名添加绑定负载均衡后，可执行 [步骤3：验证测试](https://cloud.tencent.com/document/product/627/40767)。
