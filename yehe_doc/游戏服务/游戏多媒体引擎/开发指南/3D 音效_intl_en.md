This document describes how to integrate with and debug GME APIs for 3D sound effects.

## Use Cases

In general voice chat for room entry, the player voice has no 3D sound effects, and players can only have simple interactions with each other. With the 3D sound effect, players can expose their direction and position information while speaking, and their voice can change in real time along with the distance. The 3D sound effect feature delivers players a more real and immersive communication and battle experience in battle royale games.

Click [here](https://intl.cloud.tencent.com/document/product/607/50220) to download the demo and try out the 3D sound effect.

## Prerequisites

- **Activated Voice Chat Service**: See [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782)**.
- **You have integrated the GME SDK**, including core APIs and voice chat APIs. For more information, see [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), and [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545).

## Directions

### Implementation flowchart

The 3D sound effect implementation flowchart is as follows. The blue part is new integration steps compared with general voice chat for room entry:
<img src="https://qcloudimg.tencent-cloud.cn/raw/af3b21c8c6ff552c887ee369f9c217c6.jpg" width="500px">

### Initializing the 3D sound effect engine

This function is used to initialize the 3D sound effect engine and needs to be called after room entry. You must call this API before using the 3D sound effect, even if you want to enable only the 3D sound effect reception rather than the 3D sound effect playback.

#### Function prototype 

```
public abstract int InitSpatializer(string modelPath)
```

| Parameter | Type | Description |
| --------- | ------ | ------------------------- |
| modelPath | string | The absolute path of the 3D sound effect resource file |

The 3D sound effect resource file needs to be downloaded to your local disk, please select one according to the SDK version:

- For SDK versions earlier than 2.8, click [here](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_2.X_3d_model) to download (MD5: d0b76aa64c46598788c2f35f5a8a8694).
- For SDK 2.8-2.9.5, click [here](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/public/GME_2.8_3d_model.dat) to download (MD5: 3d4d04b3949e267e34ca809e8a0b9243).
- For SDK 2.9.6 or later, as 3D sound effect resource files are embedded, you can leave `modelPath` empty.

For GME SDK release updates, see [Product Updates](https://intl.cloud.tencent.com/document/product/607/35323).

<dx-alert infotype="explain" title="About resource path">

- Taking Unity as an example, we recommend you put the 3D sound effect resource file in the `StreamingAssets` directory of the project and copy it to the corresponding directory of different platforms based on the content of the **copyFileFromAssetsToPersistent** function in `SampleCode`.
- Taking Unreal Engine as an example, copy the 3D model file and read the path based on the content of the **CopyAllAssetsToExternal** function in `SampleCode`.
  </dx-alert>

### Enabling or disabling the 3D sound effect

This function is used to enable or disable the 3D sound effect. You can hear the 3D sound after enabling it.

#### Function prototype

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)
```

| Parameter        | Type | Description                                              |
| ----------- | ---- | ------------------------------------------------- |
| enable      | bool | You can hear the 3D sound effect after enabling it                           |
| applyToTeam | bool | Specifies whether the 3D sound effect is enabled within the team and takes effect only when `enable` is `true` |

### Obtaining the status of 3D sound effect

This function is used to obtain the status of 3D sound effect.

#### Function prototype 

```
public abstract bool IsEnableSpatializer()
```

| Returned Value | Description |
| ------ | -------- |
| true   | Enabled |
| false  | Disabled |

### Setting the 3D sound effect attenuation range

The 3D sound effect attenuation range needs to be set. We recommend you set it to `100`.

#### The relationship between distance and sound attenuation

In the 3D sound effect, the sound will begin to attenuate to almost zero as the distance to the sound source exceeds a specified threshold (range/10).

| Distance (Unit in Engine) | Attenuation Coefficient                     |
| -------------------- | ---------------------------- |
| 0 < N < range/10     | 1.0 (no attenuation) |
| N ≥ range/10 | range/10/N         |

![](https://qcloudimg.tencent-cloud.cn/raw/4aece18def3601de5380e62406af7f13.jpg)

#### Function prototype

```
public abstract void UpdateAudioRecvRange(int range)
```

| Parameter  | Type | Description                                       |
| ----- | ---- | ------------------------------------------------------------ |
| range | int  | The range within which the sound effect can be heard in distance unit used by the game engine. We recommend you set it to `100`. |



### Updating the sound source position (including orientation)

This function is used to update the position information of the sound source. It can be called every frame to implement the 3D sound effect.

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

### Local position API (for VR scenarios)

This API is suitable for scenarios with high requirements for 3D position changes on VR devices. This feature is an advanced API and can be used only on GME 2.9.2 or later.

- In general 3D scenarios, the user only needs to use the `UpdateSelfPosition` function to update the position information and send it to other users over the network. `UpdateOtherPosition` can also pass in the position information of other players locally without using the network, making it suitable for VR game scenarios.
- To avoid conflicting with the remotely updated coordinates, if you call `UpdateOtherPosition`, remote coordinates will be discarded, which will affect the next room entry. Therefore, **to update the player coordinates locally, update the coordinates of all players**.

#### Function prototype

```
public abstract int UpdateOtherPosition(int position[3])
```

| Parameter | Type | Description |
| -------- | ----- | ---------------------------------------------- |
| position | int[] | Remote position. The coordinate order is front, right, and top |



<dx-alert infotype="notice" title="Note">
To update player coordinates locally, traverse **all player coordinates** and pass them in through this API.
</dx-alert>

### 3D sound effect blocklist API

> !This API takes effect on GME SDK 2.9.3 or later.

Currently, the 3D sound effect feature will take effect for all users in the room after being called. However, in some special scenarios, you may not want to see that someone's voice attenuates because of the 3D sound effect. In this case, you can call this API to add the user to the 3D sound effect blocklist, and voice of the specified `openid` will no longer have the 3D sound effect.

```
virtual int AddSpatializerBlacklist(const char* openId); 
```

To remove the `openid` from the blocklist, you need to call the following API:

```
virtual int RemoveSpatializerBlacklist(const char* openId); 
```

To clear the blocklist, you need to call the following API:

```
virtual int ClearSpatializerBlacklist(); 
```

## Troubleshooting

If the voice has no 3D sound effects after this feature is connected, you can troubleshoot as follows:

1. Check whether users have successfully entered the room, turned on the mic, and can hear each other.
2. Check whether a stereo headset is used.
3. Check whether the returned value of `InitSpatializer` is `0`.
4. Check whether the value of `UpdateAudioRecvRange` is too small.
5. Check whether the `UpdateSelfPosition` API is called periodically.
6. Troubleshoot the problem by referring to [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223).


