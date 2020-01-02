開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグ・アクセスを手軽に実行できるように、ここで、Gaming Multimedia Engine 3Dサウンドエフェクトのアクセス技術ドキュメントについて説明させていただきます。

## 3Dサウンドエフェクトエンジンを初期化する
この関数は、3Dサウンドエフェクトエンジンを初期化するために使用され、入室した後に呼び出します。このインターフェイスは、3Dサウンドエフェクトを使用する前に呼び出す必要があります、3Dサウンドエフェクトを送信せず受信するのみのユーザーでも、このインターフェイスを呼び出す必要があります。

####  関数のプロトタイプ 

```
public abstract int InitSpatializer(string modelPath)
```

|パラメータ|タイプ|意味|
| ------- |---------|------|
| modelPath    |string    |3Dサウンドエフェクトリソースファイルのパスです。3Dサウンドエフェクトのモデルファイルをこのパスから[ダウンロード](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_2.X_3d_model)して（md5: d0b76aa64c46598788c2f35f5a8a8694）ローカルに保存し、このパラメータを介して保存パスをSDKに転送します|

## 3Dサウンドエフェクトのオン/オフ
この関数は、3Dサウンドエフェクトをオン/オフにするために使用されます。オンにした後、3Dサウンドエフェクトが聞こえます。

####  関数のプロトタイプ

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)
```

|パラメータ|タイプ|意味|
| ------- |---------|------|
| enable    |bool    |オンにした後、3Dサウンドエフェクトが聞こえます|
| applyToTeam  |bool    |3D音声はチーム内で機能するかどうかを示します、enbleがtrueである場合にのみ有効です|

## 現在の3Dサウンドエフェクトの状態を取得する
この関数は、現在の3Dサウンドエフェクトの状態を取得するために使用されます。

####  関数のプロトタイプ 

```
public abstract bool IsEnableSpatializer()
```

|戻り値|意味|
| ------- |---------|
| true    |オンになっています    |
| false    |オフになっています|  

## 音源の方位を更新する（向きを含む）
この関数は、音源の方位情報を更新するために使用され、フレームごとに呼び出すと、3Dサウンドエフェクトを実現できます。

### 距離と音の減衰の関係
3Dサウンドエフェクトでは、音源のボリュームは音源の距離と減衰関係にあります。単位距離がrangeを超えた後、ボリュームはほぼゼロまで減衰します。

|距離範囲（エンジンユニット）|減衰式|
| ------- |---------|
| 0 < N < range/10  |減衰係数：1.0（ボリュームは減衰しない）です|
| N ≥ range/10|減衰係数：range/10/N        |

![](https://main.qcloudimg.com/raw/50e745c853ab0e3f9f3bbef9d9cfc401.jpg)

####  関数のプロトタイプ

```
public abstract void UpdateAudioRecvRange(int range)
```

|パラメータ     | タイプ         |意味|
| ------------- |-------------|-------------|
| range |int  |サウンドエフェクトが受信できる範囲を設定します|

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```


|パラメータ     | タイプ         |意味|
| ------------- |-------------|-------------
| position   |int[]||世界座標での自己座標、順序は前、右、上です|
| axisForward   |float[]  |自己座標の前軸の単位ベクトルです|
| axisRight    |float[]  |自己座標系の右軸の単位ベクトルです|
| axisUp    |float[]  |自己座標系の上軸の単位ベクトルです|

####  サンプルコード

#### Unreal

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

#### Unity

```
Transform selftrans = currentPlayer.gameObject.transform;
Matrix4x4 matrix = Matrix4x4.TRS(Vector3.zero, selftrans.rotation, Vector3.one);
int[] position = new int[3] { selftrans.position.z, selftrans.position.x, selftrans.position.y };
float[] axisForward = new float[3] { matrix.m22, matrix.m02, matrix.m12 };
float[] axisRight = new float[3] { matrix.m20, matrix.m00, matrix.m10 };
float[] axisUp = new float[3] { matrix.m21, matrix.m01, matrix.m11 };
ITMGContext.GetInstance().GetRoom().UpdateSelfPosition(position, axisForward, axisRight, axisUp);
```







