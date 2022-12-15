'TencentEffectApi'는 Tencent Effect Flutter SDK의 핵심 API 클래스입니다. 효과 강도 설정 및 애니메이션 효과 적용을 포함한 기능을 제공합니다.

## Public 멤버 함수

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [initXmagic](#initxmagic)                                    | 데이터 초기화, Tencent Effect SDK를 사용하기 전에 이 API를 호출해야 합니다                    |
| [setLicense](#setlicense)                                    | 뷰티 필터 라이선스를 구성합니다                                                 |
| [setXmagicLogLevel](#setxmagicloglevel)                      | SDK의 log 레벨을 설정하고, 디버깅을 위해서는 Log.DEBUG로 설정하고 공식 릴리스를 위해서는 Log.WARN으로 설정하는 것이 좋습니다. 프로덕션 환경에서 Log.DEBUG로 설정하면 대량의 로그 데이터 출력이 애플리케이션의 성능에 영향을 줄 수 있습니다  |
| [onResume](#onresume)                                        | 렌더링 재개, 페이지가 표시될 때 이 API를 호출합니다                                     |
| [onPause](#onpause)                                          | 렌더링 일시 중지, 페이지가 보이지 않을 때 이 API를 호출합니다                                   |
| [updateProperty](#updateproperty)                            | 뷰티 필터 속성 업데이트, 이 API는 모든 스레드에서 호출할 수 있습니다                    |
| [setOnCreateXmagicApiErrorListener](#setoncreatexmagicapierrorlistener) | 뷰티 필터 객체를 만들기 위한 콜백 구성, 오류가 발생하면 콜백이 트리거됩니다         |
| [setTipsListener](#settipslistener)                          | 애니메이션 프롬프트 콜백 함수를 설정하여 프런트 엔드 페이지에 프롬프트를 표시합니다       |
| [setYTDataListener](#setytdatalistener)                      | 안면 인식 포인트 포지셔닝 정보 등의 데이터 콜백을 설정합니다(S1-05 및 S1-06 패키지에만 해당) |
| [setAIDataListener](#setaidatalistener)                      | 안면 인식, 제스처, 신체 점검 상태 콜백을 설정합니다                           |
| [isBeautyAuthorized](#isbeautyauthorized)                    | 현재 lic 라이선스가 어떤 뷰티 필터를 지원하는지 판단합니다. BEAUTY 및 BODY_BEAUTY 유형의 뷰티 필터 항목 점검만 지원됩니다. 점검된 결과는 각 뷰티 필터 객체의 XmagicProperty.isAuth 필드에 할당됩니다 |
| [isSupportBeauty](#issupportbeauty)                          | 현재 모델이 뷰티 필터(OpenGL3.0)를 지원하는지 확인합니다                      |
| [getDeviceAbilities](#getdeviceabilities)                    | 현재 장치에서 지원하는 원자 기능 테이블을 반환합니다                                 |
| [isDeviceSupport](#isdevicesupport)                          | 애니메이션 리소스 목록을 SDK에 전달하여 점검 실행 후 XmagicProperty.isSupport 필드는 원자성 기능을 사용할 수 있는지 여부를 식별합니다. 클릭 제한은 XmagicProperty.isSupport에 따라 UI 레이어에서 제어하거나 리소스 목록에서 직접 삭제할 수 있습니다 |
| [getPropertyRequiredAbilities](#getpropertyrequiredabilities) | 애니메이션 리소스 목록을 전달하고 각 리소스에서 사용하는 SDK 원자 기능 목록을 반환합니다 |

##  

## API 설명

### initXmagic

이 API는 Tencent Effect SDK를 초기화하는 데 사용됩니다..
```dart
void initXmagic(String xmagicResDir,InitXmagicCallBack callBack);

typedef InitXmagicCallBack = void Function(bool reslut);
```

#### 매개변수
| 매개변수                        | 의미               |
| --------------------------- | ------------------ |
| String xmagicResDir         | 리소스 디렉터리 |
| InitXmagicCallBack callBack | 초기화 콜백     |

------

### setLicense

이 API는 뷰티 필터 라이선스를 설정하는 데 사용됩니다.

```dart
  ///Tencent Effect 라이선스 설정
void setLicense(String licenseKey, String licenseUrl, LicenseCheckListener checkListener);
///인증 결과 콜백
typedef LicenseCheckListener = void Function(int errorCode, String msg);
```

#### 매개변수

| 매개변수                               | 의미             |
| ---------------------------------- | :--------------- |
| String licenseKey                  | LicenseKey |
| String licenseUrl                  | LicenseUrl |
| LicenseCheckListener checkListener | 승인 결과의 콜백 |

------

### setXmagicLogLevel

SDK의 log 레벨을 설정하는 데 사용되는 API

```dart
void setXmagicLogLevel(int logLevel);
```

#### 매개변수

| 매개변수         | 의미                               |
| ------------ | :--------------------------------- |
| int logLevel | LogLevel에 정의된 유형을 사용하여 로그 수준 설정 |

------

### onResume

뷰티 필터 렌더링을 재개하는 데 사용되는 API

```dart
void onResume();
```

### onPause

뷰티 필터 렌더링을 일시 중지하는 데 사용되는 API

```dart
void onPause();
```

------

### updateProperty

이 API는 뷰티 필터 값, 애니메이션 효과 또는 필터를 설정하는 데 사용됩니다. 모든 스레드에서 호출할 수 있습니다.

```dart
void updateProperty(XmagicProperty xmagicProperty);
```

#### 매개변수

| 매개변수                          | 의미             |
| ----------------------------- | :--------------- |
| XmagicProperty xmagicProperty | 뷰티 필터 속성의 객체 |

------

### setOnCreateXmagicApiErrorListener

뷰티 필터 객체 생성을 위한 오류에 대한 콜백을 구성하는 데 사용되는 API

```dart
  void setOnCreateXmagicApiErrorListener(OnCreateXmagicApiErrorListener? errorListener);
///뷰티 필터 객체 생성 오류에 대한 콜백
typedef OnCreateXmagicApiErrorListener = void Function(String errorMsg, int code);
```

#### 매개변수

| 매개변수                                          | 의미                           |
| --------------------------------------------- | :----------------------------- |
| OnCreateXmagicApiErrorListener? errorListener | 뷰티 필터 객체 생성 오류에 대한 콜백 |

에러 코드 반환 의미 대조표:

| 에러 코드  | 의미                    |
| ---- | --------------------- |
| -1   | 알 수 없는 오류                 |
| -100 | 3D 엔진 리소스 초기화 실패                    |
| -200 | GAN 소재 미지원             |
| -300 | 장치는 이 소재 컴포넌트 미지원           |
| -400 | 템플릿 JSON 콘텐츠가 비어 있음           |
| -500 | SDK 버전이 너무 낮음              |
| -600 | 분할 미지원                |
| -700 | OpenGL 미지원                    |
| -800 | 스크립트 미지원                |
| 5000 | 2160×3840 이상의 해상도로 배경 이미지 분할 |
| 5001 | 키잉을 위한 메모리가 부족                    |
| 5002 | 분할된 배경 비디오 리졸브에 실패했습니다.           |
| 5003 | 키잉할 비디오의 길이가 200초보다 김                    |
| 5004 | 키잉에 대해 지원되지 않는 비디오 형식                    |

------

### setTipsListener

애니메이션 프롬프트 콜백 함수를 설정하여 프런트 엔드 페이지에 프롬프트를 표시합니다. 예를 들어, 일부 소재는 사용자 고개 끄덕임, 손바닥 펼치기, 손 하트 등을 나타냅니다.

```dart
void setTipsListener(XmagicTipsListener? xmagicTipsListener);

abstract class XmagicTipsListener {
  /// tips 표시. Show the tip.
  /// @param tips tips 문자열.Tip's content
  /// @param tipsIcon tips의 icon. Tip's icon
  /// @param type tips 유형, 0으로 설정하면 문자열과 icon 모두 표시, 1로 설정하면 pag 소재에 icon만 표시됩니다. tips category, 0 means that both strings and icons are displayed, 1 means that only the icon is displayed for the pag material
  /// @param duration tips 시간(밀리초). Tips display duration, milliseconds
  void tipsNeedShow(String tips, String tipsIcon, int type, int duration);

  /// *
  /// tips 숨기기. Hide the tip.
  /// @param tips tips 문자열. Tip's content
  /// @param tipsIcon tips의 icon. Tip's icon
  /// @param type tips 유형, 0으로 설정하면 문자열과 icon 모두 표시, 1로 설정하면 pag 소재에 icon만 표시됩니다. tips category, 0 means that both strings and icons are displayed, 1 means that only the icon is displayed for the pag material
  void tipsNeedHide(String tips, String tipsIcon, int type);
}
```

#### 매개변수

| 매개변수                                  | 의미             |
| ------------------------------------- | ---------------- |
| XmagicTipsListener xmagicTipsListener | 콜백 구현 클래스  |

------

### setYTDataListener

안면 인식 포지셔닝 정보 등 데이터 콜백을 설정합니다.
```dart
  /// 얼굴 키포인트 및 기타 데이터의 콜백 구성(S1-05 및 S1-06에서만 사용 가능)
void setYTDataListener(XmagicYTDataListener? xmagicYTDataListener);
안면 인식 정보 등 데이터 콜백 설정

abstract class XmagicYTDataListener {
  //YouTu AI 데이터 콜백입니다.
  void onYTDataUpdate(String data);
}
```
onYTDataUpdate 는 JSON string 구조를 반환하고 최대 5개의 안면 인식 정보를 반환합니다.
```
{
 "face_info":[{
  "trace_id":5,
  "face_256_point":[
    180.0,
    112.2,
    ...
  ],
  "face_256_visible":[
    0.85,
    ...
  ],
  "out_of_screen":true,
  "left_eye_high_vis_ratio:1.0,
  "right_eye_high_vis_ratio":1.0,
  "left_eyebrow_high_vis_ratio":1.0,
  "right_eyebrow_high_vis_ratio":1.0,
  "mouth_high_vis_ratio":1.0
 },
 ...
 ]
}
```

#### 필드 의미

| 필드                           | 유형    | 값범위                           | 설명                            |
| -------------------------- |-------------------------- | --------------------------- | --------------------------- |
| trace_id                     | int   | [1,INF)                      | 안면 인식 ID. 연속 스트리밍 과정에서 동일한 ID를 가진 사람들을 동일한 얼굴로 간주할 수 있음 |
| face_256_point               | float | [0,screenWidth] 또는 [0,screenHeight] | 총 512개의 숫자, 256개의 안면 인식 키 포인트가 있으며 화면의 왼쪽 상단 모서리는 (0,0)  |
| face_256_visible             | float | [0,1]                               | 안면 인식 256 키 포인트 가시도                    |
| out_of_screen                | bool  | true/false                          | 얼굴이 프레임 밖에 있는지 여부                    |
| left_eye_high_vis_ratio      | float | [0,1]                               | 왼쪽 눈 높이 가시성 포인트의 비율                    |
| right_eye_high_vis_ratio     | float | [0,1]                               | 오른쪽 눈 높이 가시성 포인트의 비율                    |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | 왼쪽 눈썹 높이 가시성 포인트의 비율                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | 오른쪽 눈썹 높이 가시성 포인트의 비율                   |
| mouth_high_vis_ratio         | float | [0,1]                               | 입 높이 가시성 포인트의 비율                                     |

#### 매개변수

| 매개변수                                           | 의미             |
| ---------------------------------------------- | ---------------- |
| XmagicYTDataListener      xmagicYTDataListener | 콜백 함수 구현 클래스  |

------

### setAIDataListener

얼굴, 몸, 손짓이 감지되면 해당 부분의 포인트 정보를 콜백합니다.

```dart
void setAIDataListener(XmagicAIDataListener? aiDataListener);
  
abstract class XmagicAIDataListener {
  void onFaceDataUpdated(String faceDataList);

  void onHandDataUpdated(String handDataList);

  void onBodyDataUpdated(String bodyDataList);
}
```

------

### isBeautyAuthorized

현재 License 인증이 지원하는 뷰티 필터 또는 몸매 보정 아이템을 결정합니다. BEAUTY 및 BODY_BEAUTY 유형의 뷰티 필터 항목 점검만 지원됩니다. 점검된 결과는 각 뷰티 필터 객체의 'XmagicProperty.isAuth' 필드에 할당됩니다. isAuth 필드가 false인 경우 UI에서 이러한 항목 게이트에 대한 액세스를 차단할 수 있습니다.

```
Future<List<XmagicProperty>> isBeautyAuthorized(
      List<XmagicProperty> properties);
```

#### 매개변수

| 매개변수                            | 의미               |
| ------------------------------- | ------------------ |
| List&lt;XmagicProperty> properties | 점검할 뷰티 필터 아이템 |

------

### isSupportBeauty

현재 모델이 뷰티 필터(OpenGL3.0)를 지원하는지 확인합니다.

```dart
  Future&lt;bool> isSupportBeauty();
```

#### 반환

반환 값 bool: 뷰티 필터 지원 여부.

------

### getDeviceAbilities

이 API는 현재 장치에서 지원하는 Tencent Effect 기능 목록을 가져오는 데 사용됩니다. getPropertyRequiredAbilities와 함께 사용할 수 있습니다.

```
  Future<Map<String, bool>> getDeviceAbilities();
```

#### 반환

반환 값 `Map&lt;String,bool>`:

- key: 원자 기능 이름(소재 기능 이름에 해당).
- value: 현재 기기의 지원 여부.

------

### getPropertyRequiredAbilities

애니메이션 리소스 목록을 전달하고 각 리소스에서 사용하는 SDK 원자 기능 목록을 반환합니다.
이 방법의 사용 시나리오는 다음과 같습니다.
여러 애니메이션 소재를 구입하거나 제작했으며 이 메소드를 호출하면 각 소재가 사용해야 하는 원자 기능 목록이 반환됩니다. 예를 들어, 소재1은 기능 A, B, C를 사용해야 하고 소재2는 기능 B, C, D를 사용해야 하며 그런 다음 서버에 그러한 기능 목록을 보관해야 합니다. 그 후, 사용자가 서버에서 애니메이션 소재를 다운로드하고자 할 때, 사용자는 먼저 getDeviceAbilities 메소드를 통해 자신의 휴대폰의 원자 기능 목록을 얻습니다(예를 들어, 휴대폰에는 기능 A, B, C가 있지만, 기능 D가 없음) 그의 기능 목록이 서버로 전송되고 서버는 장치에 기능 D가 없다고 판단하여 소재2를 사용자에게 전달하지 않습니다.

```dart
Future<Map<XmagicProperty, List<String>?>> getPropertyRequiredAbilities(
    List<XmagicProperty> assetsList);
```

#### 매개변수

| 매개변수                             | 의미               |
| ------------------------------ | ---------------- |
| List&lt;XmagicProperty> assetsList | 점검할 애니메이션 효과 목록  |

#### 반환

반환 값 Map&lt;XmagicProperty, List&lt;String>?> :

- key: 애니메이션 리소스 소재 객체 클래스.
- value: 사용된 원자 기능 목록.

------

###  isDeviceSupport

애니메이션 리소스 목록을 SDK에 전달하여 점검합니다. 실행 후 'XmagicProperty.isSupport' 필드는 소재가 사용 가능한지 여부를 식별합니다. 클릭 제한은 'XmagicProperty.isSupport'에 따라 UI 레이어에서 제어하거나 리소스 목록에서 직접 삭제할 수 있습니다.

```dart
 Future&lt;List<XmagicProperty>> isDeviceSupport(List<XmagicProperty> assetsList);
```

#### 매개변수

| 매개변수                            | 의미                     |
| ------------------------------- | ------------------------ |
| List&lt;XmagicProperty> assetsList | 점검할 애니메이션 소재 목록 |