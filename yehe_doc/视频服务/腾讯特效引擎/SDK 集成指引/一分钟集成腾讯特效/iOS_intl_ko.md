## 통합 준비

### 개발자 환경 요건

- 개발 툴 XCode 11 이상: App Store 또는 [다운로드 링크](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/iOS/2.4.1.18/demo.zip)를 클릭하십시오.
- 권장 실행 환경:
  - 기기 사양: iPhone 5 이상. iPhone 6 이하의 경우 전면 카메라는 720p까지 지원하며 1080p는 지원되지 않습니다.
  - 시스템 요구 사항: iOS 10.0 이상.

### C/C++ 레이어 개발 환경

XCode 기본 C++ 환경.

<table>
<tr><th>유형</th><th>종속 라이브러리</th></tr>
<tr>
<td>시스템 종속 라이브러리</td>
<td><ul style="margin:0">
<li/>AVFoundation
<li/>Accelerate
<li/>AssetsLibrary
<li/>CoreML
<li/>JavaScriptCore
<li/>CoreFoundation
<li/>MetalPerformanceShaders
<li/>CoreTelephony
<li/>libc++.tbd
</ul></td>
</tr>
<tr>
<td>내장 라이브러리</td>
<td><ul style="margin:0">
<li/>YTCommon(인증 정적 라이브러리)
<li/>XMagic(뷰티 필터 정적 라이브러리)
<li/>libpag(비디오 디코딩 동적 라이브러리)
</ul></td>
</tr>
</table>

## 리소스 가져오기
### 리소스
- 필수 리소스 패기지: `LightCore.bundle`
- 키잉 기능 패기지: `LightSegmentPlugin.bundle`
- 손짓 기능 패키지: `LightHandPlugin.bundle`
- 3D 기능 패기지: `Light3DPlugin.bundle`

### 가져오기 방법
- **방법1**: 프로젝트 리소스에 추가하기만 하면 됩니다.
- **방법2**: `initWithRenderSize:assetsDict: (XMagic)` 경로를 지정하려면 여기에서 `assetsDict`를 통해 각 리소스 경로를 설정할 수 있습니다.

### 권한 설정
Info.plist 파일에 해당 권한에 대한 설명을 추가하십시오. 그렇지 않으면 iOS 10 시스템에서 프로그램이 크래쉬될 수 있습니다. App이 카메라를 사용할 수 있도록 Privacy - Camera Usage Description에서 카메라 권한을 활성화하십시오.

## 통합 단계

[](id:step1)
### 1단계: 서명 준비
framework 서명은 General-->Masonry.framework 및 libpag.framework에서 Embed & Sign을 직접 선택할 수 있습니다.
[](id:step2)
### 2단계: 인증
1. 인증 신청 후 LicenseURL과 LicenseKEY를 받으려면 [License 가이드](https://intl.cloud.tencent.com/document/product/1143/45380)를 참고하십시오.
> ! 일반적인 상황에서는 app이 한 번만 성공적으로 연결되면 인증 프로세스를 완료할 수 있으므로 License 파일을 프로젝트의 프로젝트 디렉터리에 넣을 **필요가 없습니다**. 하지만 app이 인터넷에 연결되지 않은 상태에서도 SDK 관련 기능을 사용해야 하는 경우 license 파일을 다운로드하여 프로젝트 디렉터리에 넣을 수 있으며, license 파일 이름은 반드시 v_cube.license여야 합니다.
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
<td>다운로드 링크 실패, 네트워크 설정을 확인하십시오.</td>
</tr><tr>
<td>-4</td>
<td>로컬에서 읽은 TE 인증 정보가 비어 있습니다. 이는 IO 실패로 인해 발생할 수 있습니다.</td>
</tr><tr>
<td>-5</td>
<td>VCUBE TEMP License 파일 읽기 내용이 비어 있습니다. 이는 IO 실패로 인한 것일 수 있습니다.</td>
</tr><tr>
<td>-6</td>
<td>v_cube.license 파일 JSON 필드가 잘못되었습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-7</td>
<td>서명 확인에 실패했습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-8</td>
<td>복호화에 실패했습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-9</td>
<td>TELicense 필드의 JSON 필드가 올바르지 않습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-10</td>
<td>네트워크에서 리졸브된 TE 인증 정보가 비어 있습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr><tr>
<td>-11</td>
<td>IO 실패로 인해 로컬 파일에 TE 인증 정보를 쓰지 못했습니다.</td>
</tr><tr>
<td>-12</td>
<td>다운로드 실패, 로컬 asset 구문 분석 실패</td>
</tr><tr>
<td>-13</td>
<td>인증 실패</td>
</tr><tr>
<td>기타</td>
<td>Tencent Cloud 팀에 문의하십시오.</td>
</tr>
</tbody></table>

[](id:step3)
### 3단계: SDK(XMagic.framework) 로딩
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

> ? 상기 단계를 완료한 후 사용자는 실제 필요에 따라 전시 타이밍 및 기타 장치 관련 환경을 제어할 수 있습니다.

## FAQ

[](id:que1)
### 질문1: 컴파일 오류: “unexpected service error: build aborted due to an internal error: unable to write manifest to-xxxx-manifest.xcbuild': mkdir(/data, S_IRWXU | S_IRWXG | S_IRWXO): Read-only file system (30):”가 보고되는 이유는 무엇입니까?

1. **File** > **Project settings** > **Build System**으로 이동하고 **Legacy Build System**을 선택합니다.
2. Xcode 13.0++  은 **File** > **Workspace Settings**에서 **Do not show a diagnostic issue about build system deprecation**을 선택해야 합니다.

[](id:que2)
### 질문2: iOS에서 리소스 가져오기 실행 후 “Xcode 12.X 버전 컴파일 Building for iOS Simulator, but the linked and embedded framework '.framework'...” 오류가 보고되는 이유는 무엇입니까?

**Buil Settings** > **Build Options** > **Validate Workspace**를 Yes로 변경한 다음**실행**을 클릭합니다.
> ?  Validate Workspace를 Yes로 변경한 후, 컴파일이 완료된 후 다시 No로 변경하면 정상적으로 실행될 수 있으니 여기에서 이 문제에 주의하시기 바랍니다.

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
