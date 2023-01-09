## chat-uikit-react集約

### ステップ1:Installation
```
$ npm install @tencentcloud/chat-uikit-react
```
### ステップ2:Usage
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

### 補足:SDKAppID、secretKeyとuserIDの取得 
［IMコンソール］(!https://console.tencentcloud.com/im)で対象アプリケーションカードをクリックして、アプリケーションの基本設定ページに進みます。例：
![](https://qcloudimg.tencent-cloud.cn/raw/3b585716a08e7ff3f0047bd7c904d048.png)
userID情報は、[IMコンソール](!https://console.tencentcloud.com/im)で作成または取得できます。対象アプリケーションカードをクリックし、アプリケーションのアカウント管理ページに進み、アカウントを作成してuserIDを取得できます。例：
![](https://qcloudimg.tencent-cloud.cn/raw/d6774e3ca2bbaf993b505d1596bdac1f.png)
