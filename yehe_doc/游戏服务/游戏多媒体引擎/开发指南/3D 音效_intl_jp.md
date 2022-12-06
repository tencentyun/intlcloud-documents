開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、このドキュメントではGME 3D効果音の導入技術を紹介します。

## ユースケース

通常の入室後のリアルタイム音声では、プレイヤーの音声に3D効果音の効果がなく、プレイヤーの間ではとても簡単なコラボライブを行うことしかできません。一方、3D位置音声を導入した後は、プレーヤーが呼びかけると自分の方位と位置情報を開示し、プレーヤーの音声も位置の変化によってリアルタイムで変化するようになっています。3D効果音は、「大逃殺」のようなプレイヤー間のコミュニケーションや戦闘体験をよりリアルにし、PUBGのように、より没入的で臨場感のある遊び方を体感できるようにしたと言えます。

[3D効果音](https://intl.cloud.tencent.com/document/product/607/50219)の効果を体験するには、「アプリケーションのダウンロード」をクリックしてください。



##  前提条件

- **リアルタイムボイスサービスが既に有効にされました**：[音声サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GME SDK導入済み**：コアインターフェースとリアルタイム音声インターフェースの導入が含まれます。詳細については、[Native SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/40858)、[Unity SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44544)、[Unreal SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44545)をご参照ください。

## 実装プロセス

### 実装フローチャート

次の図は3D効果音を実装するフローチャートです。青い部分は通常の入室リアルタイム音声と比較した導入ステップです。
<img src="https://qcloudimg.tencent-cloud.cn/raw/81f702b4e423cb048603bb5a6105f41e.png" width="500px">

### 3D効果音エンジンの初期化

この関数は、3D効果音エンジンを初期化するために使用され、入室した後に呼び出します。このインターフェースは、3D効果音を使用する前に呼び出す必要があります、3D効果音を送信せず受信するのみのユーザーでも、このインターフェースを呼び出してください。

#### 関数のプロトタイプ 

```
public abstract int InitSpatializer(string modelPath)
```

| パラメータ      | タイプ   | 意味                      |
| --------- | ------ | ------------------------- |
| modelPath | string | 3D効果音のリソースファイルの絶対パス |

パラメーター内の3D効果音リソースファイルは、別途ローカルにダウンロードしてください。導入するSDKのバージョンによって区別されます。

- v2.8以降のバージョンの場合は、[ダウンロード](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_2.X_3d_model)をクリックしてください、。md5：d0b76aa64c46598788c2f35f5a8a8694。
- v2.8以降の場合は、[ダウンロード](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/public/GME_2.8_3d_model.dat)をクリックしてください。md5：3d4d04b3949e267e34ca809e8a0b9243。

SDKのバージョンリリース履歴については[製品の最新情報](https://intl.cloud.tencent.com/document/product/607/35323)をご参照ください。

<dx-alert infotype="explain" title="关于资源路径">

- Unityの場合、プロジェクトのStreamingAssetsディレクトリに3Dファイルを配置し、SampleCodeの**copyFileFromAssetsToPersistent**関数を参照して、リソースファイルを各プラットフォームの適切なディレクトリにコピーすることをお勧めします。
- Unrealの場合、SampleCodeの**CopyAllAssetsToExternal**関数を参照して、3Dモデルファイルをコピーしてからパスを読み込みます。
  </dx-alert>

### 3D効果音のオン/オフ

この関数は、3D効果音をオン/オフにするために使用されます。オンにした後、3D効果音が聞こえます。

#### 関数のプロトタイプ

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)
```

| パラメータ        | タイプ | 意味                                              |
| ----------- | ---- | ------------------------------------------------- |
| enable      | bool | オンにすると3D効果音が聞こえる                          |
| applyToTeam | bool | 3D 音声はチーム内で機能するかどうかを示します。enbleがtrueである場合にのみ有効です。|

### 現在の3D効果音状態の取得

この関数は、現在の3D効果音の状態を取得するためのものです。

####  関数のプロトタイプ 

```
public abstract bool IsEnableSpatializer()
```

| 戻り値 | 意味     |
| ------ | -------- |
| true   | オンになっています |
| false  | オフになっています |

### 3D効果音の減衰距離の設定

減衰距離を設定する必要があります。推奨値は100です。

#### 距離と音声減衰の関係

3D効果音では、音源のボリュームは音源の距離と減衰関係にあります。単位距離がrangeを超えた後、ボリュームはほぼゼロまで減衰します。

| 距離範囲（エンジン単位） | 減衰公式                     |
| -------------------- | ---------------------------- |
| 0 < N < range/10     | 減衰係数：1.0（ボリュームは減衰しない）です |
| N ≥ range/10         | 減衰係数：range/10/N         |

![](https://main.qcloudimg.com/raw/50e745c853ab0e3f9f3bbef9d9cfc401.jpg)

####  関数のプロトタイプ

```
public abstract void UpdateAudioRecvRange(int range)
```

| パラメータ  | タイプ | 意味                                                         |
| ----- | ---- | ------------------------------------------------------------ |
| range | int  | 効果音の受信可能な範囲を設定します。推奨値は100です。この距離単位はゲームエンジン内の距離の単位です |



### 音源の方位を更新する（向きを含む）

この関数は、音源の方位情報を更新するために使用され、フレームごとに呼び出すと、3D効果音を実現できます。

####  関数のプロトタイプ

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| パラメータ        | タイプ    | 意味                                       |
| ----------- | ------- | ------------------------------------------ |
| position    | int[]   | 世界座標での自己座標であり、順序は前、右、上です |
| axisForward | float[] | ローカル座標系前軸の単位ベクトル|
| axisRight   | float[] | ローカル座標系右軸の単位ベクトル|
| axisUp      | float[] | ローカル座標系上軸の単位ベクトル|

####  サンプルコード

**Unreal**

```
FVector cameraLocation = UGameplayStatics::GetPlayerCameraManager(GetWorld(), 0)->GetCameraLocation();
FRotator cameraRotation = UGameplayStatics::GetPlayerCameraManager(GetWorld(), 0)->GetCameraRotation();
int position[] = { (int)cameraLocation.X,(int)cameraLocation.Y, (int)cameraLocation.Z };
FMatrix matrix = ((FRotationMatrix)cameraRotation);
float forward[] = { matrix.GetColumn(0).X,matrix.GetColumn(1).X,matrix.GetColumn(2).X };
float right[] = { matrix.GetColumn(0).Y,matrix.GetColumn(1).Y,matrix.GetColumn(2).Y };
float up[] = { matrix.GetColumn(0).Z,matrix.GetColumn(1).Z,matrix.GetColumn(2).Z};
ITMGContextGetInstance()->GetRoom()->UpdateSelfPosition(position, forward, right, up); 	
```

**Unity**

```
Transform selftrans = currentPlayer.gameObject.transform;
Matrix4x4 matrix = Matrix4x4.TRS(Vector3.zero, selftrans.rotation, Vector3.one);
int[] position = new int[3] { selftrans.position.z, selftrans.position.x, selftrans.position.y };
float[] axisForward = new float[3] { matrix.m22, matrix.m02, matrix.m12 };
float[] axisRight = new float[3] { matrix.m20, matrix.m00, matrix.m10 };
float[] axisUp = new float[3] { matrix.m21, matrix.m01, matrix.m11 };
ITMGContext.GetInstance().GetRoom().UpdateSelfPosition(position, axisForward, axisRight, axisUp);
```

### ローカル方位のインターフェース（VRシーン）

このインターフェースはVRデバイスの中でも、3Dの位置変化が非常に求められるシーンに適しています。この機能は高度なインターフェースであり、GME2.9.2以降が必要です。

- 通常の3Dシーンでは、ユーザーが単にUpdateSelfPosition関数を使用して自分の位置情報を更新し、ネットワークを介して他のユーザーに送信することができます。UpdateOtherPositionは、他のプレイヤーの位置情報をネットワークを経由せずに、ローカルから送信することができ、VRゲームシーンに適しています。
- リモートで更新された座標との競合を避けるために、UpdateOtherPositionを呼び出すと、リモート座標は破棄され、その影響は再びルームに入るまで残ります。したがって、**プレイヤーの座標をローカルに更新する場合は、すべてのプレイヤーの座標を更新してください**。

####  関数のプロトタイプ

```
public abstract int UpdateOtherPosition(int position[3])
```

| パラメータ     | タイプ  | 意味                                           |
| -------- | ----- | ---------------------------------------------- |
| position | int[] | 世界座標での他のプレーヤーの座標であり、順序は前、右、上です |



<dx-alert infotype="notice" title="注意">
プレイヤーの座標をローカルに更新する場合は、**すべてのプレイヤーの座標**をトラバーサルし、このインターフェースを使用して座標を渡してください。
</dx-alert>

### 3D音声のブラックリストインターフェース

> !このインターフェースは、GME2.9.3以降のSDKで有効になります。

現在、3D効果音を呼び出すとルーム内のすべての人に効果があります。特定のシーンでは、受信した人の音声が3D効果音によって減衰することが望ましくない場合、このインターフェースを呼び出すことで、その人を3D効果音ブラックリストに追加することができます。追加したら、このopenidの音声は3D効果音の影響を受けなくなります。

```
virtual int AddSpatializerBlacklist(const char* openId); 
```

このopenidをブラックリストから削除する必要がある場合は、次のインターフェースを呼び出してください。

```
virtual int RemoveSpatializerBlacklist(const char* openId); 
```

ブラックリストを空にする必要がある場合は、次のインターフェースを呼び出してください。

```
virtual int ClearSpatializerBlacklist(); 
```

## トラブルシューティング

接続後に音声をテストしても3D効果音がない場合は、次の手順に従って確認してください：

1. 正常にルームに参加したか、マイクをオンにしたか？両方が声が聞こえるか？？
2. デュアルチャネルヘッドセットに適しているか？
3. InitSpatializerインターフェースの戻り値は0か？
4. UpdateAudioRecvRangeの設定が小さすぎないか？
5. UpdateSelfPositionインターフェースが定期的に呼び出されたか？
6. [エラーコード](https://intl.cloud.tencent.com/document/product/607/33223)を使用して判断・解決します。




