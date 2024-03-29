# TUICallKit 组件快速接入

本文将介绍如何用最短的时间完成 TUICallKit 组件的接入，跟随本文档，您将完成如下几个关键步骤，并最终得到一个包含完备 UI 界面的视频通话功能。

若您想体验组件效果，可参考[TUICallKit demo 快速跑通](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)。

在接入前请检查您的桌面浏览器是否支持音视频服务，详细要求可参考[环境要求](#3-环境要求)。

## 目录
* [步骤一：开通服务](#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E5.BC.80.E9.80.9A.E6.9C.8D.E5.8A.A1)
* [步骤二：引入 TUICallKit 组件](#.E6.AD.A5.E9.AA.A4.E4.BA.8C.EF.BC.9A.E5.BC.95.E5.85.A5-tuicallkit-.E7.BB.84.E4.BB.B6)
* [步骤三：调用 TUICallKit 组件](#.E6.AD.A5.E9.AA.A4.E4.B8.89.EF.BC.9A.E8.B0.83.E7.94.A8-tuicallkit-.E7.BB.84.E4.BB.B6)
* [其他文档](#.E5.85.B6.E4.BB.96.E6.96.87.E6.A1.A3)
* [常见问题](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)
  + [1. 如何生成 UserSig？](#1-如何生成-UserSig？)
  + [2. vite 引入问题](#2-vite-引入问题)
  + [3. 环境要求](#3-环境要求)
    - (1) 对浏览器版本要求
    - (2) 对网络环境的要求
    - (3) 对网站域名协议的要求

## 步骤一：开通服务

TUICallKit 是基于腾讯云 [即时通信 IM](https://intl.cloud.tencent.com/document/product/1047/35448) 和 [实时音视频 TRTC](https://intl.cloud.tencent.com/document/product/647/35078) 两项付费 PaaS 服务构建出的音视频通信组件。您可以按照如下步骤开通相关的服务并体验 7 天的免费试用服务：

1. 登录到 [即时通信 IM 控制台](https://console.cloud.tencent.com/im)，单击**创建新应用**，在弹出的对话框中输入您的应用名称，并单击**确定**。

![](https://qcloudimg.tencent-cloud.cn/raw/ce2e34f7cd1cd14679fc5decffb469af.png)

2. 单击刚刚创建出的应用，进入**基本配置**页面，并在页面的右下角找到**开通腾讯实时音视频服务**功能区，单击**免费体验**即可开通 TUICallKit 的 7 天免费试用服务。

![](https://qcloudimg.tencent-cloud.cn/raw/796e49d9f55174aacb62bb8eb848feaf.png)

3. 在同一页面找到 **SDKAppID** 和**密钥**并记录下来，它们会在后续中被用到。

![](https://qcloudimg.tencent-cloud.cn/raw/8349ac97b261279606316331488784c3.png)


 - SDKAppID：IM 的应用 ID，用于业务隔离，即不同的 SDKAppID 的通话彼此不能互通；
 - Secretkey：IM 的应用密钥，需要和 SDKAppID 配对使用，用于签出合法使用 IM 服务的鉴权用票据 UserSig，我们会在接下来的步骤五中用到这个 Key。


## 步骤二：引入 TUICallKit 组件


### 方式1：npm 集成

通过 npm 方式下载 TUICallKit 组件，为了方便您后续的拓展，建议您将 TUICallKit 组件复制到自己工程的 `src/components/` 目录下：

```bash
# macOS
yarn add @tencentcloud/call-uikit-vue  # 如果你没装过 yarn, 可以先运行: npm install -g yarn
mkdir -p ./src/components/TUICallKit/Web && cp -r ./node_modules/@tencentcloud/call-uikit-vue/* ./src/components/TUICallKit/Web

# windows
yarn add @tencentcloud/call-uikit-vue  # 如果你没装过 yarn, 可以先运行: npm install -g yarn
xcopy .\node_modules\@tencentcloud\call-uikit-vue  .\src\components\TUICallKit\Web /i /e
```


### 方式2：源码集成

1. 从 [GitHub 下载](https://github.com/tencentyun/TUICallKit/tree/main/Web) TUICallKit 源码。复制 `TUICallKit/Web` 文件夹放置到自己到工程的 `src/components` 文件夹中，例如：

<!-- <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/e4699aaa507aa4618034463225f72cb2.png"/>  -->

<div align="center">

<img style="width:300px; max-width: inherit;" src="https://user-images.githubusercontent.com/57169560/194735247-3cbe30c6-37ab-43a4-97f0-27b8e40140cf.png"/> 
</div>

2. 进入此文件夹中，安装运行所需依赖
```shell
cd ./src/components/TUICallKit/Web 
yarn         # 如果你没装过 yarn, 可以先运行: npm install -g yarn
```


## 步骤三：调用 TUICallKit 组件

在需要展示的页面，调用 TUICallKit 的组件即可展示通话页面。


1. TUICallKit UI 引入，例如：

```js
<script lang="ts" setup>
import { TUICallKit } from "./components/TUICallKit/Web";
</script>
  
<template>
  <TUICallKit />
</template>
```


2. 登录用户与拨打电话

   2.1 若您已使用 [TUIKit](https://www.tencentcloud.com/document/product/1047/50061) 套件，则需引入下方代码，声明 TUICallKit 为插件；若未使用，则可以跳过本步骤至2.2

   ```javascript
   import { TUICallKit } from './components/TUICallKit/Web';
   TUIKit.use(TUICallKit); 
   ```

   2.2 拨打电话需保持初始化组件

   ```javascript
   import { TUICallKitServer } from './components/TUICallKit/Web';
   TUICallKitServer.init({ SDKAppID, userID, userSig }); 
   ```

>?
>- 若您使用 vite 作为启动工具，还需注意 [vite 引入问题](#2-vite-引入问题)
>- SDKAppID, SecretKey 的获取可见步骤一
>userSig 可**临时**使用 `GenerateTestUserSig.js` 中 `genTestUserSig(userID)` 函数来计算 ，例如：
>```javascript
import * as GenerateTestUserSig from "./components/TUICallKit/Web/demos/basic/public/debug/GenerateTestUserSig.js";
const { userSig } = GenerateTestUserSig.genTestUserSig(userID, SDKAppID, SecretKey);
>```



   >! 本文提到的获取 UserSig 的方案是在前端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通功能调试**。 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。
   
    2.3 在需要拨打电话的地方，执行：
   
    ```javascript
    import { TUICallKitServer } from './components/TUICallKit/Web';
    TUICallKitServer.call({ userID: "123", type: 2 }); // 双人通话
    TUICallKitServer.groupCall({ userIDList: ["xxx"], groupID: "xxx", type: 2 }); // 多人通话
    ```

    之后就可以成功拨打您的第一通电话了～更详解接口参数可参考[接口文档](https://www.tencentcloud.com/document/product/647/51015)


3. 进阶接口

本组件提供了 `beforeCalling` 和 `afterCalling` 两个回调，可以用于通知业务侧当前通话状态，

- `beforeCalling`: 通话前会执行
- `afterCalling`: 通话后执行

例如可用来进行 `<TUICallKit />` 组件的展开与折叠，如[示例 demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/src/App.vue)。

```javascript
function beforeCalling() {
  console.log("通话前 会执行此函数");
}
function afterCalling() {
  console.log("通话后 会执行此函数");
}
```

```html
<TUICallKit :beforeCalling="beforeCalling" :afterCalling="afterCalling"/>
```


## 其他文档

- [TUICallKit API](https://www.tencentcloud.com/document/product/647/51015)
- [TUICallKit demo 快速跑通](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)
- [TUICallKit 界面定制指引](https://www.tencentcloud.com/document/product/647/50997)
- [TUICallKit (Web) 常见问题](https://www.tencentcloud.com/document/product/647/51024)


## 常见问题
### 1. 如何生成 UserSig？

UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向项目的接口，在需要 UserSig 时由您的项目向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。

### 2. vite 引入问题

如果您的项目由 vite 创建，由于文件打包差异，需要在 `index.html` 中引入 `lib-generate-test-usersig.min.js`

```javascript
// index.html
<script src="./src/components/TUICallKit/Web/demos/basic/public/debug/lib-generate-test-usersig.min.js"> </script>
```

并将原来 `GenerateTestUserSig.js` 中 import 引入的方式注释

```javascript
// import * as LibGenerateTestUserSig from './lib-generate-test-usersig.min.js'
```

### 3. 环境要求

#### (1) 对浏览器版本要求

请使用最新版本的 Chrome 浏览器进行体验，本文档中所对接的组件对当前主流的桌面浏览器的支持情况如下：

<table>
<thead><tr><th>操作系统</th><th>浏览器类型</th><th>浏览器最低版本要求</th></tr></thead>
<tbody><tr>
<td>Mac OS</td>
<td>桌面版 Safari 浏览器</td>
<td>11+</td>
</tr><tr>
<td>Mac OS</td>
<td>桌面版 Chrome 浏览器</td>
<td>56+</td>
</tr><tr>
<td>Mac OS</td>
<td>桌面版 Firefox 浏览器</td>
<td>56+</td>
</tr><tr>
<td>Mac OS</td>
<td>桌面版 Edge 浏览器</td>
<td>80+</td>
</tr><tr>
<td>Windows</td>
<td>桌面版 Chrome 浏览器</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>桌面版 QQ 浏览器（极速内核）</td>
<td>10.4+</td>
</tr><tr>
<td>Windows</td>
<td>桌面版 Firefox 浏览器</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>桌面版 Edge 浏览器</td>
<td>80+</td>
</tr>
</tbody></table>


>? 详细兼容性查询，具体请参见 [浏览器支持情况](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)。同时，您可通过 [TRTC 检测页面](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) 在线检测。

#### (2) 对网络环境的要求

在使用 TUICallKit 时，用户可能因防火墙限制导致无法正常进行音视频通话，请参考 [应对防火墙限制相关](https://intl.cloud.tencent.com/document/product/647/35164) 将相应端口及域名添加至防火墙白名单中。

#### (3) 对网站域名协议的要求

出于对用户安全、隐私等问题的考虑，浏览器限制网页在 HTTPS 协议下才能正常使用本文档中所对接组件的全部功能。为确保生产环境中的用户能够顺畅体验产品功能，请将您的网站部署在 https:// 协议的域名下。

<table>
<thead><tr><th>应用场景</th><th>协议</th><th>接收（播放）</th><th>发送（上麦）</th><th>屏幕分享</th><th>备注</th></tr></thead>
<tbody><tr>
<td>生产环境</td>
<td>HTTPS 协议</td>
<td>支持</td>
<td>支持</td>
<td>支持</td>
<td>推荐</td>
</tr><tr>
<td>生产环境</td>
<td>HTTP 协议</td>
<td>支持</td>
<td>不支持</td>
<td>不支持</td>
<td>-</td>
</tr><tr>
<td>本地开发环境</td>
<td>http://localhost</td>
<td>支持</td>
<td>支持</td>
<td>支持</td>
<td>推荐</td>
</tr><tr>
<td>本地开发环境</td>
<td>http://127.0.0.1</td>
<td>支持</td>
<td>支持</td>
<td>支持</td>
<td>-</td>
</tr><tr>
<td>本地开发环境</td>
<td>http://[本机IP]</td>
<td>支持</td>
<td>不支持</td>
<td>不支持</td>
<td>-</td>
</tr><tr>
<td>本地开发环境</td>
<td align="left">file:///</td>
<td>支持</td>
<td>支持</td>
<td>支持</td>
<td>-</td>
</tr>
</tbody></table>
