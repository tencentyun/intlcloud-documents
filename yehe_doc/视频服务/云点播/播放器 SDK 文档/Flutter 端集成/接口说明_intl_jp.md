## SuperPlayerPluginクラス

### setGlobalLicense

**説明**

Licenseを設定します

Licenseを申請後、以下のインターフェースでLicenseを初期化します。起動時に行うことをお勧めします。Licenseを設定していないとビデオの再生に失敗します。

**インターフェース**

```dart
static Future<void> setGlobalLicense(String licenceUrl, String licenceKey) async;
```

**パラメータの説明**

| パラメータ名     | タイプ   | 説明          |
| ---------- | ------ | -------------- |
| licenceUrl | String | licenceのurl |
| licenceKey | String | licenceの key |

**戻り値**

なし


### createVodPlayer

**説明**

ネイティブ層のVODプレーヤーインスタンスを作成します。`TXVodPlayerController`を使用している場合はすでに統合されているため、追加で作成する必要はありません。

**インターフェース**

```dart
static Future<int?> createVodPlayer() async;
```

**パラメータの説明**

なし

**戻り値**

| 戻り値 | タイプ   | 説明               |
| ------ | ------ | ------------------ |
| playerId | int | プレーヤーID |


### createLivePlayer

**説明**

ネイティブ層のVODプレーヤーインスタンスを作成します。`TXVodPlayerController`を使用している場合はすでに統合されているため、追加で作成する必要はありません

**インターフェース**

```dart
static Future<int?> createLivePlayer() async;
```

**パラメータの説明**

なし

**戻り値**

| 戻り値 | タイプ   | 説明               |
| ------ | ------ | ------------------ |
| playerId | int | プレーヤーID |


### setConsoleEnabled

**説明**

プレーヤーネイティブログ出力を有効または無効にします

**インターフェース**

```dart
static Future<int?> setConsoleEnabled() async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| enabled | bool | プレーヤーログの有効化または無効化 |

**戻り値**

なし


### releasePlayer

**説明**

対応するプレーヤーのリソースを解放します。

**インターフェース**

```dart
static Future<int?> releasePlayer(int? playerId) async;
```

**パラメータの説明**

なし

**戻り値**

なし


### setGlobalMaxCacheSize

**説明**

再生エンジンの最大キャッシュのサイズを設定します。設定後は設定値に応じて自動的にCacheディレクトリのファイルをクリーンアップします

**インターフェース**

```dart
static Future<void> setGlobalMaxCacheSize(int size) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| size | int | 最大キャッシュサイズ（単位：MB） |

**戻り値**

なし


### setGlobalCacheFolderPath

**説明**

このキャッシュパスはデフォルトではAppサンドボックスのディレクトリ下に設定されます。パラメータは対応するキャッシュディレクトリのものを渡すだけでよく、絶対パス全体を渡す必要はありません。

**インターフェース**

```dart
static Future<bool> setGlobalCacheFolderPath(String postfixPath) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| postfixPath | String | キャッシュディレクトリ。このキャッシュパスはデフォルトではappサンドボックスのディレクトリ下に設定されます。postfixPathは対応するキャッシュディレクトリのものを渡すだけでよく、絶対パス全体を渡す必要はありません。Androidプラットフォーム：ビデオはsdcardのAndroid/data/your-pkg-name/files/testCacheディレクトリにキャッシュされます。iOSプラットフォームではビデオはサンドボックスのDocuments/testCacheディレクトリにキャッシュされます。 |

**戻り値**

なし


### setLogLevel

**説明**

ログ出力レベルを設定します

**インターフェース**

```dart
static Future<void> setLogLevel(int logLevel) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| logLevel | int | 0:全レベルのログを出力 </br> 1:DEBUG、INFO、WARNING、ERRORおよびFATALレベルのログを出力 </br> 2:INFO、WARNNING、ERRORおよびFATALレベルのログを出力 </br> 3:WARNNING、ERRORおよびFATALレベルのログを出力 </br> 4:ERRORおよびFATALレベルのログを出力 </br> 5:FATALレベルのログのみを出力 </br> 6:sdkログを何も出力しない|

