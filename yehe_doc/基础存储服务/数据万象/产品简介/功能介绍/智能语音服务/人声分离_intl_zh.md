## 简介

人声分离能够将同一素材中的人声与背景音分离开来生成新的独立音频文件，便于您后续对剥离了伴奏、杂音的素材做其他风格的艺术加工。

## 适用场景

#### 后期混音

针对分离后的人声、背景音、伴奏等做变声、混音等多种风格艺术加工。

#### 影视综宣发

针对不同用户兴趣取向，快速分离人声叠加所需 BGM 背景声进行素材混剪。

## 使用方法

您可通过任务或工作流方式使用人声分离转码功能。为了提高效率，减少用户的重复操作，数据万象推出了模板功能，模板是任务及工作流中的一个配置项。您可将常用参数组合保存为模板，在后续操作中直接复用模板，无需在每次开启任务时重新设定参数，从而提高操作效率。您可自定义人声分离模板：

自定义模板：您可通过 [控制台方式](https://intl.cloud.tencent.com/document/product/1045/43606) 创建模板，或通过 API 方式 [创建](https://intl.cloud.tencent.com/document/product/1045/49916) 、[修改](https://intl.cloud.tencent.com/document/product/1045/49930) 、[查找](https://intl.cloud.tencent.com/document/product/1045/49919) 、[删除](https://intl.cloud.tencent.com/document/product/1045/49918) 模板。


### 通过任务方式

对于存储在对象存储上的存量数据，您可通过创建任务来实现人声分离。人声分离任务您可选择控制台或 API 进行创建。

- 控制台方式：您可使用数据万象控制台，可视化创建任务，使用详情请见 [人声分离任务文档](https://intl.cloud.tencent.com/document/product/1045/43605)。
- API 方式：您可使用 API 接口创建人声分离任务，使用详情请见 [API 文档](https://intl.cloud.tencent.com/document/product/1045/48946)。


### 通过工作流方式

数据万象提供工作流服务，您可选择对某一存储桶或特定路径开启工作流，开启后上传至该存储桶或路径的文件将自动进行人声分离操作，并将分离后的音频文件保存在指定位置。

#### 创建工作流

您可使用数据万象控制台创建工作流，详情请见 [工作流文档](https://intl.cloud.tencent.com/document/product/1045/43604)。

#### 删除、查询、搜索工作流

您可使用 API 接口进行 [删除工作流](https://intl.cloud.tencent.com/document/product/1045/43734)、[查询工作流](https://intl.cloud.tencent.com/document/product/1045/50339)、[测试工作流](https://intl.cloud.tencent.com/document/product/1045/50340) 操作。
