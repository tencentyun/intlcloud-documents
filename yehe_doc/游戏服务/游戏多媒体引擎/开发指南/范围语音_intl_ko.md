## 기능 소개
음성 채팅방에서는 사용자가 일정 거리 내에서 다른 사용자와 실시간 음성 통화를 할 수 있습니다. 이 기능은 비즈니스 레이어를 통해 GME 클라이언트 API를 호출하여 음원 방향을 업데이트하고 로컬의 위치를 ​​서버에 알립니다. 서버는 **로컬 세계 좌표+로컬이 수신한 오디오 범위**와 **기타 엔드의 세계 좌표 + 기타 엔드가 수신한 오디오 범위**를 판단한 후 서버는 플레이어 범위 내의 오디오 스트림을 전달합니다. 기본적으로 플레이어에 가장 가까운 20개의 오디오 스트림을 전달합니다.

음원의 위치를 ​​업데이트하는 목적은 로컬의 위치를 ​​서버에 알리고, 서버는 로컬 세계 좌표+로컬이 수신한 오디오 범위와 기타 엔드 세계 좌표 + 기타 엔드가 수신한 오디오 범위를 판단하여 레인지 보이스 효과를 구현하는 것입니다.

## 사용 사례

### 배틀 로얄 게임
**배틀 로얄 게임 및 서바이벌 슈팅 모바일 게임**에서 ‘팀원만’ 또는 ‘모든 사람’ 음성 모드를 제공합니다. 게임 설정에서 플레이어 선택에 따라:
- ‘팀원만’ 모드를 사용하면 같은 팀의 팀원이 말하는 음성만 들립니다.
- ‘모든 사람’ 모드를 사용하면 팀원의 목소리와 일정 범위 내의 다른 플레이어의 음성을 들을 수 있습니다.

### 몰입형 버츄얼 시나리오
예를 들어 **게임 콘서트**와 같은 가상의 시나리오에서 가수는 가상의 방에서 레인지 보이스를 통해 노래를 부를 수 있고, 객석에 있는 모든 시청자들은 노래를 듣고 일정 범위 내의 다른 관객과 소통할 수 있습니다. 같은 방에 있는 수만 명의 사람들이 동시에 마이크를 활성화할 수 있습니다.

## 데모 효과

