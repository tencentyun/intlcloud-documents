

本文档主要介绍如何通过控制台对日志主题进行增删更新等操作。



## 新增日志主题

1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls)，在左侧导航栏中单击【日志集管理】。
2. 找到已创建的日志集，在其右侧操作栏中，单击【查看】，进入日志集详情页面。
3. 单击【新增日志主题】，在新增日志主题窗口中，填写如下相关信息：
	- 日志主题名称：例如：nginx。
	- 主题分区（Partition）数量： 主题分区介绍请参见 [主题分区介绍](https://intl.cloud.tencent.com/document/product/614/33779)，默认新建1个分区。
		![](https://main.qcloudimg.com/raw/79b2a94628f6f42e68104ccefc09a052.png)
4. 单击【确定】，新增日志主题。
5. 日志主题新增成功，将进入日志主题管理页。
   ![](https://main.qcloudimg.com/raw/925a17d45f409d56b7f8d78da99bc1b1.png)

## 删除日志主题

1. 进入 [日志集管理](https://console.cloud.tencent.com/cls/logset/) 页面，单击日志集名称。
2. 找到您需要删除的日志主题，在其右侧操作栏中，单击【删除】。
>日志主题一旦删除，主题配置和日志数据不可恢复，请谨慎操作。
>![](https://main.qcloudimg.com/raw/8486812ce98ed7da7005be687ba230e4.png)
3. 在弹出的确认删除窗口中，单击【确定删除】，即可删除该日志主题。
   ![](https://main.qcloudimg.com/raw/1ac10a1f6f8ef2129bc189eebd5d88f1.png)



## 更新日志主题名称

1. 进入 [日志集管理](https://console.cloud.tencent.com/cls/logset/) 页面，单击日志集名称。
2. 找到您需要删除的日志主题，在其右侧操作栏中，单击【管理】。
3. 进入日志主题详情页，切换到【基本信息】，单击右侧的【编辑】，进入编辑模式。
   ![](https://main.qcloudimg.com/raw/773ad418bf1a29a33b94e0f99a931eb4.png)
   4.修改主题名称，然后单击【保存】，完成编辑日志主题信息。

