This document describes how to access and debug the GME APIs for range voice.

GME's range voice service is dedicatedly developed for games similar to PUBG. Different from team voice room, it has the following core capabilities:
1. It provides "team only" and "everyone" voice modes unique to **PUBG-like games and battle royale games**.
2. Relying on its range determination capability, **it enables high numbers of users** to mic on for voice chat in the same voice room.



## Basic Concepts

### Range voice room

Before using range voice, you need to call the `SetRangeAudioTeamID` API to set the team ID (`TeamID`) and then call the `EnterRoom` API to enter the room. If the specified `TeamID` is not equal to 0 during room entry, range voice room mode will be triggered.

### Voice mode

During range voice room entry, there are two available voice modes:

| Voice Mode | Parameter Name | Feature |
| -------- | ---------------------- | ------------------------------------------------------------ |
| Everyone | RANGE_AUDIO_MODE_WORLD | In this mode, other players within a certain range can hear the local player, while teammates can always talk with each other regardless of range |
| Team only | RANGE_AUDIO_MODE_TEAM | Only teammates can hear the local player |

**In different voice modes, the specific sound reachability is as follows:**
a. Players in the same team can hear each other regardless of distance or voice mode.
b. Players in different teams can hear each other only if they are in "Everyone" voice mode and within a certain distance.

