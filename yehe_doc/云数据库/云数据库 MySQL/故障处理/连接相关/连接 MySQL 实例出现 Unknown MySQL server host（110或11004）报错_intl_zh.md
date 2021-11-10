## 现象描述
使用外网地址连接云数据库 MySQL 实例时，提示**Unknown MySQL server host**报错信息。
![](https://main.qcloudimg.com/raw/b75b23dd5f306336145dab1719eeb1c7.png)

## 可能原因
外网地址不正确。

## 解决思路
检查实例的外网地址是否已开启、输入是否正确。

## 处理步骤
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，找到目标实例，单击实例 ID，进入实例详情页面。
2. 在实例详情页的**外网地址**处，检查外网地址是否开启。
 - 若是，请执行 [步骤3](#step3)。
 - 若否，请单击**外网地址**处的**开启**开启外网地址，然后执行 [步骤3](#step3)。
 >?
 >- 若有外网地址和外网端口信息，说明已开启外网地址。
 >- 外网地址开启限制，请参见 [连接实例](https://intl.cloud.tencent.com/document/product/236/37788)。
 >
![](https://main.qcloudimg.com/raw/eb085d53fb6f569d763412bba5afcf11.png)
3. [](id:step3)检查客户端输入的外网地址与实例的外网地址是否一致。
 - 若是，请执行 [步骤4](#step4)。
 - 若否，请复制如下截图红框处的**外网地址**，在客户端输入正确的外网地址，然后执行 [步骤4](#step4)。
 ![](https://main.qcloudimg.com/raw/27246f1777099c9e34b8dd26a89693eb.png)
4. [](id:step4)通过 ping 连接外网地址，检查解析是否正常。
 - 若正常，会返回具体网络延迟，故障处理结束。
 - 若不正常，会返回 Unknown host 报错，请[提交工单](https://console.cloud.tencent.com/workorder/category)处理。

