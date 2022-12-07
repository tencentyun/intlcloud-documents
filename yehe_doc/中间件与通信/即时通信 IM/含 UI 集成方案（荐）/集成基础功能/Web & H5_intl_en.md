## Integrating chat-uikit-react

### Step 1. Installation
```
$ npm install @tencentcloud/chat-uikit-react
```
### Step 2. Usage
```tsx
import React, { useEffect, useState } from 'react';
import { TUIKit } from '@tencentcloud/chat-uikit-react';
import '@tencentcloud/chat-uikit-react/dist/cjs/index.css';
import TIM, { ChatSDK } from 'tim-js-sdk/tim-js-friendship';
import TIMUploadPlugin from 'tim-upload-plugin';

// Create TIM instance and log in
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

### Tips: Obtaining SDKAppID, secretKey, and userID 
To obtain the SDKAppID and secretKey, log in to the [IM console](!https://console.tencentcloud.com/im), click the target app card, and go to the basic configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/3b585716a08e7ff3f0047bd7c904d048.png)
To obtain the userID, go to the [IM console](!https://console.tencentcloud.com/im), click the target app card, go to the account management page, and create an account.
![](https://qcloudimg.tencent-cloud.cn/raw/d6774e3ca2bbaf993b505d1596bdac1f.png)
