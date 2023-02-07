## 操作场景
本功能适用于站点下函数触发规则的如下操作：  
- 支持站点下函数触发规则的增删改查。  
- 支持快速调整触发规则的优先级，适用于请求 URL 匹配到多个触发规则的情况下快速调整执行位置的顺序，位置在前的触发规则将会执行，位置在后的触发规则将不会执行。  

## 操作介绍 
### 新建触发规则
1. 登录 [边缘安全加速平台](https://console.cloud.tencent.com/edgeone) 控制台，在左侧导航栏中，单击**边缘函数** > **触发配置**。
2. 在触发配置页面，单击规则列表右侧的![](https://qcloudimg.tencent-cloud.cn/raw/03f10b28b4a75b8cc534e433375ed0d2.png)，配置相关参数。<br><img src="https://qcloudimg.tencent-cloud.cn/raw/db4c3d3cbc06081bc5f983a4a86f29a8.png" width=700px>
参数说明  
 - 站点：默认显示当前站点名称。  
 - 描述：非必填项，最多可支持60个字符。  
 - 触发条件：按需选择匹配类型、运算符和值，更多参数详情请参见 [规则引擎](https://intl.cloud.tencent.com/document/product/1145/46151)。
 - 执行函数：下拉选择已创建的函数。  
3. 单击**确定**，即可完成触发规则的新建。    


### 编辑触发规则
1. 在触发配置页面，选择需要修改的规则，单击**编辑**。
![](https://qcloudimg.tencent-cloud.cn/raw/09f759146da6faa18987643891aadd8c.png)
2. 在编辑触发规则对话框中，修改相关参数，单击**确定**即可完成触发规则的编辑。<br><img src="https://qcloudimg.tencent-cloud.cn/raw/9532ef02ef91e6472f8b9f52810a47e2.png" width=700px>


### 查询触发规则
在触发配置页面，单击规则列表右侧的![](https://qcloudimg.tencent-cloud.cn/raw/cc51996cbb1a4eb77dfc9b452a88d7c0.png)，在搜索的输入框中填写规则 ID 的关键词即可完成查询。
![](https://qcloudimg.tencent-cloud.cn/raw/bb46d805f0ffe30dc00ad6478601ea82.png)


### 删除触发规则
1. 在触发配置页面，单击规则列表右侧的![](https://qcloudimg.tencent-cloud.cn/raw/341a70c7c6f3c3770463fa7a3ef7c101.png)图标。
2. 选择需要删除的规则，单击![](https://qcloudimg.tencent-cloud.cn/raw/00b18e737c0759a826082e59ea95d5ad.png)图标。
![](https://qcloudimg.tencent-cloud.cn/raw/6d86865dea1667ba79dc18085c444e93.png)
3. 在确认删除对话框中，单击**确认删除**，即可完成触发规则的删除。
![](https://qcloudimg.tencent-cloud.cn/raw/f8d06b6e97d5485860acf2c901dc0599.png)


### 触发规则优先级调整
1. 在触发配置页面，单击规则列表右侧的![](https://qcloudimg.tencent-cloud.cn/raw/341a70c7c6f3c3770463fa7a3ef7c101.png)图标。
2. 选择需要调整的规则，单击![](https://qcloudimg.tencent-cloud.cn/raw/d07f725689d5f191c101504e40bea070.png)上移规则或![](https://qcloudimg.tencent-cloud.cn/raw/993e3ac84f60d1bec83bbeb2d2161ab1.png)下移规则，单击**保存**即可完成优先级调整。
>?若请求 URL 匹配到多个触发规则的情况下（如x下图序号为01和02的触发规则）位置在前的触发规则将会执行（如下图序号01规则），位置在后的触发规则将不会执行（如下图序号02规则）。

![](https://qcloudimg.tencent-cloud.cn/raw/83b800971fa64e3b8acb21dae46baeee.png)

