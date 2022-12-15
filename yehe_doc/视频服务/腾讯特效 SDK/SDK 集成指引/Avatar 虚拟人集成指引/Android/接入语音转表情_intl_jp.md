## 機能説明
オーディオデータを入力すると、Apple ARKitの標準である52種類の表情のデータが出力されます。詳細については、[ARFaceAnchor](https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation)をご参照ください。これらの表情データを利用して、Unityに渡してモデルを動かすといった、さらに進んだ開発を行うことができます。

## アクセス方法
### 方法1：Tencent Effect SDKによる接続
音声から表情への変換は、Tencent Effect SDKに統合されているため、最初の接続はTencent Effectのドキュメントに従って行う必要があります。
1. [Tencent Effect SDK完全版](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/latest/xmagic_ALL_android_latest.zip)をダウンロードします。
2. [Tencent Effectの独立した統合](https://intl.cloud.tencent.com/document/product/1143/45385)のドキュメントを参照して統合を完了します。

### 方法2：独立した音声表情変換SDKによる接続
音声から表情への変換のみが必要で、Tencent Effect SDKの機能を使用する必要がない場合は、独立した音声表情変換SDKの使用を検討することができます。aarパッケージは約6MBです。このSDKの取得については、アーキテクトまたは販売担当者までご連絡ください。

## 統合の手順

1. **Licenseを設定します**。[認証](https://intl.cloud.tencent.com/document/product/1143/45385#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83)をご参照ください。
2. **モデルファイルの設定**：必要なモデルファイルをassetsからappのプライベートディレクトリにコピーしてください（例：`context.getFilesDir() + "/my_models_dir/audio2exp"`）。その後、Audio2ExpApiの`init(String modelPath)`インターフェースを呼び出した際、パラメータ`context.getFilesDir() + "/my_models_dir"`を渡します
モデルファイルはSDKパッケージにあります。場所は次のとおりです。
![](https://qcloudimg.tencent-cloud.cn/raw/383c572788f49611abd56626266f44a7.png)

## インターフェースの説明
<table>
<thead>
<tr>
<th>インターフェース</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td><code>public int Audio2ExpApi.init(String modelPath);</code></td>
<td>初期化し、モデルのパスを渡します。上記の説明をご覧ください。戻り値が0の場合は成功です</td>
</tr>
<tr>
<td><code>public float[] Audio2ExpApi.parseAudio(float[] inputData);</code></td>
<td>入力するのはオーディオデータであり、シングルチャネル、16Kサンプルレート、配列の長さは267（すなわち267のサンプリングポイント）である必要があります。出力されるデータは長さが52のfloat配列で、52の表情ベースを表し、値は-1～1の間で、順序は<a href="https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation">Apple標準順</a>です</td>
</tr>
<tr>
<td><code>public int Audio2ExpApi.release();</code></td>
<td>使用完了後に呼び出し、リソースを解放します</td>
</tr>
</tbody></table>

## 統合コード例
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
										}else{
												// license check failed
										}
								}
						});
				}
		});
}
```

>? 完全なサンプルコードについては、[美顔エフェクトSDK demoプロジェクト](https://intl.cloud.tencent.com/document/product/1143/45374)をご参照ください。
- 録音については `com.tencent.demo.avatar.audio.AudioCapturer`をご参照ください。
- インターフェースの使用については`com.tencent.demo.avatar.activity.Audio2ExpActivity`およびその関連クラスをご参照ください。