본문은 3D 음향 효과를 위한 GME(Game Multimedia Engine) API에 액세스하고 디버깅하는 방법을 설명합니다.

## 시나리오

일반적인 채팅방 내 실시간 음성 채팅에서는 플레이어의 음성에 3D 효과음이 없으며, 플레이어끼리 간단한 인터랙션만 가능합니다. 하지만 3D 음향 효과를 적용하면 플레이어는 말하는 동안 방향과 위치 정보를 노출할 수 있으며 거리에 따라 음성이 실시간으로 변경될 수 있습니다. 3D 음향 효과 기능은 플레이어에게 <배틀 로얄 게임>에서 보다 현실적이고 몰입감 있는 커뮤니케이션과 전투 경험을 제공합니다.

클릭하여 데모를 다운로드하고 [3D 음향 효과](https://intl.cloud.tencent.com/document/product/607/50219) 기능을 사용해 볼 수 있습니다.



## 전제 조건

- **실시간 음성 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME SDK에 액세스**: 핵심 API 및 음성 채팅 API에 대한 액세스를 포함합니다. 자세한 내용은 [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.

## 구현 프로세스

### 구현 순서도

3D 음향 효과 구현 순서도는 다음과 같습니다. 파란색 부분은 채팅방 내 일반 음성 채팅과 비교했을 때 추가되는 연결 단계입니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/af3b21c8c6ff552c887ee369f9c217c6.jpg" width="500px">

### 3D 음향 효과 엔진 초기화

이 함수는 3D 효과음 엔진을 초기화하며 방에 들어간 후 호출합니다. 3D 효과음을 사용하기 전에 꼭 이 API를 먼저 호출해야 합니다. 3D 효과음을 수락만 하고 발송하지 않는 유저도 이 API를 호출해야 합니다.

#### 함수 프로토타입 

```
public abstract int InitSpatializer(string modelPath)
```

| 매개변수      | 유형   | 의미                      |
| --------- | ------ | ------------------------- |
| modelPath | string | 3D 음향 효과 리소스 파일의 절대 경로 |

3D 음향 효과 리소스 파일을 로컬 디스크에 다운로드해야 합니다. SDK 버전에 따라 하나를 선택하십시오.

- v2.8 이전 버전의 경우 [여기](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_2.X_3d_model)를 클릭하여 다운로드하십시오(md5 값: d0b76aa64c46598788c2f35f5a8a8694).
- v2.8 이상 버전의 경우 [여기](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/public/GME_2.8_3d_model.dat)를 클릭하여 다운로드하십시오(md5 값: 3d4d04b3949e267e34ca809e8a0b9243).

GME SDK 릴리스 업데이트는 [릴리스 노트](https://intl.cloud.tencent.com/document/product/607/35323)를 참고하십시오.

<dx-alert infotype="explain" title="리소스 경로에 대한 참고 사항">

- Unity를 예로 들면 3D 음향 효과 리소스 파일을 프로젝트의 StreamingAssets 디렉터리에 넣고 SampleCode의 **copyFileFromAssetsToPersistent** 함수 내용을 기반으로 다른 플랫폼의 해당 디렉터리에 복사하는 것이 좋습니다.
- Unreal Engine을 예로 들면 3D 모델 파일을 복사하고 SampleCode의 **CopyAllAssetsToExternal** 함수 내용을 기반으로 경로를 읽습니다.
  </dx-alert>

### 3D 음향 효과 활성화/비활성화

이 함수는 3D 음향 효과를 활성화하거나 비활성화하는 데 사용됩니다. 활성화 후 3D 사운드를 들을 수 있습니다.

#### 함수 프로토타입

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)
```

| 매개변수        | 유형 | 의미                                              |
| ----------- | ---- | ------------------------------------------------- |
| enable      | bool | 활성화 후 3D 음향 효과를 들을 수 있습니다                          |
| applyToTeam | bool | 팀 내에서 3D 음향 효과를 활성화할지 여부를 지정하고 enable이 true인 경우에만 적용됩니다 |

### 기존 3D 음향 효과 상태 획득

이 함수는 기존 3D 효과음 상태를 읽어옵니다.

#### 함수 프로토타입 

```
public abstract bool IsEnableSpatializer()
```

| 반환된 값 | 설명     |
| ------ | -------- |
| true   | 활성화 상태 |
| false  | 비활성화 상태 |

### 3D 음향 효과 감쇠 범위 설정

3D 음향 효과 감쇠 범위를 설정해야 합니다. 100으로 설정하는 것이 좋습니다.

#### 거리와 사운드의 감쇠 관계

3D 사운드 효과에서 사운드 소스까지의 거리가 지정된 임계값(range/10)을 초과하면 사운드가 거의 0으로 감쇠되기 시작합니다.

| 거리(엔진의 단위) | 감쇠 계수                     |
| -------------------- | ---------------------------- |
| 0 < N < range/10     | 1.0 (감쇠 없음) |
| N ≥ range/10         | range/10/N         |

![](https://main.qcloudimg.com/raw/50e745c853ab0e3f9f3bbef9d9cfc401.jpg)

#### 함수 프로토타입

```
public abstract void UpdateAudioRecvRange(int range)
```

| 매개변수  | 유형 | 의미                                                         |
| ----- | ---- | ------------------------------------------------------------ |
| range | int  | 게임 엔진에서 사용하는 거리 단위로 음향 효과를 들을 수 있는 범위입니다. 100으로 설정하는 것이 좋습니다. |



### 음원 위치 업데이트(방향 포함)

이 함수는 음원의 위치 정보를 업데이트하는 데 사용됩니다. 3D 음향 효과를 구현하기 위해 매 프레임마다 호출할 수 있습니다.

#### 함수 프로토타입

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| 매개변수        | 유형   | 의미                                       |
| ----------- | ------- | ------------------------------------------ |
| position    | int[]   | 세계 좌표 시스템의 로컬 위치(앞쪽, 오른쪽 및 위쪽) |
| axisForward | float[] | 로컬 좌표 시스템의 순방향 벡터                   |
| axisRight   | float[] | 로컬 좌표 시스템의 오른쪽 벡터                   |
| axisUp      | float[] | 로컬 좌표 시스템의 위쪽 벡터                   |

#### 예시 코드

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

### 로컬 위치 API(VR 시나리오용)

이 API는 VR 장치에서 3D 위치 변경에 대한 요구 사항이 높은 시나리오에 적합합니다. 이 기능은 고급 API이며 GME 2.9.2 이상에서만 사용할 수 있습니다.

- 일반적인 3D 시나리오에서 사용자는 UpdateSelfPosition 함수를 사용하여 위치 정보를 업데이트하고 네트워크를 통해 다른 사용자에게 보내기만 하면 됩니다. UpdateOtherPosition은 또한 네트워크를 사용하지 않고 로컬로 다른 플레이어의 위치 정보를 전달할 수 있으므로 VR 게임 시나리오에 적합합니다.
- 원격으로 업데이트된 좌표와의 충돌을 피하기 위해 UpdateOtherPosition을 호출하면 원격 좌표가 삭제되어 다음 방 입장에 영향을 미칩니다. 따라서 **로컬에서 플레이어 좌표를 업데이트하려면 모든 플레이어의 좌표를 업데이트하십시오**.

#### 함수 프로토타입

```
public abstract int UpdateOtherPosition(int position[3])
```

| 매개변수     | 유형  | 의미                                           |
| -------- | ----- | ---------------------------------------------- |
| position   |int[]|국제 좌표계(World Coordinate System, WCS)에서 다른 플레이어의 좌표(앞쪽, 오른쪽 및 위쪽)|



<dx-alert infotype="notice" title="주의">
플레이어 좌표를 로컬로 업데이트하려면 **모든 플레이어 좌표**를 탐색하고 이 API를 통해 전달합니다.
</dx-alert>

### 3D 사운드 효과 블록리스트 API

> !이 API는 GME SDK 2.9.3 이상에서 적용됩니다.

현재 3D 사운드 효과 기능은 호출 후 방에 있는 모든 사용자에게 적용됩니다. 그러나 일부 특수 시나리오에서는 3D 사운드 효과로 인해 누군가의 목소리가 감쇠되는 것을 보고 싶지 않을 수 있습니다. 이 경우 이 API를 호출하여 3D 사운드 효과 블록리스트에 사용자를 추가할 수 있으며 지정된 openid의 음성에는 더 이상 3D 사운드 효과가 없습니다.

```
virtual int AddSpatializerBlacklist(const char* openId); 
```

블록리스트에서 openid를 제거하려면 다음 API를 호출해야 합니다.

```
virtual int RemoveSpatializerBlacklist(const char* openId); 
```

블록리스트를 지우려면 다음 API를 호출해야 합니다.

```
virtual int ClearSpatializerBlacklist(); 
```

## 문제 해결

이 기능을 연결한 후 음성에 3D 음향 효과가 없으면 다음과 같이 문제를 해결할 수 있습니다.

1. 사용자가 방에 성공적으로 입장했는지, 마이크를 활성화했는지, 서로의 소리를 들을 수 있는지 확인합니다.
2. 스테레오 헤드셋 사용 여부를 확인합니다.
3. InitSpatializer의 반환 값이 0인지 확인합니다.
4. UpdateAudioRecvRange의 값이 너무 작은지 확인합니다.
5. UpdateSelfPosition API가 주기적으로 호출되는지 확인합니다.
6. [에러 코드](https://intl.cloud.tencent.com/document/product/607/33223)를 참고하여 문제를 해결하십시오.




