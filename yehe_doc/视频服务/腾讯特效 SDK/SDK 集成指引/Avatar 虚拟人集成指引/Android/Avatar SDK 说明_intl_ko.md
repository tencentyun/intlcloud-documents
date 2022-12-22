## SDK 통합
SDK 다운로드 및 통합 방법, 라이선스 설정 방법, Demo 프로젝트 실행 방법은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45385)를 참고하십시오.

## 아바타 소재 준비

압축 해제 후 SDK 패키지의 `MotionRes/avatarRes` 디렉터리에서 찾을 수 있는 다양한 얼굴 사용자 정의 및 드레스업 자료 세트를 제공합니다. 다른 애니메이션 효과 소재와 마찬가지로 프로젝트의 assets 디렉터리에 copy해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f712ea1424c224b5cac36403c4c218bf.png)

## 아바타 DIY 및 SDK API
<table>
<tr>
	<th style="text-align:center">아바타 DIY</th>
	<th style="text-align:center">사진 기반 아바타 DIY</th>
</tr>
<tr>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/744618a7c9dfb622b3bd0e19e2d4969f.jpg" width=650></td>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/343aea35f8fd235f15cb029402577373.jpg" width=550></td>
</tr>
</table>

아래 섹션에서는 데이터 로드, 아바타 사용자 지정 및 사진 기반 아바타 DIY를 위한 API를 포함하여 XMagicApi의 API에 대한 설명을 제공합니다.

### 1. 아바타 소재 로딩(loadAvatar)

