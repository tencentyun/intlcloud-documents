## 통합 준비

1. [Demo 패키지](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/iOS/2.4.1vcube/TRTC-API-Example.zip)를 다운로드하고 압축을 풀고, Demo 프로젝트에서 실제 항목 프로젝트로 xmagic 모듈(bundle, XmagicIconRes, Xmagic 폴더)을 가져옵니다.
2. SDK 디렉터리에서 `libpag.framework`, `Masonry.framework`, `XMagic.framework`, `YTCommonXMagic.framework`를 가져옵니다.
3. framework 서명 **General--> Masonry.framework** 및 **libpag.framework**에서 **Embed & Sign**을 선택합니다.
4. Bundle ID를 신청한 테스트 인증과 동일하게 수정합니다.

## SDK 인터페이스 통합 

- [1단계](#step1) 및 [2단계](#step2)는 Demo 프로젝트의 ThirdBeautyViewController 클래스의 viewDidLoad, buildBeautySDK 메소드를 참고하시기 바라며, Xmagic 인증은 AppDelegate 클래스의 application 메소드에서 수행됩니다.
- [4단계](#step4)부터 [7단계](#step7)까지 Demo 프로젝트의 ThirdBeautyViewController와 BeautyView 클래스의 해당 인스턴스 코드를 참고하시기 바랍니다.

### 1단계: 인증 초기화[](id:step1)

1. 먼저 프로젝트 AppDelegate의 didFinishLaunchingWithOptions에 다음 인증 코드를 추가합니다. 여기서 LicenseURL 및 LicenseKey는 Tencent Cloud 공식 웹사이트에서 신청한 인증 정보입니다. [License 가이드](https://intl.cloud.tencent.com/document/product/1143/45380)를 참고하십시오.
```
[TXLiveBase setLicenceURL:LicenseURL key:LicenseKey];
```
2. Xmagic 인증: 해당 비즈니스 모듈의 초기화 코드에 URL과 KEY를 설정하고 License 다운로드를 트리거하고 사용 전에 임시 다운로드하는 것을 피하십시오. AppDelegate의 didFinishLaunchingWithOptions 메소드에서도 다운로드가 실행될 수 있습니다. LicenseURL 및 LicenseKey는 콘솔이 License를 바인딩할 때 생성되는 인증 정보입니다.
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
</tr>
<tr>
<td>-3</td>
<td>다운로드 단계 실패, 네트워크 설정을 확인하십시오.</td>
</tr>
<tr>
<td>-4</td>
<td>로컬에서 읽은 TE 인증 정보가 비어 있습니다. 이는 IO 실패로 인해 발생할 수 있습니다.</td>
</tr>
<tr>
<td>-5</td>
<td>VCUBE TEMP License 파일 읽기 내용이 비어 있습니다. 이는 IO 실패로 인한 것일 수 있습니다.</td>
</tr>
<tr>
<td>-6</td>
<td>v_cube.license 파일 JSON 필드가 잘못되었습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-7</td>
<td>서명 확인에 실패했습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-8</td>
<td>복호화에 실패했습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-9</td>
<td>TELicense 필드의 JSON 필드가 올바르지 않습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-10</td>
<td>네트워크에서 리졸브된 TE 인증 정보가 비어 있습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-11</td>
<td>IO 실패로 인해 로컬 파일에 TE 인증 정보를 쓰지 못했습니다.</td>
</tr>
<tr>
<td>-12</td>
<td>다운로드 실패, 로컬 asset 구문 분석 실패</td>
</tr>
<tr>
<td>-13</td>
<td>인증 실패</td>
</tr>
<tr>
<td>기타</td>
<td>Tencent Cloud 팀에 문의하십시오.</td>
</tr>
</tbody></table>

### 2단계: SDK 소재 리소스 경로 설정[](id:step2)

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

### 5단계: [](id:step5) 렌더링
비디오 프레임 콜백 인터페이스에서 YTProcessInput을 구성하고 렌더링 처리를 위해 SDK에 전달합니다. Demo의 ThirdBeautyViewController를 참고하십시오.
```objectivec
 [self.xMagicKit process:inputCPU withOrigin:YtLightImageOriginTopLeft withOrientation:YtLightCameraRotation0]
```

### 6단계: SDK 일시 중지/복구 [](id:step6)

```objectivec
[self.beautyKit onPause];
[self.beautyKit onResume];
```

### 7단계: 레이아웃 에 SDK 뷰티 필터 패널 추가[](id:step7)
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

