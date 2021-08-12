
Basic APIs for beauty filter, makeup filter, and animated widgets.

### setBeautyStyle

This API is used to set the beauty filter type.
```
void setBeautyStyle(int beautyStyle) 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| beautyStyle | int | Beauty filter style. 0: smooth; 1: natural; 2: misty. |

### setFilter

This API is used to specify the material filter effect.
```
void setFilter(Bitmap bmp)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| bmp | Bitmap | Filter image. |

>?Filter images must be in the PNG format. The filter lookup table image used in the demo is located in `app/src/main/res/drawable-xxhdpi/`.

***

### setFilterStrength

This API is used to set the strength of a filter.
```
void setFilterStrength(float strength)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| strength | float | Value range: 0-1. The larger the value, the more obvious the effect. Default value: 0.5. |

__Introduction__

In application scenarios such as shows, a high strength is required to highlight the characteristics of hosts. The default strength is 0.5, and if it is not sufficient, it can be adjusted with the following APIs.

***

### setGreenScreenFile

This API is used to set the green screen effect for videos. It works only in the Enterprise Edition.
```
boolean setGreenScreenFile(String path)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | String | Path to the video file, which can be in MP4 format. null: disable the effect. |

__Introduction__

The green screen feature here is not intelligent keying. It requires that a green screen exists behind the recorded person or object for further chroma keying.

### setBeautyLevel

This API is used to set the strength of the beauty filter.
```
void setBeautyLevel(int beautyLevel)
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| beautyLevel | int | Strength of the beauty filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |


### setWhitenessLevel

This API is used to set the strength of the skin brightening filter.
```
void setWhitenessLevel(int whitenessLevel)
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| whitenessLevel | int | Strength of the skin brightening filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |


### setRuddyLevel

