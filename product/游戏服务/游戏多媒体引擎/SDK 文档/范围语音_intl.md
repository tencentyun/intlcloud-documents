## Overview

Thank you for using Tencent Cloud Game Multimedia Engine (GME) SDK. This document describes how to access GME's range voice service to make it easy for developers to debug and access the APIs of GME.


GME range voice is a customized product specifically developed for battle royale games. Different from team audio room, it has the following core capabilities:

#### 1. It provides "Team Only" and "Everyone" audio modes unique to battle royale games;

#### 2. Relying on its range determination capability, it enables massive numbers of users to turn on the microphone for voice chat in the same audio room.


## Basic Concepts

### 1. If the specified TeamID ! is 0 when the user enters the room, range audio room mode is triggered;

### 2. When the user enters a range audio room, there are two audio modes to choose from:

| Audio mode | Parameter name | Function |
| -------- | ---------------------- | -------------------------------------------- |
| Everyone | RANGE_AUDIO_MODE_WORLD | In this mode, other users within a certain range can hear the user |
| Team only | RANGE_AUDIO_MODE_TEAM | Only teammates can hear the user |

### 3. For different audio modes, the specific sound reachability is as follows:

  #### Suppose that player A selects the option "Everyone", the table below lists the possible cases of sound reachability for player B in different audio modes:

  | Are they in the same team?	| Are they within the range? 	| Audio mode	| Can A hear B? 	| Can B hear A?	|
  | -----------------	| ------------ | ------------ |--------------------------	|--------------------------	|
  | Yes 		| Yes 		 	|MODE_WORLD	| Yes		| Yes		|
  | Yes		| Yes		 	|MODE_TEAM	| Yes		| Yes		|
  | Yes		| No		 	|MODE_WORLD	| Yes		| Yes		|
  | Yes		| No		 	|MODE_TEAM	| Yes		| Yes		|
  | No 		| Yes		 	|MODE_WORLD	| Yes		| Yes		|
  | No		| Yes			|MODE_TEAM	| No	| No	|
  | No		| No		 	|MODE_WORLD	| No	| No	|
  | No		| No			|MODE_TEAM	| No	| No	|

  #### Suppose that player A selects the option "Team only", the table below lists the possible cases of sound reachability for player B in different audio modes:

  | Are they in the same team?	| Are they within the range? 	| Audio status	| Can A hear B? 	| Can B hear A?	|
  | -----------------	| ------------ | ------------ |--------------------------	|--------------------------	|
  | Yes 		| Yes 		 	|MODE_WORLD	| Yes		| Yes		|
  | Yes		| Yes		 	|MODE_TEAM	| Yes		| Yes		|
  | Yes		| No		 	|MODE_WORLD	| Yes		| Yes		|
  | Yes		| No		 	|MODE_TEAM	| Yes		| Yes		|
  | No		| Yes		 	|MODE_WORLD	| No	| No	|
  | No		| Yes			|MODE_TEAM	| No	| No	|
  | No		| No		 	|MODE_WORLD	| No	| No	|
  | No		| No			|MODE_TEAM	| No	| No	|


### 4. Notes for the voice range:
  - No matter whether teammates are within the voice range, they can voice chat with one another.
  - To set the voice reception range, use the UpdateAudioRecvRange API
  - Auido modes can be switched in real time in the range audio room. However, it is not supported to change the TeamID, which must be specified before entering the room.




## How to Use

Different from general team audio rooms, when using range voice capabilities, the following two APIs must be called before EnterRoom:

### 1. Set TeamID

- The team ID can be set by this method, which must be called before EnterRoom; otherwise, it will directly return the error code AV_ERR_ROOM_NOT_EXITED(1202)

- This parameter will not be automatically reset to 0 when exiting the room, so once it is decided to call this audio mode, please call this method to set the TeamID before each EnterRoom

#### Function Prototype
```
ITMGContext SetRangeAudioTeamID(int teamID)
```

| Parameter | Type | Meaning |
| ------------- |:-------------:|-------------
| teamID | int | Team ID, used for uplink/downlink audio stream control in range voice.				 When TeamID is 0, the voice chat mode is team voice chat; the default value is 0.

### 2. Set AudioMode

- The audio mode can be modified by this method, which can be called either before or after entering the room.

- Calling this method before entering the room affects the next time the user enters the room

- Calling this method after entering the room will directly change the current user's audio mode

- This parameter will not be automatically reset to MODE_WORLD when exiting the room, so once it is decided to call this method, please call this method to set the audioMode before each EnterRoom

> Function prototype
  
```
ITMGRoom int SetRangeAudioMode(RANGE_AUDIO_MODE rangeAudioMode)
```

| Parameter | Type | Meaning |
| ------------- |:-------------:|-------------|
| rangeAudioMode | int | 0(MODE_WORLD) means "Everyone", while 1(MODE_TEAM) means "Team only" |


### 3. Set Voice Reception Range

- This method is used to set the voice reception range (subject to the game engine) and only can be called after successfully entering the room
  
- This method must be used in conjunction with UpdateSelfPosition which updates the sound source position

#### Function Prototype 

```
ITMGRoom int UpdateAudioRecvRange(int range)
```

| Parameter | Type | Meaning |
| ------------- |-------------|-------------|
| range |int | Maximum audio reception range |				

#### Sample Code  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```

### 4. Update Sound Source Position

- This function is used to update the sound source position information and can be called only after successfully entering the room.

- In this product form, only the position is required and no sound orientation is required.

- The distance between the sound source and the listener is determined through the combination of the source's SelfPostion and the listener's SelfPostion and AudioRecvRange


#### Function Prototype

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| Parameter | Type | Meaning |
| ------------- |-------------|-------------|
| position   	|int[]		| Self-position; the coordinate order is front, right and top |
| axisForward   |float[]  	| Ignore in this product |
| axisRight    	|float[]  	| Ignore in this product |
| axisUp    	|float[]  	| Ignore in this product |
