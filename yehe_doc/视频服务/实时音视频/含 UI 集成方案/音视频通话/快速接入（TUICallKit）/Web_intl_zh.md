本文将介绍如何用最短的时间完成 TUICallKit 组件的接入，跟随本文档，您将完成如下几个关键步骤，并最终得到一个包含完备 UI 界面的视频通话功能。

若您想体验组件效果，可参考[TUICallKit demo 快速跑通](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)。

在接入前请检查您的桌面浏览器是否支持音视频服务，详细要求可参考[环境要求](https://www.tencentcloud.com/document/product/647/50993#1b83cb8f-4c54-43f3-863d-579786ab78bc)。

[](id:step1)
## 步骤一：开通服务

TUICallKit 是基于腾讯云 [即时通信 IM](https://intl.cloud.tencent.com/document/product/1047/35448) 和 [实时音视频 TRTC](https://intl.cloud.tencent.com/document/product/647/35078) 两项付费 PaaS 服务构建出的音视频通信组件。您可以按照如下步骤开通相关的服务并体验 60 天的免费试用服务：

1. 登录到 [即时通信 IM 控制台](https://console.cloud.tencent.com/im)，单击**创建新应用**，在弹出的对话框中输入您的应用名称，并单击**确定**。
![img](https://qcloudimg.tencent-cloud.cn/raw/ce2e34f7cd1cd14679fc5decffb469af.png)

2. 单击刚刚创建出的应用，进入**基本配置**页面，并在页面的右下角找到**开通腾讯实时音视频服务**功能区，单击下方 音视频通话能力-免费体验 ，在弹出的免费开通音视频通话能力体验版对话框中，单击免费开通，即可开通 TUICallKit 的 60 天免费试用服务。
![img](https://qcloudimg.tencent-cloud.cn/raw/796e49d9f55174aacb62bb8eb848feaf.png)

3. 在同一页面找到 **SDKAppID** 和**密钥**并记录下来，它们会在后续中被用到。
	![img](https://qcloudimg.tencent-cloud.cn/raw/8349ac97b261279606316331488784c3.png)
	- SDKAppID：IM 的应用 ID，用于业务隔离，即不同的 SDKAppID 的通话彼此不能互通；
	- Secretkey：IM 的应用密钥，需要和 SDKAppID 配对使用，用于签出合法使用 IM 服务的鉴权用票据 UserSig，我们会在接下来的步骤五中用到这个 Key。

[](id:step2)
## 步骤二：引入 TUICallKit 组件

1. 从 [GitHub 下载](https://github.com/tencentyun/TUICallKit/tree/main/Web) TUICallKit 源码。复制 `TUICallKit/Web` 文件夹放置到自己到工程的 `src/components` 文件夹中，例如：
![img](https://qcloudimg.tencent-cloud.cn/image/document/b90fbef92c17090688ebc0c9b4577037.png)

1. 进入此文件夹中，安装运行所需依赖
```shell
cd ./src/components/TUICallKit/Web 
yarn                                  // 若当前环境未安装 yarn 包管理工具，可使用 npm install -g yarn 进行安装
```

[](id:step3)
## 步骤三：生成 UserSig

若已生成 UserSig，可跳过本步骤至 [步骤四](#step4)

1. 设置初始化的相关参数，其中 SDKAppID 和密钥等信息，可通过 [即时通信 IM 控制台](https://console.tencentcloud.com/im) 获取，单击目标应用卡片，进入应用的基础配置页面。例如：
![img](https://qcloudimg.tencent-cloud.cn/raw/95ab37db3b8c371d7fa86af24b5a6aad.png)

2. 在基本信息区域，单击显示密钥，复制并保存密钥信息至 `TUICallKit/Web/demos/basic/public/debug/GenerateTestUserSig.js` 文件。
![img](https://qcloudimg.tencent-cloud.cn/raw/8cbbf4515e40f0e3bc0062b2c17a635e.png)

3. 在步骤四中，即可使用 `GenerateTestUserSig.js` 中 `genTestUserSig(userID)` 函数来计算 userSig，例如：
```javascript
import * as GenerateTestUserSig from "../public/debug/GenerateTestUserSig.js";
const { userSig } = GenerateTestUserSig.genTestUserSig(userID);
```

4. 若您使用 vite 作为启动工具，还需注意 [vite 引入问题](https://www.tencentcloud.com/document/product/647/50993#f020d04e-5439-4679-bc6e-716f7329b60a)。

>! 发布前请务必删除此文件，本文提到的获取 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通功能调试**。 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://www.tencentcloud.com/document/product/1047/34385)。

[](id:step4)
## 步骤四：调用 TUICallKit 组件

在需要展示的页面，调用 TUICallKit 的组件即可展示通话页面。

1. TUICallKit UI 引入，例如：
```js
<script lang="ts" setup>
import { TUICallKit } from "./src/components/TUICallKit/Web";
</script>
  
<template>
  <div class="call-kit-container">
    <TUICallKit />
  </div>
</template>
  
<style scoped>
.call-kit-container {
  width: 50rem;
  height: 35rem;
  border-radius: 16px;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
}
</style>
```

2. 登录用户与拨打电话
    2.1 若您已使用 [TUIKit](https://www.tencentcloud.com/document/product/1047/50061) 套件，则需引入下方代码，声明 TUICallKit 为插件；若未使用，则不需要引入下方代码
  ```
    import { TUICallKit } from './src/components/TUICallKit/Web/src/index';
    TUIKit.use(TUICallKit);
  ```

  2.2 可以在需要登录的地方，执行：
  ```
    import { TUICallKitServer } from './src/components/TUICallKit/Web/src/index';
    TUICallKitServer.init({ SDKAppID, userID, userSig }); 
  ```
>? userSig 可在[步骤三](#step3)中获取

	2.3 在需要拨打电话的地方，执行：
	```
		import { TUICallKitServer } from './src/components/TUICallKit/Web/src/index';
		TUICallKitServer.call({ userID, type }); // 双人通话
		TUICallKitServer.groupCall({ userIDList, groupID, type }); // 多人通话
	```
	完成后即可成功拨打您的第一通电话，更详解接口参数请参见 [接口文档](https://www.tencentcloud.com/document/product/647/51015)。

3. 进阶接口
	本组件提供了 `beforeCalling` 和 `afterCalling` 两个回调，可以用于通知业务侧当前通话状态。
	- `beforeCalling`：通话前会执行
	- `afterCalling`：通话后执行

例如可用来进行 <`TUICallKit />;` 组件的展开与折叠，如[示例 demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/src/App.vue)。
```javascript
function beforeCalling() {
  console.log("通话前 会执行此函数");
}
function afterCalling() {
  console.log("通话后 会执行此函数");
}
```
```javascript
<TUICallKit :beforeCalling="beforeCalling" :afterCalling="afterCalling"/>
```

## 其他文档

- [TUICallKit API](https://github.com/tencentyun/TUICallKit/blob/main/Web/docs/API.md)
- [TUICallKit demo 快速跑通](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)
- [TUICallKit 界面定制指引](https://github.com/tencentyun/TUICallKit/blob/main/Web/docs/UI Customization.md)
- [TUICallKit (Web) 常见问题](https://www.tencentcloud.com/document/product/647/51024)


## 常见问题

### 1. 如何生成 UserSig？

UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向项目的接口，在需要 UserSig 时由您的项目向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://www.tencentcloud.com/document/product/1047/34385?lang=en&pg=)。

### 2. vite 引入问题

如果您的项目由 vite 创建，由于文件打包差异，需要在 `index.html` 中引入 `lib-generate-test-usersig.min.js`
```javascript
// index.html
<script src="/public/debug/lib-generate-test-usersig.min.js"> </script>
```

并将原来 `GenerateTestUserSig.js` 中 import 引入的方式注释

```javascript
// import * as LibGenerateTestUserSig from './lib-generate-test-usersig.min.js'
```

### 3. 环境要求

#### 对浏览器版本要求

| 操作系统 | 浏览器类型                   | 浏览器最低版本要求 |
| -------- | ---------------------------- | ------------------ |
| Mac OS   | 桌面版 Safari 浏览器         | 11+                |
| Mac OS   | 桌面版 Chrome 浏览器         | 56+                |
| Mac OS   | 桌面版 Firefox 浏览器        | 56+                |
| Mac OS   | 桌面版 Edge 浏览器           | 80+                |
| Windows  | 桌面版 Chrome 浏览器         | 56+                |
| Windows  | 桌面版 QQ 浏览器（极速内核） | 10.4+              |
| Windows  | 桌面版 Firefox 浏览器        | 56+                |
| Windows  | 桌面版 Edge 浏览器           | 80+                |

>?详细兼容性查询，具体请参见 [浏览器支持情况](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html)。同时，您可通过 [TRTC 检测页面](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) 在线检测。

#### 对网络环境的要求

在使用 TUICallKit 时，用户可能因防火墙限制导致无法正常进行音视频通话，请参考 [应对防火墙限制相关](https://www.tencentcloud.com/document/product/647/35164) 将相应端口及域名添加至防火墙白名单中。

#### 对网站域名协议的要求

出于对用户安全、隐私等问题的考虑，浏览器限制网页在 HTTPS 协议下才能正常使用本文档中所对接组件的全部功能。为确保生产环境中的用户能够顺畅体验产品功能，请将您的网站部署在 **https://** 协议的域名下。

>! 本地开发可以通过 `http://localhost` 或者 `file://` 协议进行访问。

URL 域名及协议支持情况请参考如下表格：

| 应用场景     | 协议             | 接收（播放） | 发送（推流） | 屏幕分享 | 备注 |
| ------------ | ---------------- | ------------ | ------------ | -------- | ---- |
| 生产环境     | HTTPS 协议       | 支持         | 支持         | 支持     | 推荐 |
| 生产环境     | HTTP 协议        | 支持         | 不支持       | 不支持   | -    |
| 本地调试环境 | http://localhost | 支持         | 支持         | 支持     | 推荐 |
| 本地调试环境 | http://127.0.0.1 | 支持         | 支持         | 支持     | -    |
| 本地调试环境 | http://[本机IP]  | 支持         | 不支持       | 不支持   | -    |
| 本地调试环境 | file:///         | 支持         | 支持         | 支持     | -    |
