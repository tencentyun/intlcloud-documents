[](id:step1)
## 1단계: Demo 프로젝트 압축 해제

1. Tencent Effect를 통합한 [TRTC Demo](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.115.vcube/TRTC-API-Example.zip) 프로젝트를 다운로드합니다.
2. Demo 프로젝트의 xmagic 모듈을 실제 항목 프로젝트로 가져옵니다.

[](id:step2)

## 2단계: app 모듈의 build.gradle 열기
1. applicationId를 신청된 테스트 인증과 일치하는 패키지 이름으로 수정합니다.
2. gson 종속성 설정을 추가합니다.
```groovy
configurations{
	all*.exclude group:'com.google.code.gson'
}
```

[](id:step3)
## 3단계: SDK 인터페이스 통합
Demo 프로젝트의 ThirdBeautyActivity 클래스를 참고하십시오.
1. **인증:**
```java
  //인증 시 주의사항 및 오류 코드 내용은 다음을 참고하십시오. https://cloud.tencent.com/document/product/616/65891#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83
XMagicImpl.checkAuth((errorCode, msg) -> {
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    showLoadResourceView();
                } else {
                    TXCLog.e(TAG, "인증 실패, 인증 url 및 key를 확인하십시오" + errorCode + " " + msg);
                }
            });
```
2. **소재 초기화:**
```java
private void showLoadResourceView() {
        if (XmagicLoadAssetsView.isCopyedRes) {
            XmagicResParser.parseRes(getApplicationContext());
            initXMagic();
        } else {
            loadAssetsView = new XmagicLoadAssetsView(this);
            loadAssetsView.setOnAssetsLoadFinishListener(() -> {
                XmagicResParser.parseRes(getApplicationContext());
                initXMagic();
            });
        }
    }
```
3. **푸시 설정 활성화:**
```java
mTRTCCloud.setLocalVideoProcessListener(TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_Texture_2D, TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_TEXTURE, new TRTCCloudListener.TRTCVideoFrameListener() {
    @Override
    public void onGLContextCreated() {
    }
    @Override
    public int onProcessVideoFrame(TRTCCloudDef.TRTCVideoFrame srcFrame, TRTCCloudDef.TRTCVideoFrame dstFrame) {
    }
    @Override
    public void onGLContextDestory() {
    }
});
```
4. **textureId를 SDK에 불러오기 및 렌더링 처리:**
TRTCVideoFrameListener 인터페이스의 `onProcessVideoFrame(TRTCCloudDef.TRTCVideoFrame srcFrame, TRTCCloudDef.TRTCVideoFrame dstFrame)` 메소드에 다음 코드를 추가합니다. 
```
dstFrame.texture.textureId = mXMagic.process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
```
5. **SDK 일시 중지/비활성화:**
onPause()는 뷰티 필터를 일시 중지에 사용되며, Activity/Fragment 라이프사이클 메소드에서 실행할 수 있습니다. onDestroy 메소드는 GL 스레드에서 호출해야 합니다. (onTextureDestroyed 메소드에서 XMagicImpl 객체의 `onDestroy()` 호출 가능), 자세한 사용법은 Demo를 참고하십시오.
```java
mXMagic.onPause();   //일시 정지. Activity의 onPause 메소드와 연결
mXMagic.onDestroy();  //폐기. GL 스레드에서 호출
```
6. **레이아웃에 SDK 뷰티 필터 패널 추가**:
```xml
    <RelativeLayout
        android:layout_above="@+id/ll_edit_info"
        android:id="@+id/livepusher_bp_beauty_pannel"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
```
7. **패널 초기화:**
```java
      private void initXMagic() {
          if (mXMagic == null) {
              mXMagic = new XMagicImpl(this, mBeautyPanelView);
          }else{
              mXMagic.onResume();
          }
      }
```

    자세한 내용은 Demo 프로젝트의 `ThirdBeautyActivity.initXMagic();` 메소드를 참고하십시오.

