
Basic functions for beauty filter, makeup filter, and animated effect pendants.

### setBeautyStyle

This API is used to set beauty filter type. 
```
- (void)setBeautyStyle:(TXBeautyStyle)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | TXBeautyStyle | Beauty filter style. `TXBeautyStyleSmooth` indicates smooth; `TXBeautyStyleNature` indicates natural; and `TXBeautyStylePitu` indicates misty |

### setBeautyLevel

This API is used to set effect level of the beauty filter.
```
- (void)setBeautyLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the beauty filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setWhitenessLevel

This API is used to set effect level of the brightening filter.
```
- (void)setWhitenessLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the brightening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setRuddyLevel

This API is used to set effect level of the rosy skin filter.
```
- (void)setRuddyLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the rosy skin filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setEyeScaleLevel

This API is used to set effect level of the eye enlarging filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setEyeScaleLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the eye enlarging filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setFaceSlimLevel

This API is used to set effect level of the face slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setFaceSlimLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the face slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setFaceVLevel

This API is used to set effect level of the chin slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setFaceVLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the chin slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setChinLevel

This API is used to set effect level of the chin lengthening/shortening or shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setChinLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the chin lengthening/shortening filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates that the chin is shortened, while a value greater than 0 indicates that the chin is lengthened. |

### setFaceShortLevel

This API is used to set effect level of the face shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setFaceShortLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the face shortening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setNoseSlimLevel

This API is used to set effect level of the nose slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setNoseSlimLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the nose slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setEyeLightenLevel

This API is used to set effect level of the eye brightening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setEyeLightenLevel:(float)level 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the eye brightening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setToothWhitenLevel

This API is used to set effect level of the teeth whitening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setToothWhitenLevel:(float)level 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the teeth whitening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setWrinkleRemoveLevel

This API is used to set effect level of the wrinkle removal filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setWrinkleRemoveLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the wrinkle removal filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setPounchRemoveLevel
This API is used to set effect level of the eye bag removal filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setPounchRemoveLevel:(float)level 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the eye bag removal filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setSmileLinesRemoveLevel

This API is used to set effect level of the smile line removal filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setSmileLinesRemoveLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the smile line removal filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setForeheadLevel
This API is used to set effect level of the hairline lowering filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setForeheadLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the hairline lowering filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the lower the hairline. |

### setEyeDistanceLevel
This API is used to set effect level of the eye distance shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setEyeDistanceLevel:(float)level 
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the eye distance shortening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the shorter the eye distance. |

### setEyeAngleLevel
This API is used to set effect level of the eye tilting filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setEyeAngleLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the eye tilting filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more upward the outer eye corners, and the more downward the inner eye corners. |


### setMouthShapeLevel
This API is used to set effect level of the mouth narrowing filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).

```
- (void)setMouthShapeLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the mouth narrowing filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the smaller the mouth. |

### setNoseWingLevel
This API is used to set effect level of the nose wing narrowing filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setNoseWingLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the nose wing narrowing filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the smaller the nose wing. |


### setNosePositionLevel
This API is used to set nose position (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setNosePositionLevel:(float)level
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Nose position level. Value range: 0–9; 0 indicates that the effect is disabled, and the greater the value, the lower the nose position. |

### setLipsThicknessLevel
This API is used to set effect level of the lip thickening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).

```
- (void)setLipsThicknessLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the lip thickening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the thicker the lips. |

### setFaceBeautyLevel
This API is used to set effect level of the face shape filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setFaceBeautyLevel:(float)level
```
__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | float | Effect level of the face shape filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

### setMotionTmpl

This API is used to select AI animated effect pendant (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setMotionTmpl:(nullable NSString *)tmplName inDir:(nullable NSString *)tmplDir
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| tmplDir | NSString * | Directory of the animated effect. |
| tmplName | NSString * | Animated effect name. |

### setMotionMute

This API is used to mute animated effect (it takes effect only in TRTC Commercial edition and is invalid in other editions). Some animated effects have audio effects, which can be disabled through this API when they are played back.
```
- (void)setMotionMute:(BOOL)motionMute
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| motionMute | BOOL | YES: mutes; NO: does not mute. |

 

