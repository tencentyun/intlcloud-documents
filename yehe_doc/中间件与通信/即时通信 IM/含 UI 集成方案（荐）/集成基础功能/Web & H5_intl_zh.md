- [](id:required)
  ## 开发环境要求
  - React^18.0
  - TypeScript
  - node（12.13.0 ≤ node 版本 ≤ 17.0.0, 推荐使用 Node.js 官方 LTS 版本 16.17.0）
  - npm（版本请与 node 版本匹配）

  ## chat-uikit-react 集成

  ### 步骤1：创建项目

  创建一个新的React项目，您可自行选择是否需要使用ts模版。
  <dx-codeblock>
  :::  shell
  npx create-react-app sample-chat --template typescript
  :::
  </dx-codeblock>

  创建项目完成后，切换到项目所在目录。
  <dx-codeblock>
  :::  shell
  cd sample-chat
  :::
  </dx-codeblock>

  ### 步骤2：下载 chat-uikit-react 组件

  通过 npm 方式下载  [chat-uikit-react](https://www.npmjs.com/package/@tencentcloud/chat-uikit-react) 并在项目中使用，另外在 GitHub 中也提供相关的[开源代码](https://github.com/TencentCloud/chat-uikit-react)，您也可在此基础上进行开发您自己的组件库。
  <dx-codeblock>
  :::  shell
  npm install @tencentcloud/chat-uikit-react
  :::
  </dx-codeblock>

  [](id:step3)
  ### 步骤3：引入 chat-uikit-react 组件
  [](id:step3)

  替换App.tsx中的内容，或者您可以新建一个组件引入
  >! 以下代码中未填入 `SDKAppID`、`userID` 和 `userSig`，需在[步骤四](#step4)中获取相关信息后进行替换。

   <dx-codeblock>
  :::  tsx
  import React, { useEffect, useState } from 'react';
  import { TUIKit } from '@tencentcloud/chat-uikit-react';
  import '@tencentcloud/chat-uikit-react/dist/cjs/index.css';
  import TIM, { ChatSDK } from 'tim-js-sdk/tim-js-friendship';
  import TIMUploadPlugin from 'tim-upload-plugin';

  // create tim instance && login
  const init = async ():Promise<ChatSDK> => {
  	return new Promise((resolve, reject) => {
  		const tim = TIM.create({ SDKAppID: 0 });
  		tim?.registerPlugin({ 'tim-upload-plugin': TIMUploadPlugin });
  		const onReady = () => { resolve(tim); };
  		tim.on(TIM.EVENT.SDK_READY, onReady);
  		tim.login({
  			userID: 'xxx',
  			userSig: 'xxx',
  		});
  	});
  }

  export default function SampleChat() {
  	const [tim, setTim] = useState<ChatSDK>();
  	useEffect(() => {
  		(async ()=>{
  			const tim = await init()
  			setTim(tim)
  		})()
  	}, [])

  	return (
  		<div style={{height: '100vh',width: '100vw'}}>
  			<TUIKit tim={tim}></TUIKit>
  		</div>
  	);
  }
  :::
  </dx-codeblock>

  ### 步骤4：获取 SDKAppID、userID 和 userSig
  [](id:step4)
  - SDKAppID：SDKAppID 是腾讯云 IM 服务区分客户帐号的唯一标识。我们建议每一个独立的 App 都申请一个新的 SDKAppID。不同 SDKAppID 之间的消息是天然隔离的，不能互通。
    您可以在 [即时通信 IM 控制台](https://console.tencentcloud.com/im) 查看所有的 SDKAppID，单击 **创建新应用**，可以创建新的 SDKAppID。
    ![](https://qcloudimg.tencent-cloud.cn/raw/897506a32765ad504c261d3a8b545307.png)

  - userID：用户 ID。自行填写或者通过 [即时通信 IM 控制台](https://console.tencentcloud.com/im) 进行创建和获取，单击目标应用卡片，进入应用的账号管理页面，即可创建账号并获取 userID。例如：

  <img style="width:870px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/d6774e3ca2bbaf993b505d1596bdac1f.png"/>

  - userSig：用户登录即时通信 IM 的密码，其本质是对 UserID 等信息加密后得到的密文。进入 [即时通信 IM 控制台](https://console.tencentcloud.com/im)，选择辅助工具下的 [UserSig生成&校验](https://console.tencentcloud.com/im/tool-usersig) ,userSig相关介绍参见 [生成 UserSig](https://www.tencentcloud.com/document/product/1047/34385)。
    ![](https://qcloudimg.tencent-cloud.cn/raw/1613698480f2a0d660e458ef9e519730.png)

  ### 步骤5：启动项目

  <dx-codeblock>
  :::  shell
   npm run start
  :::
  </dx-codeblock>

  >!1. 请确保 [步骤三](#step3) 代码中  `SDKAppID`、`userID` 和 `userSig` 均已成功替换，如未替换将会导致项目表现异常。
  >2. `userID` 和 `userSig`  为一一对应关系，具体参考 [生成 UserSig](https://www.tencentcloud.com/document/product/1071/39471)。
  >3. 如遇到项目启动失败，请检查 [开发环境要求](#required) 是否满足。

  ### 步骤6：发送您的第一条消息
  1. 项目启动成功后，点击“+”图标，创建会话。
  2. 在输入框中搜索另一个用户的 userID（参考：[步骤4 -> 创建账号并获取 `userID`](#step4)）。
  3. 点击用户头像发起会话。
  4. 在输入框输入消息，按下"enter"键发送。
     ![](https://web.sdk.qcloud.com/im/demo/TUIkit/react-static/images/chat-English.gif)

  ## 常见问题

  #### 什么是 UserSig？

  UserSig 是用户登录即时通信 IM 的密码，其本质是对 UserID 等信息加密后得到的密文。

  #### 如何生成 UserSig？

  UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向项目的接口，在需要 UserSig 时由您的项目向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://www.tencentcloud.com/document/product/1047/34385)。

  > !本文示例代码采用的获取 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通功能调试**。 正确的 UserSig 签发方式请参见上文。


  ## 相关文档

  - [SDK API 手册](https://www.tencentcloud.com/document/product/1047/33999)
