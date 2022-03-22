## 통합 준비[](id:ready)

1. [Demo 패키지](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/iOS/2.4.1vcube/UGSV-API-Example.zip)를 다운로드하고 압축 해제합니다. Demo 프로젝트의 xmagic 모듈(bundle, XmagicIconRes 아래에 있는 파일 2개, **Record** > **View** 폴더에 있는 파일)을 실제 항목의 프로젝트로 가져옵니다.
2. lib 디렉터리에서 `libpag.framework`, `Masonry.framework`, `XMagic.framework` 및 `YTCommonXMagic.framework`를 가져옵니다.
3. framework 서명 **General--> Masonry.framework** 및 **libpag.framework**에서 **Embed & Sign**을 선택합니다.
4. Bundle ID를 신청한 테스트 권한과 동일하게 수정합니다.

## SDK 인터페이스 통합 [](id:step)

- [1단계](#step1) 및 [2단계](#step2)는 Demo 프로젝트의 UGCKitRecordViewController 클래스 viewDidLoad, buildBeautySDK 메소드를 참고하십시오.
- [4단계](#step4)부터 [7단계](#step7)까지 Demo 프로젝트의 UGCKitRecordViewController 및 BeautyView 클래스 관련 인스턴스 코드를 참고하십시오.

### 1단계: 인증 초기화[](id:step1)
1. 프로젝트 AppDelegate의 didFinishLaunchingWithOptions에 다음 코드를 추가합니다. 여기서 LicenseURL과 LicenseKey는 Tencent Cloud 공식 웹사이트에서 신청한 인증 정보입니다. [License 가이드](https://intl.cloud.tencent.com/document/product/1143/45380)를 참고하십시오.
```
[TXUGCBase setLicenceURL:LicenseURL key:LicenseKey];

[TELicenseCheck setTELicense:@"https://license.vod2.myqcloud.com/license/v2/1258289294_1/v_cube.license" key:@"3c16909893f53b9600bc63941162cea3" completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
              if (authresult == TELicenseCheckOk) {
                   NSLog(@"인증 성공");
               } else {
                   NSLog(@"인증 실패");
               }
       }];
```
2. 인증 코드는 Demo의 UGCKitRecordViewController 클래스 viewDidLoad에 있는 인증 코드를 참고하십시오.
```
NSString *licenseInfo = [TXUGCBase getLicenceInfo];
NSData *jsonData = [licenseInfo dataUsingEncoding:NSUTF8StringEncoding];
NSError *err = nil;
NSDictionary *dic = [NSJSONSerialization JSONObjectWithData:jsonData
options:NSJSONReadingMutableContainers error:&err];
NSString *xmagicLicBase64Str = [dic objectForKey:@"TELicense"];

//xmagic 인증 초기화
int authRet = [XMagicAuthManager initAuthByString:xmagicLicBase64Str withSecretKey:@""];// withSecretKey는 빈 문자열이며 내용을 채울 필요가 없습니다.
NSLog(@"xmagic auth ret : %i", authRet);
NSLog(@"xmagic auth version : %@", [XMagicAuthManager getVersion]);
```

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
```
// Register log
[self.beautyKit registerSDKEventListener:self];
[self.beautyKit registerLoggerListener:self withDefaultLevel:YT_SDK_ERROR_LEVEL];
```

### 4단계: 뷰티 필터의 다양한 효과 설정[](id:step4)

```
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

### 5단계: 렌더링[](id:step5)
UGSV 사전 처리 프레임 콜백 인터페이스에서 YTProcessInput을 구성하고 textureId를 SDK에 전달하여 렌더링합니다.

```
 [self.xMagicKit process:inputCPU withOrigin:YtLightImageOriginTopLeft withOrientation:YtLightCameraRotation0]
```

### 6단계: SDK 일시 중지/복구 [](id:step6)

```
[self.beautyKit onPause];
[self.beautyKit onResume];
```

### 7단계: 레이아웃에 SDK 뷰티 필터 패널 추가[](id:step7)

```
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
