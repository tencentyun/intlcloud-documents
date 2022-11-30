本 SDK 主要功能在于提供给您快速、安全地接入 [Web 美颜特效](https://www.tencentcloud.com/document/product/1143/51226)，并使用所有功能。

## 流程说明
SDK 实现了简洁低侵入性的接口提供接入，您只需要初始化实例，将渲染节点添加到自己的页面即可快速实现 **Web 美颜特效**功能。
<img src="https://qcloudimg.tencent-cloud.cn/raw/a691e17a2a028c9fa00a92f37091465b.jpg" style="zoom:50%;" />

## 安装
本 SDK 使用 npm 包提供 Web 端的 SDK。
```
npm install tencentcloud-webar
```

## 接入 SDK

- Web 端我们提供了内置 Camera 与自定义流两种初始化方式。
	- [内置相机与播放器](https://intl.cloud.tencent.com/document/product/1143/50101)：使用了内置的摄像头与播放器封装，调用简单迅速，交互功能丰富。
	- [自定义流接入](https://intl.cloud.tencent.com/document/product/1143/50102)：适用于有自己维护媒体流的需求或者要求更高的灵活性与可控性的场景。

## 设置美颜和特效
详情可参见 [设置美颜和特效](https://intl.cloud.tencent.com/document/product/1143/50104)。

## 人像分割（0.2.0版本新增）
开启人像分割可以支持设置背景功能，仅在 Web 端支持，详情请参见 [使用人像分割](https://intl.cloud.tencent.com/document/product/1143/50105)。

## 3D特效（0.3.0版本新增）
支持Web 端，调用方式同设置特效一致，详情请参见 [设置美颜和特效](https://www.tencentcloud.com/document/product/1143/50104)。

## Animoji 表情与虚拟形象（0.3.0版本新增）
依赖 WebGL2 运行环境，目前仅支持 Web 端，详情请参见 [使用表情和虚拟形象](https://www.tencentcloud.com/document/product/1143/51231)。


## 参数与方法说明
请参见 [参数与方法](https://intl.cloud.tencent.com/document/product/1143/50106)。

## 兼容性处理

| 浏览器   | 支持平台 |
| -----   | --- |
| Chrome  | 桌面端、Android、iOS |
| Safari  | 桌面端、iOS |
| FireFox | 桌面端、Android、iOS |
| QQ webview | Android |
| 微信 webview | Android/iOS 微信8.0.16以上|


>? **SDK 0.2.1 版本新增硬件加速检测功能：**
Web 端美颜 SDK 需要浏览器支持并开启硬件加速才能够流畅渲染，因此 SDK 提供了检测方法供业务提前判断，如不支持则进行屏蔽处理。
```javascript
import {ArSdk, isWebGLSupported} from 'tencentcloud-webar'

if(isWebGLSupported()) {
	const sdk = new ArSdk({
		...
	})
} else {
	// 屏蔽逻辑
}
```
