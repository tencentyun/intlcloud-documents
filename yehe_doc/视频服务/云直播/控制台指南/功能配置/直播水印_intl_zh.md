云直播提供水印功能，通过直播画面叠加水印图片实现视频防盗效果。本文将向您介绍如何通过控制台创建、绑定、解绑、修改及删除水印模板。
**创建直播水印模板有以下两种方式：**
- 通过云直播控制台创建水印模板，具体操作请参见 [创建水印模板](#Watermark)。
- 通过 API 调用生成水印模板，具体操作请参见  [添加水印](https://intl.cloud.tencent.com/document/product/267/30826)。


## 注意事项
- 模板创建成功后，可在推流域名下进行关联。关联成功后5分钟 - 10分钟生效。
- 控制台的水印模板管理为域名维度，暂时无法取消关联接口创建的规则，如果是通过水印管理接口关联指定流的，则需要通过调用 [删除水印规则](https://intl.cloud.tencent.com/document/product/267/30823) 解除关联。
- 模板绑定、修改和解绑均只影响更新后的直播流，已经在直播中的流不会受影响；直播中的流需要断流重推才会使用新的规则。


## 前提条件

已开通腾讯云直播服务，并添加 [推流域名](https://intl.cloud.tencent.com/document/product/267/35970)。

<span id="Watermark"></span>
## 创建水印模板

1. 登录云直播控制台，进入【功能配置】>[【直播水印】](https://console.cloud.tencent.com/live/config/watermark)。
2. 单击【创建水印模板】，进入水印模板创建页。
3. 填写水印名称，仅支持填写中文、英文、数字、_、-，不超过30个字符。
4. 单击【选择图片】上传水印图片。
>! 为了最佳视觉效果，水印应为透明图片 png 格式；图片大小小于2M。
5. 设置水印图片显示位置，可通过以下两种方式进行调节：
  - 在水印图片配置栏上拖动图片位置。
  - 设置位置显示 X 轴方向和 Y 轴方向。
6. 单击【保存】即可。
![](https://main.qcloudimg.com/raw/aea9634d78972f2f72fd2c4c74d90f35.png)

<span id="conect"></span>
## 关联域名
1. 登录云直播控制台，进入【功能配置】>[【直播水印】](https://console.cloud.tencent.com/live/config/watermark)。
2. 通过以下方式进入域名绑定窗口。
  - **直接关联域名**：点击左上方的【绑定域名】。
![](https://main.qcloudimg.com/raw/f28cd640fdd290b2c2ee60a1669860ac.png)
  -  **新水印模板创建成功后关联域名**：[水印模板创建](#Watermark) 成功后，单击提醒框中的【去绑定域名】。
![](https://main.qcloudimg.com/raw/ea00262e98e51ebdf0d92d99d23c8a2d.png)
3. 在域名绑定窗口中，选择您需绑定的**水印模板**及**推流域名**，单击【确定】即可绑定成功。
![](https://main.qcloudimg.com/raw/e8197d5a79656a0692b0d5f9e84191da.png)
>? 支持通过单击【添加】为当前模板绑定多个推流域名。

<span id="untie"></span>
## 解除绑定
1. 登录云直播控制台，进入【功能配置】>[【直播水印】](https://console.cloud.tencent.com/live/config/watermark)。
2. 选择已关联域名的水印模板，单击【解绑】。
    ![](https://main.qcloudimg.com/raw/7c1b81f6df67607321355d654f3f9eec.png)
3. 确认是否解绑当前关联域名，单击【确定】即可解绑。
    ![](https://main.qcloudimg.com/raw/3b845efa0aae58546955a2bd06841eca.png)

<span id="change"></span>
## 修改模板

1. 进入【功能配置】>[【直播水印】](https://console.cloud.tencent.com/live/config/watermark)。
2. 选择您已创建成功的水印模板，并单击右侧的【编辑】，即可进入修改模板信息。
3. 单击【保存】即可。

![](https://main.qcloudimg.com/raw/7a8c0d24f6d813244b4f4d1b5a333f87.png)

>? 若您需查看水印模板在画面上的效果，可单击【预览】查看。

<span id="delete"></span>
## 删除模板
若模板已被关联，需要先解绑模板，才可以进行删除操作，具体解绑操作请参见 [解除绑定](#untie)。
1. 进入【功能配置】>[【直播水印】](https://console.cloud.tencent.com/live/config/watermark)。
2. 选择您已创建成功的水印模板，单击右上方的【删除】。
3. 确认是否删除当前水印模板，单击【确定】即可成功删除。

![](https://qcloudimg.tencent-cloud.cn/raw/7a405987e7494de1f4551b3e90d00408.png)

## 相关操作
**域名维度绑定**和**解绑**水印模板的具体操作及相关说明，请参见 [水印配置](https://intl.cloud.tencent.com/document/product/267/31064)。

