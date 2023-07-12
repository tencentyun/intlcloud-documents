## 简介

视频截帧为数据万象提供的视频某一时间节点的截图功能，可对截帧开始时间点、截帧间隔、截帧数量、输出图片尺寸、输出格式等进行自定义设置，满足多种截帧需求。视频截帧功能可实现对新上传的视频文件或已上传的视频文件进行截帧。

>? 视频截帧为收费功能。计费详情请查看 [媒体处理费用](https://intl.cloud.tencent.com/document/product/1045/49489)。
>


## 适用场景

数据万象视频截帧功能适用于视频采样、视频特定帧截取、随机截帧等场景。


## 使用方法

您可通过任务和工作流方式分别使用视频截帧功能。为了提高效率，减少用户的重复操作，数据万象推出了模板功能，模板是任务和工作流中的一个配置项。用户可将常用参数组合保存为模板，在后续操作中直接复用模板，无需在每次开启任务时重新设定参数，从而提高操作效率。您可使用系统预设模板或自定义模板：
- 系统预设模板：目前数据万象提供了多种视频截帧的预设模板，覆盖了大部分的截帧需求，您可在 [数据万象控制台](https://console.cloud.tencent.com/ci) 查看所有系统预设模板。
- 自定义模板：您可通过 [控制台方式](https://intl.cloud.tencent.com/document/product/1045/43606) 创建模板，或通过 API 方式 [创建](https://intl.cloud.tencent.com/document/product/1045/49909)、[修改](https://intl.cloud.tencent.com/document/product/1045/49923)、[查找](https://intl.cloud.tencent.com/document/product/1045/49919)、[删除](https://intl.cloud.tencent.com/document/product/1045/49918) 模板。


### 任务

对于存储在对象存储 COS 上的存量数据，您可创建视频截帧任务，进行截帧操作。

- 控制台方式：您可使用数据万象控制台，可视化创建任务，详情请见 [视频截帧任务文档](https://intl.cloud.tencent.com/document/product/1045/43605)。
- API 方式：您可使用 API 接口，创建视频截帧任务，详情请见 [ API 文档](https://intl.cloud.tencent.com/document/product/1045/48938)。


### 工作流

数据万象提供工作流服务，您可选择对某一存储桶或特定路径开启工作流，开启后上传至该存储桶或路径的视频将自动进行截帧操作，并将截帧保存在指定位置。

#### 创建工作流

您可使用数据万象控制台创建工作流，详情请见 [创建工作流文档](https://intl.cloud.tencent.com/document/product/1045/43604)。

#### API 创建、删除、查询、更新工作流

您可使用 API 接口进行 [创建工作流](https://intl.cloud.tencent.com/document/product/1045/43733)、[删除工作流](https://intl.cloud.tencent.com/document/product/1045/43734)、[查询工作流](https://intl.cloud.tencent.com/document/product/1045/50339)、[更新工作流](https://intl.cloud.tencent.com/document/product/1045/43738) 操作。
