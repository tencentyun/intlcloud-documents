## IM React Native SDK 0.1.9 @2022.12.05

- 추가: 멀티미디어 메시지 온라인 URL(url)은 더 이상 기본적으로 반환되지 않습니다. `getMessageOnlineUrl` API를 호출하여 가져와야 합니다.
- 추가: 멀티미디어 메시지 로컬 URL(localurl)이 더 이상 기본적으로 반환되지 않습니다. downloadMessage API를 호출하여 메시지를 성공적으로 다운로드한 후에만 반환됩니다.
- 추가: `onMessageDownloadProgressCallback` 콜백이 `advanceMessageListener`에 추가되고 멀티미디어 메시지 다운로드 진행률이 업데이트될 때 트리거됩니다.
- 추가: 메시지 확장 기능이 추가되었습니다. 자세한 내용은 메시지-메시지 확장을 참고하십시오.
- 추가: 기본 Native SDK가 6.9.3557로 업그레이드되었습니다.

>?멀티미디어 메시지 및 파일 메시지가 크게 변경되었습니다. 처음 세 가지 업데이트에 따라 이러한 메시지를 얻고 렌더링하기 위한 기존 로직을 수정하십시오. 그렇지 않으면 메시지가 표시되지 않습니다. 수정 과정에서 궁금한 점이 있으면 언제든지 [문의하기](https://www.tencentcloud.com/contact-us)로 연락주십시오.

## IM React Native SDK 0.1.0 @2022.07.14
- 사용자에게 공식으로 제공되었습니다.

>? 이것은 IM React Native의 첫 번째 릴리스이며 후속 버전이 지속적으로 업데이트될 것입니다.
