Tencent 특수 효과 SDK 핵심 인터페이스 클래스 'XmagicApi.java'는 SDK 초기화, 뷰티 필터 값 업데이트, 애니메이션 호출 등 기능에 사용됩니다.

## Public 멤버 함수

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [XmagicApi](#xmagicapi)                                      | 구조 함수.                                                   |
| [updateProperty](#updateproperty)                            | 속성 업데이트. 모든 스레드에서 호출할 수 있습니다.                                |
| [updateProperties](#updateproperties)                        | 속성 업데이트. 모든 스레드에서 호출할 수 있습니다.                                 |
| [setTipsListener](#settipslistener)                          | 애니메이션 프롬프트 콜백 함수를 설정하여 프런트 엔드 페이지에 프롬프트를 표시합니다.       |
| [setYTDataListener](#setytdatalistener)                      | 안면 인식 포인트 포지셔닝 정보 등의 데이터 콜백을 설정합니다(S1-05 및 S1-06 패키지에만 해당). |
| [setAIDataListener](#setaidatalistener)                      | 안면 인식, 제스처, 신체 점검 상태 콜백을 설정합니다.                           |
| [onPause](#onpause)                                          | 사운드 재생 일시 중지. Activity onPause 라이프사이클과 바인딩할 수 있습니다.           |
| [onResume](#onresume)                                        | 렌더링 복구. Activity onResume 라이프사이클과 바인딩할 수 있습니다.              |
| [onDestroy](#ondestroy)                                      | xmagic 폐기. GL 스레드에서 호출해야 합니다.                             |
| [process](#process)                                          | SDK 렌더링 데이터 수신 메소드. 카메라 데이터 콜백 함수에서 사용할 수 있습니다.         |
| [onPauseAudio](#onpauseaudio)                                | 이 함수는 오디오만 중지하고 GL 스레드는 릴리스할 필요가 없을 때 호출합니다.         |
| [sensorChanged](#sensorchanged)                              | 현재 휴대폰이 회전하는 각도를 판단하여 AI가 사람의 얼굴을 인식할 수 있는 각도 판단 근거를 조정합니다. |
| [isDeviceSupport](#isdevicesupport)                          | 애니메이션 리소스 목록을 SDK에 전달하여 점검 실행 후 XmagicProperty.isSupport 필드는 원자성 기능을 사용할 수 있는지 여부를 식별합니다. 클릭 제한은 XmagicProperty.isSupport에 따라 UI 레이어에서 제어하거나 리소스 목록에서 직접 삭제할 수 있습니다. |
| [getPropertyRequiredAbilities](#getpropertyrequiredabilities) | 애니메이션 리소스 목록을 전달하고 각 리소스에서 사용하는 SDK 원자 기능 목록을 반환합니다. |
| [getDeviceAbilities](#getdeviceabilities)                    | 현재 장치에서 지원하는 원자 기능 테이블을 반환합니다.                                 |
| [isSupportBeauty](#issupportbeauty)                          | 현재 모델이 뷰티 필터(OpenGL3.0)를 지원하는지 확인합니다.                      |
| [isBeautyAuthorized](#isbeautyauthorized)                    | 현재 lic 라이선스가 어떤 뷰티 필터를 지원하는지 판단합니다. BEAUTY 및 BODY_BEAUTY 유형의 뷰티 필터 항목 점검만 지원됩니다. 점검된 결과는 각 뷰티 필터 객체의 XmagicProperty.isAuth 필드에 할당됩니다. |
| [setXmagicStreamType](#setxmagicstreamtype)                  | 입력 데이터 유형 설정. 기본 값은 Android camera 데이터 스트림입니다.               |
| [setXmagicLogLevel](#setxmagicloglevel)                      | SDK의 log 레벨을 설정하고, 개발 디버깅을 제안할 때는 `Log.DEBUG`로 설정하고, 정식 배포 시에는 `Log.WARN`으로 설정합니다. 만약 정식으로 배포 시 `Log.DEBUG`로 설정할 경우, 대량의 로그가 성능에 영향을 줄 수 있습니다.<br><b>new XmagicApi() 다음에 호출합니다.</b> |

## 정적 함수

| API               | 설명         |
| ----------------- | ---------- |
| [setLibPathAndLoad](#setlibpathandload) | libPath 설정. |

## Public 멤버 함수 설명

### XmagicApi

구조 함수.
```
XmagicApi(Context context, String resDir)
XmagicApi(Context context, String resDir,OnXmagicPropertyErrorListener xmagicPropertyErrorListener)
```

#### 매개변수
<table>
<thead>
<tr>
<th>매개변수</th>
<th>의미</th>
</tr>
</thead>
<tbody><tr>
<td>Context context</td>
<td>컨텍스트.</td>
</tr>
<tr>
<td>String resDir</td>
<td>리소스 파일 리스트.<ul style="margin:0">
<li>SDK 리소스 파일이 assets에 내장되어 있다면 SDK를 처음 사용하기 전에 App의 프라이빗 디렉터리에 리소스 copy: 먼저 <code>XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath())</code>를 통해 리소스 경로를 설정한 다음 <code>XmagicResParser.copyRes(getApplicationContext())</code>를 통해 리소스 복사를 완료합니다. 자세한 내용은 Demo의<code>LaunchActivity.java</code>를 참고하십시오.</li>
<li>인터넷에서 SDK 리소스 파일을 다운로드 받은 경우 다운로드 완료 후 <code>XmagicResParser.setResPath(validAssetsDirectory)</code>를 통해 리소스 경로를 설정합니다.</li>
<li><code>XmagicResParser.getResPath()</code>를 통해 이전에 설정한 경로를 가져옵니다.</li></ul></td>
</tr>
<tr>
<td>OnXmagicPropertyErrorListener xmagicPropertyErrorListener</td>
<td>오류 콜백 인터페이스.</td>
</tr>
</tbody></table>
에러 코드 반환 의미 대조표:

| 에러 코드  | 의미                    |
| ---- | --------------------- |
| -1   | 알 수 없는 오류.                 |
| -100 | 3D 엔진 리소스 초기화에 실패했습니다.          |
| -200 | GAN 소재는 지원되지 않습니다.             |
| -300 | 장치는 이 소재 컴포넌트를 지원하지 않습니다.           |
| -400 | 템플릿 JSON 콘텐츠가 비어 있습니다.           |
| -500 | SDK 버전이 너무 낮습니다.              |
| -600 | 분할은 지원되지 않습니다.                |
| -700 | OpenGL은 지원되지 않습니다.            |
| -800 | 스크립트는 지원되지 않습니다.                |
| 5000 | 2160×3840 이상의 해상도로 배경 이미지를 분할합니다. |
| 5001 | 배경 이미지를 분할하는 데 필요한 메모리가 부족합니다.         |
| 5002 | 분할된 배경 비디오 리졸브에 실패했습니다.           |
| 5003 | 분할된 배경 비디오가 200초를 초과했습니다.         |
| 5004 | 분할 배경 비디오 형식은 지원되지 않습니다.          |

------

### updateProperty

특정 뷰티 필터 값, 애니메이션 또는 필터 변경 시 모든 스레드에서 호출할 수 있습니다.

```
void updateProperty(XmagicProperty<?> p) 
```

#### 매개변수
<table>
<thead>
<tr>
<th>매개변수</th>
<th>의미</th>
</tr>
</thead>
<tbody><tr>
<td>XmagicProperty&lt;?&gt; p</td>
<td>Tencent 특수 효과 데이터 엔터티 클래스.
<ul style="margin:0"><li>‘피부 보정’을 예로 들면 다음과 같이 new 인스턴스를 만들 수 있습니다.<br><code>new XmagicProperty&lt;&gt;(Category.BEAUTY,  null,  null,  BeautyConstant.BEAUTY_SMOOTH, new XmagicPropertyValues(0, 100, 50, 0, 1)));</code>.</li><li>‘2D Animated Bunny Sauce’를 예로 들면 다음과 같이 새 인스턴스를 만들 수 있습니다.<br><code>new XmagicProperty&lt;&gt;(Category.MOTION, "video_tutujiang" ,  ‘애니메이션 파일 경로’,  null, null);</code>.<br>더 많은 예시는 Demo 프로젝트의 <code>XmagicResParser.java</code>를 참고하십시오.</li></ul></td>
</tr>
</tbody></table>

***

### updateProperties

모든 스레드에서 호출할 수 있는 특정 뷰티 필터 값 또는 애니메이션, 필터를 일괄 변경합니다.

```
void updateProperties(List<XmagicProperty<?>> properties)
```

#### 매개변수

| 매개변수                                | 의미                         |
| ----------------------------------- | ---------------------------- |
| (List&lt;XmagicProperty&lt;?>> properties | 자세한 내용은 updateProperty 메소드에 대한 설명을 참고하십시오. |

***

### setTipsListener

애니메이션 프롬프트 콜백 함수를 설정하여 프런트 엔드 페이지에 프롬프트를 표시합니다. 예를 들어, 일부 소재는 사용자 고개 끄덕임, 손바닥 펼치기, 손 하트 등을 나타냅니다.

```
void setTipsListener(XmagicApi.XmagicTipsListener effectTipsListener) 
```

#### 매개변수

| 매개변수                                            | 의미                                 |
| ----------------------------------------------- | ------------------------------------ |
| XmagicApi.XmagicTipsListener effectTipsListener | 콜백 함수 구현 클래스. 콜백이 반드시 메인 스레드에 있는 것은 아닙니다. |

------

### setYTDataListener
안면 인식 포지셔닝 정보 등 데이터 콜백을 설정합니다.
```
void setYTDataListener(XmagicApi.XmagicYTDataListener ytDataListener)
안면 인식 정보 등 데이터 콜백 설정

public interface XmagicYTDataListener {
    void onYTDataUpdate(String data)
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
| trace_id                     | int   | [1,INF)                      | 안면 인식 ID. 연속 스트리밍 과정에서 동일한 ID를 가진 사람들을 동일한 얼굴로 간주할 수 있습니다. |
| face_256_point               | float | [0,screenWidth] 또는 [0,screenHeight] | 총 512개의 숫자, 256개의 안면 인식 키 포인트가 있으며 화면의 왼쪽 상단 모서리는 (0,0)입니다. |
| face_256_visible             | float | [0,1]                        | 안면 인식 256 키포인트 가시도.                  |
| out_of_screen                | bool  | true/false                   | 얼굴이 프레임 밖에 있는지 여부.                       |
| left_eye_high_vis_ratio      | float | [0,1]                        | 왼쪽 눈 높이 가시성 포인트의 비율입니다.                   |
| right_eye_high_vis_ratio     | float | [0,1]                        | 오른쪽 눈 높이 가시도 포인트의 비율입니다.                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | 왼쪽 눈썹 높이 가시성 포인트의 비율입니다.                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | 오른쪽 눈썹 높이 가시성 포인트의 비율입니다.                   |
| mouth_high_vis_ratio         | float | [0,1]                        | 입 높이 가시성 포인트의 비율입니다.                    |

#### 매개변수

| 매개변수                                            | 의미       |
| --------------------------------------------- | -------- |
| XmagicApi.XmagicYTDataListener ytDataListener | 콜백 함수 구현 클래스. |

------

### setAIDataListener

얼굴, 몸, 손짓이 감지되면 해당 부분의 포인트 정보를 콜백합니다.

```
public interface OnAIDataListener {

    void onFaceDataUpdated(List<FaceData> faceDataList);
    void onHandDataUpdated(List<HandData> handDataList);
    void onBodyDataUpdated(List<BodyData> bodyDataList);

}
```

### onPause

렌더링 일시 중지는 Activity onPause 라이프사이클과 바인딩될 수 있으며 현재는 내부적으로 'onPauseAudio'만 호출됩니다.

```
void onPause() 
```

------

### onResume

Activity onResume 라이프사이클에 바인딩될 수 있는 렌더링을 복구합니다.

```
void onResume() 
```

------

### onDestroy

GL 스레드 리소스를 정리하려면 GL 스레드 내에서 호출해야 합니다. 예시 코드:

```java
//예시 코드 MainActivity.java 참고
glSurfaceView.queueEvent(() -> {
                if (mXmagicApi != null) {
                    mXmagicApi.onPause();
                    mXmagicApi.onDestroy();
                }
            });
            
//예시 코드 ImageInputActivity.java 참고
@Override
protected void onDestroy() {

    if (mHandler != null) {
        mHandler.destroy(() -> {
            if (mXmagicApi != null) {
                mXmagicApi.onPause();
                mXmagicApi.onDestroy();
        		}
    		});
    		mHandler.waitDone();
    }

    XmagicPanelDataManager.getInstance().clearData();
    super.onDestroy();
}
```

### process

SDK 렌더링으로 데이터를 받는 방법은 카메라 데이터 콜백 함수 내에서 사용할 수 있습니다.

```
//텍스처 렌더링
int process(int srcTextureId, int srcTextureWidth, int srcTextureHeight) 
//bitmap 렌더링
Bitmap process(Bitmap bitmap, boolean needReset){
```

#### 매개변수

| 매개변수                   | 의미                                                         |
| ---------------------- | ------------------------------------------------------------ |
| int srcTextureId       | 렌더링할 텍스처입니다.                                           |
| id int srcTextureWidth | 렌더링할 텍스처 너비입니다.                                         |
| int srcTextureHeight   | 렌더링할 텍스처 높이입니다.                                         |
| Bitmap bitmap          | 권장되는 최대 크기는 2160×4096입니다. 이 크기보다 큰 사진은 얼굴 인식 결과가 좋지 않거나 얼굴을 인식할 수 없으며 OOM 문제가 발생할 수 있습니다. |
| boolean needReset      | <li/>이미지를 전환합니다.<li/>분할을 처음 사용합니다.<li/>애니메이션을 처음 사용합니다.<li/>메이크업을 처음 사용합니다.<br>이러한 시나리오에서 needReset은 true로 설정합니다. |

------

### onPauseAudio

이 함수는 오디오만 중지하고 GL 스레드는 릴리스할 필요가 없을 때 호출합니다.

```
void onPauseAudio() 
```

------

### sensorChanged

현재 휴대폰이 회전하는 각도를 판단하여 AI의 안면 인식 각도 판단 근거를 조정할 수 있으며, 자이로스코프 센서 콜백 함수 내에서 호출됩니다.

```
void sensorChanged(SensorEvent event, Sensor accelerometer) 
```

#### 매개변수

| 매개변수                   | 의미                                   |
| -------------------- | ------------------------------------ |
| SensorEvent event    | 자이로스코프 센서 콜백 함수 'onSensorChanged'에 의해 반환된 이벤트 객체 클래스입니다. |
| Sensor accelerometer | 자이로스코프 센서 예시.                            |

------

### isDeviceSupport

애니메이션 리소스 목록을 SDK에 전달하여 점검합니다. 실행 후 'XmagicProperty.isSupport' 필드는 소재가 사용 가능한지 여부를 식별합니다. 클릭 제한은 'XmagicProperty.isSupport'에 따라 UI 레이어에서 제어하거나 리소스 목록에서 직접 삭제할 수 있습니다.

```
void isDeviceSupport(List<XmagicProperty<?>> assetsList)
```

#### 매개변수

| 매개변수                                 | 의미           |
| ---------------------------------- | ------------ |
| List&lt;XmagicProperty&lt;?>> assetsList | 점검할 애니메이션 소재 목록입니다. |

------

### getPropertyRequiredAbilities

애니메이션 리소스 목록을 전달하고 각 리소스에서 사용하는 SDK 원자 기능 목록을 반환합니다.
이 방법의 사용 시나리오는 다음과 같습니다.
여러 애니메이션 소재를 구입하거나 제작했으며 이 메소드를 호출하면 각 소재가 사용해야 하는 원자 기능 목록이 반환됩니다. 예를 들어, 소재1은 기능 A, B, C를 사용해야 하고 소재2는 기능 B, C, D를 사용해야 하며 그런 다음 서버에 그러한 기능 목록을 보관해야 합니다. 그 후, 사용자가 서버에서 애니메이션 소재를 다운로드하고자 할 때, 사용자는 먼저 getDeviceAbilities 메소드를 통해 자신의 휴대폰의 원자 기능 목록을 얻습니다(예를 들어, 휴대폰에는 기능 A, B, C가 있지만, 기능 D가 없음) 그의 기능 목록이 서버로 전송되고 서버는 장치에 기능 D가 없다고 판단하여 소재2를 사용자에게 전달하지 않습니다.

#### 매개변수

| 매개변수                             | 의미               |
| ------------------------------ | ---------------- |
| List&lt;XmagicProperty&lt;?>> assets | 원자 기능을 점검하기 위한 애니메이션 리소스 목록입니다. |

#### 반환

반환 값 `Map<XmagicProperty<?>,ArrayList<String>>` : 

- key: 애니메이션 리소스 소재 객체 클래스.
- value: 사용된 원자 기능 목록.

------

### getDeviceAbilities

현재 장치에서 지원하는 원자적 기능 테이블을 반환합니다. getPropertyRequiredAbilities 메소드와 함께 사용되며 자세한 내용은 getPropertyRequiredAbilities 설명을 참고하십시오.

```
Map<String,Boolean> getDeviceAbilities() 
```

#### 반환

반환 값 `Map<String,Boolean>`: 
- key: 원자 기능 이름(소재 기능 이름에 해당).
- value: 현재 기기의 지원 여부.

------

### isSupportBeauty

현재 모델이 뷰티 필터(OpenGL3.0)를 지원하는지 확인합니다.

```
boolean isSupportBeauty() 
```

#### 반환

반환 값 boolean: 뷰티 필터 지원 여부.

------

### isBeautyAuthorized

현재 License 인증이 지원하는 뷰티 필터 또는 몸매 보정 아이템을 결정합니다. BEAUTY 및 BODY_BEAUTY 유형의 뷰티 필터 항목 점검만 지원됩니다. 점검된 결과는 각 뷰티 필터 객체의 'XmagicProperty.isAuth' 필드에 할당됩니다. isAuth 필드가 false인 경우 UI에서 이러한 항목 게이트에 대한 액세스를 차단할 수 있습니다.

```
void isBeautyAuthorized(List<XmagicProperty<?>> properties) 
```

#### 매개변수

| 매개변수                                 | 의미        |
| ---------------------------------- | --------- |
| List&lt;XmagicProperty&lt;?>> properties | 점검할 뷰티 필터 아이템. |

------

### setXmagicStreamType

입력 데이터 유형. 기본 값은 Android camera 데이터 스트림(XmagicApi.PROCESS_TYPE_CAMERA_STREAM)입니다.

```
void setXmagicStreamType(int type)
```

#### 매개변수

| 매개변수       | 의미                                                                                                                                        |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| int type | 데이터 원본 유형에는 두 가지 옵션이 있습니다. <ul style="margin:0"><li/><code>XmagicApi.PROCESS_TYPE_CAMERA_STREAM</code>: 카메라 데이터 원본.<li/><code>XmagicApi.PROCESS_TYPE_PICTURE_DATA</code>: 이미지 데이터 원본.</ul> |

------

## 정적 함수 설명

### setLibPathAndLoad

so 경로를 설정하고 로딩을 트리거합니다. so가 assets에 내장되어 있으면 이 메소드를 호출할 필요가 없습니다. so가 동적으로 다운로드 되는 경우 인증 및 `new XmagicApi` 전에 호출되어야 합니다. 
- null 전달: 기본 경로에서 so를 로딩하는 것을 의미하며, so가 APK 패키지에 내장되어 있음을 확인하십시오.
- 비 null 전달: `data/data/packagename/files/xmagic_libs`와 같이 이 디렉터리에서 로딩됩니다.

```
static boolean setLibPathAndLoad(String path) 
```

#### 매개변수

| 매개변수          | 의미      |
| ----------- | ------- |
| String path | so 라이브러리 저장 경로. |

