## 集成 chat-uikit-react

### 步骤一：Installation
```
$ npm install @tencentcloud/chat-uikit-react
```
### 步骤二：Usage
```tsx
import React, { useEffect, useState } from 'react';
import { TUIKit } from '@tencentcloud/chat-uikit-react';
import '@tencentcloud/chat-uikit-react/dist/cjs/index.css';
import TIM, { ChatSDK } from 'tim-js-sdk/tim-js-friendship';
import TIMUploadPlugin from 'tim-upload-plugin';

// create tim instance && login
const init = async () => {
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

export function SampleChat() {
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
```

### 补充：获取 SDKAppID、secretKey 以及 userID 
通过 [即时通信 IM 控制台](!https://console.tencentcloud.com/im)，单击目标应用卡片，进入应用的基础配置页面。例如：
![](https://qcloudimg.tencent-cloud.cn/raw/3b585716a08e7ff3f0047bd7c904d048.png)
userID 信息，可通过 [即时通信 IM 控制台](!https://console.tencentcloud.com/im) 进行创建和获取，单击目标应用卡片，进入应用的账号管理页面，即可创建账号并获取 userID。例如：
![](https://qcloudimg.tencent-cloud.cn/raw/d6774e3ca2bbaf993b505d1596bdac1f.png)
