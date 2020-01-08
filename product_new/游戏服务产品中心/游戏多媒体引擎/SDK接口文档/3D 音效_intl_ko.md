개발자가 Tencent Cloud Game Multimedia Engine(GME) 제품 API를 테스트하고 액세스하는 편의성을 위해 GME 3D 효과음을 액세스하는 기술 파일을 소개드립니다.

## 3D 효과음 엔진 초기화
이 함수는 3D 효과음 엔진을 초기화하며 방에 들어간 후 호출합니다. 3D 효과음을 사용하기 전에 꼭 이 API를 먼저 호출해야 합니다. 3D 효과음을 수락만 하고 발송하지 않는 유저도 이 API를 호출해야 합니다.

### 함수 프로토타입 

```
public abstract int InitSpatializer(string modelPath)
```

|파라미터|타입|의미 |
| ------- |---------|------|
| modelPath    |string    |3D 효과음 리소스 파일 경로, 3D 효과음 모델링 파일은 여기에서 [다운로드](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_2.X_3d_model)하세요，md5: d0b76aa64c46598788c2f35f5a8a8694, 로컬에 저장하며, 파라미터를 통해 저장 경로를 SDK에 전송합니다|

## 3D 효과음 온 혹은 오프
이 함수는 3D 효과음을 온 혹은 오프할 수 있습니다. 온하면 3D 효과음을 들을 수 있습니다.

### 함수 프로토타입

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)
```

|파라미터|타입|의미 |
| ------- |---------|------|
| enable    |bool    |오픈 시에 3D 효과음을 들을 수 있습니다|
| applyToTeam  |bool    |3D 음성은 소규모 팀 내부 적용 관련하여, 오직 enble이 true일 경우에만 적용합니다|

## 기존 3D 효과음 상태 획득
이 함수는 기존 3D 효과음 상태를 읽어옵니다.

### 함수 프로토타입 

```
public abstract bool IsEnableSpatializer()
```

|리턴값|의미|
| ------- |---------|
| true    |오픈 상태    |
| false    |종료 상태|

## 음원 위치 업데이트(방향 포함)
이 함수는 음원 방위각 메시지를 업데이트합니다. 프레임당 호출하여 3D 효과음 이펙트를 구현합니다.

### 거리와 사운드 페이드 관계
3D 효과음의 경우, 음원 사운드 크기와 음원 거리는 일정한 페이드 관계가 존재합니다. 단위 거리가 range를 초과하면 사운드는 거의 0 수준으로 페이드합니다.

|거리 범위(엔진 단위)|페이드 수식|
| ------- |---------|
| 0 < N < range/10  |페이드 계수: 1.0(사운드 페이드가 없음)|
| N ≥ range/10|페이드 계수: range/10/N        |

### 함수 프로토타입

```
public abstract void UpdateAudioRecvRange(int range)
```

|파라미터     | 타입         |의미|
| ------------- |-------------|-------------|
| range |int  |효과음이 수락 가능한 범위 설정|

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```


|파라미터     | 타입         |의미|
| ------------- |-------------|-------------|
| position   |int[]|월드 좌표계에 위치한 좌표, 순서는 앞측, 우측, 위측|
| axisForward   |float[]  |자체 좌표계 앞축 단위 벡터|
| axisRight    |float[]  |자체 좌표계 우축 단위 벡터|
| axisUp    |float[]  |자체 좌표계 윗축 단위 벡터|

### 예시 코드

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