[시나리오 기반 Demo](https://intl.cloud.tencent.com/document/product/607/50220)를 다운로드하여 3D 음향 효과와 다양한 음성을 경험할 수 있습니다.


## 기본 개념

레인지 보이스 기능에는 **음성 모드**, **음성 수신 범위** 및 **TeamID**의 세 가지 개념이 포함됩니다.

### 음성 모드

사용자가 레인지 음성 채팅방에 방에 들어갈 때 사용자는 두 가지 음성 모드 중에서 선택할 수 있습니다.

| 음성 모드 | 매개변수 이름               | 기능                                         |
| -------- | ---------------------- | ------------------------------------------------------------ |
| 모든 사람   | RANGE_AUDIO_MODE_WORLD | <li>이 모드에서 로컬 플레이어는 특정 범위 내에 있는 다른 플레이어의 소리를 들을 수 있고 그들도 이 모드에 있는 경우 대화할 수 있습니다. </li> <li>팀원들은 서로의 말을 들을 수 있습니다. |
| 팀원만   | RANGE_AUDIO_MODE_TEAM  | <li>팀원만 서로의 말을 들을 수 있습니다                               |

> ! 팀원은 거리와 음성 모드에 관계없이 서로 대화할 수 있습니다.

### 음성 수신 범위

![](https://main.qcloudimg.com/raw/fccdd2f96b75e350adf9de934590b4f7.png)
음성 모드가 **모든 사람(RANGE_AUDIO_MODE_WORLD)**으로 설정된 경우 수신 범위는 UpdateAudioRecvRange API에 따라 달라집니다.

서로 다른 팀의 플레이어 A와 B가 음성 모드를 **모든 사람(RANGE_AUDIO_MODE_WORLD)**으로 설정했다고 가정합니다.

| 플레이어 좌표   | 음성 수신 범위 | 다른 플레이어의 음성 도달 가능성                                   | 팀원의 음성 도달 가능성         |
| ---------- | ------------ | -------------------------------------------------------- | -------------------------- |
| A(0,0,0) | 10 미터         | 플레이어 B는 플레이어로부터 10미터 이내에 있으므로 플레이어 B의 소리를 들을 수 있습니다    | 팀원끼리 대화가 가능합니다 |
| B（0,8,0） | 5 미터          | 플레이어 A가 5미터 이상 떨어져 있기 때문에 플레이어는 플레이어 A의 소리를 들을 수 없습니다 | 팀원끼리 대화가 가능합니다 |

<dx-alert infotype="explain" title="">
구체적인 플레이어의 음성 도달 가능성에 대한 자세한 내용은 [레인지 보이스](https://intl.cloud.tencent.com/document/product/607/17972)를 참고하십시오.
</dx-alert>

### TeamID

레인지 보이스 기능을 사용하려면 SetRangeAudioTeamID API를 호출하여 팀 ID(TeamID)를 설정한 후 EnterRoom API를 호출하여 방에 입장해야 합니다.

- 음성 채팅방 입장 시 지정한 TeamID != 0인 경우 레인지 음성 채팅방 모드로 진입하게 됩니다. 사용자가 음성 채팅방 입장 시 TeamID를 1로 설정하고 음성 모드를 RANGE_AUDIO_MODE_TEAM으로 설정하면 TeamID = 1인 구성원만 사용자의 음성을 들을 수 있습니다. 사용자가 음성 모드를 RANGE_AUDIO_MODE_WORLD로 설정하면 TeamID = 1인 구성원뿐만 아니라 일정 범위 내의 플레이어도 사용자의 음성을 들을 수 있습니다.
<table>
   <tr>
      <th>TeamID</th>
      <th>음성 모드</th>
			<th>범위</th>
      <th>음성 도달 가능성</th>
   </tr>
   <tr>
      <td  rowspan="2">TeamID != 0, TeamID = 1이라고 가정 </td>
      <td> RANGE_AUDIO_MODE_TEAM</td>
			  <td> 10 미터</td>
      <td>사용자는 TeamID = 1인 구성원과만 대화 가능</td>
   </tr>
   <tr>
      <td> RANGE_AUDIO_MODE_WORLD</td>
      <td> 10 미터</td>
			 <td>사용자는 TeamID = 1인 구성원 및 RANGE_AUDIO_MODE_WORLD 음성 모드의 구성원과 10m 이내의 같은 방에서 대화 가능</td>
   </tr>
</table>   
- 사용자가 TeamID = 0으로 설정된 음성 채팅방에 입장하면 방에 있는 모든 구성원(음성 모드에 관계없이)이 사용자의 음성을 들을 수 있는 레인지 보이스 호스트 모드로 들어갑니다.
<table>
   <tr>
      <th>TeamID</th>
      <th>TeamID 수정 시간</th>
			<th>범위</th>
      <th>음성 도달 가능성</th>
   </tr>
   <tr>
      <td  rowspan="2">TeamID = 0 </td>
      <td> 방 입장 전에는 TeamID != 0이며, 입장 후에는 TeamID = 0로 변경  </td>
			  <td> 10 미터</td>
      <td><li>방에 있는 모든 구성원(음성 모드에 관계없이)은 사용자의 음성을 들을 수 있습니다 <li>사용자는 TeamID = 0인 구성원과 대화할 수 있습니다 <li>사용자는 같은 방에서 10미터 이내의 RANGE_AUDIO_MODE_WORLD 음성 모드로 구성원의 음성을 들을 수 있습니다</td>
   </tr>
   <tr>
      <td> 방 입장 전 TeamID = 0, TeamID = 0로 방 입장</td>
      <td> 10 미터</td>
			 <td><li>방에 있는 모든 구성원(음성 모드에 관계없이)은 사용자의 음성을 들을 수 있습니다 <li>사용자는 TeamID = 0인 구성원과 대화할 수 있습니다 <li>사용자는 방에 있는 다른 구성원의 소리를 들을 수 없습니다</td>
   </tr>
</table>   



### 예시 시나리오

- **배틀 로얄 게임**: 배틀 로얄 게임에서는 4명의 플레이어가 한 팀으로 그룹화되며 이들을 위한 TeamID가 설정되어야 합니다. 배틀 룸은 100명의 플레이어, 즉 25개 팀을 포함할 수 있으므로 모든 팀이 동일한 음성 채팅방에 입장합니다. 전투 중 플레이어가 10m 이내의 낯선 사람과 대화하고 싶다면 플레이어는 음성을 들을 수 있는 범위를 10m로, 음성 모드를 RANGE_AUDIO_MODE_WORLD로 설정하고 마이크와 스피커를 모두 활성화할 수 있습니다. 플레이어가 팀원과만 소통하고 싶다면 음성 모드를 RANGE_AUDIO_MODE_TEAM으로 설정할 수 있습니다.
- **게임 콘서트**: 가수가 게임에서 콘서트를 하고 싶지만 플레이어와 교류할 필요가 없는 경우, 플레이어는 자신의 TeamID = OpenID로 설정하고, 음성 모드를 RANGE_AUDIO_MODE_WORLD로 설정하고, 음성을 들을 수 있는 범위를 적절한 값으로 설정하여 레인지 음성 채팅방에 입장하여 근처에 있는 플레이어와 대화할 수 있습니다. 가수가 방에 들어가기 전에 TeamID를 0으로 설정하면 방에 있는 모든 구성원이 가수의 소리를 들을 수 있지만 가수는 다른 구성원의 소리를 듣지 않습니다.
- **호스트 모드**: 가상 보드 게임과 같은 게임에서 호스트는 방에 있는 모든 구성원이 들을 수 있어야 하고 특정 범위 내의 플레이어의 소리를 들을 수 있어야 합니다. 이 경우 호스트는 TeamID != 0 값으로 설정한 상태로 방에 입장할 수 있으며, 방 입장 후 TeamID를 0으로 변경하여 방에 있는 모든 구성원이 들을 수 있고 일정 범위 내의 플레이어는 들을 수 있습니다.



## 전제 조건

- **음성 채팅 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME SDK에 액세스**: 핵심 API 및 음성 채팅 API에 대한 액세스를 포함합니다. 자세한 내용은 [Native SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/40858), [Unity SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44544), [Unreal SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.
- **만명 레인지 보이스**: 같은 방에 있는 레인지 보이스의 수가 1000개를 초과하는 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 GME 개발자에게 문의하십시오.

## 사용 프로세스

<img src="https://qcloudimg.tencent-cloud.cn/raw/4f531ae31457f031b0034d8dc39eda3c.png"  width="40%"/></img>

> !
>
> - 순서도에 따라 API를 호출해야 합니다.
> - 순서도의 파란색 부분은 레인지 보이스의 프로세스를 보여줍니다.
> - 레인지 음성 채팅방은 팀 음성 채팅방과 달리 **입장 시 원활 음질을 선택해야 합니다**.
> - 방에 들어가면 UpdateAudioRecvRange(적어도 한 번)를 호출하고 프레임당 한 번 UpdateSelfPosition을 호출합니다.


[](id:step0)
### 1. TeamID 설정

- 방 입장 전에 팀 ID를 설정하기 위해 이 API를 호출하면 다음 방 입장에 영향을 미칩니다.
- 이 API는 방 입장 후 팀 ID를 수정하기 위해 호출할 수 있습니다. 수정 사항은 즉시 적용됩니다.
- 방을 나갈 때 TeamID가 자동으로 0으로 재설정되지 않습니다. 따라서 이 음성 모드를 호출하기로 결정한 후에는 EnterRoom을 호출하기 전에 TeamID를 설정하십시오.
- 방 퇴장 후 입실 시, 방 퇴장 성공 콜백이 반환된 후 다시 팀 ID 설정 API를 호출합니다.

#### 함수 프로토타입

```
ITMGContext SetRangeAudioTeamID(int teamID)
```

|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| teamID| int    | 레인지 보이스 모드에서만 사용되는 TeamID. 0(기본값)으로 설정하면 팀 음성 모드가 사용됩니다.|

### 2. 음성 모드 설정

- 방 입장 전에 음성 모드를 변경하기 위해 이 API를 호출하면 다음 방 입장에 영향을 미칩니다.
- 방 입장 후 음성 모드를 변경하기 위해 이 API를 호출하면 현재 음성 모드가 바로 변경됩니다.
- 이 매개변수는 방을 나갈 때 자동으로 MODE_WORLD로 재설정되지 않습니다. 따라서 이 메소드를 호출하기로 결정하였다면 EnterRoom을 호출하기 전에 수행하십시오.

#### 함수 프로토타입

```
ITMGRoom int SetRangeAudioMode(RANGE_AUDIO_MODE rangeAudioMode)
```

| 매개변수        | 유형 | 설명                                              |
| -------------- | :--: | ----------------------------------------------------- |
| rangeAudioMode |int  | 0(MODE_WORLD)은 ‘모든 사람’, 1(MODE_TEAM)은 ‘팀원만’을 의미합니다|

### 3. 음성 채팅방 입장

EnterRoom을 호출하여 음성 채팅방에 들어가기 전에 SetRangeAudioTeamID 및 SetRangeAudioMode라는 두 가지 API를 호출해야 합니다.

#### 함수 프로토타입

```
ITMGContext.GetInstance(this).EnterRoom(roomId,ITMG_ROOM_TYPE_FLUENCY, authBuffer); 
```

음성 채팅방 입장 시 원활 음질을 선택하고, 방 입장 콜백을 수신 및 처리합니다.

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	//반환된 Data 분석
            int nErrCode = data.getIntExtra("result" , -1);
            String strErrMsg = data.getStringExtra("error_info");

            if (nErrCode == AVError.AV_OK)
            {
                //방 입장에 대한 성공 응답을 받으면 작업을 진행할 수 있습니다
                ScrollView_ShowLog("EnterRoom success");
                Log.i(TAG,"EnterRoom success!");
            }
            else
            {
                //방 입장에 실패한 경우 반환되는 에러 메시지를 분석해야 합니다
                ScrollView_ShowLog("EnterRoom fail :" + strErrMsg);
                Log.i(TAG,"EnterRoom fail!");
            }  
        }
	}
```

방에 들어가면 UpdateAudioRecvRange(적어도 한 번)를 호출하고 UpdateSelfPosition을 프레임당 한 번 호출합니다.

### 4. 음성 수신 범위 설정

- 이 메소드는 음성 수신 범위(게임 엔진에 따름) 설정에 사용되며 **방 입장 성공 후에만 호출할 수 있습니다**.
- 이 메소드는 UpdateSelfPosition과 함께 사용하여 음원 위치를 업데이트해야 합니다.
- 이 메소드는 한 번만 호출하면 적용되며 매개변수 값을 수정할 수 있습니다.

#### 함수 프로토타입 

```
ITMGRoom int UpdateAudioRecvRange(int range)
```

| 매개변수 | 유형 | 설명                                       |
| ----- | ---- | ------------------------------------------ |
| range | int  | 최대 음성 수신 범위, 단위: 게임 엔진에서 사용하는 거리 단위 |

#### 예시 코드  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```

### 5. 음원 위치 업데이트

음원 위치 업데이트의 목적은 로컬 플레이어의 위치를 서버에 알리기 위함입니다. 시스템은 **원격 좌표 및 음성 수신 범위**와 **로컬 좌표 및 음성 수신 범위**를 확인하여 레인지 보이스를 구현합니다.

- 이 기능은 음원 위치 정보를 업데이트하는 데 사용됩니다. **방 입장이 성공한 후에만 호출**할 수 있으며 **프레임당 한 번만 호출**해야 합니다. Unity 엔진을 예로 들면 Update에서 이 API를 호출해야 합니다.
- 레인지 보이스가 활성화된 경우 음원 위치를 업데이트해야 합니다. 범위 결정이 필요하지 않더라도 **이 API는 여전히 방 입장 후 한 번 호출해야 합니다**.
- 동시에 3D 음향 효과를 활성화하려면 아래의 [3D 음향 효과](https://intl.cloud.tencent.com/document/product/607/17972) 섹션에 지정된 대로 axisForward, axisRight 및 axisUp 매개변수를 설정합니다.

#### 함수 프로토타입

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| 매개변수        | 유형   | 의미                                       |
| ----------- | ------- | ------------------------------------------ |
| position    | int[]   | 세계 좌표 시스템의 로컬 위치(앞쪽, 오른쪽 및 위쪽) |
| axisForward |float[] |이 매개변수는 이 제품에서 무시해도 됨                         |
| axisRight   |float[] |이 매개변수는 이 제품에서 무시해도 됨                         |
| axisUp      |float[] |이 매개변수는 이 제품에서 무시해도 됨                         |

## 레인지 보이스와 3D 음향 효과 결합

레인지 보이스 기능은 거리를 통해 소리의 도달 가능성을 제어합니다. 보다 몰입감 있는 경험을 원하신다면 3D 음향 효과와 함께 사용하는 것을 권장합니다.

## 사용 프로세스

레인지 보이스를 사용하면서 3D 음향 효과를 사용하려면 1, 2, 3단계를 완료한 후 3D 엔진을 초기화하고 3D 음향 효과를 엽니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/39fb54637b7957509d00ed440f7ae0a9.png"  width="40%"/></img>

> ?순서도의 파란색 부분은 3D 음향 효과의 프로세스를 보여줍니다.

### 전제 조건

[레인지 보이스 사용](#step0)을 참고하여 1, 2, 3단계를 완료하십시오.

### 4. 3D 음향 효과 엔진 초기화

이 함수는 3D 음향 효과 엔진을 초기화하는 데 사용되며 방 입장 후 호출해야 합니다. 3D 음향 효과 재생이 아닌 3D 음향 효과 수신만 가능하게 하고 싶은 경우에도 3D 음향 효과 사용 전에 이 API를 호출해야 합니다.

#### 함수 프로토타입 

```
public abstract int InitSpatializer(string modelPath)
```

| 매개변수      | 유형   | 설명                      |
| --------- | ------ | ------------------------------------------------------------ |
| modelPath | string |공란만 입력 |

### 5. 3D 음향 효과 활성화/비활성화

이 함수는 3D 음향 효과를 활성화하거나 비활성화하는 데 사용됩니다. 활성화 후 3D 음향 효과를 들을 수 있습니다.

#### 함수 프로토타입

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)

```

| 매개변수        | 유형 | 설명                                              |
| ----------- | ---- | -------------------------------------------------- |
| enable      | bool | 활성화 후 3D 음향 효과를 들을 수 있습니다                          |
| applyToTeam | bool | 팀 내에서 3D 음향 효과를 활성화할지 여부를 지정합니다. enble이 true인 경우에만 적용됩니다. |

IsEnableSpatializer API를 사용하여 3D 음향 효과 상태를 가져올 수 있습니다.

### 6. 음성이 들리는 범위 설정 (3D 음향 효과용)

- 이 메소드는 음성 수신 범위(게임 엔진에 따름) 설정에 사용되며 **방 입장 성공 후에만 호출할 수 있습니다**.
- 이 메소드는 UpdateSelfPosition과 함께 사용하여 음원 위치를 업데이트해야 합니다.
- 이 메소드는 한 번만 호출하면 됩니다.
- 3D 음향 효과에서 사운드 소스까지의 거리가 지정된 임계값(range/10)을 초과하면 사운드가 거의 0으로 감쇠되기 시작합니다.
- 거리와 소음 감쇠의 관계에 대한 자세한 내용은 부록을 참고하십시오.

#### 함수 프로토타입 

```
ITMGRoom int UpdateAudioRecvRange(int range)

```

| 매개변수  | 유형 | 설명                                       |
| ----- | ---- | ------------------------------------------ |
| range | int  | 최대 음성 수신 범위, 단위: 게임 엔진에서 사용하는 거리 단위  |

#### 예시 코드  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);

```

### 7. 음원 위치 업데이트(3D 음향 효과용)

음원 위치 업데이트의 목적은 로컬 플레이어의 위치를 서버에 알리기 위함입니다. 시스템은 **원격 좌표 및 음성 수신 범위**와 **로컬 좌표 및 음성 수신 범위**를 확인하여 레인지 보이스를 구현합니다.


- 이 기능은 음원 위치 정보를 업데이트하는 데 사용됩니다. **방 입장이 성공한 후에만 호출**할 수 있으며 **프레임당 한 번만 호출**해야 합니다. Unity 엔진을 예로 들면 Update에서 이 API를 호출해야 합니다.
- **예시 코드를 복사하고 호출하여 이 기능을 사용할 수 있습니다**.

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
int position[] = { 
    (int)cameraLocation.X,
    (int)cameraLocation.Y,
    (int)cameraLocation.Z };
FMatrix matrix = ((FRotationMatrix)cameraRotation);
float forward[] = { 
    matrix.GetColumn(0).X,
    matrix.GetColumn(1).X,
    matrix.GetColumn(2).X };
float right[] = { 
    matrix.GetColumn(0).Y,
    matrix.GetColumn(1).Y,
    matrix.GetColumn(2).Y };
float up[] = { 
    matrix.GetColumn(0).Z,
    matrix.GetColumn(1).Z,
    matrix.GetColumn(2).Z};
ITMGContextGetInstance()->GetRoom()->UpdateSelfPosition(position, forward, right, up); 

```

**Unity**

```
Transform selftrans = currentPlayer.gameObject.transform;
Matrix4x4 matrix = Matrix4x4.TRS(Vector3.zero, selftrans.rotation, Vector3.one);
int[] position = new int[3] { 
    selftrans.position.z,
    selftrans.position.x,
    selftrans.position.y};
float[] axisForward = new float[3] { 
    matrix.m22,
    matrix.m02,
    matrix.m12 };
float[] axisRight = new float[3] { 
    matrix.m20,
    matrix.m00,
    matrix.m10 };
float[] axisUp = new float[3] { 
    matrix.m21,
    matrix.m01,
    matrix.m11 };
ITMGContext.GetInstance().GetRoom().UpdateSelfPosition(position, axisForward, axisRight, axisUp);

```


### 호스트 3D 음향 효과 사용 중지

시나리오에 레인지 보이스 호스트 모드를 사용하는 플레이어가 있는 경우, 즉 방에 있는 모든 플레이어가 그의 음성을 들어야 하는 경우 [3D 음성 블록리스트 API](https://intl.cloud.tencent.com/document/product/607/18218)를 참고하여 모든 수신측에서 3D 음성 블록리스트에 호스트를 추가합니다. 이를 통해 3D 음성 기능의 감쇠 효과가 호스트의 사운드 도달 가능성에 미치는 영향을 방지합니다.

다양한 역할의 API 호출 순서는 다음과 같습니다.

<table>
<tr>
<td rowspan="1" colSpan="1" >호스트 API 시간 순서</td>
<td rowspan="1" colSpan="1" >청취자 API 시간 순서</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" ><img src="https://qcloudimg.tencent-cloud.cn/raw/beeb060d2ed5ee1c6b2ac6a9085c3561.jpeg"  width="100%"/></img></td>
<td rowspan="1" colSpan="1" ><img src="https://qcloudimg.tencent-cloud.cn/raw/431d6a477c227002245730c20215405e.jpeg"  width="89%"/></img></td>
</tr>
</table>



## 부록

### 음성 모드

각 음성 모드의 플레이어 음성 도달 가능성은 다음과 같습니다.

- 플레이어 A가 ‘모든 사람’ 모드를 선택한 경우, 각 음성 모드에서 플레이어 B의 음성 도달 가능성은 다음과 같습니다:
<table>
<thead>
<tr>
<th >같은 팀 여부</th>
<th>범위 내 여부</th>
<th>음성 모드</th>
<th>A와 B가 서로 들을 수 있는지 여부</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="4">같은 팀</td>
<td rowspan="2">Yes</td>
<td>MODE_WORLD</td>
<td>Yes</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="2">No</td>
<td>MODE_WORLD</td>
<td>Yes</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="4">다른 팀</td>
<td rowspan="2">Yes</td>
<td>MODE_WORLD</td>
<td>Yes</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>No</td>
</tr>
<tr>
<td rowspan="2">No</td>
<td>MODE_WORLD</td>
<td>No</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>No</td>
</tr>
</tbody></table>
- 플레이어 A가 ‘팀원만’ 모드를 선택한 경우, 각 음성 모드에서 플레이어 B의 음성 도달 가능성은 다음과 같습니다:
<table>
<thead>
<tr>
<th >같은 팀 여부</th>
<th>범위 내 여부</th>
<th>음성 모드</th>
<th>A와 B가 서로 들을 수 있는지 여부</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="4">같은 팀</td>
<td rowspan="2">Yes</td>
<td>MODE_WORLD</td>
<td>Yes</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="2">No</td>
<td>MODE_WORLD</td>
<td>Yes</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="4">다른 팀</td>
<td rowspan="2">Yes</td>
<td>MODE_WORLD</td>
<td>No</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>No</td>
</tr>
<tr>
<td rowspan="2">No</td>
<td>MODE_WORLD</td>
<td>No</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>No</td>
</tr>
</tbody></table>



### 거리와 사운드 감쇠 관계

3D 음향 효과에서 사운드 소스까지의 거리가 지정된 임계값(range/10)을 초과하면 사운드가 거의 0으로 감쇠되기 시작합니다.

| 거리(엔진의 단위) | 감쇠 계수                     |
| -------------------- | ---------------------------- |
| 0 < N < range/10     | 1.0 (감쇠 없음) |
| N ≥ range/10         | range/10/N         |

![](https://main.qcloudimg.com/raw/4a71a93f7c91ecd70f50968875f95087.png)
