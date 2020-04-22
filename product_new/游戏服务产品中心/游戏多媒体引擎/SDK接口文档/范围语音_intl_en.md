This document describes how to access and debug GME APIs for the range voice feature.

GME range voice is a customized product specifically developed for games like PUBG. Different from team audio room, it has the following core capabilities:
1. It provides "Team Only" and "Everyone" audio modes unique to games like PUBG.
2. Relying on its range determination capability, it enables massive numbers of users to enable the mic for voice chat in the same audio room.



## Basic Concepts
#### 1. If the specified `TeamID` is not equal to 0 when the user enters the room, range audio room mode will be triggered.
#### 2. When the user enters a range audio room, there are two audio modes to choose from:

| Audio Mode | Parameter Name | Feature |
| -------- | ---------------------- | -------------------------------------------- |
| Everyone | RANGE_AUDIO_MODE_WORLD | In this mode, other users within a certain range can hear the user |
| Team only | RANGE_AUDIO_MODE_TEAM | Only teammates can hear the user |

#### 3. In different audio modes, the specific sound reachability is as follows:
a. Regardless of the distance and audio mode, two players on the same team can always hear each other.
b. If two players on different teams both enable the "Everyone" audio mode, they can hear each other within the range.

The specific sound reachability is as follows:
- If player A selects the option "Everyone", then the possible cases of sound reachability for player B in different audio modes will be as listed below:

| In the Same Team?	| Within the Range?	| Audio Mode	| Can A Hear B? 	| Can B Hear A?	|
| -----------------	| ------------ | ------------ |--------------------------	|--------------------------	|
| Yes 		| Yes 		 	|MODE_WORLD	| Yes		| Yes		|
| Yes		| Yes		 	|MODE_TEAM	| Yes		| Yes		|
| Yes		| No		 	|MODE_WORLD	| Yes		| Yes		|
| Yes		| No		 	|MODE_TEAM	| Yes		| Yes		|
| No 		| Yes		 	|MODE_WORLD	| Yes		| Yes		|
| No		| Yes			|MODE_TEAM	| No	| No	|
| No		| No		 	|MODE_WORLD	| No	| No	|
| No		| No			|MODE_TEAM	| No	| No	|

- If player A selects the option "Team Only", then the possible cases of sound reachability for player B in different audio modes will be as listed below:

| In the Same Team?	| Within the Range?	| Audio Mode	| Can A Hear B? 	| Can B Hear A?	|
| -----------------	| ------------ | ------------ |--------------------------	|--------------------------	|
| Yes 		| Yes 		 	|MODE_WORLD	| Yes		| Yes		|
| Yes		| Yes		 	|MODE_TEAM	| Yes		| Yes		|
| Yes		| No		 	|MODE_WORLD	| Yes		| Yes		|
| Yes		| No		 	|MODE_TEAM	| Yes		| Yes		|
| No		| Yes		 	|MODE_WORLD	| No	| No	|
| No		| Yes			|MODE_TEAM	| No	| No	|
| No		| No		 	|MODE_WORLD	| No	| No	|
| No		| No			|MODE_TEAM	| No	| No	|


#### 4. Notes on voice range:
 - No matter whether teammates are within the voice range, they can voice chat with each other.
 - To set the voice reception range, use the `UpdateAudioRecvRange` API.
 - Audio modes can be switched in real time in the range audio room. However, `TeamID` cannot be changed in the room, which must be specified before room entry.
 - To use range voice, room entry must be performed with smooth sound quality (i.e., RoomType = 1)



## Directions
Different from general team audio rooms, when the range voice feature is used, room entry must be performed with smooth sound quality, and the following two APIs must be called before `EnterRoom`:

### 1. Set `TeamID`
- The team ID can be set by this method, which must be called before `EnterRoom`; otherwise, it will directly return the error code `AV_ERR_ROOM_NOT_EXITED(1202)`.
- This parameter will not be automatically reset to 0 upon room exit; therefore, once you decide to call this audio mode, please call this method to set the `TeamID` before each call of `EnterRoom`.

#### Function prototype

```
ITMGContext SetRangeAudioTeamID(int teamID)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------
| teamID		|int    		| Team ID, which is used for upstream/downstream audio stream control in range voice. When `TeamID` is 0, the voice chat mode will be general team voice chat. The default value is 0.

### 2. Set `AudioMode`
- The audio mode can be modified by this method, which can be called either before or after room entry.
- Calling this method before room entry will affect the mode in the next room entry.
- Calling this method after room entry will directly change the current user's audio mode.
- This parameter will not be automatically reset to `MODE_WORLD` upon room exit; therefore, once you decide to call this method, please call it to set the `audioMode` before each call of `EnterRoom`.

#### Function prototype
  
```
ITMGRoom int SetRangeAudioMode(RANGE_AUDIO_MODE rangeAudioMode)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| rangeAudioMode    |int     | 0(MODE_WORLD) means "Everyone", while 1(MODE_TEAM) means "Team Only" |


### 3. Set the voice reception range
- This method is used to set the voice reception range (subject to game engine) and only can be called after successful room entry.
- This method must be used in conjunction with `UpdateSelfPosition` which updates the sound source position.

#### Function prototype 

```
ITMGRoom int UpdateAudioRecvRange(int range)
```

| Parameter | Type | Description |
| ------------- |-------------|-------------|
| range    |int         | Maximum audio reception range				|

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```

### 4. Update the sound source position
- This function is used to update the sound source position information and can be called only after successful room entry.
- In this product form, only position is required, while sound orientation is not.
- The distance between the sound source and the listener is determined through the combination of the source's `SelfPostion` and the listener's `SelfPostion` and `AudioRecvRange`.


#### Function prototype

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| Parameter | Type | Description |
| ------------- |-------------|-------------
| position   	|int[]		| Self-position; the coordinate order is front, right, and top |
| axisForward   |float[]  	| This parameter can be ignored in this product |
| axisRight    	|float[]  	| This parameter can be ignored in this product |
| axisUp    	|float[]  	| This parameter can be ignored in this product |
