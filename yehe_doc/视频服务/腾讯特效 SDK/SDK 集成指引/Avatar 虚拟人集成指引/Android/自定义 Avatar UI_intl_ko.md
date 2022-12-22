## Demo UI 설명
<img src="https://qcloudimg.tencent-cloud.cn/raw/1b25592a83e2e7f38ded001ca8c0b93b.png" style="zoom: 67%;" />

## 구현 방식
패널 구성 데이터는 어디에나 저장할 수 있습니다. Demo에서는 assets에 있습니다. 패널 파일을 처음 사용하면 설치 디렉터리에 복사됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b178070d012fca8cbbf275c0b1e84f44.png)

**Json 구조와 패널 요소 간의 매핑**:

- 왼쪽 Json 파일의 item은 오른쪽의 최상위 레벨 메뉴에 해당합니다. head는 메뉴의 첫 번째 icon에 해당합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6547824e221494545e5353e8dce5e1cc.png" style="zoom:67%;" />
- 왼쪽의 subTabs는 두 번째 레벨 메뉴에 해당합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0cb8236d813fc9ec278b7026063a7b88.png" style="zoom:67%;" />
- 왼쪽 icon은 resources 폴더에 구성되어 있습니다. 오른쪽 파일은 패널 데이터입니다. **category 필드를 사용하여 연결**할 수 있습니다. SDK는 resources 폴더의 데이터를 파싱하고 파싱된 데이터를 map에 출력합니다. map의 key는 category 값에 해당합니다. `panel.json` 파일이 파싱된 후 SDK의 API를 사용하여 데이터를 가져오고 연결할 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2ad79a0d0efcb34cc5c1816975badfd8.png" style="zoom:67%;" />

## Demo의 주요 클래스
경로: `com.tencent.demo.avater.AvatarResManager.java`

### 1. Avatar 리소스 로딩
```java
/**
     * 아바타 리소스를 로딩하기 위해 사용
     *
     * @param xmagicApi      XmagicApi 객체
     * @param avatarResName  이름
     * @param avatarSaveData 로딩 모델의 기본 설정, 기본 구성이 없으면 null 전달
     */
    public void loadAvatarRes(XmagicApi xmagicApi, String avatarResName, String avatarSaveData)
```

### 2. 패널 데이터 가져오기
```java
 /**
     * avatar 패널 데이터 가져오기
     *
     * @param avatarResName      avatar 소재 이름
     * @param avatarDataCallBack API는 파일에 액세스합니다. 이 작업은 child 스레드에서 수행되며 얻은 데이터는 메인 스레드의 콜백에서 반환됩니다.
     *                           반환된 데이터에는 이미 resources 디렉터리의 데이터가 포함되어 있습니다
     */
    public void getAvatarData(String avatarResName, String avatarSaveData, LoadAvatarDataCallBack avatarDataCallBack)
```

### 3 패널 데이터에서 사용자 설정 또는 기본 설정 가져오기
```java
//패널 파일에서 사용자 설정 또는 기본 설정 가져오기
public static List<AvatarData> getUsedAvatarData(List<MainTab> mainTabList) 
```

### 4. 모델의 배경 데이터 가져오기
```java
 /**
     * plane Config 데이터 가져오기
     *
     * @param avatarResName 리소스 이름
     * @param avatarType    배경 유형
     * @return
     */
    public AvatarData getAvatarPlaneTypeConfig(String avatarResName, AvatarBgType avatarBgType) 
```

## 부록

이 섹션에서는 [MainTab.java](#maintab) 및 [SubTab.java](#subtab)의 필드에 대한 설명을 제공합니다.

### MainTab

| 필드 | 유형  | 필수 여부 | 설명  |
| ----------- | ----------- | ----------- | ----------- |
| id   | String| Yes | 주 메뉴 옵션의 전역적으로 고유한 식별자 |
| label| String| No | 기본 메뉴 옵션의 이름( Demo에는 표시되지 않음       |
| iconUrl        | String| Yes | 선택하지 않은 경우 아이콘의 URL |
| checkedIconUrl | String| Yes | 선택 시 아이콘의 URL |
| subTabs | [SubTab 목록](#subtab) | Yes       | 2단계 메뉴의 옵션 |

### SubTab

| 필드 | 유형     | 필수 | 설명 |
| --------------- | -------- | -------- | ----------- |
| label | String   | Yes       | 2단계 메뉴 옵션의 이름 |
| category | String   | Yes       | SDK의 `com.tencent.xmagic.avatar.AvatarCategory` 클래스에 정의된 2단계 메뉴 옵션의 카테고리 |
| relatedCategory | String   | No       | 관련 카테고리입니다. 예를 들어, 헤어 컬러는 헤어스타일 카테고리의 관련 카테고리입니다. 사용자가 헤어스타일을 변경할 때 헤어스타일 옵션의 이 필드를 현재 사용 중인 헤어 컬러(헤어 컬러 옵션의 category 값)로 설정해야 합니다. 현재 이 필드는 type이 TYPE_SELECTOR인 경우에만 적용 가능합니다. |
| avatarDataList  | 리스트 | Yes | [AvatarIcon 목록 데이터](#avataricon) |

### AvatarIcon

| 필드 | 유형 | 필수 여부 | 설명 |
| ----------- | ----------- | ----------- | ----------- |
|id| String| Yes |SDK에서 반환된 AvatarData의 ID에 해당하는 속성 ID |
| icon | String| Yes       | 아이콘의 URL 또는 ARGB 형식의 색상(‘#FF0085CF’)    |
| type | Int   | Yes       | 디스플레이 유형, 유효한 값: `AvatarData.TYPE_SLIDER`(슬라이더), `AvatarData.TYPE_SELECTOR`(icon) |
| selected    | boolean | Yes       | type이 AvatarData.TYPE_SELECTOR인 경우 이 필드는 item이 선택되었는지 여부를 표시 |
| downloadUrl | String| No | 구성 파일의 동적 다운로드 주소 |
| category    | String| Yes | SubTab의 category와 동일             |
| labels | Map&lt;String, String&gt; | No       | 패널 왼쪽의 label, type이 AvatarData.TYPE_SLIDER인 경우 이 필드는 비어 있지 않음 |
| avatarData  | AvatarData      | Yes       | SDK에 정의된 속성 작업 클래스 |