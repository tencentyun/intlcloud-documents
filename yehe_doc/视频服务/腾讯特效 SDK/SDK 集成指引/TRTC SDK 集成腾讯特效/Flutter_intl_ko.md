## 1단계: 뷰티 필터 리소스 다운로드 및 통합

1. 구매한 패키지의 해당 SDK를 [다운로드](https://intl.cloud.tencent.com/document/product/1143/45377)합니다.
2. 자신의 프로젝트에 리소스 파일을 추가합니다.
<dx-tabs>
::: Android
1. app에서 build.gradle을 열고 패키지의 maven 주소를 추가합니다. 예를 들어 S1-04를 구매한 경우 다음을 추가합니다.
```groovy
dependencies{
      implementation 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release'
   }
```
**[문서](https://intl.cloud.tencent.com/document/product/1143/45385)에서 다양한 패키지의 maven 주소를 확인할 수 있습니다.**
2. app에서 src/main/assets 폴더를 찾습니다(이 폴더가 없으면 새로 만듭니다). MotionRes 폴더가 있는지 확인합니다. `../src/main/assets`에 복사합니다.
3. app에서 AndroidManifest.xml을 열고 application에 다음 태그를 추가합니다.
```xml
 <uses-native-library
           android:name="libOpenCL.so"
           android:required="true" />
```
다음과 같이 표시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/adca155b8fa60600465bdfc6e78ebb2b.png)
:::
::: iOS
1. 프로젝트에 뷰티 필터 리소스를 추가합니다(리소스는 스크린샷과 다를 수 있음).
![](https://qcloudimg.tencent-cloud.cn/raw/e5cb4984aa2bfa14fd4f837acf465cfa.png)
2. demo/lib/producer에 있는 BeautyDataManager, BeautyPropertyProducer, BeautyPropertyProducerAndroid 및 BeautyPropertyProducerIOS의 네 가지 클래스를 Flutter 프로젝트에 복사합니다. 뷰티 필터 패널에서 뷰티 필터 리소스 및 표시 뷰티 필터 옵션을 구성하는 데 사용됩니다.
:::
</dx-tabs>


## 2단계: Flutter SDK 참조

프로젝트의 pubspec.yaml 파일에 다음 참조를 추가합니다.
```json
 tencent_effect_flutter:
   git:
     url: https://github.com/TencentCloud/tencenteffect-sdk-flutter
```

## 3단계: TRTC와 Tencent Effect 결합
<dx-tabs>
::: Android
다음 코드를 application 클래스의 oncreate(또는 FlutterActivity의 onCreate)에 추가합니다.
```jav
TRTCCloudPlugin.register(new XmagicProcesserFactory());
```
:::
::: iOS
AppDelegate 클래스의 didFinishLaunchingWithOptions에 다음 코드를 추가합니다.
```objective-c
XmagicProcesserFactory *instance = [[XmagicProcesserFactory alloc] init];
[TencentTRTCCloud registerWithCustomBeautyProcesserFactory:instance];
```
다음과 같이 표시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3f2de0a60696f18daedde2228d65076a.png)

:::
</dx-tabs>

## 4단계: 리소스 초기화 API 호출
```dart
  String dir =  await BeautyDataManager.getInstance().getResDir();
   TXLog.printlog('파일 경로: $dir');
   TencentEffectApi.getApi()?.initXmagic(dir,(reslut) {
     _isInitResource = reslut;
     callBack.call(reslut);
     if (!reslut) {
       Fluttertoast.showToast(msg: "리소스 초기화 실패");
     }
   }); TencentEffectApi.getApi()?.initXmagic((reslut) {
     if (!reslut) {
       Fluttertoast.showToast(msg: "리소스 초기화 실패");
     }
   });
```

## 5단계: 라이선스 설정
```dart
TencentEffectApi.getApi()?.setLicense(licenseKey, licenseUrl,
           (errorCode, msg) {
         TXLog.printlog("인증 결과 출력 errorCode = $errorCode   msg = $msg");
         if (errorCode == 0) {
            //인증 성공
         }
       });
```

## 6단계: 뷰티 필터 활성화
```dart
///뷰티 필터 활성화
 var enableCustomVideo = await trtcCloud.enableCustomVideoProcess(open);
```

## 7단계: 뷰티 필터 속성 설정

```dart
    TencentEffectApi.getApi()?.updateProperty(_xmagicProperty!);
///_xmagicProperty는 BeautyDataManager.getInstance().getAllPannelData();를 호출하여 모든 속성을 가져오고 updateProperty를 호출하여 속성을 설정할 수 있습니다.
```

## 8단계: 기타 속성 설정

- **오디오 효과 일시 중지**
```dart
 TencentEffectApi.getApi()?.onPause();  
```
- **오디오 효과 재개**
```dart
TencentEffectApi.getApi()?.onResume();
```
- **뷰티 필터 이벤트 수신**
```dart
TencentEffectApi.getApi()
       ?.setOnCreateXmagicApiErrorListener((errorMsg, code) {
         TXLog.printlog("뷰티 필터 객체 생성 오류 errorMsg = $errorMsg , code = $code");
   });   ///뷰티 필터 객체를 생성하기 전에 리스너를 설정해야 합니다.
```
- **얼굴, 제스처, 신체 감지 결과 콜백 설정**
```dart
TencentEffectApi.getApi()?.setAIDataListener(XmagicAIDataListenerImp());
```
- **애니메이션 효과 팁에 대한 콜백 구성**
```dart
TencentEffectApi.getApi()?.setTipsListener(XmagicTipsListenerImp());
```
- **얼굴 키포인트 및 기타 데이터의 콜백 구성(S1-05 및 S1-06에서만 사용 가능)**
```dart
TencentEffectApi.getApi()?.setYTDataListener((data) {
     TXLog.printlog("setYTDataListener  $data");
   });
```
- **모든 콜백을 제거합니다**. 페이지를 종료할 때 모든 콜백을 제거해야 합니다.
```dart
 TencentEffectApi.getApi()?.setOnCreateXmagicApiErrorListener(null);
 TencentEffectApi.getApi()?.setAIDataListener(null);
 TencentEffectApi.getApi()?.setYTDataListener(null);
 TencentEffectApi.getApi()?.setTipsListener(null);
```

>? API에 대한 자세한 내용은 API 설명서를 참고하십시오. 기타는 Demo 프로젝트를 참고하십시오.

## 9단계: 뷰티 필터 패널에 데이터 추가 및 제거
BeautyDataManager, BeautyPropertyProducer, BeautyPropertyProducerAndroid 및 BeautyPropertyProducerIOS 클래스에서 효과 패널 데이터를 사용자 지정할 수 있습니다.
- **뷰티 필터 리소스 추가**
1단계에서 설명한 대로 해당 폴더에 리소스 파일을 추가합니다. 예를 들어 2D 애니메이션 효과를 추가하려면 다음을 수행합니다.
	1. 프로젝트의 `android/xmagic/src.mian/assets/MotionRes/2dMotionRes`에 리소스를 넣습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7e91b97099e3d337de31c4893686759b.png" style="zoom:50%;" />
	2. 또한 리소스를 `ios/Runner/xmagic/2dMotionRes.bundle`에 추가합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8c806cb1c77d9c49b787ab17f77a2f0d.png" style="zoom:50%;" />
- **뷰티 필터 리소스 삭제**
귀하의 License는 패널에서 일부 뷰티 필터 또는 신체 보정 효과를 지원하지 않을 수 있습니다. 지원되지 않는 기능은 삭제할 수 있습니다.
예를 들어 립스틱 효과를 삭제하려면 BeautyPropertyProducerAndroid와 BeautyPropertyProducerIOS의 getBeautyData에서 아래 코드를 삭제합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/774aa1367fce726b17e34319d1b08bc2.png" style="zoom:50%;" />

