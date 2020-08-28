## 简介

腾讯云对象存储 COS 集成了 [数据万象](https://intl.cloud.tencent.com/document/product/1045)（Cloud Infinite，CI）专业的一体化多媒体解决方案，涵盖图片处理、审核、识别等功能，详见如下表。您可以通过 COS 的上传和处理接口来进行媒体数据的处理操作。

>
> - 图片处理功能仅支持中国公有云地域。
> - 图片处理功能为收费项，由数据万象收取，详细的计费说明请参见数据万象 [计费与定价](https://intl.cloud.tencent.com/document/product/1045/33431)。



<table>
   <tr>
      <th>服务</td>
      <th>功能</td>
      <th>说明</td>
   </tr>
   <tr>
      <td rowspan=12>基础图片处理服务</td>
      <td>缩放</td>
      <td>等比缩放、设定目标宽高缩放等多种方式</td>
   </tr>
   <tr>
      <td>裁剪</td>
      <td>普通裁剪、缩放裁剪、内切圆、人脸智能裁剪</td>
   </tr>
   <tr>
      <td>旋转</td>
      <td>自适应旋转、普通旋转</td>
   </tr>
   <tr>
      <td>格式转换</td>
      <td>格式转换、GIF 格式优化、渐进显示</td>
   </tr>
   <tr>
      <td>质量变换</td>
      <td>针对 JPG 和 WEBP 图片进行质量变换</td>
   </tr>
   <tr>
      <td>高斯模糊</td>
      <td>对图片进行模糊处理</td>
   </tr>
   <tr>
      <td>锐化</td>
      <td>对图片进行锐化处理</td>
   </tr>
   <tr>
      <td>添加水印</td>
      <td>图片水印、文字水印</td>
   </tr>
   <tr>
      <td>获取图片信息</td>
      <td>基本信息、EXIF 信息、主色调</td>
   </tr>
   <tr>
      <td>去除元信息</td>
      <td>包括 EXIF 信息</td>
   </tr>
   <tr>
      <td>快速缩略模板</td>
      <td>快速实现图片格式转换、缩略、剪裁等功能，生成缩略图</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443">样式设置</a></td>
      <td>设置图片的样式，方便管理不同需求的图片</td>
   </tr>
</table>



## 使用方法

#### 使用对象存储控制台

您可以使用对象存储控制台进行图片处理设置，详情请参见 [开启图片处理](https://intl.cloud.tencent.com/document/product/436/35278)。

#### 使用 REST API

您可以通过对象存储提供的 API 进行图片处理设置。

