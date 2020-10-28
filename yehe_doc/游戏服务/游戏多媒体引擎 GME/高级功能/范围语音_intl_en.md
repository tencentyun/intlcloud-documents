This document describes how to integrate and debug the GME APIs for range voice.

GME's range voice service is specially developed for games similar to PUBG. Different from a team voice room, a range voice room has the following core capabilities:
1. It provides the "Team only" and "Everyone" voice modes unique to **games like PUBG and Battle Royale**.
2. Relying on its range determination capability, it enables **high numbers of users** to voice chat using their mic in the same voice room.



## Concepts

### Range voice room

Before using range voice, you need to call the `SetRangeAudioTeamID` API to set the team ID (`teamID`) and then call the `EnterRoom` API to enter the room. If the specified `teamID` is not set to `0` before room entry, a range voice room will be used.

### Voice mode

When the user enters a range voice room, the user can choose from two voice modes:

| Voice Mode | Parameter Name | Feature |
| -------- | ---------------------- | ------------------------------------------------------------ |
| Everyone | RANGE_AUDIO_MODE_WORLD | In this mode, every one within a certain range can hear the user as he or she chats with his or her teammates |
| Team only | RANGE_AUDIO_MODE_TEAM | Only teammates can hear the user |

**In different voice modes, the specific sound reachability is as follows:**
a. Players in the same team can hear each other regardless of how far apart they are or what voice modes they use.
b. Players in different teams can hear each other only if they are all in the "Everyone" voice mode and within a certain distance.

>?For more information on the specific sound reachability of players, please see “Appendix” in [Range Voice](https://intl.cloud.tencent.com/document/product/607/17972).


### Voice reception range

If the voice mode is set to **Everyone** (`RANGE_AUDIO_MODE_WORLD`), the voice reachability will be subject to the `UpdateAudioRecvRange` API.

 - Regardless of whether teammates are within the voice range, they can always talk with each other.
 - To set the voice reception range, use the `UpdateAudioRecvRange` API.
 - Voice modes can be switched in real time in the range voice room. However, changing the `teamID`, which must be specified before room entry, in the range voice room is not supported.
 - To use range voice, room entry must be performed with smooth sound quality (i.e., RoomType = 1).

![](https://main.qcloudimg.com/raw/fccdd2f96b75e350adf9de934590b4f7.png)


## Directions

Different from a team voice room, a range voice room must use smooth sound quality, and `SetRangeAudioTeamID` and `SetRangeAudioMode` must be called before `EnterRoom`. Call `UpdateAudioRecvRange` after successful room entry and call `UpdateSelfPosition` once per each frame.

If you want to use the 3D sound effect at the same time, please do so as instructed in “Simultaneous Use of the 3D Sound Effect” in [Range Voice](https://intl.cloud.tencent.com/document/product/607/17972) after completing steps 1 and 2 below.

### 1. Set `teamID`

- The team ID (`teamID`) must be set by calling the method `SetRangeAudioTeamID` before `EnterRoom`. Otherwise, GME will return the error code `AV_ERR_ROOM_NOT_EXITED(1202)`.

>!This parameter will not be automatically reset to `0` upon room exit. Therefore, once you decide to use range voice, please call this method to set `teamID` before calling `EnterRoom` each time.

#### Function prototype

```
ITMGContext SetRangeAudioTeamID(int teamID)
```

| Parameter | Type | Description |
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

| Parameter | Type | Description |
| -------------- | :--: | ----------------------------------------------------- |
| rangeAudioMode    |int     | `0` (MODE_WORLD): everyone; `1` (MODE_TEAM): team only |

### 3. Enter a voice room
Before entering a voice room by calling `EnterRoom`, you need to call the following two APIs: `SetRangeAudioTeamID` and `SetRangeAudioMode`.
```
ITMGContext.GetInstance(this).EnterRoom(roomId,ITMG_ROOM_TYPE_FLUENCY, authBuffer); 
```
Be sure to use smooth sound quality for the voice room, and monitor and process the callback for room entry.
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	//Analyze the returned result
            int nErrCode = data.getIntExtra("result" , -1);
            String strErrMsg = data.getStringExtra("error_info");

            if (nErrCode == AVError.AV_OK)
            {
                //Return a success response for room entry. You can proceed with your operation
                ScrollView_ShowLog("EnterRoom success");
                Log.i(TAG,"EnterRoom success!");
            }
            else
            {
                //Failed to enter the room. You need to analyze the returned error message
                ScrollView_ShowLog("EnterRoom fail :" + strErrMsg);
                Log.i(TAG,"EnterRoom fail!");
            }  
        }
	}
```
Once you enter the room, call `UpdateAudioRecvRange` and call `UpdateSelfPosition` once per each frame.


### 4. Set the voice reception range

- This method is used to set the voice reception range (subject to your own game engine) and can be called **only after successful room entry**.
- This method must be used in conjunction with `UpdateSelfPosition` to update the sound source position.
- This method only needs to be called once.

#### Function prototype 

```
ITMGRoom int UpdateAudioRecvRange(int range)
```

| Parameter | Type | Description |
| ----- | ---- | ------------------------------------------ |
| range | int | Maximum voice reception range in the distance unit used by the game engine |

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```

### 5. Update the sound source position

To update the sound source position is to inform the server of the local player's position. The system implements range voice by checking the **local coordinates and the voice reception range** against the **remote coordinates and the voice reception range**.
- This function is used to update the sound source position information. It can be called only **after successful room entry** and needs to be called **once per each frame**. Taking the Unity engine as an example, this API needs to be called in `Update`.
- If range voice is enabled, the sound source position must be updated. Even if range determination is not required, **this API still needs to be called once after room entry**.
- If you want to enable the 3D sound effect at the same time, set the `axisForward`, `axisRight`, and `axisUp` parameters as specified in the “Simultaneous Use of the 3D Sound Effect” section below.



#### Function prototype

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| Parameter | Type | Description |
| ----------- | ------- | ------------------------------------------ |
| position | int[] | Local position (forward, right and up) in the world coordinate system |
| axisForward | float[] | This parameter can be ignored in this product                         |
| axisRight   | float[] | This parameter can be ignored in this product                         |
| axisUp      | float[] | This parameter can be ignored in this product                         |


## Simultaneous Use of the 3D Sound Effect

You can enable both the 3D sound effect and the range voice at the same time by following the steps below:

The following steps need to be performed after steps 1, 2 and 3 above are completed.

### 1. Initialize the 3D sound effect engine

This function is used to initialize the 3D sound effect engine and needs to be called after room entry. You must call this API before using the 3D sound effect. Even if you want to enable only the 3D sound effect reception and not playback, you still need to call this API.

#### Function prototype 

```
public abstract int InitSpatializer(string modelPath)
```

| Parameter | Type | Description |
| --------- | ------ | ------------------------------------------------------------ |
| modelPath | string | Path of the 3D sound effect resource file. Please download the 3D sound effect model file [here](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_2.X_3d_model) (MD5 checksum: d0b76aa64c46598788c2f35f5a8a8694) and store it locally. Its storage path is passed in to the SDK through this parameter. You must use this official file |

### 2. Enable/disable the 3D sound effect

This function is used to enable/disable the 3D sound effect. You can hear the 3D sound after enabling it.


#### Function prototype

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)
```

| Parameter | Type | Description |
| ----------- | ---- | ------------------------------------------------- |
| enable | bool | After enabling the 3D sound effect, you can hear the 3D sound effect |
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

| Parameter | Type | Description |
| ----- | ---- | ------------------------------------------ |
| range | int | Maximum voice reception range in the distance unit used by the game engine |

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```


