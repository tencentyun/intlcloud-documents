User Generated Short Video(UGSV) 엔터프라이즈 버전은 단종되었으며 뷰티 필터 모듈은 Tencent Effect(TE) SDK를 구성하기 위해 분리되었습니다. Tencent Effect SDK는 보다 자연스러운 뷰티 효과, 보다 강력한 기능 및 보다 유연한 통합 방법을 제공합니다. 본문에서는 UGSV 엔터프라이즈 버전에서 Tencent Effect SDK로 마이그레이션하는 방법을 설명합니다.

## 주의 사항
1. xmagic 모듈에서 glide 라이브러리의 버전 번호를 실제 버전 번호와 동일하게 수정합니다.
2. xmagic 모듈의 가장 오래된 버전 번호를 실제 버전 번호와 동일하게 수정합니다.


## 통합 단계
### 1단계: Demo 프로젝트 압축 해제
1. TE SDK가 통합된 [UGSV Demo](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.115.vcube/UGSV_Demo.zip)를 다운로드합니다. 이 Demo는 TE SDK S1-04 에디션을 기반으로 제작되었습니다.
2. Demo의 SDK 파일을 실제로 사용하는 SDK용 파일로 교체합니다. 구체적 작업은 다음 단계를 따르십시오.
   - xmagic 모듈의 libs 디렉터리에 있는 `.aar` 파일을 SDK의 libs에 있는 `.aar` 파일로 교체합니다.
   - xmagic 모듈의 `../src/main/assets`에 있는 모든 파일을 SDK의 `assets/`에 있는 파일로 교체합니다. SDK 패키지의 MotionRes 폴더에 파일이 있으면 `../src/main/assets` 디렉터리에도 복사합니다.
   - xmagic 모듈의 `../src/main/jniLibs`에 있는 모든 .so 파일을 SDK 패키지의 jniLibs에 있는 .so 파일로 교체합니다. (arm64-v8a 및 armeabi-v7a에 대한 .so 파일을 얻으려면 jinLibs 폴더에 있는 ZIP 파일의 압축을 해제해야 합니다.)
3. Demo 프로젝트의  xmagic 모듈을 실제 항목 프로젝트로 가져옵니다.

### 2단계: SDK 버전 업그레이드
SDK를 Enterprise 버전에서 Professional 버전으로 업그레이드하십시오.
- **교체 전**: `implementation 'com.tencent.liteav:LiteAVSDK_Enterprise:latest.release'`
- **교체 후**: `implementation 'com.tencent.liteav:LiteAVSDK_Professional:latest.release'`

### 3단계: 뷰티 필터 License 설정
1. 다음과 같이 프로젝트의 application에서 oncreate 메소드를 호출합니다.
```java
XMagicImpl.init(this);
XMagicImpl.checkAuth(null);
```
2. XMagicImpl 클래스의 콘텐츠를 획득한 TE SDK ***License URL 및 Key**로 교체합니다.

### 4단계: 코드 구현
UGSV 녹화 페이지 TCVideoRecordActivity.java를 예로 듭니다.

1. `TCVideoRecordActivity.java` 클래스에 다음 변수 코드를 추가합니다.
```java
private XMagicImpl mXMagic;
private int isPause = 0;//0 일시 중지되지 않음, 1일시 중지됨, 2일시 중지 중, 3종료 예정
```
2. `TCVideoRecordActivity.java` 클래스의 onCreate 메소드 뒤에 다음 코드를 추가합니다.
```java
TXUGCRecord instance = TXUGCRecord.getInstance(this);
instance.setVideoProcessListener(new TXUGCRecord.VideoCustomProcessListener() {
	 @Override
	 public int onTextureCustomProcess(int textureId, int width, int height) {
			 if (isPause == 0 && mXMagic != null) {
					 return mXMagic.process(textureId, width, height);
			 }
			 return 0;
	 }

	 @Override
	 public void onDetectFacePoints(float[] floats) {
	 }

	 @Override
	 public void onTextureDestroyed() {
			 if (Looper.getMainLooper() != Looper.myLooper()) {  //메인 스레드가 아님
					 if (isPause == 1) {
							 isPause = 2;
							 if (mXMagic != null) {
									 mXMagic.onDestroy();
							 }
							 initXMagic();
							 isPause = 0;
					 } else if (isPause == 3) {
							 if (mXMagic != null) {
									 mXMagic.onDestroy();
							 }
					 }
			 }
	 }
});
XMagicImpl.checkAuth((errorCode, msg) -> {
	 if (errorCode == TELicenseCheck.ERROR_OK) {
			 loadXmagicRes();
	 } else {
			 TXCLog.e("TAG", "인증 실패, 인증 url 및 key를 확인하십시오" + errorCode + " " + msg);
	 }
});
```
3. onStop 메소드에 다음 코드를 추가합니다.
```java
isPause = 1;
if (mXMagic != null) {
	 mXMagic.onPause();
}
```
4. onDestroy 메소드에 다음 코드를 추가합니다.
```java
isPause = 3;
XmagicPanelDataManager.getInstance().clearData();
```
5. onActivityResult 메소드 시작 부분에 다음 코드를 추가합니다.
```java
if (mXMagic != null) {
	 mXMagic.onActivityResult(requestCode, resultCode, data);
}
```
6. 이 클래스의 끝에 다음 두 메소드를 추가합니다.
```java
private void loadXmagicRes() {
	 if (XMagicImpl.isLoadedRes) {
			 XmagicResParser.parseRes(getApplicationContext());
			 initXMagic();
			 return;
	 }
	 new Thread(() -> {
			 XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath());
			 XmagicResParser.copyRes(getApplicationContext());
			 XmagicResParser.parseRes(getApplicationContext());
			 XMagicImpl.isLoadedRes = true;
			 new Handler(Looper.getMainLooper()).post(() -> {
					 initXMagic();
			 });
	 }).start();

}
/**
* 뷰티 필터 SDK 초기화
*/
private void initXMagic() {
	 if (mXMagic == null) {
			 mXMagic = new XMagicImpl(this, mUGCKitVideoRecord.getBeautyPanel());
	 }else{
			 mXMagic.onResume();
	 }
}
```

### 5단계: 다른 클래스 수정

1. AbsVideoRecordUI 클래스의 mBeautyPanel 유형을 RelativeLayout 유형으로 변경하고 getBeautyPanel() 메소드의 응답 유형을 RelativeLayout으로 변경합니다. 또한 오류를 보고하는 코드를 주석 처리하려면 해당 XML 구성을 수정해야 합니다.
2. UGCKitVideoRecord 클래스에서 오류를 보고하는 코드를 주석 처리합니다.
3. ScrollFilterView 클래스의 코드를 수정하여 mBeautyPanel 변수를 삭제하고 오류를 보고하는 코드를 주석 처리합니다.

### 6단계: beautysettingkit 모듈에 대한 종속성 삭제
ugckit 모듈의 build.gradle 파일에서 beautysettingkit 모듈에 대한 종속성을 삭제하고 프로젝트를 컴파일하여 오류를 보고하는 코드를 주석 처리합니다.