**戻り値**

なし


### setBrightness

**説明**

明るさを設定します。現在のappのみに適用します

**インターフェース**

```dart
static Future<void> setBrightness(double brightness) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| brightness | double | 明るさの値の範囲 0.0～1.0 |

**戻り値**

なし


### restorePageBrightness

**説明**

画面の明るさを元に戻します。現在のappのみに適用します

**インターフェース**

```dart
static Future<void> restorePageBrightness() async;
```

**パラメータの説明**

なし

**戻り値**

なし


### getBrightness

**説明**

現在の画面の明るさの値を取得します

**インターフェース**

```dart
static Future<double> getBrightness() async;
```

**パラメータの説明**

なし

**戻り値**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| brightness | double | 明るさの値の範囲 0.0～1.0 |


### setSystemVolume

**説明**

現在のシステム音量を設定します

**インターフェース**

```dart
static Future<void> setSystemVolume(double volume) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| volume | double | 音量の値の範囲 0.0～1.0 |

**戻り値**

なし


### getSystemVolume

**説明**

現在のシステム音量を設定します

**インターフェース**

```dart
static Future<double> getSystemVolume() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| volume | double | 音量の値の範囲 0.0～1.0 |


### abandonAudioFocus

**説明**

オーディオフォーカスを解放します。Androidにのみ適用します

**インターフェース**

```dart
static Future<double> abandonAudioFocus() async;
```

**パラメータの説明**

なし

**戻り値**

なし


### requestAudioFocus

**説明**

オーディオフォーカスの取得をリクエストします。Androidにのみ適用します

**インターフェース**

```dart
static Future<void> requestAudioFocus() async ;
```

**パラメータの説明**

なし

**戻り値**

なし


### isDeviceSupportPip

**説明**

現在のデバイスがピクチャーインピクチャーをサポートしているかどうかを判断します

**インターフェース**

```dart
static Future<int> isDeviceSupportPip() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| isDeviceSupportPip | int | 0 ピクチャーインピクチャーモードの有効化が可能です</br> -101  androidのバージョンが低すぎます </br>  -102  ピクチャーインピクチャーの権限が無効です/デバイスがピクチャーインピクチャーをサポートしていません </br> -103  現在の画面がすでに破棄されています|


### getLiteAVSDKVersion

**説明**

現在のネイティブ層Player SDKのバージョン番号を取得します

**インターフェース**

```dart
static Future<String?> getLiteAVSDKVersion() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| sdkVersion | String | 現在のPlayer SDKバージョン |


### setGlobalEnv

**説明**

liteav SDKへのアクセス環境を設定します。
Tencent Cloudが世界各地にデプロイした環境は、各地域の制作や法令の要件に従い、異なるリージョンアクセスポイントにアクセスする必要があります。

**注意**

ターゲット市場が中国大陸のお客様はこのインターフェースを呼び出さないでください。ターゲット市場が海外ユーザーの場合は、env_configの設定メソッドを把握し、Appが確実にGDPR基準を遵守できるようにする必要がありますので、テクニカルサポートを通じてご連絡ください。

**インターフェース**

```dart
static Future<int> setGlobalEnv(String envConfig) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| envConfig | String | アクセスしたい環境。SDKがデフォルトでアクセスする環境はデフォルト正式環境です |

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | int | 1 設定成功、 2 設定失敗 |



## TXVodPlayerControllerクラス


### initialize

**説明**

controllerを初期化し、共有テクスチャの割り当てをリクエストします

**インターフェース**

