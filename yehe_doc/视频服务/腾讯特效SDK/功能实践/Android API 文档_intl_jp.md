Tencent Effect SDKのコアインターフェースクラス`XmagicApi.java`は、SDKの初期化、美顔数値の更新、動的エフェクト呼び出しなどの機能に用いられます。

## Publicメンバー関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [XmagicApi](#xmagicapi)                                      | コンストラクタ。                                                   |
| [updateProperty](#updateproperty)                            | プロパティを更新します。任意のスレッドで呼び出せます。                                |
| [updateProperties](#updateproperties)                        | プロパティを更新します。任意のスレッドで呼び出せます。                                 |
| [setTipsListener](#settipslistener)                          | 動的エフェクトプロンプトのコールバック関数を設定します。プロンプトをフロントエンドのページ上に表示するために用いられます。       |
| [setYTDataListener](#setytdatalistener)                      | 顔の特徴点位置情報などのデータのコールバックを設定します（S1-05およびS1-06パッケージのみコールバックあり）。 |
| [setAIDataListener](#setaidatalistener)                      | 顔、ジェスチャー、体の検出状態のコールバックを設定します。                           |
| [onPause](#onpause)                                          | 音声の再生を一時停止します。ActivityのonPauseライフサイクルにバインドできます。           |
| [onResume](#onresume)                                        | レンダリングを再開します。ActivityのonResumeライフサイクルにバインドできます。           |
| [onDestroy](#ondestroy)                                      | xmagicを破棄します。GLスレッドで呼び出す必要があります                            |
| [process](#process)                                          | SDKレンダリングのデータを受信するメソッドです。カメラデータのコールバック関数内で使用できます。         |
| [onPauseAudio](#onpauseaudio)                                | オーディオのみ停止する必要があり、GLスレッドはリリースする必要がない場合に、この関数を呼び出すことができます。         |
| [sensorChanged](#sensorchanged)                              | 現在のスマートフォンの回転の角度を判断し、それによってAIの顔認識の判断角度の根拠を調整するために用いられます。 |
| [isDeviceSupport](#isdevicesupport)                          | 動的エフェクトリソースリストをSDKのチェック用に渡します。実行後、XmagicProperty.isSupportフィールドは、そのアトミック機能が利用可能かどうかを表します。XmagicProperty.isSupportによってUIレイヤーのクリック制限を制御することや、直接リソースリストから削除することができます。 |
| [getPropertyRequiredAbilities](#getpropertyrequiredabilities) | 動的エフェクトリソースリストを渡し、各リソースが使用できるSDKアトミック機能のリストを返します。 |
| [getDeviceAbilities](#getdeviceabilities)                    | 現在のデバイスでサポートされているアトミック機能のテーブルを返します                                 |
| [isSupportBeauty](#issupportbeauty)                          | 現在のモデルが美顔機能をサポートしているかどうかを判断します（OpenGL3.0）。                      |
| [isBeautyAuthorized](#isbeautyauthorized)                    | 現在のlic権限がどの美顔をサポートしているかを判断します。 BEAUTYおよびBODY_BEAUTYタイプの美顔項目のチェックのみサポートします。チェックの結果は各美顔オブジェクトのXmagicProperty.isAuthフィールドに割り当てられます。 |
| [setXmagicStreamType](#setxmagicstreamtype)                  | 入力データのタイプを設定します。デフォルトではAndroid cameraデータストリームです。               |
| [setXmagicLogLevel](#setxmagicloglevel)                      | SDKのlogレベルを設定します。 開発デバッグの際は`Log.DEBUG`に、正式リリースの際は`Log.WARN`にそれぞれ設定することをお勧めします。正式リリースの際に`Log.DEBUG`に設定していると、大量のログがパフォーマンスに影響する場合があります。<br><b>new XmagicApi()の後に呼び出します。</b> |

## 静的関数

| API               | 説明         |
| ----------------- | ---------- |
| [setLibPathAndLoad](#setlibpathandload) | libPathを設定します。 |

## Publicメンバー関数の説明

### XmagicApi

コンストラクタ。
```
XmagicApi(Context context, String resDir)
XmagicApi(Context context, String resDir,OnXmagicPropertyErrorListener xmagicPropertyErrorListener)
```

#### パラメータ
<table>
<thead>
<tr>
<th>パラメータ</th>
<th>意味</th>
</tr>
</thead>
<tbody><tr>
<td>Context context</td>
<td>コンテキスト。</td>
</tr>
<tr>
<td>String resDir</td>
<td>リソースファイルディレクトリ。<ul style="margin:0">
<li>SDKリソースファイルがassets内にある場合は、SDKの初回使用前にリソースをAppのプライベートディレクトリにcopyしておく必要があります。先に<code>XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath())</code>によってリソースパスを設定してから、<code>XmagicResParser.copyRes(getApplicationContext())</code>によってリソースのコピーを完了させます。詳細については、Demoの<code>LaunchActivity.java</code>をご参照ください。</li>
<li>SDKリソースファイルがネットワークからダウンロードしたものの場合は、ダウンロード成功後に、<code>XmagicResParser.setResPath(validAssetsDirectory)</code>によってリソースパスを設定します</li>
<li><code>XmagicResParser.getResPath()</code>によって、先に設定したパスを取得します。</li></ul></td>
</tr>
<tr>
<td>OnXmagicPropertyErrorListener xmagicPropertyErrorListener</td>
<td>コールバックインターフェースのエラー。</td>
</tr>
</tbody></table>
返されるエラーコードの意味対照表：

| エラーコード  | 意味                    |
| ---- | --------------------- |
| -1   | 不明なエラー。                 |
| -100 | 3Dエンジンリソースの初期化に失敗しました。          |
| -200 | GAN素材をサポートしていません。             |
| -300 | デバイスがこの素材コンポーネントをサポートしていません。           |
| -400 | テンプレートのJSONの内容が空です。           |
| -500 | SDKのバージョンが低すぎます。              |
| -600 | 分割をサポートしていません。                |
| -700 | OpenGLをサポートしていません。            |
| -800 | スクリプトをサポートしていません。                |
| 5000 | 分割背景画像の解像度が2160×3840を超えています。 |
| 5001 | 分割背景画像に必要なメモリが不足しています。         |
| 5002 | 分割背景ビデオの解析に失敗しました。           |
| 5003 | 分割背景ビデオが200秒を超えています。         |
| 5004 | 分割背景ビデオのフォーマットをサポートしていません。          |

------

### updateProperty

ある項目の美顔数値または動的エフェクト、フィルターの変更は、任意のスレッドで呼び出せます。

```
void updateProperty(XmagicProperty<?> p) 
```

#### パラメータ
<table>
<thead>
<tr>
<th>パラメータ</th>
<th>意味</th>
</tr>
</thead>
<tbody><tr>
<td>XmagicProperty&lt;?&gt; p</td>
<td>Tencent Effectのデータエンティティクラス。
<ul style="margin:0"><li>「美肌」を例にとると、次の方式でインスタンスを新しくすることができます。：<br><code>new XmagicProperty&lt;&gt;(Category.BEAUTY,  null,  null,  BeautyConstant.BEAUTY_SMOOTH, new XmagicPropertyValues(0, 100, 50, 0, 1)));</code>。</li><li>「2D動的エフェクト兔兔醤」を例にとると、次の方式でインスタンスを新しくすることができます。：<br><code>new XmagicProperty&lt;&gt;(Category.MOTION, "video_tutujiang" 、"動的エフェクトのファイルパス",  null, null);</code>。<br>その他の例については、Demoプロジェクトの<code>XmagicResParser.java</code>をご参照ください。</li></ul></td>
</tr>
</tbody></table>

***

### updateProperties

ある項目の美顔数値または動的エフェクト、フィルターの一括変更は、任意のスレッドで呼び出せます。

```
void updateProperties(List<XmagicProperty<?>> properties)
```

#### パラメータ

| パラメータ                                | 意味                         |
| ----------------------------------- | ---------------------------- |
| (List&lt;XmagicProperty&lt;?>> properties | 詳細についてはupdatePropertyメソッドの説明をご参照ください。 |

***

### setTipsListener

動的エフェクトプロンプトのコールバック関数を設定します。プロンプトをフロントエンドのページ上に表示するために用いられます。例えば素材の中には、ユーザーに、うなずく、手を伸ばす、指ハートなどを促すものがあります。

```
void setTipsListener(XmagicApi.XmagicTipsListener effectTipsListener) 
```

#### パラメータ

| パラメータ                                            | 意味                                 |
| ----------------------------------------------- | ------------------------------------ |
| XmagicApi.XmagicTipsListener effectTipsListener | コールバック関数実装クラスです。コールバックはメインスレッド内にあるとは限りません。 |

------

### setYTDataListener
顔の特徴点位置情報などのデータのコールバックを設定します。
```
void setYTDataListener(XmagicApi.XmagicYTDataListener ytDataListener)
顔の情報などのデータのコールバックを設定します

public interface XmagicYTDataListener {
    void onYTDataUpdate(String data)
}
```
onYTDataUpdateはJSON string構造を返します。最大で5つの顔の情報を返します。
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

#### フィールドの意味

| フィールド                           | タイプ    | 値の範囲                           | 説明                            |
| -------------------------- |-------------------------- | --------------------------- | --------------------------- |
| trace_id                     | int   | [1,INF)                      | 顔ID。連続ストリーム取得の過程で、IDが同一であれば同じ顔であると認識できます。 |
| face_256_point               | float | [0,screenWidth]または[0,screenHeight] | 計512個。顔の256個の重要特徴点であり、画面左上隅が(0,0)です。 |
| face_256_visible             | float | [0,1]                        | 顔の256個の重要特徴点の視認度。                  |
| out_of_screen                | bool  | true/false                   | 顔が枠外に出ていないか。                       |
| left_eye_high_vis_ratio      | float | [0,1]                        | 左目の特徴点のうち高視認度のものが占める割合。                   |
| right_eye_high_vis_ratio     | float | [0,1]                        | 右目の特徴点のうち高視認度のものが占める割合。                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | 左眉の特徴点のうち高視認度のものが占める割合。                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | 右眉の特徴点のうち高視認度のものが占める割合。                   |
| mouth_high_vis_ratio         | float | [0,1]                        | 口の特徴点のうち高視認度のものが占める割合。                    |

#### パラメータ

| パラメータ                                            | 意味       |
| --------------------------------------------- | -------- |
| XmagicApi.XmagicYTDataListener ytDataListener | コールバック関数実装クラス。 |

------

### setAIDataListener

顔、体、ジェスチャーを検出した際、これらの部位の特徴点位置情報をコールバックします

```
public interface OnAIDataListener {

    void onFaceDataUpdated(List<FaceData> faceDataList);
    void onHandDataUpdated(List<HandData> handDataList);
    void onBodyDataUpdated(List<BodyData> bodyDataList);

}
```

### onPause

レンダリングを一時停止します。ActivityのonPauseライフサイクルにバインドできます。現時点で内部では`onPauseAudio`のみ呼び出します。

```
void onPause() 
```

------

### onResume

レンダリングを再開します。ActivityのonResumeライフサイクルにバインドできます。

```
void onResume() 
```

------

### onDestroy

GLスレッドのリソースをクリアします。GLスレッド内で呼び出す必要があります。サンプルコードは次のとおりです。

```java
//サンプルコードはMainActivity.java参照
glSurfaceView.queueEvent(() -> {
                if (mXmagicApi != null) {
                    mXmagicApi.onPause();
                    mXmagicApi.onDestroy();
                }
            });
            
//サンプルコードはImageInputActivity.java参照
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

SDKレンダリングのデータを受信するメソッドです。カメラデータのコールバック関数内で使用できます。

```
//テクスチャのレンダリング
int process(int srcTextureId, int srcTextureWidth, int srcTextureHeight) 
//bitmapのレンダリング
Bitmap process(Bitmap bitmap, boolean needReset){
```

#### パラメータ

| パラメータ                   | 意味                                                         |
| ---------------------- | ------------------------------------------------------------ |
| int srcTextureId       | レンダリングする必要があるテクスチャ。                                           |
| id int srcTextureWidth | レンダリングする必要があるテクスチャの幅。                                         |
| int srcTextureHeight   | レンダリングする必要があるテクスチャの高さ。                                         |
| Bitmap bitmap          | 最大サイズは2160×4096までとすることをお勧めします。このサイズを超える画像は顔認識効果が低いか、または顔であると認識できない場合があり、またOOMの問題も起こりやすいため、大きな画像は縮小してから渡すことをお勧めします。 |
| boolean needReset      | <li/>画像の切り替え。<li/>分割の初回使用。<li/>動的エフェクトの初回使用。<li/>メイクアップの初回使用。<br>これらのシーンではneedResetをtrueに設定します。 |

------

### onPauseAudio

オーディオのみ停止する必要があり、GLスレッドをリリースする必要がない場合に、この関数を呼び出すことができます。

```
void onPauseAudio() 
```

------

### sensorChanged

現在のスマートフォンの回転の角度を判断し、それによってAIの顔認識の判断角度の根拠を調整するために用いられます。ジャイロスコープセンサーコールバック関数内で呼び出す必要があります。

```
void sensorChanged(SensorEvent event, Sensor accelerometer) 
```

#### パラメータ

| パラメータ                   | 意味                                   |
| -------------------- | ------------------------------------ |
| SensorEvent event    | ジャイロスコープセンサーのコールバック関数`onSensorChanged`が返したイベントエンティティクラス。 |
| Sensor accelerometer | ジャイロスコープセンサーの例。                            |

------

### isDeviceSupport

動的エフェクトリソースリストをSDKのチェック用に渡します。実行後、XmagicProperty.isSupportフィールドは、その素材が利用可能かどうかを表します。`XmagicProperty.isSupport`によってUIレイヤーのクリック制限を制御することや、直接リソースリストから削除することができます。

```
void isDeviceSupport(List<XmagicProperty<?>> assetsList)
```

#### パラメータ

| パラメータ                                 | 意味           |
| ---------------------------------- | ------------ |
| List&lt;XmagicProperty&lt;?>> assetsList | チェックする必要がある動的エフェクト素材リスト。 |

------

### getPropertyRequiredAbilities

動的エフェクトリソースリストを渡し、各リソースが使用できるSDKアトミック機能のリストを返します。
メソッドのユースケースは次のとおりです。
いくつかの動的エフェクト素材を購入または制作し、このメソッドを呼び出すと、各素材が使用する必要があるアトミック機能のリストが返されます。例えば、素材1は機能A、B、Cを使用する必要があり、素材2は機能B、C、Dを使用する必要があるなどです。これらの機能リストをサーバー上で保持します。その後、ユーザーがサーバーから動的エフェクト素材をダウンロードしたい場合、先にgetDeviceAbilitiesメソッドによって、スマートフォンが備えるアトミック機能のリスト（このスマートフォンは機能A、B、Cを備えているが、機能Dは備えていないなど）を取得し、その機能リストをサーバーに渡すことで、サーバーがそのデバイスに機能Dが備わっていないと判断し、ユーザーに素材2を送信しないということが可能になります。

#### パラメータ

| パラメータ                             | 意味               |
| ------------------------------ | ---------------- |
| List&lt;XmagicProperty&lt;?>> assets | アトミック機能をチェックする必要がある動的エフェクトリソースリスト。 |

#### 戻り値

戻り値 `Map<XmagicProperty<?>,ArrayList<String>>` ：

- key：動的エフェクトリソース素材のエンティティクラス。
- value：使用するアトミック機能のリスト。

------

### getDeviceAbilities

現在のデバイスがサポートするアトミック機能のテーブルを返します。getPropertyRequiredAbilitiesメソッドと合わせて使用します。詳細についてはgetPropertyRequiredAbilitiesの説明をご覧ください。

```
Map<String,Boolean> getDeviceAbilities() 
```

#### 戻り値

戻り値 `Map<String,Boolean>`：
- key：アトミック機能名（素材の機能名に対応）。
- value：現在のデバイスがサポートしているかどうか。

------

### isSupportBeauty

現在のモデルが美顔（OpenGL3.0）をサポートしているかどうかを判断します。

```
boolean isSupportBeauty() 
```

#### 戻り値

戻り値boolean：美顔をサポートしているかどうか。

------

### isBeautyAuthorized

現在のLicense権限がどの美顔または美ボディをサポートしているかを判断します。 BEAUTYおよびBODY_BEAUTYタイプの美顔項目のチェックのみサポートします。チェックの結果は各美顔オブジェクトの`XmagicProperty.isAuth`フィールドに割り当てられます。isAuthフィールドがfalseの場合は、UI上でこれらの項目へのエントリーをブロックすることができます。

```
void isBeautyAuthorized(List<XmagicProperty<?>> properties) 
```

#### パラメータ

| パラメータ                                 | 意味        |
| ---------------------------------- | --------- |
| List&lt;XmagicProperty&lt;?>> properties | チェックする必要がある美顔項目。 |

------

### setXmagicStreamType

入力データのタイプを設定します。デフォルトではAndroid cameraデータストリームです（XmagicApi.PROCESS_TYPE_CAMERA_STREAM）。

```
void setXmagicStreamType(int type)
```

#### パラメータ

| パラメータ       | 意味                                                                                                                                        |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| int type | データソースのタイプには次の2種類の選択肢があります。<ul style="margin:0"><li/><code>XmagicApi.PROCESS_TYPE_CAMERA_STREAM</code>：カメラデータソース。<li/><code>XmagicApi.PROCESS_TYPE_PICTURE_DATA</code>：画像データソース。</ul> |

------

## 静的関数の説明

### setLibPathAndLoad

soのパスを設定し、ロードをトリガーします。soがassets内にある場合は、このメソッドを呼び出す必要はありません。soが動的ダウンロードしたものの場合は、認証および`new XmagicApi`の前に呼び出す必要があります。 
- nullを渡す：デフォルトのパスからsoをロードすることを表します。 soがAPKパッケージ内にあることを確認してください。
- null以外を渡す：例えば、`data/data/パッケージ名/files/xmagic_libs`などです。このディレクトリからsoをロードすることを表します。

```
static boolean setLibPathAndLoad(String path) 
```

#### パラメータ

| パラメータ          | 意味      |
| ----------- | ------- |
| String path | soライブラリ保存パス。 |

