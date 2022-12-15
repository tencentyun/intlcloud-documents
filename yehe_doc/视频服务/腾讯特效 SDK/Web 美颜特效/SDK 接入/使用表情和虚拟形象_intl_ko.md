Tencent Effect SDK는 v0.3.0부터 Animoji 가상 아바타를 지원합니다.
**이 기능은 현재 Web에서만 지원됩니다.**

## 지원 확인
Animoji와 VR 가상 아바타는 WebGL2 환경에 의존합니다. SDK는 브라우저가 기능을 지원하는지 여부를 확인할 수 있는 정적 방법을 제공합니다.
```javascript
import {ArSdk} from 'tencentcloud-webar'
if (ArSdk.isAvatarSupported()) {
    // 기능 초기화

} else {
    alert('이 브라우저는 가상 아바타를 지원하지 않습니다')
    // 기능 숨기기
}
```

## Animoji
### 모델 가져오기
초기화 후 기본 제공 모델을 가져올 수 있습니다. 현재 SDK는 네 가지 기본 제공 모델을 제공합니다.
```javascript
const avatarARList = await sdk.getAvatarList('AR')
```

>! Animoji 및 가상 아바타를 구성하면 메이크업 및 스티커와 같은 다른 효과가 자동으로 제거되며 그 반대의 경우도 마찬가지입니다.

### 모델 사용
기본 제공 모델 목록을 얻은 후 EffectId 매개변수를 지정하여 하나를 선택할 수 있습니다.
```javascript
ar.setAvatar({
  mode: 'AR', // 모드를 AR로 설정
  effectId: avatarARList[0].EffectId// 모델의 id 전달
}, () => {
  // success callback
  
});
```
### 사용자 정의 모델
사용자 지정 모델을 사용하려면 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오.


## VR 가상 아바타
### 모델 가져오기
초기화 후 내장된 아바타 모델을 얻을 수 있습니다. 현재 SDK는 10개의 내장 아바타 모델을 제공합니다.
```javascript
const avatarVRList = await sdk.getAvatarList('VR')
```

### 모드 설정
```javascript

ar.setAvatar({
  mode: 'VR', // mode를 AR로 설정
  effectId: avatarVRList[0].EffectId, // 아바타 모델의 id 전달
  backgroundUrl: 'https://webar-static.tencent-cloud.com/assets/background/1.jpg',
}, () => {
    // success callback

  
});
```

>! 모드를 VR로 설정하면 배경 이미지의 URL도 지정해야 합니다. 지정하지 않으면 검정색 배경이 사용됩니다.

### 사용자 정의 모델
두 가지 방법으로 Tencent Effect SDK에서 사용할 가상 아바타를 사용자 지정할 수 있습니다.
- 방법1: `readyplayer.me`
- 방법2: [Vroid](https://vroid.com/en/studio)

모델을 내보낸 후 CDN에 업로드하고 URL을 사용하여 SDK에서 구성해야 합니다.
```javascript
ar.setAvatar({
  mode: 'VR', // mode를 AR로 설정
  url: 'https://xxxx.glb', // 내장 모델의 id 전달
  backgroundUrl: 'https://webar-static.tencent-cloud.com/assets/background/1.jpg',
}, () => {
    // success callback

});
```
현재 사용자 지정 모델은 GLB 및 VRM 형식만 지원합니다.
