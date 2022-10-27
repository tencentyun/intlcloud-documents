This document describes how to access and debug GME APIs for range voice.

## Use Cases

GME's range voice feature is specifically provided for voice scenarios where range needs to be implemented. It is suitable for the following use cases:

1. It provides the "team only" and "everyone" voice modes unique to **battle royale games and survival shooter mobile games**.
2. In a voice room, a user can talk with other users within a certain distance, and all the users can hear the host speaking. Therefore, this feature is suitable for **game concerts**.

## Demo Effects

You can click [Free Demo](https://intl.cloud.tencent.com/document/product/607/50219) and download to experience 3D sound effects and range voice.

<img src="https://qcloudimg.tencent-cloud.cn/raw/23cd82f978016559de9c40a413dc23b9.png"  width="70%"/></img>

## Concepts

The range voice feature involves three concepts: **voice mode**, **range for hearing the voice**, and **TeamID**.

### Voice mode

When the user enters a range voice room, the user can choose from two voice modes:

| Voice Mode | Parameter Name               | Feature                       |
| -------- | ---------------------- | ------------------------------------------------------------ |
| Everyone   | RANGE_AUDIO_MODE_WORLD | <li>In this mode, the local player can be heard by other players within a certain range and can talk with them if they are also in this mode.</li> <li>Teammates can hear each other. |
| Team only   | RANGE_AUDIO_MODE_TEAM  | <li>Only teammates can hear each other.                                       |

> ! Teammates can talk with each other regardless of the distance and voice mode.

### Range for hearing the voice

![](https://main.qcloudimg.com/raw/fccdd2f96b75e350adf9de934590b4f7.png)
If the voice mode is set to **Everyone** (`RANGE_AUDIO_MODE_WORLD`), the range for hearing the voice will be subject to the `UpdateAudioRecvRange` API.

Suppose players A and B in different teams both set their voice modes to **Everyone** (`RANGE_AUDIO_MODE_WORLD`):

| Player Coordinates | Range for Hearing the Voice | Voice Reachability of Another Player  | Voice Reachability of Teammates |
| ---------- | ------------ | -------------------------------------------------------- | -------------------------- |
| A (0,0,0) | 10 meters         | The player can hear player B, as player B is within 10 meters of the player.    | Teammates can talk with each other. |
| B (0,8,0) | 5 meters          | The player cannot hear player A, as player A is more than 5 meters away.  | Teammates can talk with each other. |

<dx-alert infotype="explain" title="">
For more information on the specific voice reachability of players, see [Range Voice](https://intl.cloud.tencent.com/document/product/607/17972).
</dx-alert>

### TeamID

To use the range voice feature, you need to call the `SetRangeAudioTeamID` API to set the team ID (TeamID) and then call the `EnterRoom` API to enter the room.

- If `TeamID` specified during voice room entry is not `0`, a user will enter the range voice room mode. If a user sets `TeamID` to `1` and the voice mode to `RANGE_AUDIO_MODE_TEAM` when entering a voice room, only members whose `TeamID` is `1` can hear the user. If the user sets the voice mode to `RANGE_AUDIO_MODE_WORLD`, players within a certain range as well as members whose `TeamID` is `1` can hear the user.

<table>
   <tr>
      <th>TeamID</th>
      <th>Voice Mode</th>
			<th>Range</th>
      <th>Voice Reachability</th>
   </tr>
   <tr>
      <td  rowspan="2">`TeamID` is not `0`. Suppose `TeamID` is `1`.</td>
      <td>RANGE_AUDIO_MODE_TEAM</td>
			  <td>10 meters</td>
      <td>The user can talk with only members whose `TeamID` is `1`.</td>
   </tr>
   <tr>
      <td>RANGE_AUDIO_MODE_WORLD</td>
      <td>10 meters</td>
			 <td>The user can talk with members whose `TeamID` is `1` and members in `RANGE_AUDIO_MODE_WORLD` voice mode within 10 meters in the same room.</td>
   </tr>
</table>   





- If a user enters a voice room with `TeamID` set to `0`, the user will enter the range voice host mode, where all members in the room (regardless of their voice mode) can hear the user.

<table>
   <tr>
      <th>TeamID</th>
      <th>TeamID Modification Time</th>
			<th>Range</th>
      <th>Voice Reachability</th>
   </tr>
   <tr>
      <td  rowspan="2">`TeamID` is `0`</td>
      <td>`TeamID` is not `0` before room entry and is changed to `0` after room entry.</td>
			  <td>10 meters</td>
      <td><li>All members in the room (regardless of their voice mode) can hear the user.<li>The user can talk with members whose `TeamID` is `0`.<li>The user can hear members in `RANGE_AUDIO_MODE_WORLD` voice mode within 10 meters in the same room.</td>
   </tr>
   <tr>
      <td>`TeamID` is `0` before and during room entry.</td>
      <td>10 meters</td>
			 <td><li>All members in the room (regardless of their voice mode) can hear the user.<li>The user can talk with members whose `TeamID` is `0`.<li>The user cannot hear other members in the room.</td>
   </tr>
</table>   



### Sample scenarios

- **Battle royale game**: In a battle royale game, every four players are grouped into a team, and a team ID (`TeamID`) needs to be set for them. A battle room can contain 100 players, i.e., 25 teams, so all those teams enter the same voice room. In a battle, if a player wants to communicate with a stranger within 10 meters, the player can set the range for hearing the voice to 10 meters and the voice mode to `RANGE_AUDIO_MODE_WORLD` and enable both the mic and speaker. If the player wants to communicate with only teammates, the player can set the voice mode to `RANGE_AUDIO_MODE_TEAM`.
- **Game concert**: If a singer wants to hold a concert in a game but doesn't need to interact with players, players can enter the range voice room with their `TeamID` set to `OpenID`, voice mode set to `RANGE_AUDIO_MODE_WORLD`, and range for hearing the voice set to an appropriate value so as to talk with players nearby. The singer can set `TeamID` to `0` before entering the room to be heard by all members in the room without hearing other members.
- **Host mode**: In a game such as virtual board game, the host needs to be heard by all members in the room and hear players within a certain range. In this case, the host can enter the room with `TeamID` set to a non-0 value and change `TeamID` to `0` after room entry, so as to be heard by all members in the room while hearing players within a certain range.



## Prerequisites

- **Activated the real-time voice service**: See [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- **Accessed to GME SDK**: includes access of core APIs and Voice Chat APIs. For details, please see [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858), [Unity SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/44544), [Unreal SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/44545).

## Directions

<img src="https://qcloudimg.tencent-cloud.cn/raw/4f531ae31457f031b0034d8dc39eda3c.png"  width="60%"/></img>

> !
>
> - Be sure to follow the flowchart to call the API.
> - The blue part of the flowchart shows the process of the range voice.
> - A range voice room is different from a team voice room in that **you must select the smooth sound quality when entering the range voice room.**
> - Once you enter the room, call `UpdateAudioRecvRange` (once at least) and call `UpdateSelfPosition` once per frame.


[](id:step0)
### 1. Set `TeamID`

- Calling this API to set the team ID before room entry will affect the next room entry.
- This API can be called to modify the team ID after room entry. The modification will take effect immediately.
- `TeamID` will not be automatically reset to `0` upon room exit. Therefore, once you decide to call this voice mode, do so to set the `TeamID` before each call of `EnterRoom`.
- When entering a room after exiting the room, call the API for setting the team ID again after the callback for successful room exit is returned.

#### Function prototype

```
ITMGContext SetRangeAudioTeamID(int teamID)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| teamID		| int    		| Team ID, which is used in range voice mode only.  When it is set to `0` (default), the team voice mode is used.

### 2. Set the voice mode

- Calling this API to change the voice mode before room entry will affect the next room entry.
- Calling this API to change the voice mode after room entry will directly change the current voice mode.
- This parameter will not be automatically reset to `MODE_WORLD` upon room exit. Therefore, once you decide to call this method, do so before each call of `EnterRoom`.

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
           	// Analyze the returned data
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

### 4. Set the range for hearing the voice

- This method is used to set the voice reception range (subject to the game engine) and can be called **only after successful room entry**.
- This method must be used in conjunction with `UpdateSelfPosition` to update the sound source position.
- This method only needs to be called once to take effect, and the parameter value can be modified.

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
- If you want to enable the 3D sound effect at the same time, set the `axisForward`, `axisRight`, and `axisUp` parameters as specified in the “Simultaneous Use of the 3D Sound Effect” section below.

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

## Range Voice Combined with 3D Sound Effect

The range voice feature controls the reachability of sound through distance. It is recommended to use with 3D sound effects if you want a more immersive experience.

## Directions

If you want to use 3D sound effects while using range voice, please complete the step 1, 2, 3 and then initialize 3D engine and open 3D sound effects.

<img src="https://qcloudimg.tencent-cloud.cn/raw/39fb54637b7957509d00ed440f7ae0a9.png"  width="60%"/></img>

> ?The blue part of the flowchart shows the process of the 3D sound effect.

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
| ----------- | ---- | -------------------------------------------------- |
| enable      | bool | You can hear the 3D sound effect after enabling it,                           |
| applyToTeam | bool | Specifies whether the 3D sound effect is enabled within the team and takes effect only when `enable` is `true` |

The `IsEnableSpatializer ` API can be used to get the 3D sound effect status.

### 3. Set the range for hearing the voice (for the 3D sound effect)

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

- The table below lists the possible cases of voice reachability for player B in different voice modes if player A selects the "Everyone" mode:

<table>
<thead>
<tr>
<th>In the Same Team</th>
<th>Within the Range</th>
<th>Voice Mode</th>
<th>Can A and B Hear Each Other</th>
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



- The table below lists the possible cases of voice reachability for player B in different voice modes if player A selects the "Team only" mode:

<table>
<thead>
<tr>
<th>In the Same Team</th>
<th>Within the Range</th>
<th>Voice Mode</th>
<th>Can A and B Hear Each Other</th>
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
