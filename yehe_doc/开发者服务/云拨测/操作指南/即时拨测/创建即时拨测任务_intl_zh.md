本文将为您介绍如何新建单次拨测任务。

## 操作步骤
1. 登录 [云拨测控制台](https://console.cloud.tencent.com/cat/probe/tasklist)。
2. 在左侧菜单栏中单击 **即时拨测**。
3. 单击任务列表页面上方的 **新建任务**。配置基本信息：
 - 选择拨测任务类型：即时拨测仅支持网络质量、页面性能、文件下载三个任务类型。
 - 选择已创建的定时拨测任务地址或输入新的拨测地址。
4. 拨测参数配置为选填项，可参见下列文档进行配置：
 - [新建网络质量任务类型](https://www.tencentcloud.com/document/product/1169/51995)。
 - [新建页面性能任务类型](https://www.tencentcloud.com/document/product/1169/51995)。
 - [新建文件下载任务类型](https://www.tencentcloud.com/document/product/1169/51995)。
5. 配置完后单击 **开始测试**。成功创建后将会跳转到即时探测的历史诊断页面。等待1-3分钟后，即可查看拨测数据。
   <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/fX3L919_intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png" width="100%">
> ?即时拨测根据您选择的拨测点，按照 [按量后付费价格计费](https://www.tencentcloud.com/document/product/1169/52032)，不可使用套餐包额度进行抵扣。由于即时拨测为单次拨测，单次计费为： 拨测节点x拨测单价。假设您选择了100个 机房（IDC ）拨测点，机房（IDC ）拨测单价为0.0048美元/次。则单次收费为：0.0048*100=00.48美元。