```dart
Future<void> initialize({bool? onlyAudio}) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| onlyAudio | bool | オプションです。オーディオのみのプレーヤーかどうか |

**戻り値の説明**

なし


### startVodPlay

**注意**

バージョン10.7より、startPlayはstartVodPlayに変更され、正常に再生を行うには{@link SuperPlayerPlugin#setGlobalLicense}でのLicenceの設定が必要になりました。これを行わなければ再生が失敗します（ブラックスクリーン）。設定はグローバルで1回行うだけです。ライブストリーミングLicence、UGSV Licenceおよびビデオ再生Licenceがすべて使用できます。上記のLicenceをまだ取得していない場合は、[テスト版Licenceの無料申請](https://www.tencentcloud.com/document/product/266/51098)をスピーディーに行うことで正常に再生できますが、正式版Licenseは[購入](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license)する必要があります。

**説明**

ビデオ再生urlを使用して再生します。

**インターフェース**

```dart
Future<bool> startVodPlay(String url) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| url | String | 再生したいビデオurl |

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | bool | 作成に成功したかどうか |


### startVodPlayWithParams

**注意**

バージョン10.7より、startPlayはstartVodPlayに変更され、正常に再生を行うには{@link SuperPlayerPlugin#setGlobalLicense}でのLicenceの設定が必要になりました。これを行わなければ再生が失敗します（ブラックスクリーン）。設定はグローバルで1回行うだけです。ライブストリーミングLicence、UGSV Licenceおよびビデオ再生Licenceがすべて使用できます。上記のLicenceをまだ取得していない場合は、[テスト版Licenceを無料でクイック申請](https://www.tencentcloud.com/document/product/266/51098)すれば正常に再生できますが、正式版Licenseは[購入](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license)する必要があります。

**説明**

ビデオfieldを使用して再生します。

**インターフェース**

```dart
Future<void> startVodPlayWithParams(TXPlayInfoParams params) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| appId | int | アプリケーションappId。入力必須 |
| fileId | String | ファイルid。入力必須 |
| timeout | String | 暗号化リンクのタイムアウトタイムスタンプ。16進数の小文字文字列に変換し、Tencent Cloud CDNサーバーがこの時刻に基づいてこのリンクが有効かどうかを判断します |
| exper | String | プレビュー時間。単位：秒 |
| us | String | 固有識別子のリクエスト。リンクに一意性を持たせます |
| sign | String | リンク不正アクセス防止署名。[リンク不正アクセス防止製品ドキュメント](https://www.tencentcloud.com/document/product/266/33984)をご参照ください |
| https | String | httpsリクエストを使用するかどうか。デフォルトではfalseです |

**戻り値の説明**

なし


### pause

**説明**

現在再生中のビデオを一時停止します

**インターフェース**

```dart
Future<void> pause() async;
```

**パラメータの説明**

なし

**戻り値の説明**

なし


### resume

**説明**

現在一時停止状態のビデオの再生を再開します

**インターフェース**

```dart
Future<void> resume() async;
```

**パラメータの説明**

なし

**戻り値の説明**

なし


### stop

**説明**

現在再生中のビデオを停止します

**インターフェース**

```dart
Future<bool> stop({bool isNeedClear = false}) async;
```
**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| isNeedClear | bool | 最後のフレームをクリアするかどうか |

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | bool | 停止に成功したかどうか |


### setIsAutoPlay

**説明**

この後再生するビデオについて、startVodPlayでビデオアドレスをロードした後、直接自動再生するかどうかを設定します

**インターフェース**

```dart
Future<void> setIsAutoPlay({bool? isAutoPlay}) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| isAutoPlay | bool | 自動的に再生するかどうか |

**戻り値の説明**

なし


### isPlaying

**説明**

現在のプレーヤーが再生中かどうかです

**インターフェース**

```dart
Future<bool> isPlaying() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| isAutoPlay | bool | 再生中かどうか |


### setMute

**説明**

現在の再生をミュートするかどうかを設定します

**インターフェース**

```dart
Future<void> setMute(bool mute) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| mute | bool | ミュートするかどうか |

**戻り値の説明**

なし


### setLoop

**説明**

ビデオ再生の完了後にループ再生を行うかどうか

**インターフェース**

```dart
Future<void> setLoop(bool loop) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| loop | bool | ループ再生を行うかどうか |

**戻り値の説明**

なし


### seek

**説明**

進捗を指定の位置に調整します

**インターフェース**

```dart
_controller.seek(progress);
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| progress | double | 調整したい再生時間。単位は秒です 。|

**戻り値の説明**

なし


### setRate

**説明**

ビデオ再生の速度を設定します

**インターフェース**

```dart
Future<void> setRate(double rate) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| rate | double | ビデオの再生速度。デフォルトでは1.0 |

**戻り値の説明**

なし


### getSupportedBitrates

**説明**

現在再生中のビデオがサポートするビットレートを取得します

**インターフェース**

```dart
Future<List?> getSupportedBitrates() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| 戻り値 | タイプ   | 説明               |
| ------ | ------ | ------------------ |
| index | int | ビットレート番号 |
| width | int | ビットレートに対応するビデオ幅 |
| height | int | ビットレートに対応するビデオの高さ |
| bitrate | int | ビットレート値 |

### getBitrateIndex

**説明**

設定したビットレート番号を取得します

**インターフェース**

```dart
Future<int> getBitrateIndex() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| 戻り値 | タイプ   | 説明               |
| ------ | ------ | ------------------ |
| index | int | ビットレート番号 |


### setBitrateIndex

**説明**

ビットレート番号によって現在のビットレートを設定します

**インターフェース**

```dart
Future<void> setBitrateIndex(int index) async;
```

**パラメータの説明**

| 戻り値 | タイプ   | 説明               |
| ------ | ------ | ------------------ |
| index | int | ビットレート番号。 -1を渡した場合、アダプティブビットレートストリーミングをオンにすることを表します。 |

**戻り値の説明**

なし


### setStartTime

**説明**

再生開始時間を指定します

**インターフェース**

```dart
Future<void> setStartTime(double startTime) async;
```

**パラメータの説明**

| 戻り値 | タイプ   | 説明               |
| ------ | ------ | ------------------ |
| startTime | double | 再生開始時間。単位：秒 |

**戻り値の説明**

なし


### setAudioPlayoutVolume

**説明**

ビデオの音量の大きさを設定します

**インターフェース**

```dart
Future<void> setAudioPlayoutVolume(int volume) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| volume | int | ビデオの音量の大きさ。範囲は0～100 |

**戻り値の説明**

なし


### setRequestAudioFocus

**説明**

オーディオフォーカスの取得をリクエストします。Androidに適用します

**インターフェース**

```dart
Future<bool> setRequestAudioFocus(bool focus) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| focus | bool | フォーカスを設定するかどうか |

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | bool | フォーカスの設定に成功したかどうか |


### setConfig

**説明**

プレーヤーの設定を行います

**インターフェース**

```dart
Future<void> setConfig(FTXVodPlayConfig config) async ;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| config | FTXVodPlayConfig | `FTXVodPlayConfigクラス`をご参照ください |


**戻り値の説明**

なし


### getCurrentPlaybackTime

**説明**

現在の再生時間を取得します。単位：秒

**インターフェース**

```dart
Future<double> getCurrentPlaybackTime() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| playbackTime | double | 現在の再生時間。単位：秒 |


### getBufferDuration

**説明**

現在のビデオのキャッシュ済みの時間を取得します。単位：秒

**インターフェース**

```dart
 Future<double> getBufferDuration();
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| playbackTime | double | 現在のビデオのキャッシュ済みの時間。単位：秒 |


### getPlayableDuration

**説明**

現在再生中のビデオの再生可能時間を取得します。単位：秒

**インターフェース**

```dart
 Future<double> getPlayableDuration() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| playableDuration | double | 現在のビデオの再生可能時間。単位：秒 |


### getWidth

**説明**

現在再生中のビデオの幅を取得します

**インターフェース**

```dart
Future<int> getWidth() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| width | int | 現在のビデオ幅 |


### getHeight

**説明**

現在再生中のビデオの高さを取得します

**インターフェース**

```dart
Future<int> getHeight() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| height | int | 現在のビデオの高さ |


### setToken

**説明**

暗号化HLSのtokenです。この値を設定すると、プレーヤーはURL内のファイル名の前にvoddrm.tokenを自動的に追加します

**インターフェース**

```dart
Future<void> setToken(String? token) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| token | String | 再生ビデオのtoken |

**戻り値の説明**

なし


### isLoop

**説明**

現在のプレーヤーがループ再生状態かどうかを取得します

**インターフェース**

```dart
Future<bool> isLoop() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| isLoop | bool | プレーヤーがループ再生状態かどうか |


### enableHardwareDecode

**説明**

ハードウェアデコード再生の有効化/無効化。設定後すぐではなく、再度再生を行った際に効力を発します

**インターフェース**

```dart
Future<bool> enableHardwareDecode(bool enable);
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| enable | bool | ハードウェアデコード有効化の有無 |

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | bool | ハードウェアデコード/ソフトウェアデコード設定結果 |


### dispose

**説明**

controllerを破棄します。このメソッドを呼び出すと、すべての通知イベントを破棄し、プレーヤーを解放します

**インターフェース**

```dart
void dispose() async;
```

**パラメータの説明**

なし

**戻り値の説明**

なし


### getDuration

**説明**

ビデオの合計時間を取得します

**インターフェース**

```dart
Future<double> getDuration() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| duration | double | ビデオの合計時間。単位：秒 |


### enterPictureInPictureMode

**説明**

ピクチャーインピクチャーモードに進みます

**インターフェース**

```dart
Future<int> enterPictureInPictureMode({String? backIconForAndroid, String? playIconForAndroid, String? pauseIconForAndroid, String? forwardIconForAndroid}) async;
```

**パラメータの説明**

このパラメータはandroidプラットフォームにのみ適用します

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| backIcon | String | 戻るボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |
| playIcon | String | 再生ボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |
| pauseIcon | String | 一時停止ボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |
| forwardIcon | String | 早送りボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |

**戻り値の説明**

| パラメータ名 | 値   | 説明               |
| ------ | ------ | ------------------ |
| NO_ERROR | 0 | 起動に成功しました。エラーはありません |
| ERROR_PIP_LOWER_VERSION | -101 | androidのバージョンが低すぎ、ピクチャーインピクチャーモードをサポートしていません |
| ERROR_PIP_DENIED_PERMISSION | -102 | ピクチャーインピクチャーモードの権限が有効になっていないか、または現在のデバイスがピクチャーインピクチャーをサポートしていません |
| ERROR_PIP_ACTIVITY_DESTROYED | -103 | 現在の画面がすでに破棄されています |
| ERROR_IOS_PIP_DEVICE_NOT_SUPPORT | -104 | デバイスまたはシステムバージョンがサポートされていません（PIPはiPad iOS9以降でサポート）。iOSにのみ適用します|
| ERROR_IOS_PIP_PLAYER_NOT_SUPPORT | -105 | プレーヤーをサポートしていません。iOSにのみ適用します|
| ERROR_IOS_PIP_VIDEO_NOT_SUPPORT | -106 | ビデオをサポートしていません。iOSにのみ適用します|
| ERROR_IOS_PIP_IS_NOT_POSSIBLE | -107 | PIPコントローラは利用できません。iOSにのみ適用します|
| ERROR_IOS_PIP_FROM_SYSTEM | -108 | PIPコントローラエラー。iOSにのみ適用します|
| ERROR_IOS_PIP_PLAYER_NOT_EXIST | -109 | プレーヤーオブジェクトが存在しません。iOSにのみ適用します|
| ERROR_IOS_PIP_IS_RUNNING | -110 | PIP機能はすでに実行されています。iOSにのみ適用します|
| ERROR_IOS_PIP_NOT_RUNNING | -111 | PIP機能は起動していません。iOSにのみ適用します|



## FTXVodPlayConfigクラス

#### 属性設定についての説明


| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| connectRetryCount | int | プレーヤーの再接続回数。SDKとサーバーの接続が異常によって切断された場合、SDKはサーバーとの再接続を試行します。この値によってSDKの再接続回数を設定します |
| connectRetryInterval | int | プレーヤーの再接続間隔。SDKとサーバーの接続が異常によって切断された場合、SDKはサーバーとの再接続を試行します。この値によって2回の再接続間隔時間を設定します |
| timeout | int | プレーヤーの接続タイムアウト時間 |
| playerType | int | プレーヤータイプ。0 VOD、1 ライブストリーミング、2 ライブストリーミングプレイバック |
| headers | Map | カスタムhttp headers |
| enableAccurateSeek | bool | 正確にseekするかどうか。デフォルトではtrueです |
| autoRotate | bool | mp4ファイルを再生する際、trueに設定すると、ファイル内の回転角度に応じて自動的に回転します。回転角度はPLAY_EVT_CHANGE_ROTATIONイベントから取得できます。デフォルトではtrueです |
| smoothSwitchBitrate | bool | マルチビットレートHLSのスムーズな切り替え。デフォルトではfalseです。falseに設定すると、マルチビットレートアドレスを開く速度が速くなります。trueに設定すると、IDRが合っている場合にビットレートをスムーズに切り替えることができます |
| cacheMp4ExtName | String | mp4キャッシュファイルの拡張子。デフォルトではmp4です |
| progressInterval | int | プログレスコールバック間隔を設定します。設定しない場合、SDKはデフォルトで0.5秒ごとに1回コールバックを行います。単位はミリ秒 |
| maxBufferSize | int | 最大再生バッファサイズ（単位：MB） 。この設定はplayableDurationに影響します。設定値が大きいほど事前キャッシュが多くなります|
| maxPreloadSize | int | プリロードの最大バッファサイズ（単位：MB） |
| firstStartPlayBufferTime | int | 最初のバッファリングでロードする必要があるデータ時間（単位：ms）。デフォルト値は100ms|
| nextStartPlayBufferTime | int | バッファ時（バッファデータが不十分であることによる二次バッファ、またはseekによるドラッグバッファ）に少なくともどのくらいのデータをキャッシュするとバッファを終了できるかです。単位はmsで、デフォルト値では250msです |
| overlayKey | String | HLSセキュリティ強化暗号化/復号key|
| overlayIv | String | HLSセキュリティ強化暗号化/復号Iv|
| extInfoMap | Map | 周知する必要がないいくつかの特別な設定|
| enableRenderProcess | bool | ロード後にレンダリングの後処理サービスを許可するかどうかです。デフォルトでは有効です。有効化後に解像度プラグインが存在した場合は、デフォルトでロードします|
| preferredResolution | int | 優先的に再生する解像度。preferredResolution = width * height|


## TXLivePlayerControllerクラス


### initialize

**説明**

controllerを初期化し、共有テクスチャの割り当てをリクエストします

**インターフェース**

```dart
Future<void> initialize({bool? onlyAudio}) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| onlyAudio | bool | オプションです。オーディオのみのプレーヤーかどうか |

**戻り値の説明**

なし


### startLivePlay

**注意**

バージョン10.7より、startPlayはstartLivePlayに変更され、正常に再生を行うには{@link SuperPlayerPlugin#setGlobalLicense}でのLicenceの設定が必要になりました。これを行わなければ再生が失敗します（ブラックスクリーン）。設定はグローバルで1回行うだけです。ライブストリーミングLicence、UGSV Licenceおよびビデオ再生Licenceがすべて使用できます。上記のLicenceをまだ取得していない場合は、[テスト版Licenceを無料でクイック申請](https://www.tencentcloud.com/document/product/266/51098)すれば正常に再生できますが、正式版Licenseは[購入](https://www.tencentcloud.com/document/product/266/510988#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license)する必要があります。

**説明**

ビデオ再生urlを使用して再生します。

**インターフェース**

```dart
Future<bool> play(String url, {int? playType}) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| url | String | 再生したいビデオurl |
| playType | int | オプションです。サポートする再生タイプ。デフォルトではRTMPライブストリーミングで、LIVE_RTMP、LIVE_FLV、LIVE_RTMP_ACC、VOD_HLSをサポートしています。詳細についてはTXPlayTypeをご参照ください |

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | bool | 作成に成功したかどうか |


### pause

**説明**

現在再生中のビデオを一時停止します

**インターフェース**

```dart
Future<void> pause() async;
```

**パラメータの説明**

なし

**戻り値の説明**

なし


### resume

**説明**

現在一時停止状態のビデオの再生を再開します


**インターフェース**

```dart
Future<void> resume() async;
```

**パラメータの説明**

なし

**戻り値の説明**

なし


### stop

**説明**

現在再生中のビデオを停止します

**インターフェース**

```dart
Future<bool> stop({bool isNeedClear = false}) async;
```
**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| isNeedClear | bool | 最後のフレームをクリアするかどうか |

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | bool | 停止に成功したかどうか |


### setIsAutoPlay

**説明**

この後再生するビデオについて、startVodPlayでビデオアドレスをロードした後、直接自動再生するかどうかを設定します

**インターフェース**

```dart
Future<void> setIsAutoPlay({bool? isAutoPlay}) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| isAutoPlay | bool | 自動的に再生するかどうか |

**戻り値の説明**

なし


### isPlaying

**説明**

現在のプレーヤーが再生中かどうかです

**インターフェース**

```dart
Future<bool> isPlaying() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| isAutoPlay | bool | 再生中かどうか |


### setMute

**説明**

現在の再生をミュートするかどうかを設定します

**インターフェース**

```dart
Future<void> setMute(bool mute) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| mute | bool | ミュートするかどうか |

**戻り値の説明**

なし


### setVolume

**説明**

ビデオの音量の大きさを設定します

**インターフェース**

```dart
 Future<void> setVolume(int volume);
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| volume | int | ビデオの音量の大きさ。範囲は0～100 |

**戻り値の説明**

なし


### setLiveMode

**説明**

ライブストリーミングモードを設定します

**インターフェース**

```dart
Future<void> setLiveMode(TXPlayerLiveMode mode) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| mode | int | ライブストリーミングモード、自動モード、超高速モード、スムーズモード |

**戻り値の説明**

なし


### setAppID

**説明**

appIDを設定します。クラウドで使用します

**インターフェース**

```dart
Future<void> setAppID(int appId) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| appId | int | appId |

**戻り値の説明**

なし


### resumeLive

**説明**

タイムシフト再生を停止し、ライブストリーミングに戻ります

**インターフェース**

```dart
Future<int> resumeLive() async;
```

**パラメータの説明**

なし

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | int | 1 成功、 0 失敗 |


### setConfig

**説明**

プレーヤーの設定を行います

**インターフェース**

```dart
Future<void> setConfig(FTXLivePlayConfig config) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| config | FTXLivePlayConfig | `FTXLivePlayConfigクラス`をご参照ください |

**戻り値の説明**

なし


### enableHardwareDecode

**説明**

ハードウェアデコード再生の有効化/無効化。設定後すぐではなく、再度再生を行った際に効力を発します

**インターフェース**

```dart
Future<bool> enableHardwareDecode(bool enable);
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| enable | bool | ハードウェアデコード有効化の有無 |

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | bool | ハードウェアデコード/ソフトウェアデコード設定結果 |


### enterPictureInPictureMode

**説明**

ピクチャーインピクチャーモードに進みます。Android端末のみでサポートしています。iOS端末のライブストリーミングでは現在ピクチャーインピクチャーモードをサポートしていません

**インターフェース**

```dart
Future<int> enterPictureInPictureMode({String? backIconForAndroid, String? playIconForAndroid, String? pauseIconForAndroid, String? forwardIconForAndroid}) async;
```

**パラメータの説明**

このパラメータはandroidプラットフォームにのみ適用します

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| backIcon | String | 戻るボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |
| playIcon | String | 再生ボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |
| pauseIcon | String | 一時停止ボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |
| forwardIcon | String | 早送りボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |

**戻り値の説明**

| パラメータ名 | 値   | 説明               |
| ------ | ------ | ------------------ |
| NO_ERROR | 0 | 起動に成功しました。エラーはありません |
| ERROR_PIP_LOWER_VERSION | -101 | androidのバージョンが低すぎ、ピクチャーインピクチャーモードをサポートしていません |
| ERROR_PIP_DENIED_PERMISSION | -102 | ピクチャーインピクチャーモードの権限が有効になっていないか、または現在のデバイスがピクチャーインピクチャーをサポートしていません |
| ERROR_PIP_ACTIVITY_DESTROYED | -103 | 現在の画面がすでに破棄されています |
| ERROR_IOS_PIP_DEVICE_NOT_SUPPORT | -104 | デバイスまたはシステムバージョンがサポートされていません（PIPはiPad iOS9以降でサポート）。iOSにのみ適用します|
| ERROR_IOS_PIP_PLAYER_NOT_SUPPORT | -105 | プレーヤーをサポートしていません。iOSにのみ適用します|
| ERROR_IOS_PIP_VIDEO_NOT_SUPPORT | -106 | ビデオをサポートしていません。iOSにのみ適用します|
| ERROR_IOS_PIP_IS_NOT_POSSIBLE | -107 | PIPコントローラは利用できません。iOSにのみ適用します|
| ERROR_IOS_PIP_FROM_SYSTEM | -108 | PIPコントローラエラー。iOSにのみ適用します|
| ERROR_IOS_PIP_PLAYER_NOT_EXIST | -109 | プレーヤーオブジェクトが存在しません。iOSにのみ適用します|
| ERROR_IOS_PIP_IS_RUNNING | -110 | PIP機能はすでに実行されています。iOSにのみ適用します|
| ERROR_IOS_PIP_NOT_RUNNING | -111 | PIP機能は起動していません。iOSにのみ適用します|


### dispose

**説明**

controllerを破棄します。このメソッドを呼び出すと、すべての通知イベントを破棄し、プレーヤーを解放します

**インターフェース**

```dart
void dispose() async;
```

**パラメータの説明**

なし

**戻り値の説明**

なし



### switchStream

**説明**

再生ストリームを切り替えます

**インターフェース**

```dart
Future<int> switchStream(String url) async;
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| url | String | 切り替えたいビデオソース|

**戻り値の説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| result | int | 切り替えの結果 |


## FTXLivePlayConfigクラス

#### 属性設定についての説明

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| cacheTime | double | プレーヤーのキャッシュ時間。単位：秒。値は0より大きい必要があります。デフォルト値は5 |
| maxAutoAdjustCacheTime | double | プレーヤーのキャッシュ自動調整の最大時間で、単位は秒です。値は0より大きい必要があります。デフォルト値は5 |
| minAutoAdjustCacheTime | double | プレーヤーのキャッシュ自動調整の最小時間で、単位は秒です。値は0より大きい必要があります。デフォルト値は1 |
| videoBlockThreshold | int | プレーヤービデオラグのアラート閾値で、単位はミリ秒。レンダリング間隔がこの閾値を超えるラグがある場合のみPLAY_WARNING_VIDEO_PLAY_LAGを通知します |
| connectRetryCount | int | プレーヤーにネットワーク接続切断が発生した場合のSDKのデフォルトでのリトライ回数。値の範囲は1～10、デフォルト値：3。 |
| connectRetryInterval | int | ネットワーク再接続の時間間隔。単位：秒。値の範囲は3～30、デフォルト値は3です。 |
| autoAdjustCacheTime | bool | プレーヤーのキャッシュ時間を自動調整するかどうか。デフォルト値：true。true：自動調整を有効にします。自動調整の最大値と最小値はそれぞれmaxCacheTimeとminCacheTimeを変更することで設定できます。false：自動調整を無効にし、デフォルトの指定キャッシュ時間(1s)を採用します。cacheTimeを変更することでキャッシュ時間を調整できます |
| enableAec | bool | エコー除去有効化の有無。デフォルト値はfalse |
| enableMessage | bool | メッセージチャネル有効化の有無。デフォルト値はtrue |
| enableMetaData | bool | MetaDataのコールバック有効化の有無。デフォルト値はNO。 true：SDKはEVT_PLAY_GET_METADATAメッセージによってビデオストリームのMetaDataをスローします。false：SDKはビデオストリームのMetaDataをスローしません。 |
| flvSessionKey | String | HTTPヘッダー情報コールバックの有効化の有無。デフォルト値は“” |
