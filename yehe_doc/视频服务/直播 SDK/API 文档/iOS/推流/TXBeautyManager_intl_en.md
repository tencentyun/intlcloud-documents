
Basic APIs for beauty filter, makeup filter, and animated widgets.

### setBeautyStyle 

This API is used to set the beauty filter type. 
```
- (void)setBeautyStyle:(TXBeautyStyle)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | TXBeautyStyle | Beauty filter style. `TXBeautyStyleSmooth` indicates smooth; `TXBeautyStyleNature` indicates natural; and `TXBeautyStylePitu` indicates misty. |


### setFilter

This API is used to specify the material filter effect.
```
- (void)setFilter:(TXImage *)image 
```

>?Filter images must be in the PNG format. The filter lookup table image used in the demo is located in `TXLiteAVDemo/Resource/Beauty/filter/FilterResource.bundle`.

***

### setSpecialRatio

This API is used to set the strength of a filter.
```
- (void)setFilterStrength:(float)strength 
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
- (void)setGreenScreenFile:(NString *)file 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| file | NString * | Path to the video file, which can be in MP4 format. nil: disable the effect. |

__Introduction__

The green screen feature here is not intelligent keying. It requires that a green screen exists behind the recorded person or object for further chroma keying.

### setBeautyLevel

This API is used to set the strength of the beauty filter.
```
- (void)setBeautyLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the beauty filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect.  |

### setWhitenessLevel

This API is used to set the strength of the skin brightening filter.
```
- (void)setWhitenessLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the skin brightening filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setRuddyLevel

This API is used to set the strength of the rosy skin filter.
```
- (void)setRuddyLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the rosy skin filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setEyeScaleLevel

This API is used to set the strength of the eye enlarging filter. It works only in the Enterprise Edition.
```
- (void)setEyeScaleLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the eye enlarging filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setFaceSlimLevel

This API is used to set the strength of the face slimming filter. It works only in the Enterprise Edition.
```
- (void)setFaceSlimLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the face slimming filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setFaceVLevel

This API is used to set the strength of the chin slimming filter. It works only in the Enterprise Edition.
```
- (void)setFaceVLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the chin slimming filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setChinLevel

This API is used to set the strength of the jaw shrinking or expanding filter. It works only in the Enterprise Edition.
```
- (void)setChinLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the jaw shrinking or expanding filter. Value range: -9 to 9. 0 means disabling the filter. Values less than 0 mean shrinking the jaw, and values greater than 0 mean expanding the jaw. |

### setFaceShortLevel

This API is used to set the strength of the face shortening filter. It works only in the Enterprise Edition.
```
- (void)setFaceShortLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the face shortening filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setNoseSlimLevel

This API is used to set the strength of the nose slimming filter. It works only in the Enterprise Edition.
```
- (void)setNoseSlimLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the nose slimming filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setEyeLightenLevel

This API is used to set the strength of the eye brightening filter. It works only in the Enterprise Edition.
```
- (void)setEyeLightenLevel:(float)level 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the eye brightening filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setToothWhitenLevel

This API is used to set the strength of the teeth whitening filter. It works only in the Enterprise Edition.
```
- (void)setToothWhitenLevel:(float)level 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the teeth whitening filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setWrinkleRemoveLevel

This API is used to set the strength of the wrinkle removal filter. It works only in the Enterprise Edition.
```
- (void)setWrinkleRemoveLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the wrinkle removal filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setPounchRemoveLevel
This API is used to set the strength of the eye bag removal filter. It works only in the Enterprise Edition.
```
- (void)setPounchRemoveLevel:(float)level 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the eye bag removal filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setSmileLinesRemoveLevel

This API is used to set the strength of the smile line removal filter. It works only in the Enterprise Edition.
```
- (void)setSmileLinesRemoveLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the smile line removal filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setForeheadLevel
This API is used to set the strength of the hairline lowering filter. It works only in the Enterprise Edition.
```
- (void)setForeheadLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the hairline lowering filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the lower the hairline. |

### setEyeDistanceLevel
This API is used to set the strength of the eye distance shortening filter. It works only in the Enterprise Edition.
```
- (void)setEyeDistanceLevel:(float)level 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the eye distance shortening filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the shorter the eye distance. |

### setEyeAngleLevel
This API is used to set the strength of the eye tilting filter. It works only in the Enterprise Edition.
```
- (void)setEyeAngleLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the eye tilting filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more upward the outer eye corners, and the more downward the inner eye corners. |


### setMouthShapeLevel
This API is used to set the strength of the mouth narrowing filter. It works only in the Enterprise Edition.

```
- (void)setMouthShapeLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the mouth narrowing filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the smaller the mouth. |

### setNoseWingLevel
This API is used to set the strength of the nose wing narrowing filter. It works only in the Enterprise Edition.
```
- (void)setNoseWingLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the nose wing narrowing filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the smaller the nose wing. |


### setNosePositionLevel
This API is used to set nose position. It works only in the Enterprise Edition.
```
- (void)setNosePositionLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Nose position level. Value range: 0-9. 0 means disabling the filter. The larger the value, the lower the nose position. |

### setLipsThicknessLevel
This API is used to set the strength of the lip thickening filter. It works only in the Enterprise Edition.

```
- (void)setLipsThicknessLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the lip thickening filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the thicker the lips. |

### setFaceBeautyLevel
This API is used to set the strength of the face shape filter. It works only in the Enterprise Edition.
```
- (void)setFaceBeautyLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Strength of the face shape filter. Value range: 0-9. 0 means disabling the filter. The larger the value, the more obvious the effect. |

### setMotionTmpl

This API is used to select AI animated effect widgets. It works only in the Enterprise Edition.
```
- (void)setMotionTmpl:(nullable NSString *)tmplName inDir:(nullable NSString *)tmplDir
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| tmplDir | NSString * | Directory of the animated effect. |
| tmplName | NSString * | Animated effect name. |

### setMotionMute

This API is used to mute animated effects. It works only in the Enterprise Edition. Some animated effects have audio effects, which can be disabled through this API when they are played back.
```
- (void)setMotionMute:(BOOL)motionMute
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| motionMute | BOOL | YES: mute. NO: unmute. |

 

