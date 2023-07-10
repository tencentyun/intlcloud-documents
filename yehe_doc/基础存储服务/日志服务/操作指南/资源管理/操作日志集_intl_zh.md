本文档主要介绍如何通过控制台操作日志集。

## 新增日志集

1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls)，在左侧导航栏中单击【日志集管理】。
2. 进入日志集管理页面，选择日志集的地域。
>
> - 若收集云服务器或其他云产品日志，日志服务地域建议选择相同地域。
> - 日志集一旦创建，地域属性将无法修改。
3. 单击【创建日志集】，在弹出的创建日志集窗口中，填写相关信息：
	- 日志集名称：例如 project_test。
	- 保存时间：支持保存3 - 90天。（若需更长保存时间，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们）
    ![](https://main.qcloudimg.com/raw/4e5da331257c6df2f7a981bcd31b4229.png)
4. 单击【确定】，即可创建日志集。



## 删除日志集

1. 进入 [日志集管理](https://console.cloud.tencent.com/cls/logset) 页面。
2. 找到您需要删除的日志集，在其右侧操作栏中，单击【删除】。
>删除日志集之前，需清空所包含的全部日志主题。
>![](https://main.qcloudimg.com/raw/8fe145e4a6ad7ec126352e50f7c1619d.png)
3. 在弹出的确认删除窗口中，单击【确定删除】，即可删除该日志集。
   ![](https://main.qcloudimg.com/raw/09032e04fe4e6fdb2432306ce140f937.png)





## 更新日志集名称

1. 进入 [日志集管理](https://console.cloud.tencent.com/cls/logset) 页面。
2. 找到您需要更新名称的日志集，在其右侧操作栏中，单击【查看】，进入日志集详情页面。
3. 进入日志集详情后，如果需要编辑日志集信息，可单击基本信息右侧的【编辑】。
   ![](https://main.qcloudimg.com/raw/e8c49e75c44c8a9dbd83323d05fecde6.png)
4. 进入编辑状态后，修改日志集信息，最后单击【保存】，即可更新日志集信息。
   ![](https://main.qcloudimg.com/raw/41fd0e8a08ba9cdbe37751e835b1a4ef.png)

