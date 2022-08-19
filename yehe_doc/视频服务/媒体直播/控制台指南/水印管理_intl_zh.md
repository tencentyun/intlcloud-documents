水印功能是指将静态图片或文字叠加到StreamLive的视频输出上。其中，静态图片是指静止不动的图像，仅限PNG或JPG格式。

## 查看水印
点击左侧导航栏中的**Watermark Management**，在页面中可以查看已创建的水印列表，包括水印图片预览、水印文字展示、图像大小、宽高等信息。
![](https://qcloudimg.tencent-cloud.cn/raw/0cd3973c8d34202dff84257a9ae3eddc.png)

## 添加水印
如需添加新的水印，在**Watermark Management**页面，单击**Create Template**按钮，在添加页面进行配置：
![](https://qcloudimg.tencent-cloud.cn/raw/a919f169397bef249904ae88c3a08b23.png)
通用配置：

- **Template Name**：水印模版名称，可输入字符可为数字，大小写字母及下划线，长度限制为16个字符。
- **Watermark Type**：水印类型，可通过下拉列表选择Text Watermark文字水印或Image Watermark静态图片水印。
- **Origin**：水印原始位置，可通过下拉列表分别选择Top Left(左上)、Bottom Left(左下)、Top Right(右上)、Bottom Right(右下)。
- **Vertical Offset**：垂直方向相对于原始位置的偏移量。
- **Horizontal Offset**：水平方向相当于原始位置的偏移量。

### 添加文字水印
- **Watermark Text**：添加文字水印时为必选项，即要叠加在视频上的文字。
- **Front Size**：字体大小。
- **Color**：字体颜色。
![](https://qcloudimg.tencent-cloud.cn/raw/41770c54a01cb9b2eebeaf48c266a981.png)
输入完毕后点击**Confirm**按钮完成创建。

### 添加图片水印
- **Watermark Image**：添加图片水印时为必选项，可点击**Click to upload**进行图片上传或直接将图片拖拽到标记区域。
- **Watermark Size**：水印图片相对于视频输出的缩放比例，不输入或输入0表示保持水印图片的原始大小不进行缩放。
![](https://qcloudimg.tencent-cloud.cn/raw/0bc5a62b8fbe88edca116802414ae9be.png)
输入完毕后点击**Confirm**按钮完成创建。

## 查找水印
在水印列表页面右上角输入框中，输入水印模版名或水印ID：
![](https://qcloudimg.tencent-cloud.cn/raw/17bba7c53601f53fb2daa46d227146b5.png)

## 编辑水印
在水印列表中选择要编辑的水印，在**Operation**中点击**Edit**按钮即可对水印配置进行再次编辑。注:水印类型不可修改。
![](https://qcloudimg.tencent-cloud.cn/raw/e9485a741dc02eb763022d34e111a2d3.png)

## 删除水印
在水印列表中选择要删除的水印，在**Operation**中点击**Delete**按钮即可删除水印。
![](https://qcloudimg.tencent-cloud.cn/raw/6770bdf42d44e9f2b01d4b880c4ebdca.png)
如果水印已在频道中被使用，则无法进行删除操作。**Template Binding**会显示已绑定的频道数量。
![](https://qcloudimg.tencent-cloud.cn/raw/f5cbff44d5f19a16a721e7d9d5d49933.png)

## 为频道绑定水印
在创建水印模板后，可以在频道管理页面为指定频道绑定水印模板。设置方式：选择需要配置水印的频道，在**Output Group Setting**中开启**Video Watermark**开关，并在**Video Watermark Template**中选择已创建好的水印模板。
![](https://qcloudimg.tencent-cloud.cn/raw/00b231219d0e51cfb4004c018a64ff15.jpg)

>! 配置变更需要在下一次重新直播时才会生效。




