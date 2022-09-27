## 简介

数据万象智能封面功能集成了腾讯云音视频实验室先进的 AI 技术，通过对视频内容的理解，智能分析视频帧的质量、精彩程度、内容相关度，提取最优帧生成截图作为封面，提升内容吸引力。

>?
>
>- 智能封面是付费服务，按照视频时长进行计费，具体费用请参见 [媒体处理费用](https://intl.cloud.tencent.com/document/product/1045/49489)。
>- 每个视频文件将智能分析输出3张最优的关键帧。



## 适用场景

#### 视频平台

传统视频平台视频封面需经过人工浏览视频而后进行筛选，耗费大量人力，延长视频上线时间。数据万象智能封面功能可快速选出最精彩的画面作为封面，节省人力资源，提高视频上新速度。

#### 家庭相册

目前大多数家庭相册的相册轮播仅支持图片轮播，针对智能相册中的视频格式文件，可利用智能封面功能自动提取相册封面进行轮播展示，从而增加家庭相册的丰富度和使用率。

## 使用方法

### 工作流

数据万象提供工作流服务，可在视频上传时自动进行处理，并将处理结果保存在指定位置。

#### 创建工作流

您可使用数据万象控制台创建工作流，详情请见 [创建工作流](https://intl.cloud.tencent.com/document/product/1045/43604) 控制台文档。

#### API 创建、删除、查询、更新工作流

您可使用 API 接口进行 [创建工作流](https://intl.cloud.tencent.com/document/product/1045/43733)、[删除工作流](https://intl.cloud.tencent.com/document/product/1045/43734)、[查询工作流](https://intl.cloud.tencent.com/document/product/1045/50339)、[更新工作流](https://intl.cloud.tencent.com/document/product/1045/43738) 操作。



### 任务

针对存储在对象存储 COS 上的存量数据，您可创建视频转动图任务。

#### 创建任务

- 控制台方式：您可使用 [数据万象控制台](https://console.cloud.tencent.com/ci) 可视化创建任务，详情请见 [智能封面任务文档](https://intl.cloud.tencent.com/document/product/1045/43605)。
- API 方式：您可使用 API 接口，创建智能封面任务，详情请见 [API 文档](https://intl.cloud.tencent.com/document/product/1045/48937)。

#### 删除、查询、搜索任务

您可通过 API 方式对任务进行 [删除](https://intl.cloud.tencent.com/document/product/1045/49512)、[查询](https://intl.cloud.tencent.com/document/product/1045/50355) 任务信息、[搜索](https://intl.cloud.tencent.com/document/product/1045/50356) 指定条件下的任务操作。

