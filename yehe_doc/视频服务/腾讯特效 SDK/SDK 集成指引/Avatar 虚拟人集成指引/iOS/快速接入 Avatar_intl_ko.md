Avatar는 Tencent Effect SDK의 기능입니다. 사용하기 위해서는 먼저 SDK 통합 후 Avatar 소재를 추가해야 합니다. SDK 통합 방법은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45384)를 참고하십시오.

## 1단계: Avatar 소재 준비
1. Tencent Effect SDK를 통합합니다.
2. 당사 웹 사이트에서 Demo 프로젝트를 다운로드하고 압축을 풉니다.
3. Demo의 `BeautyDemo/bundle/avatarMotionRes.bundle`을 프로젝트에 복사합니다.

## 2단계: Demo UI 통합
### 통합 방법
1. 프로젝트에서 BeautyDemo와 동일한 Avatar UI를 사용하려면 다음을 수행합니다.
2. Demo의 `BeautyDemo/Avatar` 폴더에 있는 모든 클래스를 프로젝트에 복사하고 다음 코드를 추가합니다.
```objective-c
	 AvatarViewController *avatarVC = [[AvatarViewController alloc] init];
	 avatarVC.modalPresentationStyle = UIModalPresentationFullScreen;
	 avatarVC.currentDebugProcessType = AvatarPixelData; // 이미지 또는 텍스처 Id
	 [self presentViewController:avatarVC animated:YES completion:nil];
```

### Demo UI

#### 1. Demo UI[](id:demoui)
<img src="https://qcloudimg.tencent-cloud.cn/raw/1b25592a83e2e7f38ded001ca8c0b93b.png" style="zoom:66%;" />

#### 2. 구현
조작 패널의 데이터는 JSON 파일을 파싱하여 얻습니다. Demo의 `BeautyDemo/Avatar/` 디렉터리에서 이 파일을 찾을 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ae4858642c7dedcba05514a2ffed06a.png" style="zoom:100%;" />
- **JSON 구조와 패널 요소 간의 매핑**
	- head는 최상위 메뉴의 첫 번째 icon에 해당합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6547824e221494545e5353e8dce5e1cc.png" style="zoom:67%;" />
	- subTabs는 2단계 메뉴에 해당합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0cb8236d813fc9ec278b7026063a7b88.png" style="zoom:67%;" />
	- items는 3단계 메뉴에 해당합니다.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/2ad79a0d0efcb34cc5c1816975badfd8.png" style="zoom:67%;" />
- **SDK API용 Avatar 객체 데이터와 패널 데이터 연결**
아래의 첫 번째 스크린샷은 SDK에서 얻은 avatar 사전입니다(key는 categor를 나타내고 value는 avatar 데이터 배열입니다). 두 번째 스크린샷은 패널 데이터입니다. 사용자가 패널에서 아이콘을 탭하면 2단계 category(**빨간색 상자**)에서 category를 가져오고 SDK에서 반환하는 avata 사전에서 해당 카테고리의 avatarData 배열을 가져옵니다. 3단계 제목(**파란색 상자**)에서 ID를 가져온 다음 카테고리의 avatarData 배열에서 avatar 객체를 찾습니다. SDK의 updateAvatar API에 객체를 전달하여 avatar를 편집합니다.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/c908600561bded5e9f2ba20b5cde0029.png" style="zoom: 43%;" />

<img src="https://qcloudimg.tencent-cloud.cn/raw/2de257429b7abaa5e21923c292dd5c9a.png" style="zoom: 43%;" />

