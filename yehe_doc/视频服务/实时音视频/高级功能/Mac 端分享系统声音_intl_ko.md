## 시나리오의 문제점 및 솔루션
화면 공유 등 응용 시나리오에서는 시스템 오디오를 상대방에게 공유해야 하는 상황이 종종 발생하지만, Mac 컴퓨터는 기본적으로 사운드 카드에서 시스템 오디오 수집을 지원하지 않아 곤란할 때가 많습니다. 이에 따라 TRTC는 해당 시나리오에 대한 수요를 위해 Mac 시스템 오디오 녹음 기능을 제공합니다. 구체적인 액세스 방법은 다음과 같습니다.

## 통합 설명

<span id="step1"></span>
### 1단계: TRTCPrivilegedTask 라이브러리 통합  

SDK는 [TRTCPrivilegedTask](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TRTCPrivilegedTask/TRTCPrivilegedTask.tar.bz2) 라이브러리를 사용해 root 권한을 획득하므로, 버츄얼 사운드 카드 플러그 인 TRTCAudioPlugin.driver를 시스템 디렉터리 `/Library/Audio/Plug-Ins/HAL`에 설치합니다.

#### CocoaPods를 사용한 통합  
1. 현재 프로젝트의 루트 디렉터리에서 `Podfile` 파일을 연 뒤 다음 내용을 추가합니다.

```
platform :osx, '10.10'	

target 'Your Target' do
   pod 'TRTCPrivilegedTask', :podspec => 'https://pod-1252463788.cos.ap-guangzhou.myqcloud.com/liteavsdkspec/TRTCPrivilegedTask.podspec'
end
```

2. `pod install` 명령어를 실행하여 **TRTCPrivilegedTask** 라이브러리를 설치합니다.

