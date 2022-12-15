## 통합 준비[](id:ready)

1. [Demo 패키지](https://intl.cloud.tencent.com/document/product/1143/45374)를 다운로드한 후 압축을 해제하고 `demo/XiaoShiPin/` 디렉터리의 xmagickit 폴더를 프로젝트의 Podfile 디렉터리에 복사합니다.
2. Podfile에 다음 종속성을 추가하고 `pod install`을 실행하여 가져오기를 완료합니다.
```
pod 'xmagickit', :path => 'xmagickit/xmagickit.podspec'
```
3. Bundle ID를 신청한 테스트 권한과 동일하게 수정합니다.

### 개발자 환경 요건
- Xcode 11 이상: App Store 또는 [여기](https://developer.apple.com/xcode/resources/)에서 다운로드하십시오.
- 권장 실행 환경:
  - 기기 사양: iPhone 5 이상. iPhone 6 이하의 경우 전면 카메라는 720p까지 지원하며 1080p는 지원되지 않습니다.
  - 시스템 요구 사항: iOS 12.0 이상.


## SDK 인터페이스 통합 [](id:step)
### 1단계: 인증 초기화[](id:step1)
AppDelegate의 didFinishLaunchingWithOptions에 다음 코드를 추가합니다(Tencent Cloud 웹사이트에서 얻은 인증 정보에 따라 LicenseURL과 LicenseKey를 설정).
```objectivec
[TXUGCBase setLicenceURL:LicenseURL key:LicenseKey];

[TELicenseCheck setTELicense:LicenseURLkey:LicenseKey completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
              if (authresult == TELicenseCheckOk) {
                   NSLog(@"인증 성공");
               } else {
                   NSLog(@"인증 실패");
               }
       }];
```
**errorCode 인증 설명**:

| 에러 코드 | 설명                                                    |
| :----- | :------------------------------------------------------ |
| 0      | 성공. Success                                           |
| -1     | 입력 매개변수가 잘못되었습니다. 예: URL 또는 KEY가 비어 있습니다                      |
| -3     | 다운로드 실패. 네트워크 설정을 확인하십시오                            |
| -4     | 로컬 시스템에서 읽은 TE SDK 인증 정보가 비어 있습니다. 이는 I/O 실패로 인해 발생할 수 있습니다        |
| -5     | 읽은 VCUBE TEMP License 파일의 내용이 비어 있습니다. 이는 I/O 실패로 인해 발생할 수 있습니다 |
| -6     | v_cube.license 파일의 JSON 필드가 올바르지 않습니다. 도움이 필요하면 Tencent Cloud에 문의하십시오 |
| -7     | 서명 검증 실패. 도움이 필요하면 Tencent Cloud에 문의하십시오                      |
| -8     | 암호 해독 실패. 도움이 필요하면 Tencent Cloud에 문의하십시오                          |
| -9     | TELicense 필드의 JSON 필드가 올바르지 않습니다. 도움이 필요한 경우 Tencent Cloud에 문의하십시오  |
| -10    | 네트워크에서 리졸브된 TE 인증 정보가 비어 있습니다. 도움이 필요한 경우 Tencent Cloud에 문의하십시오      |
| -11    | IO 실패로 인해 TE SDK 인증 정보를 로컬 파일에 쓰지 못했습니다      |
| -12    | 다운로드에 실패했으며 로컬 asset을 리졸브하지 못했습니다                         |
| -13    | 인증 실패                                                |
| 기타   | 도움이 필요한 경우 Tencent Cloud에 문의하십시오                                    |


### 2단계: SDK 소재 리소스 경로 설정 [](id:step2)

```objectivec
CGSize previewSize = [self getPreviewSizeByResolution:self.currentPreviewResolution];
NSString *beautyConfigPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
beautyConfigPath = [beautyConfigPath stringByAppendingPathComponent:@"beauty_config.json"];
NSFileManager *localFileManager=[[NSFileManager alloc] init];
BOOL isDir = YES;
NSDictionary * beautyConfigJson = @{};
if ([localFileManager fileExistsAtPath:beautyConfigPath isDirectory:&isDir] && !isDir) {
	NSString *beautyConfigJsonStr = [NSString stringWithContentsOfFile:beautyConfigPath encoding:NSUTF8StringEncoding error:nil];
	NSError *jsonError;
	NSData *objectData = [beautyConfigJsonStr dataUsingEncoding:NSUTF8StringEncoding];
	beautyConfigJson = [NSJSONSerialization JSONObjectWithData:objectData
											options:NSJSONReadingMutableContainers
											error:&jsonError];
}
NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
							@"root_path":[[NSBundle mainBundle] bundlePath],
							@"tnn_"
							@"beauty_config":beautyConfigJson
};
// Init beauty kit
self.beautyKit = [[XMagic alloc] initWithRenderSize:previewSize assetsDict:assetsDict];
```

### 3단계: 로그 및 이벤트 리스너 추가[](id:step3)
```objectivec
// Register log
[self.beautyKit registerSDKEventListener:self];
[self.beautyKit registerLoggerListener:self withDefaultLevel:YT_SDK_ERROR_LEVEL];
```

### 4단계: 뷰티 필터의 다양한 효과 설정[](id:step4)
```objectivec
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

### 5단계: 렌더링[](id:step5)
UGSV 사전 처리 프레임 콜백 인터페이스에서 YTProcessInput을 구성하고 textureId를 SDK에 전달하여 렌더링합니다.

```
 [self.xMagicKit process:inputCPU withOrigin:YtLightImageOriginTopLeft withOrientation:YtLightCameraRotation0]
```

### 6단계: SDK 일시 중지/복구 [](id:step6)

```objectivec
[self.beautyKit onPause];
[self.beautyKit onResume];
```

### 7단계: 레이아웃에 SDK 뷰티 필터 패널 추가[](id:step7)
```objectivec
UIEdgeInsets gSafeInset;
#if __IPHONE_11_0 && __IPHONE_OS_VERSION_MAX_ALLOWED >= __IPHONE_11_0
if(gSafeInset.bottom > 0){
}
if (@available(iOS 11.0, *)) {
	gSafeInset = [UIApplication sharedApplication].keyWindow.safeAreaInsets;
} else
#endif
	{
		gSafeInset = UIEdgeInsetsZero;
	}

dispatch_async(dispatch_get_main_queue(), ^{
	//뷰티 필터 옵션 인터페이스
	_vBeauty = [[BeautyView alloc] init];
	[self.view addSubview:_vBeauty];
	[_vBeauty mas_makeConstraints:^(MASConstraintMaker *make) {
		make.width.mas_equalTo(self.view);
		make.centerX.mas_equalTo(self.view);
		make.height.mas_equalTo(254);
		if(gSafeInset.bottom > 0.0){  // 전체 화면으로 조정
			make.bottom.mas_equalTo(self.view.mas_bottom).mas_offset(0);
		} else {
			make.bottom.mas_equalTo(self.view.mas_bottom).mas_offset(-10);
		}
	}];
		_vBeauty.hidden = YES;
});
```