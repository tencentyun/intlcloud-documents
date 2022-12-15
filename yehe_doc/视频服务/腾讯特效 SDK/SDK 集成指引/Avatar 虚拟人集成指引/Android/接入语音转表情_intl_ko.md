## 기능 설명
이 기능을 사용하면 오디오를 Apple ARKit의 52개  blendshape로 변환할 수 있습니다. 자세한 내용은 [ARFaceAnchor](https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation)를 참고하십시오. blendshape 데이터를 기반으로 추가 개발을 수행할 수 있습니다. 예를 들어 Unity에 데이터를 전달하여 모델을 구동할 수 있습니다.

## 통합 방식
### 방법1: Tencent Effect SDK 통합
오디오를 표정으로 변환하는 기능은 Tencent Effect SDK에 내장되어 있습니다.
1. [Tencent Effect SDK](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/latest/xmagic_ALL_android_latest.zip)의 전체 버전을 다운로드합니다.
2. SDK를 통합합니다. 자세한 지침은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45385)를 참고하십시오.

### 방법2: Audio-to-Expression SDK 통합
다른 Tencent Effect 기능이 필요하지 않은 경우 aar 파일이 약 6MB인 Audio-to-Expression SDK를 통합할 수 있습니다. SDK를 얻으려면 저희에게 연락하십시오.

## 통합 단계

1. **License를 설정합니다**. 자세한 내용은 [인증](https://intl.cloud.tencent.com/document/product/1143/45385#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83)을 참고하십시오.
2. **모델 파일 구성**: assets에서 `context.getFilesDir() + "/my_models_dir/audio2exp"`와 같은 app의 개인 디렉터리로 모델 파일을 복사합니다. 그 다음 Audio2ExpApi의 `init(String modelPath)` API를 호출하여 `context.getFilesDir() + "/my_models_dir"`을 전달합니다.
SDK 패키지에서 모델 파일을 찾을 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/383c572788f49611abd56626266f44a7.png)

## API 설명
<table>
<thead>
<tr>
<th>API</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>public int Audio2ExpApi.init(String modelPath);</code></td>
<td>SDK를 초기화합니다. 이 API를 호출할 때 모델 파일의 경로를 전달합니다. 0은 초기화에 성공했음을 나타냅니다.</td>
</tr>
<tr>
<td><code>public float[] Audio2ExpApi.parseAudio(float[] inputData);</code></td>
<td>입력은 오디오이며 1채널이어야 하며 샘플링 레이트는 16K여야 합니다. 배열 길이는 267(샘플링 포인트 267개)입니다. 출력은 52개의 blendshape에 해당하는 52개의 요소가 있는 float 배열입니다. 요소의 값 범위는 -1에서 1까지이며 순서는 <a href="https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation">Apple</a>에서 지정합니다.</td>
</tr>
<tr>
<td><code>public int Audio2ExpApi.release();</code></td>
<td>리소스를 해제합니다. 더 이상 기능을 사용할 필요가 없을 때 이 API를 호출하십시오.</td>
</tr>
</tbody></table>

## 통합 코드 예시
```
@Override
protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		findViewById(R.id.button).setOnClickListener(new OnClickListener() {
				@Override
				public void onClick(View view) {
						TELicenseCheck.getInstance().setTELicense(MainActivity.this, "https://license.vod2.myqcloud.com/license/v2/1258289294_1/v_cube.license", "3c16909893f53b9600bc63941162cea3", new TELicenseCheckListener() {
								@Override
								public void onLicenseCheckFinish(int errorCode, String s) {
										Log.d(TAG, "onLicenseCheckFinish: errorCode = "+errorCode+",msg="+s);
										if (errorCode == TELicenseCheck.ERROR_OK) {
												//license check success
												Audio2ExpApi audio2ExpApi = new Audio2ExpApi();
												int err = audio2ExpApi.init(MainActivity.this.getFilesDir() +"/models");
												Log.d(TAG, "onLicenseCheckFinish: err="+err);
												//TODO start record and parse audio data
										} else {
												// license check failed
										}
								}
						});
				}
		});
}
```

>? 전체 코드 샘플은 [Demo](https://intl.cloud.tencent.com/document/product/1143/45374)를 참고하십시오.
- 오디오 녹음은 `com.tencent.demo.avatar.audio.AudioCapturer`를 참고하십시오.
- API 사용 방법에 대한 자세한 내용은 `com.tencent.demo.avatar.activity.Audio2ExpActivity` 및 관련 클래스를 참고하십시오.