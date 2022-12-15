[](id:step1)
## 1단계: Demo  프로젝트 압축 해제
1. Tencent Effect SDK가 통합된 [UGSV Demo](https://intl.cloud.tencent.com/document/product/1143/45374)를 다운로드합니다. 이 Demo는 Tencent Effect SDK S1-04 에디션을 기반으로 제작되었습니다.
2. Demo의 SDK 파일을 실제로 사용하는 SDK용 파일로 교체합니다. 구체적 작업은 다음 단계를 따르십시오.
   - `xmagickit module`의 `build.gradle` 파일에서 다음을 찾습니다.
```groovy
api 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release'
```
[Tencent Effect SDK 통합하기(Android)](https://intl.cloud.tencent.com/document/product/1143/45385)에 설명된 대로 구매한 SDK 버전으로 교체합니다.
   - SDK 버전에 애니메이션 효과 및 필터가 포함되어 있는 경우 해당 SDK 패키지를 [다운로드](https://intl.cloud.tencent.com/document/product/1143/45377)하고 애니메이션 효과 및 필터에 대한 리소스를 `xmagickit module`의 다음 디렉터리에 추가해야 합니다.
	- 애니메이션 효과: `../assets/MotionRes`
	- 필터: `../assets/lut`
3. Demo 프로젝트의 xmagickit 모듈을 실제 항목 프로젝트로 가져옵니다.

[](id:step2)

## 2단계: 패키지 이름 수정
app에서 build.gradle을 열고 applicationId를 평가판 라이선스에 바인딩된 패키지 이름으로 설정합니다.

[](id:step3)
## 3단계: SDK API 통합
Demo의 UGCKitVideoRecord 클래스를 참고하십시오.
1. **라이선스 설정:**
```java
 //인증 시 주의사항 및 오류 코드 내용은 다음을 참고하십시오. https://intl.cloud.tencent.com/document/product/1143/45385#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83
 XMagicImpl.checkAuth(new TELicenseCheck.TELicenseCheckListener() {
            @Override
            public void onLicenseCheckFinish(int errorCode, String msg) {
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    loadXmagicRes();
                } else {
                    Log.e("TAG", "auth fail ，please check auth url and key" + errorCode + " " + msg);
                }
            }
        });
```
2. **리소스 초기화:**
```java
 private void loadXmagicRes() {
        if (XMagicImpl.isLoadedRes) {
            XmagicResParser.parseRes(mActivity.getApplicationContext());
            initXMagic();
            return;
        }
        new Thread(new Runnable() {
            @Override
            public void run() {
                XmagicResParser.copyRes(mActivity.getApplicationContext());
                XmagicResParser.parseRes(mActivity.getApplicationContext());
                XMagicImpl.isLoadedRes = true;
                new Handler(Looper.getMainLooper()).post(new Runnable() {
                    @Override
                    public void run() {
                        initXMagic();
                    }
                });
            }
        }).start();
    }
```
3. **UGSV와 뷰티 필터 바인딩:**
```java
 private void initBeauty() {
        TXUGCRecord instance = TXUGCRecord.getInstance(UGCKit.getAppContext());
        instance.setVideoProcessListener(new TXUGCRecord.VideoCustomProcessListener() {
            @Override
            public int onTextureCustomProcess(int textureId, int width, int height) {
                if (xmagicState == XMagicImpl.XmagicState.STARTED && mXMagic != null) {
                    return mXMagic.process(textureId, width, height);
                }
                return textureId;
            }

            @Override
            public void onDetectFacePoints(float[] floats) {
            }

            @Override
            public void onTextureDestroyed() {
                if (Looper.getMainLooper() != Looper.myLooper()) {  //메인 스레드가 아님
                    boolean stopped = xmagicState == XMagicImpl.XmagicState.STOPPED;
                    if (stopped || xmagicState == XMagicImpl.XmagicState.DESTROYED) {
                        if (mXMagic != null) {
                            mXMagic.onDestroy();
                        }
                    }
                    if (xmagicState == XMagicImpl.XmagicState.DESTROYED) {
                        TXUGCRecord.getInstance(UGCKit.getAppContext()).setVideoProcessListener(null);
                    }
                }
            }
        });
    }
```
4. **SDK 일시 중지/종료:**
 onPause()는 뷰티 필터 일시 중지에 사용되며, Activity/Fragment 라이프사이클 메소드에서 구현할 수 있습니다. onDestroy 메소드는 GL 스레드에서 호출해야 합니다. (onTextureDestroyed 메소드에서 XMagicImpl 객체의 `onDestroy()` 호출 가능), 자세한 내용은 Demo의 `onTextureDestroyed`를 참고하십시오.
```java
            @Override
            public void onTextureDestroyed() {
                if (Looper.getMainLooper() != Looper.myLooper()) {  //메인 스레드가 아님
                    boolean stopped = xmagicState == XMagicImpl.XmagicState.STOPPED;
                    if (stopped || xmagicState == XMagicImpl.XmagicState.DESTROYED) {
                        if (mXMagic != null) {
                            mXMagic.onDestroy();
                        }
                    }
                    if (xmagicState == XMagicImpl.XmagicState.DESTROYED) {
                        TXUGCRecord.getInstance(UGCKit.getAppContext()).setVideoProcessListener(null);
                    }
                }
            }
```
5. **뷰티 필터 패널에 대한 레이아웃 추가:**
```xml
 <RelativeLayout
        android:id="@+id/panel_layout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:visibility="gone"/>
```
6. **뷰티 필터 객체를 생성하고 뷰티 필터 패널을 추가합니다.**
```java
   private void initXMagic() {
       if (mXMagic == null) {
           mXMagic = new XMagicImpl(mActivity, getBeautyPanel());
       } else {
           mXMagic.onResume();
       }
   }
```

자세한 지침은 Demo의 UGCKitVideoRecord 클래스를 참고하십시오.

