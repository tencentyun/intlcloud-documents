本文为您介绍如何在控制台界面，快速使用腾讯云顾问进行资源巡检。

## 步骤1：登录云顾问控制台[](id:Step1)

登录 [腾讯云云顾问控制台](https://console.qcloud.com/advisor)。


<dx-alert infotype="explain" title="">
如果没有账号，请参考账号 [注册教程](https://www.tencentcloud.com/document/product/378/17985)。
</dx-alert>



## 步骤2：服务授权[](id:Step2)
首次使用时，需要授权腾讯云顾问访问相关云产品配置权限。若您已为云顾问授权，则请跳过该步骤。
在 [服务授权](https://console.qcloud.com/advisor/auth) 页面中启用服务授权，即可完成授权操作。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ed2eff6f1985dafb2522da0e4b21911b.png)


## 步骤3：开始风险评估[](id:Step3)
选择左侧导航栏中的 **[风险评估](https://console.cloud.tencent.com/advisor/assess)**，在“风险评估”页面中单击**开始评估**，后台将进行自动评估。
<dx-alert infotype="explain" title="">
- 系统默认每天自动巡检一次，您可手动触发。
- 每次评估操作时间由云资源规模大小和风险项的数量决定，预计花费数十秒至数十分钟不等的时间，页面会动态刷新评估结果，直到评估完成。
</dx-alert>



## 步骤4：查看评估结果[](id:Step4)
评估完成后，您可在 [风险评估](https://console.cloud.tencent.com/advisor/assess) 页面查看评估结果。


### 整体说明
控制台界面如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/9207f55730067bbdce03e2d0ae63b47f.png)

- **上次评估时间**：最近一次进行评估的时间。
- **颜色标记说明**：红色图标代表“高风险项”，橙色图标代表“中风险项”，绿色图标代表“健康”。
- **总览**：统计并展现所有评估项目结果。
- **安全**：按照 [安全](https://intl.cloud.tencent.com/document/product/1079/41573) 分类统计并展现评估项目结果。
- **可靠**：按照 [可靠](https://intl.cloud.tencent.com/document/product/1079/41573) 分类统计并展现评估项目结果。
- **性能**：按照 [性能](https://intl.cloud.tencent.com/document/product/1079/41573) 分类统计并展现评估项目结果。
- **成本**：按照 [成本](https://intl.cloud.tencent.com/document/product/1079/41573) 分类统计并展现评估项目结果。
- **服务限制**：按照 [服务限制](https://intl.cloud.tencent.com/document/product/1079/41573) 分类统计并展现评估项目结果。

###  风险项明细说明
单击展开风险项，可查看风险项详情。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0453e4ae143e4e74174f4b48c319729d.png)

 - **警告条件**：触发该风险项的告警规则。
 - **优化建议**：建议用户可以采取的措施，来规避该风险项。
 - **资源列表**：本次评估中，存在中高风险项的资源列表。



## 步骤5：下载评估报告[](id:Step5)
您可针对不同模块，或具体风险项生成报告。步骤如下：
1. 进入 [风险评估](https://console.cloud.tencent.com/advisor/assess) 页面，找到模块或具体风险项。单击**生成报告**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/5b5159ae3257e8866ede0e1da2ee723b.png)
2. 报告生成完毕后，单击**下载报告**。
3. 在弹出的“评估报告下载”窗口中，按需选择**评估报告EXCEL版**或**评估报告PDF版**，单击**确定**即可获取报告。


## 步骤6：专家解读评估报告（可选）[](id:Step6)
若您需要腾讯云技术专家为您解读报告，可参考该步骤操作。

1. 服务授权
进入 [服务授权](https://console.qcloud.com/advisor/auth) 页面，开启“报告解读”服务授权，授权腾讯云专家架构师读取评估报告内容。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/c60af511c770de824ab02f8d6163b940.png)
2. 专家解读
参考 [联系我们](https://www.tencentcloud.com/document/product/1079/50825) 联系腾讯云专家架构师，对报告内容进行专业的解读，并提供系统的优化建议。

