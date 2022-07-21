Tencent Real-Time Communication(TRTC)는 로컬 및 원격 화면 회전 및 렌더링 모드에 대한 사용자 정의 설정을 지원합니다.

## 로컬 화면 사용자 정의 제어
[setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams)를 호출하여 로컬 렌더링 매개변수를 설정할 수 있습니다.
```javascript
import TRTCCloud, { 
  TRTCRenderParams, TRTCVideoRotation, TRTCVideoFillMode,
  TRTCVideoMirrorType
} from 'trtc-electron-sdk';
const trtcCloud = new TRTCCloud();
const param = new TRTCRenderParams(
  TRTCVideoRotation.TRTCVideoRotation90,
  TRTCVideoFillMode.TRTCVideoFillMode_Fill,
  TRTCVideoMirrorType.TRTCVideoMirrorType_Enable
);

trtcCloud.setLocalRenderParams(param);
const localUserDom = document.querySelector('local-user');
trtcCloud.startLocalPreview(localUserDom);
```

## 원격 화면 사용자 정의 제어
[setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams)를 호출하여 원격 렌더링 매개변수를 설정할 수 있습니다.
```javascript
import TRTCCloud, { 
  TRTCRenderParams, TRTCVideoRotation, TRTCVideoFillMode,
  TRTCVideoMirrorType, TRTCVideoStreamType
} from 'trtc-electron-sdk';
const trtcCloud = new TRTCCloud();
const param = new TRTCRenderParams(
  TRTCVideoRotation.TRTCVideoRotation180,
  TRTCVideoFillMode.TRTCVideoFillMode_Fill,
  TRTCVideoMirrorType.TRTCVideoMirrorType_Disable
);

const remoteUserId = 'remoteUser';
trtcCloud.setRemoteRenderParams(remoteUserId, TRTCVideoStreamType.TRTCVideoStreamTypeBig, param);
const remoteUserDom = document.querySelector('remote-user');
trtcCloud.startRemoteView(remoteUserId, remoteUserDom, TRTCVideoStreamType.TRTCVideoStreamTypeBig);
```
