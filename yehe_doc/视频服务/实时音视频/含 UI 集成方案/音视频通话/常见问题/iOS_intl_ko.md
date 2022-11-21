### ‘The package you purchased does not support this ability’라는 오류 메시지가 표시되면 어떻게 해야 합니까?

상기 오류가 발생하면 TRTC를 활성화하지 않았거나 TRTC 패키지가 만료되었음을 나타냅니다. TRTC 활성화 방법은 [1단계: 서비스 활성화](https://www.tencentcloud.com/document/product/647/50992#step1)를 참고하십시오. 활성화 후 무료 평가판 패키지를 받을 수 있습니다.

### TRTC 패키지는 어떻게 구매하나요?

[가격 개요](https://www.tencentcloud.com/document/product/647/50553)를 참고하십시오. 질문이 있으시면 페이지 오른쪽 하단의 아이콘을 클릭하여 문의하십시오.

### TUICallKit의 소스 코드는 어떻게 수정하나요?

`CocoaPods`를 사용하여 컴포넌트를 가져옵니다.

1. 프로젝트의 `Podfile`과 동일한 디렉터리에 `TUICallKit` 폴더를 만듭니다.

2. 컴포넌트의 [GitHub 페이지](https://github.com/tencentyun/TUICalling)로 이동하여 코드를 복제하거나 다운로드하고 [**iOS**](https://github.com/tencentyun/TUICalling/tree/main/iOS)의 `TUICallKit` 및 `Resources` 폴더와 `TUICallKit.podspec` 파일을 프로젝트의 `TUICallKit` 폴더에 복사합니다.
3. `Podfile`에 다음 종속성을 추가합니다.

```objectivec
# :path => "TUICallKit.podspec의 상대 경로"
pod 'TUICallKit', :path => "TUICallKit/TUICallKit.podspec"
```

4. `pod install`을 실행합니다.

>! `TUICallKit`, `Resources` 및 `TUICallKit.podspec`이 동일한 디렉터리에 있는지 확인하십시오.

**TUICallKit을 가져온 후 다음 디렉터리 구조가 표시됩니다.**:

![](https://qcloudimg.tencent-cloud.cn/raw/91afcf4f9c3752222ef4e0589c818eed.png)

>? 폴더는 계층적으로 구성되어 소스 코드를 쉽게 보고 수정할 수 있습니다.

### TUICallKit이 내가 통합한 오디오/비디오 라이브러리와 충돌하는 경우 어떻게 해야 합니까?

Tencent Cloud의 여러 `오디오/비디오 라이브러리`를 동시에 통합할 수 없습니다. 그렇지 않으면 중복 기호 오류가 발생할 수 있습니다. 다음 방법을 사용하여 문제를 해결할 수 있습니다.

1. 'TXLiteAVSDK_TRTC'를 통합하면 중복 기호 오류가 발생하지 않습니다. `Podfile`에 다음을 추가하기만 하면 됩니다.
```objectivec
pod 'TUICallKit'
```

2. `TXLiteAVSDK_Professional`을 통합한 경우 중복 기호 오류가 발생합니다. `Podfile`에 다음을 추가할 수 있습니다.
```objectivec
pod 'TUICallKit/Professional'
```

3. `TXLiteAVSDK_Enterprise`를 통합한 경우 중복 기호 오류가 발생합니다. `TXLiteAVSDK_Professional`로 업데이트하고 `TUICallKit/Professional`을 사용하는 것이 좋습니다.

### TUICallKit을 통합할 때 ‘ld: framework not found BoringSSL clang: error: linker command failed with exit code 1 sdk’ 오류가 발생하면 어떻게 해야 합니까?

현재 'TUICallKit'이 의존하는 오디오/비디오 라이브러리는 에뮬레이터를 지원하지 않습니다. 데모 실행 또는 디버깅을 위해 실제 장치를 사용하십시오.

### TRTC 기능만 사용하면 IM SDK를 통합할 수 없나요?

**할 수 없습니다.** `TUIKit`의 모든 컴포넌트는 발신 통화 신호 및 통화 중 회선 신호와 같은 기본 로직에 대해 IM SDK에 의존합니다. 이미 `IM` 서비스를 구매했다면 'TUICallKit' 로직에 따라 사용할 수 있습니다.

### TUICallKit은 사용자 지정 벨소리를 지원합니까?

**지원합니다**. [TUICalling#setCallingBell](https://www.tencentcloud.com/document/product/647/51011#setcallingbell)을 호출하여 구현할 수 있습니다.

### CocoaPods는 어떻게 설치합니까?

터미널 창에 다음 명령어를 입력합니다(먼저 `Mac`에 `Ruby`를 설치해야 함).
```objectivec
sudo gem install cocoapods
```

### TUICallKit을 백그라운드에서 실행할 수 있습니까?

**실행할 수 있습니다**. TUICallKit이 백그라운드에서 실행되도록 하려면 프로젝트를 선택하고 **Capabilities** 탭에서 **Background Modes**를 **ON**하고 **Audio, AirPlay and Picture in Picture**를 선택합니다.

![](https://qcloudimg.tencent-cloud.cn/image/document/970de09ccdab7defb8df741fe671de33.jpeg)
