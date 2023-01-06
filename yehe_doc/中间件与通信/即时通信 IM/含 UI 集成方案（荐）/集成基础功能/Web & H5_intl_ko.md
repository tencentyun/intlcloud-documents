## chat-uikit-react 통합

### 1단계: Installation
```
$ npm install @tencentcloud/chat-uikit-react
```
### 2단계: Usage
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

### 보충: SDKAppID, secretKey 및 userID 가져오기 
[IM 콘솔](!https://console.tencentcloud.com/im)을 통해 대상 애플리케이션 카드를 클릭하여 다음과 같이 애플리케이션의 기본 설정 화면으로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3b585716a08e7ff3f0047bd7c904d048.png)
userID 정보는 [IM 콘솔](!https://console.tencentcloud.com/im)을 통해 생성 및 획득할 수 있으며 대상 애플리케이션 카드를 클릭하고 애플리케이션의 계정 관리 페이지로 이동하여 다음과 같이 계정을 생성하고 userID를 획득할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d6774e3ca2bbaf993b505d1596bdac1f.png)