>For more information on the specific sound reachability of players, please see [Appendix](https://intl.cloud.tencent.com/document/product/607/17972).


### Voice reception range

If the voice mode is set to **Everyone** (`RANGE_AUDIO_MODE_WORLD`), the voice reachability will be subject to the `UpdateAudioRecvRange` API.

 - No matter whether teammates are within the voice range, they can always talk with each other.
 - To set the voice reception range, call the `UpdateAudioRecvRange` API.
 - Voice modes can be switched in real time in the range voice room. However, it is not supported to change the `TeamID`, which must be specified before room entry.
 - To use range voice, room entry must be performed with smooth sound quality (i.e., RoomType = 1)

![](https://main.qcloudimg.com/raw/fccdd2f96b75e350adf9de934590b4f7.png)


## Directions

Different from general team voice rooms, when the range voice feature is used, room entry must be performed with smooth sound quality, and the following two APIs must be called before `EnterRoom`: `SetRangeAudioTeamID` and `SetRangeAudioMode`. Call `UpdateAudioRecvRange` after successful room entry and call `UpdateSelfPosition` once per frame.

If you want to use 3D sound effect at the same time, please do so as instructed in [Simultaneous Use of 3D Sound Effect](https://intl.cloud.tencent.com/document/product/607/17972) after completing steps 1 and 2.

### 1. Set TeamID

The `TeamID` can be set in this method before `EnterRoom`; otherwise, the following error code will be returned directly: `AV_ERR_ROOM_NOT_EXITED(1202)`.

> This parameter will not be automatically reset to 0 upon room exit; therefore, once you decide to call this voice mode, please call it to set the `TeamID` before each call of `EnterRoom`.

#### Function prototype

```
ITMGContext SetRangeAudioTeamID(int teamID)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| teamID		| int    		| Team ID, which is used for upstream/downstream audio stream control in range voice. If `TeamID` is 0 (default value), the call mode will be general team voice

### 2. Set the voice mode
- The voice mode can be changed in this method, which can be called either before or after room entry.
- Calling this method before room entry will affect the next room entry.
- Calling this method after room entry will directly change the current voice mode.
- This parameter will not be automatically reset to `MODE_WORLD` upon room exit; therefore, once you decide to call this method, please call it to set the voice mode before each call of `EnterRoom`.

#### Function prototype

```
ITMGRoom int SetRangeAudioMode(RANGE_AUDIO_MODE rangeAudioMode)
```

| Parameter | Type | Description |
| -------------- | :--: | ----------------------------------------------------- |
| rangeAudioMode | int | 0(MODE_WORLD): Everyone; 1(MODE_TEAM): Team only |


### 3. Set the voice reception range

- This method is used to set the voice reception range (subject to the game engine) and can be called only **after successful room entry**.
- This method must be used in conjunction with `UpdateSelfPosition`, which updates the sound source position.
- This method only needs to be called once to take effect.

#### Function prototype 

```
ITMGRoom int UpdateAudioRecvRange(int range)
```

| Parameter | Type | Description |
| ----- | ---- | ------------------------------------------ |
| range | int | Maximum voice reception range in the distance unit used by the engine |

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```

### 4. Update the sound source position

Updating the sound source position is to inform the server of the local player's position. The system implements range voice by checking the **local coordinates and audio reception range** against **remote coordinates and audio reception range**.
- This function is used to update the sound source position information. It can be called only **after successful room entry** and needs to be called **once per frame**. Taking the Unity engine as an example, this API needs to be called in `Update`.
- If range voice is enabled, the sound source position must be updated. Even if range determination is not required, **this API still needs to be called once after room entry**.
- If you want to enable 3D sound effect at the same time, set the `axisForward`, `axisRight`, and `axisUp` parameters as specified in the [3D Sound Effect](https://intl.cloud.tencent.com/document/product/607/17972) section below.



#### Function prototype

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| Parameter | Type | Description |
| ----------- | ------- | ------------------------------------------ |
| position | int[] | Local position. The coordinate order is front, right, and top |
| axisForward | float[] | This parameter can be ignored in this product                         |
| axisRight   | float[] | This parameter can be ignored in this product                         |
| axisUp      | float[] | This parameter can be ignored in this product                         |


## Simultaneous Use of 3D Sound Effect

You can enable both 3D sound effect and range voice at the same time in the following steps:

These steps need to be performed after steps 1 and 2 above are completed.

### 1. Initialize the 3D sound effect engine

This function is used to initialize the 3D sound effect engine and needs to be called after room entry. You must call this API before using 3D sound effect. Even if you want to enable only 3D sound effect reception but not playback, you still need to call this API.

#### Function prototype 

```
public abstract int InitSpatializer(string modelPath)
```

| Parameter | Type | Description |
| --------- | ------ | ------------------------------------------------------------ |
| modelPath | string | Path of 3D sound effect resource file. Please download the 3D sound effect model file [here](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_2.X_3d_model) (MD5 checksum: d0b76aa64c46598788c2f35f5a8a8694) and store it locally. Its storage path is passed in to the SDK through this parameter. You must use this official file |

### 2. Enable or disable 3D sound effect

This function is used to enable/disable 3D sound effect. After enabling it, you can hear 3D sound effect.


#### Function prototype

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)
```

| Parameter | Type | Description |
| ----------- | ---- | ------------------------------------------------- |
| enable | bool | After enabling 3D sound effect, you can hear 3D sound effect |
| applyToTeam | bool | It specifies whether 3D sound effect is enabled within the team and takes effect only when `enable` is `true` |

The `IsEnableSpatializer ` API can be used to get the 3D sound effect status.

### 3. Set the voice reception range (for 3D sound effect)

- This method is used to set the voice reception range (subject to the game engine) and can be called only **after successful room entry**.
- This method must be used in conjunction with `UpdateSelfPosition`, which updates the sound source position.
- This method only needs to be called once to take effect.
- In 3D sound effect, the volume level of the sound source attenuates as the distance to the sound source increases. If the unit distance exceeds the `range`, the volume level will attenuate to almost zero.
- For more information on the relationship between the distance and sound attenuation, please see the appendix.

#### Function prototype 

```
ITMGRoom int UpdateAudioRecvRange(int range)
```

| Parameter | Type | Description |
| ----- | ---- | ------------------------------------------ |
| range | int | Maximum voice reception range in the distance unit used by the engine |

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```


### 4. Update the sound source position (for 3D sound effect)

Updating the sound source position is to inform the server of the local player's position. The system implements range voice by checking the **local coordinates and audio reception range** against **remote coordinates and audio reception range**.


- This function is used to update the sound source position information. It can be called only **after successful room entry** and needs to be called **once per frame**. Taking the Unity engine as an example, this API needs to be called in `Update`.
- **Please directly copy and call the sample code to use this feature.**

#### Function prototype

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| Parameter | Type | Description |
| ----------- | ------- | ------------------------------------------ |
| position | int[] | Local position. The coordinate order is front, right, and top |
| axisForward | float[] | Unit vector of local position on the front axis |
| axisRight | float[] | Unit vector of local position on the right axis |
| axisUp | float[] | Unit vector of local position on the top axis |


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

Player sound reachability in different voice modes:

- If player A selects the option "Everyone", the table below lists the possible cases of sound reachability for player B in different voice modes:

| In the Same Team	| Within the Range	| Voice Mode	| A Can Hear B	| B Can Hear A	|
| -----------------	| ------------ | ------------ |--------------------------	|--------------------------	|
| Yes		| Yes		 	| MODE_WORLD	| Yes		| Yes		|
| Yes		| Yes		 	| MODE_TEAM	| Yes		| Yes		|
| Yes		| No		 	| MODE_WORLD	| Yes		| Yes		|
| Yes		| No		 	| MODE_TEAM	| Yes		| Yes		|
| No		| Yes		 	| MODE_WORLD	| Yes		| Yes		|
| No		| Yes			| MODE_TEAM	| No	| No	|
| No		| No		 	| MODE_WORLD	| No	| No	|
| No		| No			| MODE_TEAM	| No	| No	|

- If player A selects the option "Team only", the table below lists the possible cases of sound reachability for player B in different voice modes:

  

| In the Same Team	| Within the Range	| Voice Mode	| A Can Hear B	| B Can Hear A	|
| -----------------	| ------------ | ------------ |--------------------------	|--------------------------	|
| Yes		| Yes		 	| MODE_WORLD	| Yes		| Yes		|
| Yes		| Yes		 	| MODE_TEAM	| Yes		| Yes		|
| Yes		| No		 	| MODE_WORLD	| Yes		| Yes		|
| Yes		| No		 	| MODE_TEAM	| Yes		| Yes		|
| No		| Yes		 	| MODE_WORLD	| No	| No	|
| No		| Yes			| MODE_TEAM	| No	| No	|
| No		| No		 	| MODE_WORLD	| No	| No	|
| No		| No			| MODE_TEAM	| No	| No	|


### Relationship between distance and sound attenuation

In 3D sound effect, the volume level of the sound source attenuates as the distance to the sound source increases. If the unit distance exceeds the `range`, the volume level will attenuate to almost zero.

| Distance Range (Unit in Engine) | Attenuation Formula |
| -------------------- | ---------------------------- |
| 0 < N < range/10 | Attenuation coefficient: 1.0 (no attenuation) |
| N ≥ range/10 | Attenuation coefficient: range/10/N |

![](https://main.qcloudimg.com/raw/4a71a93f7c91ecd70f50968875f95087.png)

