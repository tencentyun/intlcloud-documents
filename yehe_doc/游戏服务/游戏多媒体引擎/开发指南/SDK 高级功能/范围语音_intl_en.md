This document describes the GME APIs for range voice.


## Use Cases

GME's range voice service is specially developed for PUBG-like games. Unlike a team voice room, a range voice room has the following core capabilities:
1. It provides the "Team only" and "Everyone" voice modes unique to **games like PUBG and Battle Royale**.
2. Relying on its range determination capability, it enables a large number of users to voice chat using their mic in the same voice room. Users within a certain range can turn on the mic, and the local receives up to 20 audio channels.


## Experience
[Download free demo](https://intl.cloud.tencent.com/document/product/607/38535#windows-.E5.B9.B3.E5.8F.B0-3d-.E8.AF.AD.E9.9F.B3.E4.BD.93.E9.AA.8C-demo)

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/linaji.gif"  width="70%"/></img>

## Concepts

### Range voice room

Before using range voice, you need to call the `SetRangeAudioTeamID` API to set the team ID (`TeamID`) and then call the `EnterRoom` API to enter the room. If the specified `TeamID` is not equal to 0 during room entry, the range voice room mode will be triggered.

### Voice mode

When the user enters a range voice room, the user can choose from two voice modes:

| Voice Mode | Parameter Name               | Feature                       |
| -------- | ---------------------- | ------------------------------------------------------------ |
| Everyone | RANGE_AUDIO_MODE_WORLD | In this mode, everyone within a certain range can hear the player as he or she chats with his or her teammates |
| Team only | RANGE_AUDIO_MODE_TEAM | Only teammates can hear the user       |

**In different voice modes, the specific sound reachability is as follows:**
a. Players in the same team can hear each other no matter how far apart they are or what voice modes they use.
b. Players in different teams can hear each other only if they are all in the "Everyone" voice mode and within a certain distance.

<dx-alert infotype="explain" title="">
For more information on the specific sound reachability of players, please see [Appendix](https://intl.cloud.tencent.com/document/product/607/17972#.E9.99.84.E5.BD.95).
</dx-alert>


### Voice reception range

If the voice mode is set to **Everyone** (`RANGE_AUDIO_MODE_WORLD`), the voice reachability will be subject to the `UpdateAudioRecvRange` API.

 - Regardless of whether teammates are within the voice range, they can always talk with each other.
 - To set the voice reception range, use the `UpdateAudioRecvRange` API.
 - Voice modes can be switched in real time in the range voice room. However, changing the `TeamID`, which must be specified before room entry, in the range voice room is not supported.
 - To use range voice, you must choose smooth sound quality when entering the room (i.e., RoomType = 1).

![](https://main.qcloudimg.com/raw/fccdd2f96b75e350adf9de934590b4f7.png)


### Examples
In a battle royale game, there are four members in a team, and they need to set a Team ID(TeamID). A voice room can contain 100 people, which is, 25 teams. In a game, if a player wants to communicate with a stranger within 10 meters, set the voice distance range to 10, set the voice mode to `RANGE_AUDIO_MODE_WORLD`, and turn on the microphone and speaker at the same time. If he wants to communicate with his teammate, set the voice mode: RANGE_AUDIO_MODE_TEAM.


## Prerequisites
- Activate Voice Chat Service. See [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/10782)**.
- Integrate with GME SDK: Core APIs and Voice Chat APIs are required. For details, see [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858), [Unity SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/44544), [Unreal SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/44545).


## Directions

A range voice room is different from a team voice room because you must choose smooth sound quality when entering the range voice room. In addition, `SetRangeAudioTeamID` and `SetRangeAudioMode`(Can be modified after entering the room) must be called before `EnterRoom` is called.

Once you enter the room, call `UpdateAudioRecvRange` (once at least), and call `UpdateSelfPosition` once per frame.

<img src="https://qcloudimg.tencent-cloud.cn/raw/4f531ae31457f031b0034d8dc39eda3c.png"  width="60%"/></img>

>!
>- Make sure to follow the flow chart to call the API.
>- The blue part of the flow chart shows the process of the range voice.






### Prerequisites
Initialize the GME and the core API has been called correctly, e.g. the Poll function is called every frame.

###1. Set TeamID[](id: step0)

- The team ID (`TeamID`) must be set by calling the API `SetRangeAudioTeamID` before `EnterRoom`. Otherwise, GME will return the error code `AV_ERR_ROOM_NOT_EXITED(1202)`. If you enter the room after exiting the room, please call the API `SetRangeAudioTeamID` after exiting the room successfully.


>!This parameter will not be automatically reset to `0` upon room exit. Therefore, once you decide to use range voice, please use this method to set `TeamID` before calling `EnterRoom` each time.




#### Function prototype

```
ITMGContext SetRangeAudioTeamID(int teamID)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| teamID|int    | Team ID, which is used for audio upstream/downstream control in range voice. When it is set to `0` (default), the team voice room is used. |

### 2. Set the voice mode
- The voice mode can be modified by calling the method `SetRangeAudioMode` either before or after room entry.
- Calling this method before room entry will affect the next room entry.
- Calling this method after room entry will directly change the current voice mode.
- This parameter will not be automatically reset to `MODE_WORLD` upon room exit. Therefore, once you decide to call this method, please do so before each call of `EnterRoom`.

#### Function prototype

```
ITMGRoom int SetRangeAudioMode(RANGE_AUDIO_MODE rangeAudioMode)
```

| Parameter           | Type | Description                                 |
| -------------- | :--: | ----------------------------------------------------- |
| rangeAudioMode | int  | `0` (MODE_WORLD): everyone; `1` (MODE_TEAM): team only |

### 3. Enter a voice room
Before entering a voice room by calling `EnterRoom`, you need to call the following two APIs: `SetRangeAudioTeamID` and `SetRangeAudioMode`.

#### Function prototype
```
ITMGContext.GetInstance(this).EnterRoom(roomId,ITMG_ROOM_TYPE_FLUENCY, authBuffer); 
```
Choose smooth sound quality when entering the voice room, and monitor and process the callback for room entry.
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	// Analyze the returned result
            int nErrCode = data.getIntExtra("result" , -1);
            String strErrMsg = data.getStringExtra("error_info");

            if (nErrCode == AVError.AV_OK)
            {
                //If you receive a success response for room entry, you can proceed with your operation
                ScrollView_ShowLog("EnterRoom success");
                Log.i(TAG,"EnterRoom success!");
            }
            else
            {
                //If you fail to enter the room, you need to analyze the returned error message
                ScrollView_ShowLog("EnterRoom fail :" + strErrMsg);
                Log.i(TAG,"EnterRoom fail!");
            }  
        }
	}
```

Once you enter the room, call `UpdateAudioRecvRange` (once at least), and call `UpdateSelfPosition` once per frame.


### 4. Set the voice reception range

- This method is used to set the voice reception range (subject to the game engine) and can be called **only after successful room entry**.
- This method must be used in conjunction with `UpdateSelfPosition` to update the sound source position.
- This method only needs to be called once.

#### Function prototype 

```
ITMGRoom int UpdateAudioRecvRange(int range)
```

| Parameter  | Type | Description                                       |
| ----- | ---- | ------------------------------------------ |
| range | int  | Maximum voice reception range in the distance unit used by the game engine|

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```

### 5. Update the sound source position

The purpose of updating the sound source position is to inform the server of the local player's position. The system implements range voice by checking the **local coordinates and voice reception range** against the **remote coordinates and voice reception range**.
- This function is used to update the sound source position information. It can be **called only after successful room entry** and needs to be **called once per frame**. Taking the Unity engine as an example, this API needs to be called in `Update`.
- If range voice is enabled, the sound source position must be updated. Even if range determination is not required, **this API still needs to be called once after room entry**.
- If you want to enable 3D sound effect at the same time, set the `axisForward`, `axisRight`, and `axisUp` parameters as specified in the [3D Sound Effect](https://intl.cloud.tencent.com/document/product/607/17972#.E5.90.8C.E6.97.B6.E4.BD.BF.E7.94.A8-3d-.E9.9F.B3.E6.95.88) section below.

#### Function prototype

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| Parameter        | Type    | Description                                       |
| ----------- | ------- | ------------------------------------------ |
| position    | int[]   | Local position (forward, right and up) in the world coordinate system |
| axisForward | float[] | This parameter can be ignored in this product                         |
| axisRight   | float[] | This parameter can be ignored in this product                         |
| axisUp      | float[] | This parameter can be ignored in this product                         |


## Range voice combined with 3D sound effects

The range voice feature controls the reachability of sound through distance. It is recommended to use with 3D sound effects if you want a more immersive experience.

## Directions
If you want to use 3D sound effects while using range voice, please complete the step 1, 2, 3 and then initialize 3D engine and open 3D sound effects.

<img src="https://qcloudimg.tencent-cloud.cn/raw/39fb54637b7957509d00ed440f7ae0a9.png"  width="60%"/></img>

>? The green part of the flow chart shows the process of the range voice.

### Prerequisites
Please see [Range Voice Usage](#step0) and complete step 1,2,3.

### 1. Initialize the 3D sound effect engine

This function is used to initialize the 3D sound effect engine and needs to be called after room entry. You must call this API before using the 3D sound effect, even if you want to enable only the 3D sound effect reception rather than the 3D sound effect playback.

#### Function prototype 

```
public abstract int InitSpatializer(string modelPath)
```

| Parameter      | Type   | Description                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| modelPath | string | Path of the 3D sound effect resource file. Please download the 3D sound effect model file [here](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_2.X_3d_model) (md5: d0b76aa64c46598788c2f35f5a8a8694) and store it locally. Its storage path is passed to the SDK through this parameter. You must use this official file. |

### 2. Enable/disable the 3D sound effect

This function is used to enable or disable the 3D sound effect. You can hear the 3D sound after enabling it.


#### Function prototype

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)
```

| Parameter        | Type | Description                                              |
| ----------- | ---- | ------------------------------------------------- |
| enable      | bool | You can hear the 3D sound effect after enabling it,                           |
| applyToTeam | bool | Specifies whether the 3D sound effect is enabled within the team and takes effect only when `enable` is `true` |

The `IsEnableSpatializer ` API can be used to get the 3D sound effect status.

### 3. Set the voice reception range (for the 3D sound effect)

- This method is used to set the voice reception range (subject to the game engine) and can be called **only after successful room entry**.
- This method must be used in conjunction with `UpdateSelfPosition` to update the sound source position.
- This method only needs to be called once.
- In the 3D sound effect, the volume level of the sound source attenuates as the distance to the sound source increases. If the unit distance exceeds the range, the volume level will attenuate to almost zero.
- For more information on the relationship between the distance and sound attenuation, please see the appendix.

#### Function prototype 

```
ITMGRoom int UpdateAudioRecvRange(int range)
```

| Parameter  | Type | Description                                       |
| ----- | ---- | ------------------------------------------ |
| range | int  | Maximum voice reception range in the distance unit used by the game engine|

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```


### 4. Update the sound source position (for the 3D sound effect)

The purpose of updating the sound source position is to inform the server of the local player's position. The system implements range voice by checking the **local coordinates and voice reception range** against the **remote coordinates and voice reception range**.



- This function is used to update the sound source position information. It can be **called only after successful room entry** and needs to be **called once per frame**. Taking the Unity engine as an example, this API needs to be called in `Update`.
- **Please directly copy the sample code to use this feature.**

#### Function prototype

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| Parameter        | Type    | Description                                       |
| ----------- | ------- | ------------------------------------------ |
| position    | int[]   | Local position (forward, right and up) in the world coordinate system |
| axisForward | float[] | Forward vector in the local coordinate system |
| axisRight   | float[] | Right vector in the local coordinate system |
| axisUp      | float[] | Up vector in the local coordinate system |


#### Sample code

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

## Appendix

### Voice modes

Player voice reachability in different voice modes is as follows:

- The table below lists the possible cases of sound reachability for player B in different voice modes if player A selects the "Everyone" mode:
<table>
<thead>
<tr>
<th>In the same team</th>
<th>Within the range</th>
<th>Voice mode</th>
<th>A and B can hear each other</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="4">Yes</td>
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
<td rowspan="4">No</td>
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


- The table below lists the possible cases of sound reachability for player B in different voice modes if player A selects the "Team only" mode:
<table>
<thead>
<tr>
<th>In the same team</th>
<th>Within the Range</th>
<th>Voice Mode</th>
<th>A and B can hear each other</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="4">Yes</td>
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
<td rowspan="4">No</td>
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


### The relationship between distance and sound attenuation

In the 3D sound effect, the sound will begin to attenuate to almost zero as the distance to the sound source exceeds a specified threshold (range/10).

| Distance (Unit in Engine) | Attenuation Coefficient                     |
| -------------------- | ---------------------------- |
| 0 < N < range/10     | 1.0 (no attenuation) |
| N ≥ range/10 | range/10/N         |

![](https://main.qcloudimg.com/raw/4a71a93f7c91ecd70f50968875f95087.png)
