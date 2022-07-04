You can customize settings for the rotation and rendering modes of local and remote video images.

## Custom Control of Local Image
You can set local rendering parameters by calling [setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams).
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

## Custom Control of Remote Image
You can set remote rendering parameters by calling [setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams).
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
