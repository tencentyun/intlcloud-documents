## 适用场景

该操作适用于在单个请求中，上传一个大小小于5GB的对象，对于大于5GB的对象，您必须使用 [分块上传](https://intl.cloud.tencent.com/document/product/436/14112) 的方式。

当您的对象较大（例如100MB）时，我们建议您在高带宽或弱网络环境中，优先使用分块上传的方式。

## 使用方法

### 使用对象存储控制台
您可以使用对象存储控制台上传对象，详情请参见 [上传对象](https://intl.cloud.tencent.com/document/product/436/13321) 控制台指南文档。

### 使用 REST API

您可以直接使用 REST API 发起简单上传对象请求，详情请参见 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) API 文档。

### 使用 SDK
您可以直接调用 SDK 的简单上传对象方法，详情请参见下列各语言 SDK 文档：
- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31463#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [C# SDK](https://intl.cloud.tencent.com/document/product/436/32869#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31467#.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A12)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31477#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
