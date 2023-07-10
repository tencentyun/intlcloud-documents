## 简介

音视频拼接可将指定的音频片段拼接在音频文件的开头或结尾，生成一个新的音频文件，或者指定的视频片段拼接在视频文件的开头或结尾，生成一个新的视频文件。
>? 音视频拼接为付费功能，隶属于文件转码计费项，按照输出文件大小进行计费。详情请参见 [媒体处理费用](https://intl.cloud.tencent.com/document/product/1045/49489)。
>



## 适用场景

数据万象音视频拼接功能适用于片头片尾添加、广告营销、视频制作等场景。

## 使用方法

您可通过任务或工作流方式使用音视频拼接功能。为了提高效率，减少用户的重复操作，数据万象推出了模板功能，模板是任务及工作流中的一个配置项。您可将常用参数组合保存为模板，在后续操作中直接复用模板，无需在每次开启任务时重新设定参数，从而提高操作效率。您可自定义音视频拼接模板：
- 自定义模板：您可通过 [控制台方式](https://intl.cloud.tencent.com/document/product/1045/43606) 创建模板，或通过 API 方式 [创建](https://intl.cloud.tencent.com/document/product/1045/49907) 、[修改](https://intl.cloud.tencent.com/document/product/1045/49921)、[查找](https://intl.cloud.tencent.com/document/product/1045/49919)、[删除](https://intl.cloud.tencent.com/document/product/1045/49918) 模板。


### 任务

对于存储在对象存储（Cloud Object Storage，COS）上的存量数据，您可通过任务方式创建音视频拼接任务。

#### 创建任务

- 控制台方式：您可使用数据万象控制台，可视化创建任务，使用详情请参见 [音视频拼接任务文档](https://intl.cloud.tencent.com/document/product/1045/43605)。
-  API 方式：您可使用 API 接口创建音视频拼接任务，使用详情请参见 [API 文档](https://intl.cloud.tencent.com/document/product/1045/48929)。

#### 删除、查询、搜索任务

您可使用 API 接口方式进行 [删除](https://intl.cloud.tencent.com/document/product/1045/49512) 任务、[查询](https://intl.cloud.tencent.com/document/product/1045/50355) 任务信息、[搜索](https://intl.cloud.tencent.com/document/product/1045/50356) 指定条件下的任务操作。

### 工作流

数据万象支持设置媒体工作流，您可以快速、灵活、按需搭建视频处理流程。每个工作流与输入存储桶的一个路径绑定，当视频文件**上传**至该路径时，该媒体工作流就会被**自动触发**，执行指定的处理操作，并将处理结果自动保存至输出存储桶的指定路径下。在工作流中可以设置**音视频拼接**任务、**文件转码**任务、**视频截帧**任务、 **视频转动图**任务和**智能封面**任务。

#### 创建工作流

您可使用数据万象控制台创建工作流，详情请参见 [创建工作流文档](https://intl.cloud.tencent.com/document/product/1045/43604)。

#### API 创建、删除、查询、更新工作流

您可使用 API 接口进行 [创建工作流](https://intl.cloud.tencent.com/document/product/1045/43733)、[删除工作流](https://intl.cloud.tencent.com/document/product/1045/43734)、[查询工作流](https://intl.cloud.tencent.com/document/product/1045/50339)、[更新工作流](https://intl.cloud.tencent.com/document/product/1045/43738) 操作。