### 4. Update the sound source position (for the 3D sound effect)

To update the sound source position is to inform the server of the local player's position. The system implements range voice by checking the **local coordinates and the voice reception range** against the **remote coordinates and the voice reception range**.

- This function is used to update the sound source position information. It can be called only **after successful room entry** and needs to be called **once per frame**. Taking the Unity engine as an example, this API needs to be called in `Update`.
- **Please directly copy the sample code to use this feature.**

#### Function prototype

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| Parameter | Type | Description |
| ----------- | ------- | ------------------------------------------ |
| position | int[] | Local position (forward, right and up) in the world coordinate system |
| axisForward | float[] | Forward vector in the local coordinate system |
| axisRight | float[] | Right vector in the local coordinate system |
| axisUp | float[] | Up vector in the local coordinate system |


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

| In the Same Team | Within the Range | Voice Mode | A Can Hear B | B Can Hear A |
| -----------------	| ------------ | ------------ |--------------------------	|--------------------------	|
| Yes 		| Yes 		 	|MODE_WORLD	| Yes		| Yes		|
| Yes		| Yes		 	|MODE_TEAM	| Yes		| Yes		|
| Yes		| No		 	|MODE_WORLD	| Yes		| Yes		|
| Yes		| No		 	|MODE_TEAM	| Yes		| Yes		|
| No 		| Yes		 	|MODE_WORLD	| Yes		| Yes		|
| No		| Yes			|MODE_TEAM	| No	| No	|
| No		| No		 	|MODE_WORLD	| No	| No	|
| No		| No			|MODE_TEAM	| No	| No	|

- The table below lists the possible cases of sound reachability for player B in different voice modes if player A selects the "Team only" mode:

| In the Same Team | Within the Range | Voice Mode | A Can Hear B | B Can Hear A |
| -----------------	| ------------ | ------------ |--------------------------	|--------------------------	|
| Yes 		| Yes 		 	|MODE_WORLD	| Yes		| Yes		|
| Yes		| Yes		 	|MODE_TEAM	| Yes		| Yes		|
| Yes		| No		 	|MODE_WORLD	| Yes		| Yes		|
| Yes		| No		 	|MODE_TEAM	| Yes		| Yes		|
| No		| Yes		 	|MODE_WORLD	| No	| No	|
| No		| Yes			|MODE_TEAM	| No	| No	|
| No		| No		 	|MODE_WORLD	| No	| No	|
| No		| No			|MODE_TEAM	| No	| No	|


### The relationship between distance and sound attenuation

In the 3D sound effect, the sound will begin to attenuate to almost zero as the distance to the sound source exceeds a specified threshold (range/10).

| Distance (Unit in Engine) | Attenuation Coefficient |
| -------------------- | ---------------------------- |
| 0 < N < range/10 | 1.0 (no attenuation) |
| N ≥ range/10 | range/10/N |

![](https://main.qcloudimg.com/raw/4a71a93f7c91ecd70f50968875f95087.png)