This API is used to set the strength of the rosy skin filter.
```
void setRuddyLevel(int ruddyLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| ruddyLevel | int | Strength of the rosy skin filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |


### setEyeScaleLevel

This API is used to set the strength of the eye enlarging filter. It works only in the Enterprise Edition.
```
void setEyeScaleLevel(int eyeScaleLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| eyeScaleLevel | int | Strength of the eye enlarging filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |


### setFaceSlimLevel

This API is used to set the strength of the face slimming filter. It works only in the Enterprise Edition.
```
void setFaceSlimLevel(int faceSlimLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceSlimLevel | int | Strength of the face slimming filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setFaceVLevel

This API is used to set the strength of the chin slimming filter. It works only in the Enterprise Edition.
```
void setFaceVLevel(int faceVLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceVLevel | int | Strength of the chin slimming filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setChinLevel

This API is used to set the strength of the jaw shrinking or expanding filter. It works only in the Enterprise Edition.
```
void setChinLevel(int chinLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| chinLevel | int | Strength of the jaw shrinking or expanding filter. Value range: -9 to 9. 0 means disabling the filter. Values less than 0 mean shrinking the jaw, and values greater than 0 mean expanding the jaw. |

### setFaceShortLevel

This API is used to set the strength of the face shortening filter. It works only in the Enterprise Edition.
```
void setFaceShortLevel(int faceShortlevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceShortlevel | int | Strength of the face slimming filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |


### setNoseSlimLevel

This API is used to set the strength of the nose slimming filter. It works only in the Enterprise Edition.
```
void setNoseSlimLevel(int noseSlimLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| noseSlimLevel | int | Strength of the face slimming filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |


### setEyeLightenLevel

This API is used to set the strength of the eye brightening filter. It works only in the Enterprise Edition.
```
void setEyeLightenLevel(int eyeLightenLevel) 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| eyeLightenLevel | int | Strength of the eye brightening filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |


### setToothWhitenLevel

This API is used to set the strength of the teeth whitening filter. It works only in the Enterprise Edition.
```
void setToothWhitenLevel(int toothWhitenLevel) 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| toothWhitenLevel | int | Strength of the teeth whitening filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |


### setWrinkleRemoveLevel

This API is used to set the strength of the wrinkle removal filter. It works only in the Enterprise Edition.
```
void setWrinkleRemoveLevel(int wrinkleRemoveLevel)
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| wrinkleRemoveLevel | int | Strength of the wrinkle removal filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |


### setPounchRemoveLevel
This API is used to set the strength of the eye bag removal filter. It works only in the Enterprise Edition.
```
void setPounchRemoveLevel(int pounchRemoveLevel) 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| pounchRemoveLevel | int | Strength of the eye bag removal filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setSmileLinesRemoveLevel

This API is used to set the strength of the smile line removal filter. It works only in the Enterprise Edition.
```
void setSmileLinesRemoveLevel(int smileLinesRemoveLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| smileLinesRemoveLevel | int | Strength of the wrinkle removal filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setForeheadLevel
This API is used to set the strength of the hairline lowering filter. It works only in the Enterprise Edition.
```
void setForeheadLevel(int foreheadLevel)
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| foreheadLevel | int | Strength of the hairline lowering filter. Value range: 0-9. 0 means disabling the filter. The greater the value of 1-9, the lower the hairline. |

### setEyeDistanceLevel
This API is used to set the strength of the eye distance shortening filter. It works only in the Enterprise Edition.
```
void setEyeDistanceLevel(int eyeDistanceLevel) 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| eyeDistanceLevel | int | Strength of the eye distance shortening filter. Value range: 0-9. 0 means disabling the filter. The greater the value of 1-9, the shorter the eye distance. |

### setEyeAngleLevel
This API is used to set the strength of the eye tilting filter. It works only in the Enterprise Edition.
```
void setEyeAngleLevel(int eyeAngleLevel)
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| eyeAngleLevel | int | Strength of the eye tilting filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more upward the outer eye corners, and the more downward the inner eye corners. |

### setMouthShapeLevel
This API is used to set the strength of the mouth narrowing filter. It works only in the Enterprise Edition.

```
void setMouthShapeLevel(int mouthShapeLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mouthShapeLevel | int | Strength of the mouth narrowing filter. Value range: 0-9. 0 means disabling the filter. The greater the value of 1-9, the smaller the mouth. |

### setNoseWingLevel 
This API is used to set the strength of the nose wing narrowing filter. It works only in the Enterprise Edition.
```
void setNoseWingLevel(int noseWingLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| noseWingLevel | int | Strength of the nose wing narrowing filter. Value range: 0-9. 0 means disabling the filter. The greater the value of 1-9, the smaller the nose wing. |

### setNosePositionLevel
This API is used to set the nose position. It works only in the Enterprise Edition.
```
void setNosePositionLevel(int nosePositionLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| nosePositionLevel | int | Nose position level. Value range: 0-9. 0 means disabling the filter. The greater the value of 1-9, the lower the nose position. |

### setLipsThicknessLevel
This API is used to set the strength of the lip thickening filter. It works only in the Enterprise Edition.

```
void setLipsThicknessLevel(int lipsThicknessLevel)
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| lipsThicknessLevel | int | Strength of the lip thickening filter. Value range: 0-9. 0 means disabling the filter. The greater the value of 1-9, the thicker the lips. |

### setFaceBeautyLevel
This API is used to set the strength of the face shape filter. It works only in the Enterprise Edition.
```
void setFaceBeautyLevel(int faceBeautyLevel)
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceBeautyLevel | int | Strength of the face shape filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setMotionTmpl

This API is used to select AI animated effect widgets. It works only in the Enterprise Edition.
```
void setMotionTmpl(String motionPath)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| motionPath | String | Path to the animated effect. |


### setMotionMute

This API is used to mute or unmute animated effects. It works only in the Enterprise Edition. Some animated effects have audio effects, which can be disabled through this API when they are played back.
```
void setMotionMute(boolean motionMute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| motionMute | boolean | true: mute. false: unmute. |




