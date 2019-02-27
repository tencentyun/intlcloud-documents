開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここではGME 3D効果音の導入技術文書を紹介します。

## 3D効果音エンジンの初期化
この関数は、3D効果音エンジンの初期化に使用され、ルームに参加した後に呼び出されます。3D効果音を使用する前にこのAPIを呼び出す必要があります。3D効果音を発信せず、ただ受信するユーザーでもこのAPIを呼び出す必要があります。

### 関数プロトタイプ 

```
public abstract int InitSpatializer(string modelPath)
```

|パラメータ	|タイプ	|意味 |
| ------- |---------|------|
| modelPath    	|string    	|3D効果音リソースファイルのパスです。3D効果音のモデルファイルは、次のサイトで[ダウンロード](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_2.X_3d_model)してください。md5: d0b76aa64c46598788c2f35f5a8a8694、ローカルに保存して、このパラメータで保存パスをSDKに渡します|

## 3D効果音のオン/オフ
この関数は3D効果音のオン/オフに使用されます。オンにすると3D効果音が聞こえます。

### 関数プロトタイプ

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)
```

|パラメータ	|タイプ	|意味 |
| ------- |---------|------|
| enable    	|bool    	|オンにすると3D効果音が聞こえる|
| applyToTeam  	|bool    	|enbleがtrueの場合にのみ、3Dボイスがチーム内で利用可能|

## 現在の3D効果音状態の取得
この関数は現在の3D効果音状態の取得に使用されます。

### 関数プロトタイプ 

```
public abstract bool IsEnableSpatializer()
```

|戻り値	|意味	|
| ------- |---------|
| true    	|オン状態    	|
| false    	|オフ状態	|  

## 音源方位のアップデート（向きを含む）
この関数は音源方位角情報のアップデートに使用されます。3D効果音はフレームごとに呼び出すことで実現されます。

###距離と音声減衰の関係
3D効果音は、音源の音量減衰は音源距離と一定の関係があります。単位距離がrangeを超えると、音量はほぼゼロになります。

|距離範囲（エンジン単位）|減衰公式	|
| ------- |---------|
| 0 < N < range/10  	|減衰係数：1.0 （音量減衰なし）	|
| N ≥ range/10|減衰係数：range/10/N        			|

![](https://main.qcloudimg.com/raw/50e745c853ab0e3f9f3bbef9d9cfc401.jpg)

### 関数プロトタイプ

```
public abstract void UpdateAudioRecvRange(int range)
```

|パラメータ    | タイプ         |意味|
| ------------- |-------------|-------------|
| range 	|int  	|効果音受信可能範囲の設定|

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```


|パラメータ    | タイプ         |意味|
| ------------- |-------------|-------------
| position   	|int[]		|ワールド座標系中の座標で、前、右、上の順序で表示|
| axisForward   |float[]  	|ローカル座標系前軸の単位ベクトル|
| axisRight    	|float[]  	|ローカル座標系右軸の単位ベクトル|
| axisUp    	|float[]  	|ローカル座標系上軸の単位ベクトル|

### サンプルコード

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








