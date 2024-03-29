## 简介
盲水印是数据万象推出的特殊水印服务，能够将水印图以**不可见形式**添加至图像频域，在图片被攻击后仍可进行水印图提取，进行鉴权追责。

数据万象提供的盲水印功能拥有半盲水印、全盲水印和文字盲水印三种类型：

| 水印类型          | 特性                                      | 适用场景                |
| ----------------- | ----------------------------------------- | ----------------------- |
| 半盲水印（type1） | 抗攻击性强，但提取水印需原图              | 小图（640px x 640px以下）使用 |
| 全盲水印（type2） | 提取方便，提取水印仅需水印图，无需对比原图 | 批量添加，批量校验      |
| 文字盲水印（type3） | 可直接将文字信息添加至图片中              | 终端信息添加            |




## 操作步骤
1.  登录 [数据万象控制台](https://console.cloud.tencent.com/ci/bucket)。
2.  在左侧导航栏中，单击**存储桶管理**，进入存储桶管理页面。
3.  选择图片所存放的存储桶，进入相应存储桶管理页面。
4.  在左侧导航栏中，单击**图片处理**。
5.  找到**盲水印**配置项，单击**编辑**，将状态修改为“开启”状态。
6.  单击**保存**，即可开启盲水印功能。
开启功能后，您可使用 [API 接口](https://intl.cloud.tencent.com/document/product/1045/43029) 在 [上传图片时添加](https://intl.cloud.tencent.com/document/product/1045/43029) 盲水印或 [对云上的图片进行添加](https://intl.cloud.tencent.com/document/product/1045/33695)，此外您也可以在 [下载时添加](https://intl.cloud.tencent.com/document/product/1045/43029) 盲水印。当您需要检测图片时，您可直接使用提取接口进行盲水印提取。

>? 盲水印为付费服务，具体费用请参见 [计费与定价](https://intl.cloud.tencent.com/document/product/1045/33431)。数据万象在每个账户在首次产生该服务用量后，将发放一个用量为6000次，有效期为2个月的免费额度资源包，超出用量或资源包到期后将正常计费。
>

