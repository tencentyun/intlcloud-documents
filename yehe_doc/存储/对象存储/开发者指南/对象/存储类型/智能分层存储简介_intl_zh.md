## 简介

智能分层存储类型为数据提供了冷热分层机制，能够根据用户数据的访问模式，自动地转换数据的冷热层级，从而降低用户数据的存储成本。

智能分层存储适用于访问模式不固定或者无法预估访问模式的数据，为用户提供了与标准存储一致的低延迟和高吞吐的产品体验，但成本上则低于标准存储。用户可以按照自身业务需求，将访问模式不固定的数据从标准存储类型转换为智能分层存储类型，降低云上存储成本。

> !
> - 智能分层存储类型当前仅支持北京、上海、广州、重庆、东京地域。
> - 智能分层存储类型为独立的存储类型，使用时将产生智能分层存储容量费用，您可以选择智能分层存储容量包进行抵扣。更多计费信息请参见 [产品定价](https://buy.cloud.tencent.com/price/cos)。

## 优势

当用户上传数据时选择以智能分层存储类型存放到 COS，COS 将周期性地监测数据访问次数，在持续一段时间没有数据访问时，将数据转移至存储成本更低的访问层。如果数据重新被访问，则会被重新转移到高频访问层上，保障数据读取性能。通过数据冷热分层存储，智能分层能够帮助用户在存储成本和读写性能之间寻找平衡点。使用智能分层存储具有以下优势：

- **成本集约**：当数据持久化存储为智能分层存储类型时，存储时间越长，则相较存储于标准存储的成本越低，最多可节约20%左右的存储成本。智能分层存储类型还参与对象存储生命周期流程，用户可以按需将智能分层存储沉降到归档存储中，进一步降低数据存储成本。
- **稳定持久**：智能分层存储提供与标准存储一致的低时延和高吞吐体验。同时，智能分层存储采用纠删码冗余存储的方式，提供了高达99.999999999%（11个9）的数据可靠性；数据分块存储，并发读写，提供高达99.95%的业务可用性。多 AZ 架构已同步智能分层特性，数据设计可靠性可高达12个9，业务设计可用性可高达99.995%。
- **便捷易用**：只需为数据指定对象存储类型，即可应用智能分层存储特性。智能分层存储作为一种存储类型，天然适配 COS 的 API、SDK、工具以及生态应用，方便用户按需管理存储在云上的数据。

## 使用方法

将数据以智能分层存储类型存放到 COS，首先需要为存储桶开启智能分层配置。开启后，用户在上传对象时将**存储类型**指定为智能分层存储类型即可。

### 使用对象存储控制台

#### 上传对象时设置为智能分层存储

用户可以参照以下步骤将对象保存为智能分层存储类型：

1. 在存储桶配置页面，开启智能分层存储配置，详细流程可参见 [设置智能分层存储](https://intl.cloud.tencent.com/document/product/436/38306) 文档。
2. 上传文件，并在上传时指定文件存储类型。文件的上传指引可参见 [上传对象](https://intl.cloud.tencent.com/document/product/436/13321) 文档。

> !存储桶的智能分层存储配置开启后，将无法关闭，请谨慎配置。

#### 将云上数据转换为智能分层

用户可以参照以下步骤将已上传的存量数据转换为智能分层存储类型：

1. 在存储桶配置页面，创建生命周期规则，详细流程可参见 [设置生命周期](https://intl.cloud.tencent.com/document/product/436/14605) 文档。
2. 设置指定的规则应用范围，将数据沉降为智能分层存储。



### 使用 REST API

您可以直接通过以下 API 配置智能分层存储：

1. 首先使用 REST API 为存储桶开启智能分层存储，请参见以下 API 文档：
	- [PUT Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38314)
	- [GET Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38315)
2. 存储桶开启智能分层存储，您可以参见以下 API 文档，将对象上传为智能分层存储类型：
	- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
	- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
	- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)
	- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
3. 如需查询对象的存储类型和所处的存储层，请参见以下 API 文档：
	- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
	- [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)
4. 您可以直接使用 REST API 删除智能分层存储类型的对象，请参见以下 API 文档部分：
	- [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)
	- [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)

### 使用 SDK

当前 COS 所发布的 SDK 都支持使用智能分层存储类型，具体方法是在文件上传时，将 StorageClass 参数设置为 INTELLIGENT_TIERING，实现直传智能分层存储。详情请参见 [SDK 概览](https://intl.cloud.tencent.com/document/product/436/6474)。



## 使用限制

使用智能分层存储存在以下限制：

- **配置限制**：首次配置后不可更改，如需更改，请 [联系我们](https://intl.cloud.tencent.com/contact-sales)。
- **初始存储层限制**：智能分层存储类型的新增对象，默认处于高频访问层；持续一段时间无访问后才会转换至低频访问层。
- **最短存储时间限制**：智能分层存储类型的对象，最短存储时间为30天；低于30天则按照30天收费。
- **最小存储单元限制**：小于64KB的对象只能持久存储于高频访问层中，不会在高频访问层和低频访问层之间转换。
- **操作限制**：不支持通过追加上传接口将对象上传为智能分层存储类型。
- **生命周期限制**：智能分层存储类型仅可转换为归档存储或者深度归档存储类型。标准存储类型沉降为智能分层存储类型时，将存储在高频访问层；低频存储类型沉降为智能分层存储类型时，将存储在低频存储访问层。
- **存储桶复制限制**：存储桶复制时，如果目标存储桶未开启智能分层存储配置，则无法将对象复制为智能分层存储类型。
