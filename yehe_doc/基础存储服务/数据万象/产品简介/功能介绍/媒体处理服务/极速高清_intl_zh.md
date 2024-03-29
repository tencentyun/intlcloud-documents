## 简介

极速高清集成了画质修复与增强、内容自适应参数选择、V265编码器等一整套视频处理解决方案。提供让视频更小更清晰的转码方式，能够保证网络资源低消耗，同时带给用户更佳的视觉体验。

>?
> - 若文件类型为视频，则支持在转码过程中同时为视频添加水印，使用详情请查看 [视频水印](https://intl.cloud.tencent.com/document/product/1045/43606) 文档。
> - 极速高清、音视频转码均含有 HDR to SDR 变换功能，HDR to SDR 变换功能可将高动态范围视频（High-Dynamic Range）转换为标准动态范围视频（Standard Dynamic Range），数据万象根据视频场景来改变动态范围下变换策略，使变换后视频的画面细节最大程度贴近原视频。
> 

## 适用场景

#### 画质提升

数据万象能够提升视频的主观画质，在集成了可选择的内容自适应参数、V265编码器等一整套视频处理解决方案的基础上让视频更小更清晰，保证网络资源低消耗，同时带给用户更佳的视觉体验。

#### 节省空间和流量

针对图片等媒体资源，极速高清转码功能可降低码率提升画质，并提供多样的压缩功能以提高压缩效率、减小文件体积与带宽压力，从而减少卡顿并节省存储空间和流量费用。

## 使用方法

您可通过任务或工作流方式使用极速高清转码功能。为了提高效率，减少用户的重复操作，数据万象推出了模板功能，模板是任务及工作流中的一个配置项。您可将常用参数组合保存为模板，在后续操作中直接复用模板，无需在每次开启任务时重新设定参数，从而提高操作效率。您可自定义极速高清模板：

自定义模板：您可通过 [控制台方式](https://intl.cloud.tencent.com/document/product/1045/43606) 创建模板，或通过 API 方式 [创建](https://intl.cloud.tencent.com/document/product/1045/49908) 、[修改](https://intl.cloud.tencent.com/document/product/1045/49922) 、[查找](https://intl.cloud.tencent.com/document/product/1045/49919) 、[删除](https://intl.cloud.tencent.com/document/product/1045/49918) 模板。


### 通过任务方式

对于存储在对象存储上的存量数据，您可通过创建任务来实现极速高清转码。极速高清转码任务您可选择控制台或 API 进行创建。

- 控制台方式：您可使用数据万象控制台，可视化创建任务，使用详情请见 [极速高清转码任务文档](https://intl.cloud.tencent.com/document/product/1045/43605)。
>? 您可通过在音视频转码或极速高清转码模板中的高级设置选项打开 HDR to SDR 开关。
>
- API 方式：您可使用 API 接口创建极速高清转码任务，使用详情请见 [API 文档](https://intl.cloud.tencent.com/document/product/1045/48935)。
>? 您可使用 API 接口创建转码模板，在转码模板中打开 HDR to SDR 开关，使用详情请见 [API 文档](https://intl.cloud.tencent.com/document/product/1045/49912)。
>

### 通过工作流方式

数据万象提供工作流服务，您可选择对某一存储桶或特定路径开启工作流，开启后上传至该存储桶或路径的文件将自动进行转码操作，并将转码后的文件保存在指定位置。

#### 创建工作流

您可使用数据万象控制台创建工作流，详情请见 [工作流文档](https://intl.cloud.tencent.com/document/product/1045/43604)。

#### API 创建、删除、查询、更新工作流

您可使用 API 接口进行 [创建工作流](https://intl.cloud.tencent.com/document/product/1045/43733)、[删除工作流](https://intl.cloud.tencent.com/document/product/1045/43734)、[查询工作流](https://intl.cloud.tencent.com/document/product/1045/50339)、[更新工作流](https://intl.cloud.tencent.com/document/product/1045/43738) 操作。

