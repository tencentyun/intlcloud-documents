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


## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 上传时使用图片处理

下面示例展示了如何在上传图片时自动实现图片处理。

图片上传完成后，COS 会存储原始图片和已处理过的图片。后续用户可以通过普通的下载请求获取处理结果。

#### 示例代码

[//]: # ".cssg-snippet-upload-with-pic-operation"
```cs
PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);

JObject o = new JObject();
// 不返回原图
o["is_pic_info"] = 0;
JArray rules = new JArray();
JObject rule = new JObject();
rule["bucket"] = bucket;
rule["fileid"] = "desample_photo.jpg";
//处理参数
rule["rule"] = "imageMogr2/thumbnail/400x400";
rules.Add(rule);
o["rules"] = rules;

string ruleString = o.ToString(Formatting.None);
request.SetRequestHeader("Pic-Operations", ruleString);
//执行请求
PutObjectResult result = cosXml.PutObject(request);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs) 查看。


## 对云上数据进行图片处理

下面示例展示了如何在对已存储在 COS 的图片进行相应处理操作，并将结果存入到 COS。

#### 示例代码

[//]: # ".cssg-snippet-process-with-pic-operation"
```cs
JObject o = new JObject();
// 不返回原图
o["is_pic_info"] = 0;
JArray rules = new JArray();
JObject rule = new JObject();
rule["bucket"] = bucket;
rule["fileid"] = "desample_photo.jpg";
//处理参数
rule["rule"] = "imageMogr2/thumbnail/400x400";
rules.Add(rule);
o["rules"] = rules;
string ruleString = o.ToString(Formatting.None);

ImageProcessRequest request = new ImageProcessRequest(bucket, key, ruleString);
ImageProcessResult result = cosXml.ImageProcess(request);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs) 查看。