```java
public void loadAvatar(XmagicProperty<?> property, UpdatePropertyListener updatePropertyListener)
```
아바타 소재는 다른 애니메이션 효과 소재와 같은 방식으로 로딩됩니다. loadAvatar API는 [updateProperty](https://intl.cloud.tencent.com/document/product/1143/45399) API와 동일합니다.

### 2. Avatar 소스 데이터 로딩(getAvatarConfig)

```java
public static Map<String,List<AvatarData>> getAvatarConfig(String avatarResPath, String savedAvatarConfigs)
```

- 입력 매개변수:
	- **avatarResPath**: `/data/data/com.tencent.pitumotiondemo.effects/files/xmagic/MotionRes/avatarRes/animoji_0624`와 같이 사용자 모바일 장치에 있는 avatar 소재의 절대 경로입니다.
	- **savedAvatarConfigs**: 사용자가 마지막으로 아바타를 DIY한 시점부터 저장된 아바타 구성 데이터(JSON 문자열)입니다. 아바타를 처음으로 DIY하거나 구성 데이터가 저장되지 않은 경우 null을 전달합니다.
- 출력 매개변수:
  이 API는 key가 category에 해당하고 value가 category의 데이터에 해당하는 map을 반환합니다. 자세한 내용은 AvatarCategory 클래스를 참고하십시오. 애플리케이션 레이어가 map을 가져온 후 필요에 따라 UI에 데이터를 표시합니다.

### 3. 얼굴 DIY 및 옷 입히기(updateAvatar)

```java
public void updateAvatar(List<AvatarData> avatarDataList, UpdateAvatarConfigListener upDataAvatarConfigListener)
```
이 API가 호출되면 아바타 미리보기가 실시간으로 업데이트됩니다. 각 AvatarData 객체는 구성(예: 헤어스타일 변경)에 해당합니다. 여러 AvatarData 객체를 API 호출에 전달하여 아바타의 여러 측면을 편집할 수 있습니다(예: 헤어스타일 및 머리 색상 변경). API는 전달된 AvatarData 객체의 유효성을 검사합니다. 객체가 유효하면 SDK로 전달됩니다. 그렇지 않으면 callback이 전송됩니다.
- 예를 들어 헤어스타일을 변경하기 위해 AvatarData 객체가 전달되었지만 로컬 장치에서 헤어 모델 파일(AvatarData의 value로 지정됨)을 찾을 수 없는 경우 AvatarData 객체는 유효하지 않은 것으로 간주됩니다.
- 또한 홍채 이미지를 변경하기 위해 AvatarData 객체가 전달되었지만 로컬 장치에서 이미지 파일(AvatarData의 value로 지정됨)을 찾을 수 없는 경우 AvatarData 객체는 유효하지 않은 것으로 간주됩니다.

### 4. 아바타 설정 내보내기(exportAvatar)
```java
public static String exportAvatar(List<AvatarData> avatarDataList)
```
사용자가 아바타를 편집하면 selected 값이나 AvatarData의 모양 변경 값이 변경됩니다. 편집 후 새로운 AvatarData 목록이 생성되고 json 문자열로 내보낼 수 있습니다. 로컬에 저장하거나 서버에 업로드할 수 있습니다.
문자열은 다음 목적으로 내보내집니다.
- 다음 번에 XMagicApi의 loadAvatar를 호출하여 Avatar 소재를 로드할 때 XMagicProperty의 customConfigs를 JSON 문자열로 설정해야 미리보기에서 마지막으로 아바타 설정을 기억할 수 있습니다.
- 또한 getAllAvatarData를 호출하여 selected와 Avatar 소스 데이터의 모양 변경 값을 업데이트할 때 이 JSON 문자열을 전달해야 합니다.

### 5. 사진을 기반으로 아바타 DIY(createAvatarByPhoto)
이 API가 작동하려면 SDK가 인터넷에 연결되어 있어야 합니다.

```java
public void createAvatarByPhoto(String photoPath, List<String> avatarResPaths, boolean isMale,
            final FaceAttributeListener faceAttributeListener)
```

- **photoPath**: 사진 경로입니다. 얼굴이 사진 중앙에 오도록 합니다. 이상적으로는 사진에 얼굴이 하나만 포함되어야 합니다. 여러 개가 있는 경우 SDK는 임의로 하나를 선택합니다. 인식 결과를 보장하려면 사진의 짧은 면이 500px보다 길어야 합니다.
- **avatarResPaths**: 여러 세트의 Avatar 소재를 전달할 수 있으며 SDK는 사진 분석 결과에 따라 가장 적합한 세트를 선택합니다. 참고: 현재 한 세트의 소재만 지원됩니다. 여러 세트가 전달되면 SDK는 첫 번째 세트를 사용합니다.
- **isMale**: 사람이 남성인지 여부. 현재 이 속성은 사용되지 않습니다. 그러나 미래에 있을 수 있습니다. 올바른 값을 전달하는 것이 좋습니다.
- **faceAttributeListener**: 사용자 지정이 실패하면 `void onError(int errCode, String msg)`가 반환됩니다. 성공하면 `void onFinish(String matchedResPath, String srcData)`가 반환되며 첫 번째 매개변수는 매칭된 Avatar 소재의 경로를 나타내고 두 번째 매개변수는 매칭 결과입니다(exportAvatar의 반환 값과 동일).
- onError의 에러 코드는 `FaceAttributeHelper.java`에 정의되어 있습니다.

```
    public static final int ERROR_NO_AUTH = 1;//권한 부족
    public static final int ERROR_RES_INVALID = 5;//전달된 Avatar 소재 경로가 유효하지 않음
    public static final int ERROR_PHOTO_INVALID = 10;//사진 읽기 실패
    public static final int ERROR_NETWORK_REQUEST_FAILED = 20;//인터넷 연결 실패
    public static final int ERROR_DATA_PARSE_FAILED = 30;//네트워크에서 반환된 데이터 파싱 실패
    public static final int ERROR_ANALYZE_FAILED = 40;//얼굴 인식 실패
    public static final int ERROR_AVATAR_SOURCE_DATA_EMPTY = 50;//Avatar 소스 데이터 로딩 실패
```

### 6. 다운로드한 구성 파일(addAvatarResource) 저장

```
public static Pair<Integer, List<AvatarData>> addAvatarResource(String resourceRootPath, String category, String zipFilePath)
```

Avatar 소재를 동적으로 다운로드하는 경우에 사용하는 API입니다. 예를 들어 10개의 헤어스타일을 제공하고 그 중 하나가 장치에 동적으로 다운로드된다고 가정합니다. 다운로드한 ZIP 파일의 경로를 SDK에 전달하려면 이 API를 호출해야 합니다. SDK는 파일을 파싱하여 해당 category의 폴더에 저장합니다. 다음에 getAllAvatarData를 호출하면 SDK가 새로 추가된 데이터를 반환합니다.
매개변수 설명:

- **resourceRootPath**: /data/data/com.tencent.pitumotiondemo.effects/files/xmagic/MotionRes/avatarRes/animoji_0624와 같은 Avatar 소재의 루트 디렉터리
- **category**: 다운로드한 자료의 카테고리
- **zipFilePath**: 다운로드한 zip 파일의 경로
API는 `Pair<Integer, List<AvatarData>>`를 반환합니다. 여기서 pair.first는 에러 코드이고 pair.second는 새로 추가된 데이터입니다.
에러 코드는 다음과 같습니다.

```
    public interface AvatarActionErrorCode {
        int OK = 0;
        int ADD_AVATAR_RES_INVALID_PARAMS = 1000;
        int ADD_AVATAR_RES_ROOT_RESOURCE_NOT_EXIST = 1001;
        int ADD_AVATAR_RES_ZIP_FILE_NOT_EXIST = 1002;
        int ADD_AVATAR_RES_UNZIP_FILE_FAILED = 1003;
        int ADD_AVATAR_RES_COPY_FILE_FAILED = 1004;
    }
```

### 7. AvatarData 호출
AvatarData 클래스는 위 API의 핵심입니다. AvatarData에는 다음 필드가 포함됩니다.

```
public class AvatarData {
    /**
     * 선택자(selector) 데이터입니다. 예를 들어 안경의 경우 여러 종류의 안경이 제공되며 하나만 선택할 수 있습니다.
     */
    public static final int TYPE_SELECTOR = 0;

    /**
     * 뺨 너비와 같은 슬라이더(slider) 데이터입니다.
     */
    public static final int TYPE_SLIDER = 1;

    //얼굴 모양 및 눈매 조정 등의 카테고리입니다. 표준 category는 AvatarCategory.java에 정의되어 있습니다. 요구 사항을 충족하지 못하는 경우 category를 사용자 지정할 수 있습니다(기존 category와 동일하지 않은지 확인).
    //이 필드는 비워둘 수 없습니다.
    public String category;

    //아바타 구성 item의 ID입니다.
    //예를 들어, 각 유형의 안경에는 고유한 id가 있습니다. 각 조정 항목도 마찬가지입니다.
    //이 필드는 비워둘 수 없습니다.
    public String id;

    //TYPE_SELECTOR 또는 TYPE_SLIDER
    public int type;

    //type이 selector인 경우 이 필드는 항목이 선택되었는지 여부를 나타냅니다
    public boolean selected = false;

    //각 아이콘 또는 조정 항목에는 구성 세부 정보의 세 가지 측면이 있습니다.
    public String entityName;
    public String action;
    public JsonObject value;
}
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
- 항목이 slider 타입일 경우 AvatarData에서 value를 변경하여 구성합니다. value 필드는 여러 key-value 쌍을 포함하는 JsonObject입니다. key-value 쌍의 value를 슬라이더 값으로 설정합니다.

## AvatarData에 대한 추가 정보
AvatarData의 세 가지 핵심 필드는 entityName, action 및 value이며 SDK가 구성 데이터를 파싱할 때 해당 값이 자동으로 입력됩니다. 대부분의 경우 이 세 필드의 세부 정보를 처리할 필요가 없습니다. 그러나 슬라이더 데이터의 경우 value 필드의 key-value 쌍을 구문 분석하고 UI에 설정된 슬라이더 값을 기반으로 구성해야 합니다.
AvatarData의 세 가지 핵심 필드는 [entityName](#entityName), [action](#action) 및 [value](#action)입니다.

[](id:entityName)
### entityName 필드

entityName은 얼굴, 눈, 머리카락, 상의 또는 신발과 같이 편집할 아바타 부분을 지정합니다.

[](id:action)
### action 및 value 필드
action 필드는 entityName에서 수행할 작업(action)을 나타냅니다. 다섯 가지 action 옵션은 SDK의 AvatarAction.java에 정의되어 있으며 각 action의 의미 및 value에 대한 요구 사항은 다음과 같습니다.

| action         | 의미                                                         | value에 대한 요구 사항                                                    |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| changeColor    | 기본 색상과 이미션(emission) 색상을 포함하는 현재 재질의 색상을 변경합니다.           | value는 JsonObject여야 하며 필수 항목입니다. 소재 사용자 지정 툴에 의해 자동으로 생성됩니다.              |
| changeTexture  | 색상 텍스처 맵, 금속/거칠기 텍스처 맵, AO(ambient occlusion) 맵, 노멀 맵 및 이미션(emissio) 맵을 포함하여 현재 재질의 맵을 수정합니다. | value는 JsonObject여야 하며 필수 항목입니다. 소재 사용자 지정 툴에 의해 자동으로 생성됩니다.              |
| shapeValue     | blendShape 값을 수정합니다. 이 작업은 종종 얼굴 특징을 미세 조정하는 데 사용됩니다.               | value는 JsonObject여야 하며(key는 도형 이름이고 value는 float임) 필수 항목입니다. 소재 사용자 지정 툴에 의해 자동으로 생성됩니다. |
| replace        | 예를 들어 안경, 헤어스타일 또는 옷과 같은 서브 모델을 대체합니다.                       | value는 3D 변환 정보, 모델 경로 및 새 서브 모델의 재질 경로를 설명하는 JsonObject여야 합니다. 소재 사용자 지정 툴에 의해 자동으로 생성됩니다. 서브 모델을 숨기려면 null로 설정합니다. |
| basicTransform | 위치, 회전 및 크기 조정 설정을 조정합니다. 이 작업은 확대/축소 또는 각도를 변경하여 전체 보기와 절반 길이 보기 사이를 전환하는 데 자주 사용됩니다. | value는 JsonObject여야 하며 필수 항목입니다. 소재 사용자 지정 툴에 의해 자동으로 생성됩니다.              |

## Avatar DIY 데이터 구성

avatar 구성은 resources 폴더(소재/custom_configs/resources)에 저장됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fcc5d2d5173afe13008b8369c63b1a32.png)

대부분의 경우 구성 파일은 자동으로 생성되며 수동으로 구성할 필요가 없습니다.
구성을 자동으로 생성하려면 TencentEffectStudio를 사용하여 당사 표준에 따라 소재를 디자인하고 당사에서 제공하는 resource_generator_gui App을 실행하십시오(현재 MacOS에서만 사용 가능). 자세한 내용은 [Tencent Cloud 아바타 디자인 매뉴얼](https://doc.weixin.qq.com/doc/w3_ALoA-gYYAAgV0MAAbjtQfO4EWXhI9?scode=AJEAIQdfAAoU7K9sLCAGMA3QZFAAg&version=4.0.19.6020&platform=win)을 참고하십시오.
