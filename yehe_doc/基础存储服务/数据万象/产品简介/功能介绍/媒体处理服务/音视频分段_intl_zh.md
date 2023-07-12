## 简介

音视频分段可按指定时长将音视频切分为若干片段，以提升您后期操作的效率，在分段时您还可以改变音视频片段的容器格式。

>? 使用音视频分段功能时，若仅分段，则不收费。如果改变封装格式，则需收取转封装费用，费用隶属于音视频转码中的转封装计费项，按照输出文件时长进行计费，详情请参见 [媒体处理费用](https://intl.cloud.tencent.com/document/product/1045/49489)。
>

## 适用场景

数据万象音视频分段功能适用于大媒体文件切分场景。

## 使用方法

您可通过任务或工作流方式使用音视频分段功能。

### 通过任务方式

对于存储在对象存储（Cloud Object Storage，COS）上的存量数据，您可选择控制台或 API 方式创建音视频分段任务。

#### 创建任务

- 控制台方式：您可使用数据万象控制台，可视化创建任务，使用详情请参见 [创建音视频分段任务](https://intl.cloud.tencent.com/document/product/1045/43605)。
- API 方式：您可使用 API 接口创建音视频分段任务，使用详情请参见 [API 文档](https://intl.cloud.tencent.com/document/product/1045/48936)。

#### 删除、查询、搜索任务

您可使用 API 接口方式进行 [删除](https://intl.cloud.tencent.com/document/product/1045/49512) 任务、[查询](https://intl.cloud.tencent.com/document/product/1045/50355) 任务信息、[搜索](https://intl.cloud.tencent.com/document/product/1045/50356) 指定条件下的任务操作。

### 通过工作流方式

数据万象提供工作流服务，您可选择对某一存储桶或特定路径开启工作流，开启后上传至该存储桶或路径的文件将自动进行音视频分段操作，并将音视频片段保存在指定位置。

#### 创建工作流

您可使用数据万象控制台创建工作流，详情请参见 [创建工作流文档](https://intl.cloud.tencent.com/document/product/1045/43604)。

#### API 创建、删除、查询、更新工作流

您可使用 API 接口进行 [创建工作流](https://intl.cloud.tencent.com/document/product/1045/43733)、[删除工作流](https://intl.cloud.tencent.com/document/product/1045/43734)、[查询工作流](https://intl.cloud.tencent.com/document/product/1045/50339)、[更新工作流](https://intl.cloud.tencent.com/document/product/1045/43738) 操作。