>?
>- 프로젝트의 루트 디렉터리에 `Podfile` 파일이 없는 경우, 먼저 `pod init` 명령어를 실행하여 파일을 생성한 뒤 다음 내용을 추가합니다.
>- CocoaPods 설치 방법은 [CocoaPods 공식 홈페이지 설치 설명](https://guides.cocoapods.org/using/getting-started.html)을 참조하십시오.

#### 수동 통합
1. [TRTCPrivilegedTask](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TRTCPrivilegedTask/TRTCPrivilegedTask.tar.bz2) 라이브러리를 다운로드합니다.
2. Xcode 프로그래밍 프로젝트를 열어 압축 해제한 파일 libPrivilegedTask.a를 프로그램으로 가져옵니다.
3. 실행할 타깃을 선택하고 Build Phases를 선택합니다. Link Binary with Libraries를 펼치고 아래쪽에 있는 [+] 버튼을 클릭하여 종속 라이브러리 `libPrivilegedTask.a`를 추가합니다.  
![libPrivilegedTask.a](https://main.qcloudimg.com/raw/cc5b3365e72cee80cda7f0db0a4e1b62.png)  


<span id="step2"></span>
### 2단계: App Sandbox 기능 취소  
App의 entitlements 설명 파일에서 **App Sandbox** 항목을 삭제합니다.  
![Sandbox](https://main.qcloudimg.com/raw/98fed5571040f24c2891f4b87ddce15e.png)  


<span id="step3"></span>
### 3단계: 버츄얼 사운드 카드 플러그 인 패키징  
[TRTCPrivilegedTask 라이브러리 통합](#step1) 및 [App Sandbox 기능 취소](#step2)를 완료한 후, 처음 시스템 오디오 녹음 기능 사용 시 SDK는 네트워크에서 버츄얼 사운드 카드 플러그 인을 다운로드 및 설치합니다. 해당 과정을 신속하게 진행하고 싶은 경우, 다음 이미지와 같이 `TXLiteAVSDK_TRTC_Mac.framework`의 PlugIns 디렉터리에 있는 버츄얼 사운드 카드 플러그 인 `TRTCAudioPlugin.driver`을 App Bundle의 Resources 디렉터리에 패키징합니다.  
![플러그 인 패키징](https://main.qcloudimg.com/raw/b04b805d4848f2ecd6fd7dcc83176a9e.png)
또는 다음 이미지와 같이 App Bundle의 PlugIns 디렉터리로 복사합니다.  
![플러그 인 패키징2](https://main.qcloudimg.com/raw/05fb5c6ec4dba74c3b5fb880ed28033e.png)  


<span id="step4"></span>
### 4단계: 시스템 오디오 수집 시작  
[startSystemAudioLoopback](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) 인터페이스를 호출하여 시스템 오디오 수집을 시작하고, 이를 오디오 업스트림에 혼합합니다. 인터페이스에서 실행이 완료되면 [onSystemAudioLoopbackError](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a8644f5136138d13ffa8e0ea68f5c3676)를 통해 완료 또는 실패 결과를 콜백합니다.

```
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud startLocalAudio];
[trtcCloud startSystemAudioLoopback];
```

>! TRTCPrivilegedTask 라이브러리 통합 및 App Sandbox 기능 취소 후 처음 startSystemAudioLoopback 호출 시 다음 이미지와 같이 root 권한을 획득할 수 있습니다.    
>[예]를 클릭하면 버츄얼 사운드 카드 플러그 인이 자동으로 설치됩니다.



<span id="step5"></span>

### 5단계: 시스템 오디오 수집 중지 

[stopSystemAudioLoopback](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) 인터페이스를 호출하여 시스템 사운드 수집을 중지합니다.

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud stopSystemAudioLoopback];
```

<span id="step6"></span>
### 6단계: 시스템 사운드 수집 음량 설정

[setSystemAudioLoopbackVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) 인터페이스를 호출하여 시스템 사운드 수집 음량을 설정합니다.

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud setSystemAudioLoopbackVolume:80];
```

## 결론

- TRTC는 Mac에서 버츄얼 사운드 카드 플러그 인 `TRTCAudioPlugin.driver`를 통해 시스템 오디오를 녹음합니다. 이 버츄얼 사운드 카드 플러그 인은 시스템 디렉터리 `/Library/Audio/Plug-Ins/HAL`에 복사하여 오디오 서비스를 재시작하면 적용됩니다. `실행`의 `기타` 폴더에 있는 `오디오 MIDI 설정` 애플리케이션으로 버츄얼 사운드 카드 플러그 인이 정상적으로 설치되었는지 확인할 수 있으며, 해당 애플리케이션의 디바이스 리스트에 'TRTC Audio Device'가 있으면 TRTC 버츄얼 사운드 카드 플러그 인이 정상적으로 설치된 것입니다.  
- [TRTCPrivilegedTask 라이브러리 통합](#step1) 및 [App Sandbox 기능 취소](#step2)는 TRTC SDK에 버츄얼 사운드 플러그 인 자동 설치를 위한 root 권한을 제공합니다. TRTCPrivilegedTask 라이브러리를 통합하지않고 App Sandbox 기능을 유지하는 경우, SDK는 버츄얼 사운드 카드 플러그 인을 자동으로 설치하지 않습니다. 단, 시스템에 이미 버츄얼 사운드 카드 플러그 인이 설치되어 있는 경우 시스템 오디오 녹음 기능은 정상적으로 사용할 수 있습니다.
> ? 위 방법 외에도 수동으로 버츄얼 사운드 카드 플러그 인을 설치하여 해당 기능을 통합할 수 있습니다.
> 1. `TXLiteAVSDK_TRTC_Mac.framework`의 PlugIns 디렉터리에 있는 `TRTCAudioPlugin.driver`를 시스템 디렉터리 `/Library/Audio/Plug-Ins/HAL`로 복사합니다.
> 2. 시스템 오디오 서비스를 재시작합니다. 

#### 시스템 오디오 서비스 bash 재시작
```
 sudo cp -R TXLiteAVSDK_TRTC_Mac.framework/PlugIns/TRTCAudioPlugin.driver /Library/Audio/Plug-Ins/HAL  
 sudo kill -9 `ps ax|grep 'coreaudio[a-z]' |awk '{print $1}'`
```
<span id="note"></span>

## 주의 사항
- App Sandbox 기능을 취소하면 App에서 획득한 사용자 경로가 변경됩니다.  
NSSearchPathForDirectoriesInDomains 등 시스템 메소드를 통해 획득한 ` ~/Documents`, `~/Library` 등의 디렉터리는 샌드박스 디렉터리에서 사용자 디렉터리인 `/Users/사용자 이름/Documents`, `/Users/사용자 이름/Library`로 전환됩니다.
- TRTCPrivilegedTask 라이브러리를 통합하면 Mac App Store에 App을 출시하지 못할 수도 있습니다.  
SDK에서 버츄얼 사운드 카드 플러그 인 자동 설치 시 App Sandbox 기능을 비활성화하고 root 권한을 획득해야 합니다. 이 경우 Mac App Store에 App을 출시하지 못할 수 있으며, 자세한 내용은 [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/#hardware-compatibility)를 참조하십시오.  
App Store에 App을 출시해야 하거나 Sandbox 기능을 사용해야 할 경우 버츄얼 사운드 카드 플러그 인 수동 설치를 권장합니다.  
