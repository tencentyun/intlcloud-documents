## 통합 준비
1. [SDK Download](https://intl.cloud.tencent.com/document/product/1143/45377) 후 압축을 해제합니다.
2. **다음 파일 준비:**
<table>
<tbody><tr><th>파일 유형</th><th>설명</th></tr>
<tr>
<td>xmagic-xxx.aar</td><td>SDK, 필수</td>
</tr><tr>
<td>../assets/</td><td>알고리즘 모델, 소재 리소스 패키지, 필수</td>
</tr><tr>
<td>../jniLibs</td><td>so 라이브러리, 필수</td>
</tr></tbody></table>

## 리소스 가져오기
<dx-tabs>
::: 수동 통합
#### 통합
- 상기 파일로 준비된 모든 `.aar` 파일을 app 프로젝트의 `libs` 디렉터리에 추가합니다.
- SDK 패키지의 assets/에 있는 모든 파일을 `../src/main/assets` 디렉터리에 복사합니다. SDK 패키지의 MotionRes 폴더에 파일이 있으면 `../src/main/assets` 디렉터리에도 복사합니다.
- jniLibs 폴더를 프로젝트의 `../src/main/jniLibs` 디렉터리에 복사합니다.

#### 가져오기 방법
app 모듈의 `build.gradle`을 열고 종속 참조 테이블을 추가합니다.

```groovy
android{
    ...
    defaultConfig {
        applicationId "인증된 lic 라이선스에 바인딩된 패키지 이름으로 수정"
        ....
    }
    packagingOptions {
        pickFirst ’**/libc++_shared.so’
    }
}

dependencies{
    ...
    compile fileTree(dir: 'libs', include: ['*.jar','*.aar'])//추가 *.aar
}
```
>! Google의 Gson 라이브러리가 프로젝트에 통합되지 않은 경우 다음 종속성을 추가해야 합니다.
```groovy
dependencies{
    implementation 'com.google.code.gson:gson:2.8.2'
}
```
:::
::: Maven 통합
Tencent Effect SDK를 mavenCentral에 이미 배포했다면 gradle 자동 다운로드 설정을 통해 업데이트할 수 있습니다.

1. dependencies에서 Tencent Effect SDK 종속을 추가합니다.
```groovy
dependencies{
	//예시: S1-04 패키지는 다음과 같습니다
	implementation 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release'
}
```
2. defaultConfig에서 App이 사용하는 CPU 구성을 지정합니다.
```
defaultConfig {
	ndk {
		abiFilters "armeabi-v7a", "arm64-v8a"
	}
}
```
>? 현재 Effect SDK는 armeabi-v7a 및 arm64-v8a를 지원합니다.

3. ![img](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)**Sync Now**를 클릭하여 SDK를 자동으로 다운로드하고 프로젝트에 통합합니다.
4. 패키지에 애니메이션 효과 및 필터 기능이 포함된 경우 [SDK 다운로드 페이지](https://intl.cloud.tencent.com/document/product/1143/45377)에서 해당 리소스를 다운로드하고 애니메이션 효과 및 필터 자료를 프로젝트 아래의 다음 디렉터리에 배치해야 합니다.
	- 애니메이션 효과: `../assets/MotionRes`      
	- 필터: `../assets/lut`

#### 각 패키지에 해당하는 Maven 주소

| 버전    | Maven 주소                                                    |
| ------- | ------------------------------------------------------------ |
| A1 - 01 | implementation 'com.tencent.mediacloud:TencentEffect_A1-01:latest.release' |
| A1 - 02 | implementation 'com.tencent.mediacloud:TencentEffect_A1-02:latest.release' |
| A1 - 03 | implementation 'com.tencent.mediacloud:TencentEffect_A1-03:latest.release' |
| A1 - 04 | implementation 'com.tencent.mediacloud:TencentEffect_A1-04:latest.release' |
| A1 - 05 | implementation 'com.tencent.mediacloud:TencentEffect_A1-05:latest.release' |
| A1 - 06 | implementation 'com.tencent.mediacloud:TencentEffect_A1-06:latest.release' |
| S1 - 00 | implementation 'com.tencent.mediacloud:TencentEffect_S1-00:latest.release' |
| S1 - 01 | implementation 'com.tencent.mediacloud:TencentEffect_S1-01:latest.release' |
| S1 - 02 | implementation 'com.tencent.mediacloud:TencentEffect_S1-02:latest.release' |
| S1 - 03 | implementation 'com.tencent.mediacloud:TencentEffect_S1-03:latest.release' |
| S1 - 04 | implementation 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release' |
:::
::: 동적 다운로드 통합
#### assets, so, 애니메이션 리소스 가이드 동적 다운로드
패키지 크기를 줄이기 위해 SDK에 필요한 assets 리소스, so 라이브러리, 그리고 애니메이션 리소스 MotionRes(일부 기본 버전 SDK 애니메이션 리소스 없음)를 인터넷으로 변경하여 다운로드할 수 있습니다. 다운로드가 완료 후 위 파일의 경로를 SDK로 설정합니다.

Demo의 다운로드 로직을 재사용하는 것이 좋습니다. 기존 다운로드 서비스를 사용할 수도 있습니다. 동적 다운로드에 대한 자세한 지침은 [SDK Package Downsizing (Android)](https://www.tencentcloud.com/document/product/1143/47831)을 참고하십시오.
:::
</dx-tabs>


## 전체 프로세스

[](id:step1)
### 1단계: 인증

1. 라이선스를 신청하고 License URL과 License KEY를 받습니다.
>! 일반적인 상황에서는 App이 한 번만 성공적으로 연결되면 인증 프로세스가 완료되므로 License 파일을 프로젝트의 assets 디렉터리에 넣을 **필요가 없습니다**. 그러나 만약 App이 인터넷에 연결되지 않은 상태에서도 SDK 관련 기능을 사용하려면 License 파일을 assets 디렉터리에 다운로드하여 기본 설정으로 사용할 수 있습니다. 이 때 License 파일 이름은 `v_cube. license`이어야 합니다.

2. 해당 비즈니스 모듈의 초기화 코드에 URL과 KEY를 설정하여 License 다운로드를 트리거하여 사용 전 일시적으로 다운로드되는 것을 방지합니다. Application의 onCreate 메소드에서 다운로드를 트리거하는 것도 가능하지만, 이때 네트워크 권한이 없거나 네트워크 실패율이 높을 수 있기 때문에 권장하지 않습니다.
```
//license를 다운로드하거나 업데이트하기 위한 것일 뿐 인증 결과에 신경 쓰지 않는다면 네 번째 매개변수가 null로 전달됩니다.
TELicenseCheck.getInstance().setXMagicLicense(context, URL, KEY, null);
```
3. 그런 다음 실제로 뷰티 필터 기능(예시: Demo의 'LaunchActivity.java')을 사용하기 전에 인증을 수행합니다.
```java
// 네트워크에서 so 라이브러리를 다운로드한 경우 TELicenseCheck.getInstance().setTELicense를 호출하기 전에 so 경로를 설정하십시오. 그렇지 않으면 인증이 실패합니다.
// XmagicApi.setLibPathAndLoad(validLibsDirectory);
// so가 apk 패키지에 내장되어 있으면 위의 메소드를 호출할 필요가 없습니다.
TELicenseCheck.getInstance().setTELicense(context, URL, KEY, new TELicenseCheckListener() {

            @Override
            public void onLicenseCheckFinish(int errorCode, String msg) {
                //주의: 스레드 호출이 꼭 필요한 것은 아닙니다.
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    //인증 성공
                } else {
                    //인증 실패
                }
            }
        });
```

**인증 errorCode 설명:**
<table>
<thead>
<tr>
<th>에러 코드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>성공. Success</td>
</tr>
<tr>
<td>-1</td>
<td>잘못된 입력 매개변수, 예시: 빈 URL 또는 KEY</td>
</tr>
<tr>
<td>-3</td>
<td>다운로드 실패, 네트워크 설정 확인</td>
</tr>
<tr>
<td>-4</td>
<td>로컬에서 읽은 TE 인증 정보가 비어 있음, 이는 IO 실패로 인해 발생한 것일 수 있습니다.</td>
</tr>
<tr>
<td>-5</td>
<td>VCUBE TEMP License 파일 읽기 내용이 비어 있습니다. 이는 IO 실패로 인한 것일 수 있습니다.</td>
</tr>
<tr>
<td>-6</td>
<td><code>v_cube.license</code> 파일 JSON 필드가 잘못되었습니다. 처리를 위해 Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-7</td>
<td>서명 인증 실패. 처리를 위해 Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-8</td>
<td>복호화 실패. 처리를 위해 Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-9</td>
<td>TELicense 필드의 JSON 필드가 올바르지 않습니다. 처리를 위해 Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-10</td>
<td>네트워크에서 리졸브된 TE 인증 정보가 비어 있습니다. 처리를 위해 Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>-11</td>
<td>IO 실패로 인해 로컬 파일에 TE 인증 정보를 쓰지 못했습니다.</td>
</tr>
<tr>
<td>-12</td>
<td>다운로드에 실패했으며 로컬 asset의 리졸브도 실패했습니다.</td>
</tr>
<tr>
<td>-13</td>
<td>인증에 실패했습니다. 패키지에 so가 있는지 확인하거나 so 경로가 올바르게 설정되었는지 확인하십시오.</td>
</tr>
<tr>
<td>3004/3005</td>
<td>인증이 잘못되었습니다. Tencent Cloud 팀에 문의하십시오.</td>
</tr>
<tr>
<td>3015</td>
<td>Bundle Id / Package Name이 일치하지 않습니다. App 에서 사용하는 Bundle Id / Package Name이 신청한 것과 동일한지 확인하고 올바른 인증 파일이 사용되었는지 확인하십시오.</td>
</tr>
<tr>
<td>3018</td>
<td>인증 파일이 만료되었으므로 Tencent Cloud에 연장을 신청해야 합니다.</td>
</tr>
<tr>
<td>기타</td>
<td>Tencent Cloud 팀에 문의하십시오.</td>
</tr>
</tbody></table>

[](id:step2)
### 2단계: 리소스 복사
1. 리소스 파일이 assets 디렉터리에 내장된 경우 사용하기 전에 app의 개인 디렉터리에 copy해야 합니다. 미리 copy하거나 이전 단계에서 인증 성공 콜백에서 복사 작업을 수행할 수 있습니다. 예시 코드는 Demo의 'LaunchActivity.java'에 있습니다.
```
XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath());
//loading

// 리소스 파일을 프라이빗 디렉터리에 copy합니다. 한 번만 수행하면 됩니다.
XmagicResParser.copyRes(getApplicationContext());
```
2. [동적 네트워크 다운로드](#download)에서 리소스 파일을 다운로드한 경우 다운로드가 성공한 후 리소스 파일 경로를 설정해야 합니다. 예시 코드는 Demo의 'LaunchActivity.java'에 있습니다.
```
XmagicResParser.setResPath(다운로드한 리소스 파일 로컬 경로);
```

[](id:step3)
### 3단계: SDK 초기화 및 사용 방법

Tencent 특수 효과 SDK를 사용하는 라이프사이클은 대략 다음과 같습니다.
1. 뷰티 필터 UI 데이터 구성은 Demo 프로젝트를 참고하십시오.`XmagicResParser.java,XmagicUIProperty.java,XmagicPanelDataManager.java` 코드.
2. 미리보기 레이아웃에 GLSurfaceView를 추가합니다.  
```java
<android.opengl.GLSurfaceView
android:id="@+id/camera_gl_surface_view"
android:layout_width="match_parent"
android:layout_height="match_parent" />
```
3. (옵션) 카메라를 빠르게 구현합니다.
Demo 프로젝트의 com.tencent.demo.camera 디렉터리를 프로젝트에 복사합니다. 카메라 기능을 빠르게 구현하려면 'PreviewMgr' 클래스를 사용하십시오. 자세한 구현 방법은 Demo 프로젝트의 'MainActivity.java'를 참고하십시오.
```java
//카메라 초기화
mPreviewMgr = new PreviewMgr();
//레이아웃의 GlSurfaceView 예제를 카메라 툴 클래스에 전달
mPreviewMgr.onCreate(mGlSurfaceView,false);
//미리보기 텍스처 데이터 콜백 함수 가입
mPreviewMgr.setCustomTextureProcessor((textureId, textureWidth, textureHeight) -> {
	if (mXmagicApi == null) {
			return textureId;
	}
	//렌더링을 위해 뷰티 필터 sdk 호출
	int outTexture = mXmagicApi.process(textureId, textureWidth, textureHeight);
	return outTexture;
});

//Activity의 onResume 메소드에서 카메라 실행
mPreviewMgr.onResume(this, 1280, 720);
```
4. 뷰티 필터 SDK를 초기화하고 Activity의 'onResume()' 메소드에 넣는 것을 권장합니다.
```java
mXmagicApi = new XmagicApi(this, XmagicResParser.getResPath(),new XmagicApi.OnXmagicPropertyErrorListener()); 
```

- **매개변수**
 <table>
 <tr><th>매개변수</th><th>의미</th></tr><tr><td>Context context</td><td>컨텍스트</td>
 </tr><tr>
 <td>String resDir</td><td>리소스 파일 디렉터리, 자세한 내용은 <a href="#step2">2단계</a>를 참고하십시오.</td>
 </tr><tr>
 <td>OnXmagicPropertyErrorListener errorListener</td><td>콜백 함수 구현 클래스</td>
 </tr></table>

- **반환**
 오류 코드 의미는 [API 문서](https://intl.cloud.tencent.com/document/product/1143/45399)를 참고하십시오.
5. 소재 프롬프트 콜백 함수를 추가합니다(메소드 콜백은 서브 스레드에서 실행될 수 있음). 고개 끄덕임, 손바닥 내밀기, 손 하트 등 일부 소재는 사용자에게 프롬프트를 표시합니다. 이 콜백은 바로 유사한 프롬프트를 보여주기 위한 것입니다.
```
mXmagicApi.setTipsListener(new XmagicTipsListener() {
	final XmagicToast mToast = new XmagicToast();
	@Override
	public void tipsNeedShow(String tips, String tipsIcon, int type, int duration) {
		mToast.show(MainActivity.this, tips, duration);
	}

	@Override
	public void tipsNeedHide(String tips, String tipsIcon, int type) {
		mToast.dismiss();
	}
});
```

6. 뷰티 필터 SDK는 데이터의 각 프레임을 처리하고 해당 처리 결과를 반환합니다.
```
int outTexture = mXmagicApi.process(textureId, textureWidth, textureHeight);
```

7. 지정된 유형의 뷰티 필터 특수 효과 값을 업데이트합니다.
```java
// 사용 가능한 입력 속성은 XmagicResParser.parseRes()에서 가져오기
mXmagicApi.updateProperty(XmagicProperty<?> p);
```
8. 뷰티 필터 SDK를 Pause하려면 Activity의 'onPause()' 라이프사이클로 바인딩하는 것이 좋습니다.
```java
//Activity의 onPause 시 호출되며 OpenGL 스레드에서 호출되어야 합니다.
mXmagicApi.onPause();
```
9. 뷰티 필터 SDK를 릴리스하고 Activity의 'onDestroy()' 라이프사이클과 바인딩하는 것이 좋습니다.
```java
//이 메소드는 GL 스레드에서 호출되어야 합니다.
mXmagicApi.onDestroy()
```