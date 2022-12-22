## SDK 통합

SDK 다운로드 및 통합 방법, 라이선스 설정 방법, Demo 프로젝트 실행 방법은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45384)를 참고하십시오.

## 아바타 소재 준비

압축 해제 후 SDK 패키지의 `MotionRes/avatarRes` 디렉터리에서 찾을 수 있는 다양한 얼굴 사용자 정의 및 드레스업 자료 세트를 제공합니다. 다른 애니메이션 효과 자료와 마찬가지로 프로젝트의 assets 디렉터리에 copy해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f712ea1424c224b5cac36403c4c218bf.png)

## 아바타 DIY 및 SDK API
<table>
<tr>
	<th style="text-align:center">아바타 DIY</th>
	<th style="text-align:center">사진 기반 아바타 DIY</th>
</tr>
<tr>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/8dab03ae9b380cca30b7fb1408a82bdd.jpg" width=650></td>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/8fe57503adf3f4f269de09edc178459f.jpg" width=550></td>
</tr>
</table>


아래 섹션에서는 데이터 로딩, 아바타 DIY 및 사진 기반 아바타 DIY를 위한 API를 포함하여 `XMagicApi의 API에 대한 설명을 제공합니다.

### 1. Avatar 소스 데이터 가져오기(`getAvatarConfig`)
```swift
+ (NSDictionary <NSString *, NSArray *>* _Nullable)getAvatarConfig:(NSString * _Nullable)resPath exportedAvatar:(NSString *_Nullable)exportedAvatar;
```

- **입력 매개변수**:
	- resPath: `/var/mobile/Containers/Data/Application/C82F1F7A-01A1-4404-8CF6-131B26B4DA1A/Library/Caches/avatarMotionRes.bundle/avatar_v2.0_male`과 같이 사용자의 모바일 장치에 있는 Avatar 소재의 절대 경로입니다.
	- exportedAvatar: 사용자가 마지막으로 아바타를 DIY했을 때부터 저장된 아바타 구성 데이터(JSON 문자열)입니다. 아바타를 처음으로 사용자 지정하거나 구성 데이터가 저장되지 않은 경우 nil을 전달하십시오.
- **출력 매개변수**:
	이 API는 NSDictionary 객체를 반환합니다. 여기서 dictionary의 key는 category(자세한 내용은 아래 TEDefine 클래스 참고)이고 value는 category의 데이터입니다. 응용 레이어가 dictionary 데이터를 가져온 후 필요에 따라 UI에 표시합니다.

### 2. 아바타 소재 로딩(loadAvatar)
```swift
- (void)loadAvatar:(NSString * _Nullable)resPath exportedAvatar:(NSString * _Nullable)exportedAvatar;
```
- **입력 매개변수**:
	- resPath: `/var/mobile/Containers/Data/Application/C82F1F7A-01A1-4404-8CF6-131B26B4DA1A/Library/Caches/avatarMotionRes.bundle/avatar_v2.0_male`과 같이 사용자의 모바일 장치에 있는 avatar 소재의 절대 경로입니다.
	- exportedAvatar: 사용자가 마지막으로 아바타를 사용자 지정했을 때부터 저장된 아바타 구성 데이터(JSON 문자열)입니다. 아바타를 처음으로 사용자 지정하거나 구성 데이터가 저장되지 않은 경우 nil을 전달하십시오.
- **출력 매개변수**:
이 API는 NSDictionary 객체를 반환합니다. 여기서 dictionary의 key는 category(자세한 내용은 아래 TEDefine 클래스 참고)이고 value는 category의 데이터입니다. 응용 레이어가 dictionary 데이터를 가져온 후 필요에 따라 UI에 표시합니다.

### 3. 얼굴 사용자 지정 및 옷 입히기(updateAvatar)
```swift
- (void)updateAvatar:(NSArray<AvatarData *> *_Nonnull)avatarDataList;
```

이 API가 호출되면 아바타 미리보기가 실시간으로 업데이트됩니다. 각 AvatarData 객체는 구성(예: 헤어스타일 변경)에 해당합니다. 여러 AvatarData 객체를 API 호출에 전달하여 아바타의 여러 측면을 편집할 수 있습니다(예: 헤어스타일 및 머리 색상 변경). API는 전달된 AvatarData 객체의 유효성을 검사합니다. 객체가 유효하면 SDK로 전달됩니다. 그렇지 않으면 callback이 전송됩니다.
- 예를 들어 헤어스타일을 변경하기 위해 AvatarData 객체가 전달되었지만 로컬 장치에서 헤어 모델 파일(AvatarData의 value로 지정됨)을 찾을 수 없는 경우 AvatarData 객체는 유효하지 않은 것으로 간주됩니다.
- 또한 홍채 이미지를 변경하기 위해 AvatarData 객체가 전달되었지만 로컬 장치에서 이미지 파일(AvatarData의 value로 지정됨)을 찾을 수 없는 경우 AvatarData 객체는 유효하지 않은 것으로 간주됩니다.

### 4. 아바타 설정 내보내기(exportAvatar)
```swift
+ (NSString *_Nullable)exportAvatar:(NSArray <AvatarData *>*_Nullable)avatarDataList;
```

사용자가 아바타를 편집하면 selected 값이나 AvatarData의 모양 값이 변경됩니다. 편집 후 새로운 AvatarData 목록이 생성되고 JSON 문자열로 내보낼 수 있습니다. 로컬에 저장하거나 서버에 업로드할 수 있습니다.
문자열은 다음 목적으로 내보내집니다.
- 다음 번에 XMagic의 **loadAvatar**를 호출하여 Avatar 소재를 로딩할 때 **exportedAvatar**를 JSON 문자열로 설정해야 미리 보기에서 마지막으로 아바타 설정을 기억할 수 있습니다.
- 또한 getAllAvatarData를 호출하여 selected와 Avatar 소스 데이터의 모양 값을 업데이트할 때 이 JSON 문자열을 전달해야 합니다.


### 5. 사진을 기반으로 아바타 DIY(createAvatarByPhoto)
이 API가 작동하려면 SDK가 인터넷에 연결되어 있어야 합니다.

```swift
+ (void)createAvatarByPhoto:(NSString * _Nullable)photoPath avatarResPaths:(NSArray <NSString *>* _Nullable)avatarResPaths isMale:(BOOL)isMale success:(nullable void (^)(NSString *_Nullable matchedResPath, NSString *_Nullable srcData))success failure:(nullable void (^)(NSInteger code, NSString *_Nullable msg))failure;
```

- **photoPath**: 사진 경로입니다. 얼굴이 사진 중앙에 오도록 합니다. 이상적으로는 사진에 얼굴이 하나만 포함되어야 합니다. 여러 개가 있는 경우 SDK는 임의로 하나를 선택합니다. 인식 결과를 보장하려면 사진의 짧은 면이 500px보다 길어야 합니다.
- **avatarResPaths**: 여러 세트의 Avatar 소재를 전달할 수 있으며 SDK는 사진 분석 결과에 따라 가장 적합한 세트를 선택합니다.
>! 현재 한 세트의 소재만 지원됩니다. 여러 세트가 전달되면 SDK는 첫 번째 세트를 사용합니다.

- **isMale**: 사람이 남성인지 여부입니다. 현재 이 속성은 사용되지 않습니다. 그러나 미래에 있을 수 있습니다. 올바른 값을 전달하는 것이 좋습니다.
- **success**: 성공적인 구성을 위한 콜백입니다. matchedResPath—일치하는 자료의 경로를 나타내고, srcData—일치 결과를 나타냅니다(exportAvatar의 반환 값과 동일).
- **failure**: 구성 실패 시 콜백입니다. code—오류 코드를 나타내고 msg—오류 메시지를 나타냅니다.

### 6. 다운로드한 구성 파일(addAvatarResource) 저장

```swift
+ (void)addAvatarResource:(NSString * _Nullable)rootPath category:(NSString * _Nullable)category filePath:(NSString * _Nullable)filePath completion:(nullable void (^)(NSError * _Nullable error, NSArray <AvatarData *>* _Nullable avatarList))completion;
```

Avatar 소재를 동적으로 다운로드하는 경우에 사용하는 API입니다. 예를 들어 10개의 헤어스타일을 제공하고 그 중 하나가 장치에 동적으로 다운로드된다고 가정합니다. 다운로드한 ZIP 파일의 경로를 SDK에 전달하려면 이 API를 호출해야 합니다. SDK는 파일을 파싱하여 해당 category의 폴더에 저장합니다. 다음에 getAllAvatarData를 호출하면 SDK가 새로 추가된 데이터를 반환합니다.

매개변수 설명:
- **rootPath**: `/var/mobile/Containers/Data/Application/C82F1F7A-01A1-4404-8CF6-131B26B4DA1A/Library/Caches/avatarMotionRes.bundle/avatar_v2.0_male`과 같은 Avatar 소재의 루트 디렉터리입니다.
- **category**: 다운로드한 자료의 카테고리입니다.
- **zipFilePath**: 다운로드한 ZIP 파일의 로컬 경로입니다.
- **completion**: 결과 콜백입니다. error—오류 메시지를 나타내고 avatarList—파싱 후 얻은 avatar 데이터 배열을 나타냅니다.

### 7. 사용자 지정 이벤트 보내기(sendCustomEvent)
이 API는 예를 들어 얼굴이 감지되지 않을 때 유휴 상태를 표시하기 위해 사용자 지정 이벤트를 보내는 데 사용됩니다.
```swift
- (void)sendCustomEvent:(NSString * _Nullable)eventKey eventValue:(NSString * _Nullable)eventValue;
```
- **eventKey**: 사용자 지정 이벤트의 key입니다. 자세한 내용은 TEDefine의 AvatarCustomEventKey를 참고하십시오.
- **eventValue**: 사용자 지정 이벤트의 value로 JSON 문자열입니다. 예를 들어 `@{@"enabel" : @(YES)}를 json 문자열로 변환하거나 @"{\\"enable\\" : true}"`를 직접 입력할 수 있습니다.

### 8. AvatarData 호출
AvatarData 클래스는 위 API의 핵심입니다. AvatarData에는 다음 필드가 포함됩니다.
```
/// @brief 구성 유형입니다.
@interface AvatarData : NSObject
/// 얼굴 모양 변경 또는 눈 조정 등. TEDefine에 정의된 표준 category가 요구 사항을 충족하지 못하는 경우 category를 사용자 지정할 수 있습니다(기존 category와 동일하지 않은지 확인). 이 필드는 비워 둘 수 없습니다.
@property (nonatomic, copy) NSString * _Nonnull category;
// 아바타 구성 item의 id입니다. 예를 들어 각 유형의 안경에는 고유한 id가 있습니다. 각 조정 항목도 마찬가지입니다. 이 필드는 비워 둘 수 없습니다.
@property (nonatomic, copy) NSString * _Nonnull Id;
// selector 또는 AvatarDataTypeSlider가 될 수 있는 유형입니다
@property (nonatomic, assign) AvatarDataType type;
/// 유형이 selector인 경우 이 필드는 항목이 선택되었는지 여부를 나타냅니다
@property (nonatomic, assign) BOOL isSelected;

