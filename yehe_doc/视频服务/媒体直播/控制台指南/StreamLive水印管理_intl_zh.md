StreamLive提供了为频道添加水印的功能，在StreamLive控制台中的Watermark Management页面，可以添加文字或水印模板。创建好的模板可以在频道管理页面进行配置。
![](https://qcloudimg.tencent-cloud.cn/raw/2be49fa4bd0ee5ec87a5dbb2f1281c3b.jpg)

### 创建水印模板

选择【Watermark Management】菜单，点击【Create Watermark Template】创建频水印模板。

#### 一、创建文字类型水印模板

系统默认选择文字类型水印模板，可以在下拉列表Watermark Type中选择图片类型水印模板。

![](https://qcloudimg.tencent-cloud.cn/raw/d7bc227e5d28378e849ce2a544be957e.jpg)

创建文字模板需要填写水印模板名称（Template Name），并填写需要显示的水印的水印内容（Watermark Text）。水印模板提供设置字体大小（25至50px）和水印颜色的功能。

可以设置水印位置时，需要注意先确定水印的初始位置，再通过垂直偏移（Vertical Offset）和水平偏移（Horizontal Offset）来调整位置细节。

![](https://qcloudimg.tencent-cloud.cn/raw/f05a8121f13d086a2073077188bcbed7.jpg)



#### 二、创建图片类型水印模板

创建图片模板需要填写水印模板名称（Template Name），并上传要显示的水印图片。水印模板提供设置字体大小（25至50px）和水印颜色的功能。

系统要求对水印图片大小进行设置，修改高度或宽度的百分比，将使图片按照对应的比例呈现在画面上。如需要保持当前水印的长宽比，则只调整高度或宽度其中一项，另一项会同比的拉伸/缩放。
![](https://qcloudimg.tencent-cloud.cn/raw/ad8955e56c150811433b4045e488af5e.jpg)

举例：
- 如宽度填写50%高度填写25%，则水印会被拉伸成宽度为整个画面宽度的一半，高度拉伸/缩放为整个画面高度的1/4。
- 如宽度填写50%高度填写0%，则水印会被拉伸成宽度为整个画面宽度的一半，高度会根据水印图片原长宽比变更。

### 为频道绑定水印模板

在创建水印模板后，可以在频道管理页面为指定频道绑定水印模板

![](https://qcloudimg.tencent-cloud.cn/raw/81b30d06e27aa8ab19ec3433356a82bd.jpg)

设置方式：选择需要配置水印的频道，在Output Group Setting中开启水印开关，并选择已创建好的水印模板。
>!  配置变更需要在下一次重新直播时才会生效。

### 管理水印模板

您可随时在水印模板管理页面添加、修改或删除水印模板。

当删除水印模板时，需要确保您已经将所有频道解绑该模板。您可在Template Binding查看水印模板当前绑定的频道，且仅有绑定数量为0时，您才可以删除这个水印模板。
![](https://qcloudimg.tencent-cloud.cn/raw/291d919592bb7c66ef63015bd154c851.jpg)


