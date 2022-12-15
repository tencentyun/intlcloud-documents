Tencent Effect SDK Flutter版のコアインターフェースクラス`TencentEffectApi`は、美顔数値の更新、動的エフェクト呼び出しなどの機能に用いられます。

## Publicメンバー関数

| API                                                          | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [initXmagic](#initxmagic)                                    | 美顔データを初期化します。美顔の使用前に必ずこのメソッドを呼び出してください                    |
| [setLicense](#setlicense)                                    | 美顔権限の承認を行います                                                 |
| [setXmagicLogLevel](#setxmagicloglevel)                      | SDKのログレベルを設定します。 開発デバッグの際はLog.DEBUGに、正式リリースの際はLog.WARNにそれぞれ設定することをお勧めします。正式リリースの際にLog.DEBUGに設定していると、大量のログがパフォーマンスに影響する場合があります  |
| [onResume](#onresume)                                        | レンダリングを再開します。ページが表示されている場合に呼び出します                                     |
| [onPause](#onpause)                                          | レンダリングを一時停止します。ページが非表示の場合に呼び出します                                   |
| [updateProperty](#updateproperty)                            | 美顔属性を更新します。任意のスレッドで呼び出せます                    |
| [setOnCreateXmagicApiErrorListener](#setoncreatexmagicapierrorlistener) | 美顔オブジェクト作成時のコールバックインターフェースを設定します（エラー発生時にこのインターフェースを呼び出します）         |
| [setTipsListener](#settipslistener)                          | 動的エフェクトプロンプトのコールバック関数を設定します。プロンプトをフロントエンドのページ上に表示するために用いられます                    |
| [setYTDataListener](#setytdatalistener)                      | 顔の特徴点位置情報などのデータのコールバックを設定します（S1-05およびS1-06パッケージのみコールバックあり）  |
| [setAIDataListener](#setaidatalistener)                      | 顔、ジェスチャー、体の検出状態のコールバックを設定します                    |
| [isBeautyAuthorized](#isbeautyauthorized)                    | 現在のlic権限がどの美顔をサポートしているかを判断します。 BEAUTYおよびBODY_BEAUTYタイプの美顔項目のチェックのみサポートします。チェックの結果は各美顔オブジェクトのXmagicProperty.isAuthフィールドに割り当てられます  |
| [isSupportBeauty](#issupportbeauty)                          | 現在のモデルが美顔機能をサポートしているかどうかを判断します（OpenGL3.0）                    |
| [getDeviceAbilities](#getdeviceabilities)                    | 現在のデバイスでサポートされているアトミック機能のテーブルを返します                                 |
| [isDeviceSupport](#isdevicesupport)                          | 動的エフェクトリソースリストをSDKのチェック用に渡します。実行後、XmagicProperty.isSupportフィールドは、そのアトミック機能が利用可能かどうかを表します。XmagicProperty.isSupportによってUIレイヤーのクリック制限を制御することや、リソースリストから直接削除することができます  |
| [getPropertyRequiredAbilities](#getpropertyrequiredabilities) | 動的エフェクトリソースリストを渡し、各リソースが使用できるSDKアトミック機能のリストを返します  |

##  

## メンバー関数の説明

### initXmagic

初期化メソッドです。
```dart
void initXmagic(String xmagicResDir,InitXmagicCallBack callBack);

typedef InitXmagicCallBack = void Function(bool reslut);
```

#### パラメータ
| パラメータ                        | 意味               |
| --------------------------- | ------------------ |
| String xmagicResDir         | リソースファイルを配置したディレクトリ |
| InitXmagicCallBack callBack | コールバックインターフェースの初期化     |

------

### setLicense

認証データを設定し、美顔権限の承認を行います

```dart
  ///美顔認証処理の実行
void setLicense(String licenseKey, String licenseUrl, LicenseCheckListener checkListener);
///権限承認検証結果のコールバックメソッド
typedef LicenseCheckListener = void Function(int errorCode, String msg);
```

#### パラメータ

| パラメータ                               | 意味             |
| ---------------------------------- | :--------------- |
| String licenseKey                  | 認証LicenseKey |
| String licenseUrl                  | 認証LicenseUrl |
| LicenseCheckListener checkListener | 権限承認結果のコールバックインターフェース |

------

### setXmagicLogLevel

SDKのログレベルを設定します

```dart
void setXmagicLogLevel(int logLevel);
```

#### パラメータ

| パラメータ         | 意味                               |
| ------------ | :--------------------------------- |
| int logLevel | LogLevelを使用して定義可能なタイプを設定します |

------

### onResume

美顔処理を再開します

```dart
void onResume();
```

### onPause

美顔処理を一時停止します

```dart
void onPause();
```

------

### updateProperty

ある項目の美顔数値または動的エフェクト、フィルターを設定します。任意のスレッドで呼び出せます。

```dart
void updateProperty(XmagicProperty xmagicProperty);
```

#### パラメータ

| パラメータ                          | 意味             |
| ----------------------------- | :--------------- |
| XmagicProperty xmagicProperty | 美顔属性パッケージ化オブジェクト |

------

### setOnCreateXmagicApiErrorListener

美顔オブジェクト作成時のエラーコールバックインターフェースを設定します

```dart
  void setOnCreateXmagicApiErrorListener(OnCreateXmagicApiErrorListener? errorListener);
///美顔インスタンス作成時のエラーコールバックメソッド
typedef OnCreateXmagicApiErrorListener = void Function(String errorMsg, int code);
```

#### パラメータ

| パラメータ                                          | 意味                           |
| --------------------------------------------- | :----------------------------- |
| OnCreateXmagicApiErrorListener? errorListener | 美顔オブジェクト作成時のエラーメッセージコールバックインターフェース |

返されるエラーコードの意味対照表：

| エラーコード  | 意味                    |
| ---- | --------------------- |
| -1   | 不明なエラー                    |
| -100 | 3Dエンジンリソースの初期化に失敗しました                    |
| -200 | GAN素材をサポートしていません           |
| -300 | デバイスがこの素材コンポーネントをサポートしていません          |
| -400 | テンプレートのJSONの内容が空です           |
| -500 | SDKのバージョンが低すぎます              |
| -600 | 分割をサポートしていません                    |
| -700 | OpenGLをサポートしていません                    |
| -800 | スクリプトをサポートしていません                    |
| 5000 | 分割背景画像の解像度が2160×3840を超えています  |
| 5001 | 分割背景画像に必要なメモリが不足しています                    |
| 5002 | 分割背景ビデオの解析に失敗しました。           |
| 5003 | 分割背景ビデオが200秒を超えています                    |
| 5004 | 分割背景ビデオのフォーマットをサポートしていません                    |

------

### setTipsListener

動的エフェクトプロンプトのコールバック関数を設定します。プロンプトをフロントエンドのページ上に表示するために用いられます。例えば素材の中には、ユーザーに、うなずく、手を伸ばす、指ハートなどを促すものがあります。

```dart
void setTipsListener(XmagicTipsListener? xmagicTipsListener);

abstract class XmagicTipsListener {
  /// tipsを表示します。Show the tip.
  /// @param tips tips文字列。Tip's content
  /// @param tipsIcon tipsのicon。Tip's icon
  /// @param type tipsタイプ。0は文字列とiconの両方を表示することを表し、1はpag素材がiconのみを表示することを表します。tips category, 0 means that both strings and icons are displayed, 1 means that only the icon is displayed for the pag material
  /// @param duration tipsは時間（ミリ秒）を表示します。Tips display duration, milliseconds
  void tipsNeedShow(String tips, String tipsIcon, int type, int duration);

  /// *
  /// tipsを非表示にします。Hide the tip.
  /// @param tips tips文字列。Tip's content
  /// @param tipsIcon tipsのicon。Tip's icon
  /// @param type tipsタイプ。0は文字列とiconの両方を表示することを表し、1はpag素材がiconのみを表示することを表します。tips category, 0 means that both strings and icons are displayed, 1 means that only the icon is displayed for the pag material
  void tipsNeedHide(String tips, String tipsIcon, int type);
}
```

#### パラメータ

| パラメータ                                  | 意味             |
| ------------------------------------- | ---------------- |
| XmagicTipsListener xmagicTipsListener | コールバック関数実装クラス  |

------

### setYTDataListener

顔の特徴点位置情報などのデータのコールバックを設定します。
```dart
  ///顔の特徴点位置情報などのデータコールバックを設定します（S1-05およびS1-06パッケージのみコールバックあり）
void setYTDataListener(XmagicYTDataListener? xmagicYTDataListener);
顔の情報などのデータのコールバックを設定します

abstract class XmagicYTDataListener {
  //Youtu AIデータコールバック。
  void onYTDataUpdate(String data);
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
| trace_id                     | int   | [1,INF)                      | 顔ID。連続ストリーム取得の過程で、IDが同一であれば同じ顔であると認識できます  |
| face_256_point               | float | [0,screenWidth]または[0,screenHeight] | 計512個。顔の256個の重要特徴点であり、画面左上隅が(0,0)です  |
| face_256_visible             | float | [0,1]                        | 顔の256個の重要特徴点の視認度                    |
| out_of_screen                | bool  | true/false                   | 顔が枠外に出ていないか                    |
| left_eye_high_vis_ratio      | float | [0,1]                        | 左目の特徴点のうち高視認度のものが占める割合                    |
| right_eye_high_vis_ratio     | float | [0,1]                        | 右目の特徴点のうち高視認度のものが占める割合                    |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | 左眉の特徴点のうち高視認度のものが占める割合                    |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | 右眉の特徴点のうち高視認度のものが占める割合                    |
| mouth_high_vis_ratio         | float | [0,1]                        | 口の特徴点のうち高視認度のものが占める割合                    |

#### パラメータ

| パラメータ                                           | 意味             |
| ---------------------------------------------- | ---------------- |
| XmagicYTDataListener      xmagicYTDataListener | コールバック関数実装クラス  |

------

### setAIDataListener

顔、体、ジェスチャーを検出した際、これらの部位の特徴点位置情報をコールバックします

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

現在のLicense権限がどの美顔または美ボディをサポートしているかを判断します。 BEAUTYおよびBODY_BEAUTYタイプの美顔項目のチェックのみサポートします。チェックの結果は各美顔オブジェクトの`XmagicProperty.isAuth`フィールドに割り当てられます。isAuthフィールドがfalseの場合は、UI上でこれらの項目へのエントリーをブロックすることができます。

```
Future<List<XmagicProperty>> isBeautyAuthorized(
      List<XmagicProperty> properties);
```

#### パラメータ

| パラメータ                            | 意味               |
| ------------------------------- | ------------------ |
| List&lt;XmagicProperty> properties | チェックする必要がある美顔項目  |

------

### isSupportBeauty

現在のモデルが美顔（OpenGL3.0）をサポートしているかどうかを判断します。

```dart
  Future&lt;bool> isSupportBeauty();
```

#### 戻り値

戻り値bool：美顔をサポートしているかどうか。

------

### getDeviceAbilities

現在のデバイスがサポートするアトミック機能のテーブルを返します。getPropertyRequiredAbilitiesメソッドと合わせて使用します。

```
  Future<Map<String, bool>> getDeviceAbilities();
```

#### 戻り値

戻り値`Map&lt;String,bool>`：

- key：アトミック機能名（素材の機能名に対応）。
- value：現在のデバイスがサポートしているかどうか。

------

### getPropertyRequiredAbilities

動的エフェクトリソースリストを渡し、各リソースが使用できるSDKアトミック機能のリストを返します。
メソッドのユースケースは次のとおりです。
いくつかの動的エフェクト素材を購入または制作し、このメソッドを呼び出すと、各素材が使用する必要があるアトミック機能のリストが返されます。例えば、素材1は機能A、B、Cを使用する必要があり、素材2は機能B、C、Dを使用する必要があるなどです。これらの機能リストをサーバー上で保持します。その後、ユーザーがサーバーから動的エフェクト素材をダウンロードしたい場合、先にgetDeviceAbilitiesメソッドによって、スマートフォンが備えるアトミック機能のリスト（このスマートフォンは機能A、B、Cを備えているが、機能Dは備えていないなど）を取得し、その機能リストをサーバーに渡すことで、サーバーがそのデバイスに機能Dが備わっていないと判断し、ユーザーに素材2を送信しないということが可能になります。

```dart
Future<Map<XmagicProperty, List<String>?>> getPropertyRequiredAbilities(
    List<XmagicProperty> assetsList);
```

#### パラメータ

| パラメータ                             | 意味               |
| ------------------------------ | ---------------- |
| List&lt;XmagicProperty> assetsList | アトミック機能をチェックする必要がある動的エフェクトリソースリスト  |

#### 戻り値

戻り値Map&lt;XmagicProperty, List&lt;String>?> ：

- key：動的エフェクトリソース素材のエンティティクラス。
- value：使用するアトミック機能のリスト。

------

###  isDeviceSupport

動的エフェクトリソースリストをSDKのチェック用に渡します。実行後、XmagicProperty.isSupportフィールドは、その素材が利用可能かどうかを表します。`XmagicProperty.isSupport`によってUIレイヤーのクリック制限を制御することや、直接リソースリストから削除することができます。

```dart
 Future&lt;List<XmagicProperty>> isDeviceSupport(List<XmagicProperty> assetsList);
```

#### パラメータ

| パラメータ                            | 意味                     |
| ------------------------------- | ------------------------ |
| List&lt;XmagicProperty> assetsList | チェックする必要がある動的エフェクト素材リスト  |