/// 편집할 아바타의 부분. 예: 얼굴, 눈, 머리, 셔츠, 신발 등. 이를 구성하는 방법은 설명서를 참고하십시오
@property (nonatomic, copy) NSString * _Nonnull entityName;
/// entityName에서 수행할 작업(action)입니다. 자세한 내용은 설명서를 참고하십시오.
@property (nonatomic, copy) NSString * _Nonnull action;
/// entityName에서 수행할 action의 세부 정보입니다. 자세한 내용은 설명서를 참고하십시오.
@property (nonatomic, copy) NSDictionary * _Nonnull value;
@end
```

AvatarData 객체는 헤어스타일 변경이나 뺨 조정과 같은 가장 작은 구성 단위입니다.
<table>
<tr>
	<th style="text-align:center">헤어스타일 변경</th>
	<th style="text-align:center">뺨 조정</th>
</tr>
<tr>
	<td><img src="https://qcloudimg.tencent-cloud.cn/raw/6c7cf2b3775fef1d72d2b95b19af878c.png"></td>
	<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9c4699e9cf0f361a728b76aa34b6486a.png"></td>
</tr>
</table>

- 항목이 selector 유형인 경우 AvatarData에서 selected 값을 변경하여 구성합니다. 예를 들어 A, B, C, D의 네 종류의 안경이 있다고 가정합니다. 사용자가 A를 선택하면 A의 selected를 true로 설정하고 B, C, D의 안경을 false로 설정합니다. 사용자가 B를 선택하면 B의 selected를 true로 설정하고 A, C, D의 selected를 false로 설정합니다.
- 항목이 slider 유형인 경우 AvatarData에서 value를 변경하여 구성합니다. value 필드는 여러 key-value 쌍을 포함하는 JsonObject입니다. key-value 쌍의value를 슬라이더 값으로 설정합니다.

## AvatarData에 대해 자세히 알아보기
SDK는 소재 루트 디렉터리의 custom_configs 디렉터리를 파싱하여 AvatarData를 가져와 애플리케이션 레이어으로 보냅니다. 일반적으로 AvatarData를 수동으로 구성할 필요가 없습니다.
AvatarData의 세 가지 핵심 필드는 [entityName](entityName), [action](#action) 및 [value](#value)이며 SDK가 구성 데이터를 파싱할 때 값이 자동으로 입력됩니다. 대부분의 경우 이 세 필드의 세부 정보를 처리할 필요가 없습니다. 그러나 슬라이더 데이터의 경우 value 필드의 key-value 쌍을 파싱하고 UI에 설정된 슬라이더 값을 기반으로 구성해야 합니다.

[](id:entityName)
### entityName 필드
entityName은 얼굴, 눈, 머리카락, 상의 또는 신발과 같이 아바타에서 편집할 부분을 지정합니다. Demo를 예로 들면 TencentEffectStudio에서 소재 프로젝트(xxx.studio)를 열면 다음 목록이 표시됩니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/06a4860a9b6f1b1cf3350d0dfbfbd68b.png" width=300>
목록의 각 항목은 아바타 부분을 나타냅니다. **항목 이름은 소재 프로젝트에서 고유해야 합니다**.

[](id:action)
### action 필드
action 필드는 entityName에서 수행할 작업(action)을 나타냅니다. 다섯 가지 action 옵션이 SDK에 정의되어 있으며 아래에 자세히 설명되어 있습니다.

| action         | 설명                                                         | value 요구 사항                                                    |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| changeColor    | 기본 색상과 이미션(emission) 색상을 포함하는 현재 재질의 색상을 변경합니다.           | value는 JsonObject여야 하며 필수 항목입니다. 자세한 내용은 아래를 참고하십시오. |
| changeTexture  | 색상 텍스처 맵, 금속/거칠기 텍스처 맵, AO(ambient occlusion) 맵, 일반 맵 및 이미션 맵을 포함하여 현재 재질의 맵을 수정합니다. | value는 JsonObject여야 하며 필수 항목입니다. 자세한 내용은 아래를 참고하십시오. |
| shapeValue     | blendShape 값을 수정합니다. 이 작업은 종종 얼굴 특징을 미세 조정하는 데 사용됩니다. | value는 JsonObject여야 하며(key는 도형 이름이고 value는 float임) 필수 항목입니다. 자세한 내용은 아래를 참고하십시오. |
| replace        | 예를 들어 안경, 헤어스타일 또는 옷과 같은 서브 모델을 대체합니다. | value는 3D 변환 정보, 모델 경로 및 새 서브 모델의 재질 경로를 설명하는 JsonObject여야 합니다. 서브 모델을 숨기려면 null로 설정합니다. 자세한 내용은 아래를 참고하십시오. |
| basicTransform | 위치, 회전 및 크기 조정 설정을 조정합니다. 이 작업은 확대/축소 또는 각도를 변경하여 전체 보기와 절반 길이 보기 사이를 전환하는 데 자주 사용됩니다. | value는 JsonObject여야 하며 필수 항목입니다. 자세한 내용은 아래를 참고하십시오. |

[](id:value)
### value 필드
<dx-tabs>
::: action은 changeColor와 동일
[](id:changeColor)
**설정 예시**:

```swift
{
		"key": "baseColorFactor",
        "value": [43, 26, 23, 255],
		"subMeshIndex":0,
		"materialIndex":0
}
```
- **key**: 이 필드는 필수입니다. 현재 재질의 기본 색상, 이미션 색상 또는 사용자 지정 색상 속성을 변경할지 여부를 지정합니다.<br>

key의 유효한 값은 현재 재질에서 사용하는 shader에 따라 다릅니다. 상기 스크린샷에서는 내장 lit_fade shader가 사용됩니다. 기본 색상의 이름은 baseColorFactor이고 이미션 색상의 이름은 emissiveFactor이므로 이 경우 baseColorFactor 및 emissiveFactor는 key의 유효한 값입니다. 재질 파일을 열어 key 값을 볼 수도 있습니다. 예를 들어 위의 예시에서 사용된 재질 파일은 `hair.fmaterial`입니다. TEStudio 프로젝트에서 찾아 엽니다. 다음과 같이 표시됩니다.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/374363dc75275181e05d02a05bb6c2dd.png" width=500>
- **value**: RGBA 형식의 색상입니다. 이 필드는 필수입니다.
- **subMeshIndex 및 materialIndex**: [](id:subMeshIndex)이 두 필드는 선택 사항입니다. 지정하지 않으면 0이 사용됩니다.
	TEStudio에서 Mesh(눈, 헤어스타일 또는 얼굴과 같은 서브 모델)는 일반적으로 서브 Mesh로 구성되지 않으며 하나의 재질만 있습니다.<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/6c4b6de62f37fb58e74d25ec8b01eaa4.png" width=300>
	<br>일부 Mesh에는 서브 Mesh와 여러 재질이 있을 수도 있습니다.<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/736b84897bb2e784ac0a3d0085591829.png" width=300>
	<br>이 경우 소재 색상 변경(changeColor) 시, submeshIndex 및 materialIndex를 사용하여 재질을 지정해야 합니다. 이 두 매개변수의 값을 결정하려면 소재 프로젝트 디렉터리에서 template.json을 열고 현재 mesh를 찾은 다음 subMeshConfigs를 찾습니다. 예를 들어 ‘hair’를 검색하면 다음과 같은 subMesh 설정이 표시됩니다.
	<img src="https://qcloudimg.tencent-cloud.cn/raw/85e39b3f3492b2aed27a67bbd3394c60.png" width=500>
	<br>그런 다음 subMeshIndex 및 materialIndex를 지정하여 특정 재질의 색상을 변경할 수 있습니다.
	:::
	::: action은 changeTexture와 동일
	[](id:changeTexture)
	**설정 예시**:
```swift
{
	"switchKey": "baseColorEnableTexture",
	"switchValue": true,
	"key": "baseColorMap",
	"value": "0622-1/Images/face_tex_base_3.png",
	"subMeshIndex":0,
	"materialIndex":0,
	"textureOptions": {
            "wrapS": "REPEAT",
            "wrapT": "REPEAT",
            "magFilter": "LINEAR",
            "minFilter": "LINEAR_MIPMAP_LINEAR",
            "sRGB": false,
            "mipmap": true,
            "samplerType": "SAMPLER_2D"
         }
}
```

- **switchKey 및 switchValue**: 이 두 필드는 필수입니다. 텍스처 맵을 표시할지 여부를 결정합니다. switchValue가 false이면 텍스처 맵이 구성되지 않으며 다른 필드를 설정할 필요가 없습니다. switchKey와 key의 값은 서로 일치해야 합니다.
- **key 및 value**: 이 두 필드는 switchValue가 true인 경우 필수입니다. value는 소재의 루트 디렉터리에 대한 맵 파일의 상대 경로(위의 예에서 표시됨) 또는 모바일 장치의 절대 경로입니다.
>? [action ==  changeColor](#changeColor)의 key와 마찬가지로 switchKey 및 key의 유효한 값은 material에서 사용하는 shader에 따라 다릅니다. 예를 들어 위의 예시에서 baseColorEnableTexture 및 baseColorMap은 Tencent Effect Studio의 내장 ‘색상 텍스처’ shader에 해당합니다. 다른 유효한 값에는 AO 텍스처와 일반 텍스처가 포함됩니다. 또한 립스틱 및 얼굴 맵과 같은 사용자 지정 shader도 제공합니다.
>- 재질 파일을 열어 각 맵의 switchKey 및 key 값을 볼 수 있습니다. 예를 들어 Demo를 살펴보십시오. face_main의 재질 파일인 face.fmaterial을 열면 다음과 같이 보입니다.
><img src="https://qcloudimg.tencent-cloud.cn/raw/0fa0653a62172412aba16b64d1bc172f.png" width=500>
>- <br>switchKey 및 key를 수정하려는 맵의 스위치 및 키 값으로 설정합니다.

- **subMeshIndex 및 materialIndex**: 이 두 필드는 선택 사항입니다. 지정하지 않으면 0이 사용됩니다. 자세한 내용은 [action ==  changeColor](#subMeshIndex)를 참고하십시오.
- **textureOptions**: 이 필드는 선택 사항입니다. 지도 언래핑 및 렌더링 스타일을 지정합니다. 특별한 요구 사항이 없는 한 이 필드를 비워 두는 것이 좋습니다.
:::
::: action은 shapeValue와 동일
[](id:shapeValue)
**구성 예시**
```
{
	"chin_length": 0.0,
	"cheek_width": 0.0,
	"chin_width": 0.0
}
```
상기 예시에는 모양 이름과 모양 변경 값이 포함되어 있습니다. 도형 이름에 대한 자세한 내용은 [Tencent Cloud 아바타 디자인 매뉴얼](https://doc.weixin.qq.com/doc/w3_ALoA-gYYAAgV0MAAbjtQfO4EWXhI9?scode=AJEAIQdfAAoU7K9sLCAGMA3QZFAAg&version=4.0.19.6020&platform=win)을 참고하십시오. 모양 변경 값의 값 범위는 -1.0에서 1.0입니다.
:::
::: action은 replace와 동일
[](id:replace)
action == replace인 경우 value는 3D 변환 정보, 모델 경로 및 서브 모델의 재질 경로를 지정합니다. 이러한 모델 정보는 소재 루트 디렉터리의 template.json에서 찾을 수 있습니다.
**설정 예시**:
```
{
	"position": {
		"x": -0.424766392,
		"y": -29.969169617,
		"z": -25.769769669
	},
	"rotation": {
		"x": 0,
		"y": 0,
		"z": 0
	},
	"scale": {
		"x": 1,
		"y": 1,
		"z": 1
	},
	"meshResourceKey": "meshFolder/glass_A.fmesh",
	"subMeshConfigs": [{
		"materialResourceKeys": ["/sdcard/xmagic_res/glass_red.fmaterial"]
	}，{
		"materialResourceKeys": ["/sdcard/xmagic_res/test1.fmaterial"，"/sdcard/xmagic_res/test2.fmaterial"]
	}]
}
```
- **position, rotation, scale**: 이 세 필드는 선택 사항입니다. 모델의 위치, 회전 및 배율 속성을 지정합니다. 지정하지 않으면 기본값이 사용됩니다. position의 기본값은 0,0,0, rotation의 기본값은 0,0,0, scale의 기본값은 1,1,1입니다.
>! rotation값은 도 단위입니다. 예를 들어 45는 45도를 나타냅니다. template.json의 eEuler 필드에 해당합니다.
- **meshResourceKey**: 이 필드는 필수입니다. 모델 mesh 파일의 경로를 지정합니다. 경로는 소재의 루트 디렉터리에 대한 mesh 파일의 상대 경로(예시 참고) 또는 모바일 장치에 있는 파일의 절대 경로일 수 있습니다.
-  **subMeshConfigs**: 이 필드는 필수입니다. [subMeshIndex 및 materialIndex](#subMeshIndex)와 같이 mesh는 여러 subMesh를 포함할 수 있으며 subMesh는 여러 재질을 포함할 수 있습니다. subMeshConfigs는 사용할 mesh의 재질을 지정합니다. materialResourceKeys는 소재의 루트 디렉터리에 대한 material  파일의 상대 경로(예시 참고) 또는 모바일 장치에 있는 파일의 절대 경로일 수 있습니다.
:::
::: action은 basicTransform과 동일
**설정 예시**:
```swift
{
	"position": {
		"x": -0.424766392,
		"y": -29.969169617,
		"z": -25.769769669
	},
	"rotation": {
		"x": 0,
		"y": 0,
		"z": 0
	},
	"scale": {
		"x": 1,
		"y": 1,
		"z": 1
	}
}
```
이 작업은 모델의 위치, 회전 및 배율을 조정합니다. 확대/축소하거나 카메라 각도를 변경하여 전체 보기와 절반 길이 보기 사이를 전환하는 데 자주 사용됩니다. position, rotation 및 scale에 대한 자세한 내용은 [action은 replace와 동일](#replace)을 참고하십시오.
:::
</dx-tabs>

## Avatar 사용자 지정 데이터 구성

Avatar 구성은 resources 폴더(`소재/custom_configs/resources`)에 저장됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fcc5d2d5173afe13008b8369c63b1a32.png)

대부분의 경우 구성 파일은 자동으로 생성되며 수동으로 구성할 필요가 없습니다.
구성을 자동으로 생성하려면 TencentEffectStudio를 사용하여 재료를 디자인하고 당사에서 제공하는 resource_generator_gui app을 실행하십시오(현재 MacOS에서만 사용 가능). 자세한 내용은 [Tencent Cloud 아바타 디자인 매뉴얼](https://doc.weixin.qq.com/doc/w3_ALoA-gYYAAgV0MAAbjtQfO4EWXhI9?scode=AJEAIQdfAAoU7K9sLCAGMA3QZFAAg&version=4.0.19.6020&platform=win)을 참고하십시오.
