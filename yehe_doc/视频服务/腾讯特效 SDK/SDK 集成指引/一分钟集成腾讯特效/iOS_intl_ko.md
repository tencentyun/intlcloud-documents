## 통합 준비

### 개발자 환경 요건

- XCode 11 이상: App Store 또는 [Demos](https://intl.cloud.tencent.com/document/product/1143/45374)에서 다운로드합니다.
- 권장 실행 환경:
  - 기기 사양: iPhone 5 이상. iPhone 6 이하의 경우 전면 카메라는 720p까지 지원하며 1080p는 지원되지 않습니다.
  - 시스템 요구 사항: iOS 10.0 이상.

### SDK 가져오기

CocoaPods를 사용하거나 SDK를 수동으로 다운로드하여 프로젝트로 가져올 수 있습니다.
<dx-tabs>
::: CocoaPods 사용
1. **CocoaPods 설치**
터미널 창에 다음 명령어를 입력합니다(먼저 Mac에 Ruby를 설치해야 함).
```
sudo gem install cocoapods
```
2. **Podfile 파일 생성**
프로젝트가 있는 경로에 들어가 다음 명령 라인을 입력하면 프로젝트 경로에 Podfile 파일이 생성됩니다.
```
pod init
```
3. **Profile 편집**
프로젝트 요구 사항에 따라 적절한 버전을 선택하고 Podfile을 편집합니다:
	- **XMagic 스탠다드 버전**
다음과 같이 Profile을 편집합니다.
```
platform : ios, ’8.0’

target ’App’ do
pod 'XMagic'
end
```
  - **XMagic 라이트 버전**
XMagic 라이트 버전의 설치 패키지는 XMagic 스탠다드 버전보다 작습니다. 기본 버전 A1-00, 기본 버전 A1-01 및 고급 버전 S1-00만 지원합니다. Profile을 다음과 같이 편집합니다.
```
platform : ios, ’8.0’

target ’App’ do
pod 'XMagic_Smart'
end
```
4. **SDK 업데이트 및 설치**
터미널 창에 다음 명령어를 입력하여 로컬 라이브러리 파일을 업데이트하고 SDK를 설치합니다.
```
pod install
```
pod 명령어 실행이 완료되면 SDK .xcworkspace 접미사가 통합된 프로그램 파일이 생성되며, 이를 더블클릭해 실행하면 됩니다.
5. **프로젝트에 뷰티필터 리소스 추가**
사용하는 Tencent Effect 패키지의 [SDK 및 뷰티필터 리소스](https://www.tencentcloud.com/document/product/1143/45377)를 다운로드하고 파일을 압축 해제한 후 **resources** 폴더 아래의 **LightCore.bundle**, **Light3DPlugin.bundle**, **LightBodyPlugin.bundle**, **LightHandPlugin.bundle**, **LightSegmentPlugin.bundle**을 제외한 **모든 bundle 리소스**를 프로젝트에 추가합니다.
6. Bundle Identifier를 라이선스에 바인딩된 Bundle Identifier로 변경합니다.
:::
::: SDK를 다운로드하고 수동으로 가져오기
1. [SDK 및 뷰티필터 리소스](https://www.tencentcloud.com/document/product/1143/45377)를 다운로드하고 압축을 해제합니다. frameworks 폴더에는 sdk가 포함되어 있고 resources 폴더에는 뷰티필터 bundle 리소스가 포함되어 있습니다.
2. Xcode 프로젝트를 열고 frameworks 폴더의 framework 를 실제 프로젝트에 추가하고 실행할 target을 선택한 다음 **General** 항목을 선택하고 **Frameworks,Libraries,and Embedded Content** 항목 펼치기를 클릭합니다. 하단의 ‘+’ 아이콘을 클릭하여 종속 라이브러리를 추가합니다. 다운로드한 `XMagic.framework`, `YTCommonXMagic.framework`, `libpag.framework` 및 필요한 종속 라이브러리 `MetalPerformanceShaders.framework`, `CoreTelephony.framework`, `JavaScriptCore.framework`, `VideoToolbox.framework`, `libc++.tbd`를 차례로 추가하고 필요에 따라 다른 툴 라이브러리 `Masonry.framework`(제어 레이아웃 라이브러리), `SSZipArchive`(파일 압축 해제 라이브러리)를 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/64aacf4305d7adf3a2bbe025920be517.png)
3. resources 폴더에 있는 뷰티필터 리소스를 실제 프로젝트에 추가합니다.
4. Bundle Identifier를 라이선스에 바인딩된 Bundle Identifier로 변경합니다.
:::
::: 동적 다운로드 통합
패키지 크기를 줄이기 위해 SDK에 필요한 모델 리소스 및 애니메이션 리소스 MotionRes(일부 기본 버전 SDK 애니메이션 리소스 없음)를 인터넷으로 변경하여 다운로드할 수 있습니다. 다운로드가 완료 후 위 파일의 경로를 SDK로 설정합니다.

Demo의 다운로드 로직을 재사용하는 것이 좋습니다. 기존 다운로드 서비스를 사용할 수도 있습니다. 동적 다운로드에 대한 자세한 지침은 [SDK 패키지 축소(iOS)](https://www.tencentcloud.com/document/product/1143/48644)를 참고하십시오.
:::
</dx-tabs>

### 권한 설정
Info.plist 파일에 해당 권한에 대한 설명을 추가하십시오. 그렇지 않으면 iOS 10 시스템에서 프로그램이 크래쉬될 수 있습니다. App이 카메라를 사용할 수 있도록 Privacy - Camera Usage Description에서 카메라 권한을 활성화하십시오.

## 통합 단계

### 1단계: 인증
1. 라이선스를 신청하고 LicenseURL과 LicenseKEY를 받습니다.
>! 일반적인 상황에서는 App이 한 번만 성공적으로 연결되면 인증 프로세스를 완료할 수 있으므로 License 파일을 프로젝트의 프로젝트 디렉터리에 넣을 **필요가 없습니다**. 하지만 App이 인터넷에 연결되지 않은 상태에서도 SDK 관련 기능을 사용하려면 License 파일을 다운로드하여 프로젝트 디렉터리에 넣을 수 있으며, License 파일 이름은 반드시 `v_cube.license`여야 합니다.
2. 해당 비즈니스 모듈의 초기화 코드에 URL과 KEY를 설정하여 license 다운로드를 트리거하여 사용 전에 임시로 다운로드하는 것을 피합니다. AppDelegate의 didFinishLaunchingWithOptions 메소드에서도 다운로드가 실행될 수 있습니다. 이 중 LicenseURL과 LicenseKey는 콘솔이 License에 바인딩될 때 생성되는 권한 정보입니다.
```
[TELicenseCheck setTELicense:LicenseURL key:LicenseKey completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
	if (authresult == TELicenseCheckOk) {
		NSLog(@"인증 성공");
	} else {
		NSLog(@"인증 실패");
	}
}];
```
**errorCode 인증 설명**:
<table>
<thead>
<tr>
<th>에러 코드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>성공. Success</td>
</tr>
<tr>
<td>-1</td>
<td>잘못된 입력 매개변수, 예시: 빈 URL 또는 KEY</td>
</tr><tr>
<td>-3</td>
<td>다운로드 실패, 네트워크 설정 확인</td>
</tr><tr>
<td>-4</td>
<td>로컬에서 읽은 TE 인증 정보가 비어 있음, 이는 IO 실패로 인해 발생한 것일 수 있습니다.</td>
</tr><tr>
<td>-5</td>
<td>VCUBE TEMP License 파일 읽기 내용이 비어 있습니다. 이는 IO 실패로 인한 것일 수 있습니다.</td>
</tr><tr>
<td>-6</td>
<td>v_cube.license 파일 JSON 필드가 잘못되었습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-7</td>
<td>서명 인증 실패. 처리를 위해 Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-8</td>
<td>복호화 실패. 처리를 위해 Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-9</td>
<td>TELicense 필드의 JSON 필드가 올바르지 않습니다. 처리를 위해 Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-10</td>
<td>네트워크에서 리졸브된 TE 인증 정보가 비어 있습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-11</td>
<td>IO 실패로 인해 로컬 파일에 TE 인증 정보를 쓰지 못했습니다.</td>
</tr><tr>
<td>-12</td>
<td>다운로드에 실패했으며 로컬 asset의 리졸브도 실패했습니다.</td>
</tr><tr>
<td>-13</td>
<td>인증 실패</td>
</tr><tr>
<td>기타</td>
<td>Tencent Cloud 팀에 문의하십시오.</td>
</tr>
</tbody></table>

[](id:step3)
### 2단계: SDK(XMagic.framework) 로딩
Tencent 특수 효과 SDK를 사용하는 라이프사이클은 대략 다음과 같습니다.
1. 뷰티 필터 관련 리소스를 로딩합니다.
```
NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
	@"root_path":[[NSBundle mainBundle] bundlePath]
};
```
2. Tencent 특수 효과 SDK를 초기화합니다.
```
initWithRenderSize:assetsDict: (XMagic)
self.beautyKit = [[XMagic alloc] initWithRenderSize:previewSize assetsDict:assetsDict];
```
3. Tencent 특수 효과 SDK는 데이터의 각 프레임을 처리하고 해당 처리 결과를 반환합니다.
```
process: (XMagic)
```
```
// 카메라 콜백에서 프레임 데이터 전달
- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection;

// 원시 데이터를 가져와 각 프레임의 렌더링 정보 처리
- (void)mycaptureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)inputSampleBuffer fromConnection:(AVCaptureConnection *)connection originImageProcess:(BOOL)originImageProcess;

// CPU를 사용하여 데이터 처리
- (YTProcessOutput*)processDataWithCpuFuc:(CMSampleBufferRef)inputSampleBuffer;

// GPU를 사용하여 데이터 처리
- (YTProcessOutput*)processDataWithGpuFuc:(CMSampleBufferRef)inputSampleBuffer;

// Tencent 특수 효과 SDK 처리 데이터 인터페이스
/// @param input 처리 데이터 정보 입력
/// @return 처리된 데이터 정보 출력
- (YTProcessOutput* _Nonnull)process:(YTProcessInput * _Nonnull)input;
```
4. Tencent 특수 효과 SDK를 릴리스합니다.
```
deinit (XMagic)
// SDK 리소스를 릴리스해야 하는 위치에서 호출
[self.beautyKit deinit]
```

>? 상기 단계를 완료한 후 사용자는 실제 필요에 따라 전시 타이밍 및 기타 장치 관련 환경을 제어할 수 있습니다.

## FAQ

[](id:que1)
### 질문1: 컴파일 오류: “unexpected service error: build aborted due to an internal error: unable to write manifest to-xxxx-manifest.xcbuild': mkdir(/data, S_IRWXU | S_IRWXG | S_IRWXO): Read-only file system (30):”가 보고되는 이유는 무엇입니까?

1. **File** > **Project settings** > **Build System**으로 이동하고 **Legacy Build System**을 선택합니다.
2. Xcode 13.0++  은 **File** > **Workspace Settings**에서 **Do not show a diagnostic issue about build system deprecation**을 선택해야 합니다.

[](id:que2)
### 질문2: iOS에서 리소스 가져오기 실행 후 “Xcode 12.X 버전 컴파일 Building for iOS Simulator, but the linked and embedded framework '.framework'...” 오류가 보고되는 이유는 무엇입니까?

**Buil Settings** > **Build Options** > **Validate Workspace**를 Yes로 변경한 다음**실행**을 클릭합니다.
>?  Validate Workspace를 Yes로 변경한 후, 컴파일이 완료된 후 다시 No로 변경하면 정상적으로 실행될 수 있으니 유의하시기 바랍니다.

[](id:que3)
### 질문3: 필터 설정이 반응이 없습니다.
아래에 설정된 값이 올바른지, 범위가 0-100인지 확인하십시오. 값이 너무 작아서 효과가 명확하지 않을 수 있습니다.

[](id:que4)
### 질문4: iOS Demo를 컴파일할 때 dSYM 생성 시 오류가 보고되는 이유는 무엇입니까?
```
PhaseScriptExecution CMake\ PostBuild\ Rules build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh
    cd /Users/zhenli/Downloads/xmagic_s106
    /bin/sh -c /Users/zhenli/Downloads/xmagic_s106/build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh

Command /bin/sh failed with exit code 1
```
 - 문제 원인: `libpag.framework 및 Masonary.framework` 재서명 실패.
 - 해결 방법:
  1. `demo/copy_framework.sh`를 엽니다.
  2. 다음 명령을 사용하여 로컬 cmake의 경로를 확인하고 `$(what cmake)`를 로컬 cmake의 절대 경로로 변경합니다.
```
which cmake
```
  3. 자신의 서명으로 모든 `Apple Development: ……`를 교체합니다.
