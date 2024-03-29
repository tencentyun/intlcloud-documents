## 简介

腾讯云对象存储 COS 集成了 [数据万象](https://intl.cloud.tencent.com/document/product/1045)（Cloud Infinite，CI）专业的一体化多媒体解决方案，涵盖以下图片处理功能，详情可见 [图片处理概述](https://intl.cloud.tencent.com/document/product/436/35280)。

<table>
   <tr>
      <th>服务</td>
      <th>功能</td>
      <th>说明</td>
   </tr>
   <tr>
      <td rowspan=12>基础图片处理服务</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">缩放</a></td>
      <td>等比缩放、设定目标宽高缩放等多种方式</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">裁剪</a></td>
      <td>普通裁剪、缩放裁剪、内切圆、人脸智能裁剪</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">旋转</a></td>
      <td>自适应旋转、普通旋转</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">格式转换</a></td>
      <td>格式转换、GIF 格式优化、渐进显示</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">质量变换</a></td>
      <td>针对 JPG 和 WEBP 图片进行质量变换</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">高斯模糊</a></td>
      <td>对图片进行模糊处理</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">锐化</a></td>
      <td>对图片进行锐化处理</td>
   </tr>
   <tr>
      <td>添加水印</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">图片水印</a>、<a href="https://intl.cloud.tencent.com/document/product/436/36374">文字水印</a></td>
   </tr>
   <tr>
      <td>获取图片信息</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">基本信息</a>、<a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF 信息</a>、<a href="https://intl.cloud.tencent.com/document/product/436/36377">主色调</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">去除元信息</a></td>
      <td>包括 EXIF 信息</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">快速缩略模板</a></td>
      <td>快速实现图片格式转换、缩略、剪裁等功能，生成缩略图</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443">样式设置</a></td>
      <td>设置图片的样式，方便管理不同需求的图片</td>
   </tr>
</table>



## 基础图片处理

### 缩放

#### 功能说明

等比缩放、设定目标宽高缩放等多种方式 。

#### 方法原型

```cpp
CosResult GetObject(const GetObjectByFileReq& request, GetObjectByFileResp* response);
```

#### 请求示例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_file);
// 指定图片的宽高为原图的50%
req.AddParam("imageMogr2/thumbnail/!50p", "");
qcloud_cos::GetObjectByFileResp resp;
qcloud_cos::CosResult result = cos.GetObject(req, &resp);
if (result.IsSucc()) {
   // 调用成功，调用 resp 的成员函数获取返回内容
} else {
   // 调用失败，调用 result 的成员函数获取错误信息
} 
```

#### 参数说明

| 参数 | 参数描述            | 类型                | 是否必填 |
| ---- | ------------------- | ------------------- | -------- |
| req  | GetObject操作的请求 | GetObjectByFileReq  | 是       |
| resp | GetObject操作的响应 | GetObjectByFileResp | 是       |



### 裁剪

#### 功能说明

跟缩放操作方法类似。