#### 3. 아이콘/제목 변경
[Demo UI](#demoui)의 위 JSON 파일을 수정하여 UI의 icon이나 제목을 변경할 수 있습니다. 예를 들어 최상위 메뉴에서 **헤더** icon을 변경하려면 아래의 iconUrl 또는 checkedIconUrl 값을 수정하면 됩니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/58e042d3fb8cb0588062dde318063a5e.png" style="zoom:57%;" />

## 3단계: 아바타 기능 사용자 지정
`BeautyDemo/Avatar/Controller`에서 **AvatarViewController** 코드를 참고할 수 있습니다.
>? 아바타 API에 대한 자세한 내용은 [Avatar APIs](https://www.tencentcloud.com/document/product/1143/51287)를 참고하십시오.

1. xmagic 객체를 생성하고 기본 Avatar 템플릿을 구성합니다.
```objectivec
- (void)buildBeautySDK {

	CGSize previewSize = CGSizeMake(kPreviewWidth, kPreviewHeight);
	NSString *beautyConfigPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
	beautyConfigPath = [beautyConfigPath stringByAppendingPathComponent:@"beauty_config.json"];
	NSFileManager *localFileManager=[[NSFileManager alloc] init];
	BOOL isDir = YES;
	NSDictionary * beautyConfigJson = @{};
	if ([localFileManager fileExistsAtPath:beautyConfigPath isDirectory:&isDir] && !isDir) {
			NSString *beautyConfigJsonStr = [NSString stringWithContentsOfFile:beautyConfigPath encoding:NSUTF8StringEncoding error:nil];
			NSError *jsonError;
			NSData *objectData = [beautyConfigJsonStr dataUsingEncoding:NSUTF8StringEncoding];
			beautyConfigJson = [NSJSONSerialization JSONObjectWithData:objectData                                                           options:NSJSONReadingMutableContainers
																															 error:&jsonError];
	}
	NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
															 @"root_path":[[NSBundle mainBundle] bundlePath],
															 @"tnn_"
															 @"beauty_config":beautyConfigJson
	};
	// Init beauty kit
	self.beautyKit = [[XMagic alloc] initWithRenderSize:previewSize assetsDict:assetsDict];
	// Register log
	[self.beautyKit registerSDKEventListener:self];
	[self.beautyKit registerLoggerListener:self withDefaultLevel:YT_SDK_ERROR_LEVEL];

	// 아바타 소재의 경로를 전달하여 기본 아바타 로딩
	AvatarGender gender = self.genderBtn.isSelected ? AvatarGenderFemale : AvatarGenderMale;
	NSString *bundlePath = [self.resManager avatarResPath:gender];
	[self.beautyKit loadAvatar:bundlePath exportedAvatar:nil];

}
```
2. Avatar 소재의 소스 데이터 가져오기
```objectivec
@implementation AvatarViewController
_resManager = [[AvatarResManager alloc] init];
NSDictionary *avatarDict = self.resManager.getMaleAvatarData;
@end


@implementation AvatarResManager

- (NSDictionary *)getMaleAvatarData
{
	if (!_maleAvatarDict) {
			NSString *resDir = [self avatarResPath:AvatarGenderFemale];
			NSString *savedConfig = [self getSavedAvatarConfigs:AvatarGenderMale];
			// SDK의 API를 호출하여 소스 데이터 파싱
			_maleAvatarDict = [XMagic getAvatarConfig:resDir exportedAvatar:savedConfig];
	}
	return _maleAvatarDict;
}
@end
```
3. 아바타 편집
```objectivec
// sdk API로 파싱된 소재 소스 데이터에서 원하는 avatar 객체를 가져와서 sdk에 전달
NSMutableArray *avatars = [NSMutableArray array];
// avatarConfig는 getAvatarConfig:exportedAvatar: sdk API로 얻은 avatar 객체
[avatars addObject:avatarConfig];
// 아래 API를 호출하여 실시간으로 아바타 수정(얼굴 수정, 옷 입히기)
[self.beautyKit updateAvatar:avatars];
```
4. 아바타 객체를 문자열로 내보내기
구성된 Avatar 객체를 문자열로 내보냅니다. 사용자 지정 위치에 저장할 수 있습니다.
```objectivec
- (BOOL)saveSelectedAvatarConfigs:(AvatarGender)gender
{
	NSMutableArray *avatarArr = [NSMutableArray array];
	NSDictionary *avatarDict = gender == AvatarGenderMale ? _maleAvatarDict : _femaleAvatarDict;
	// 1. 선택한 avatar 객체를 찾기 위해 순회
	for (NSArray *arr in avatarDict.allValues) {
			for (AvatarData *config in arr) {
					if (config.type == AvatarDataTypeSelector) {
							if (config.isSelected) {
									[avatarArr addObject:config];
							}
					} else {
							[avatarArr addObject:config];
					}
			}
	}
	// 2. sdk API를 호출하여 선택된 avatar 객체를 문자열로 내보내기
	NSString *savedConfig = [XMagic exportAvatar:avatarArr.copy];
	if (savedConfig.length <= 0) {
			return NO;
	}
	NSError *error;
	NSString *fileName = [self getSaveNameWithGender:gender];
	NSString *savePath = [_saveDir stringByAppendingPathComponent:fileName];
	// 디렉터리가 존재하는지 확인하고 없으면 디렉터리 생성
	BOOL isDir;
	if (![[NSFileManager defaultManager] fileExistsAtPath:_saveDir isDirectory:&isDir]) {
			[[NSFileManager defaultManager] createDirectoryAtPath:_saveDir withIntermediateDirectories:YES attributes:nil error:nil];
	}
	// 3. 이후 사용을 위해 내보낸 문자열을 샌드박스에 쓰기
	[savedConfig writeToFile:savePath atomically:YES encoding:NSUTF8StringEncoding error:&error];
	if (error){
			return NO;
	}
	return YES;
}
```
5. 배경 변경
```objectivec
- (void)bgExchangeClick:(UIButton *)btn
{
	btn.selected = !btn.isSelected;
	NSDictionary *avatarDict = self.resManager.getFemaleAvatarData;
	NSArray *array = avatarDict[@"background_plane"];
	AvatarData *selConfig;
	// 배경도 avatar 객체(카테고리는 `background_plane`)이며, 배경을 바꾸는 것은 기본적으로 다른 avatar 객체를 사용하는 것임
	for (AvatarData *config in array) {
			if ([config.Id isEqual:@"none"]) {
					if (btn.selected) {
							selConfig = config;
							break;
					}
			} else {
					selConfig = config;
			}
	}
	[self.beautyKit updateAvatar:@[selConfig]];
}
```