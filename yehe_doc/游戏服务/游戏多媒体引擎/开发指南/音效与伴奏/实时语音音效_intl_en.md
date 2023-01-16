This document describes the GME APIs for voice chat sound effect so that developers can easily debug and integrate them.


## Prerequisites

- **You have activated the voice chat service**. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- **You have integrated the GME SDK**, including core APIs and voice chat APIs. For more information, see [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), and [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545).
- You have successfully entered the voice room by using GME's voice chat feature and turned on the mic (EnableMic) and speaker (EnableSpeaker).


## APIs for Voice Chat Sound Effect
|API     | Description   |
| ------------- |:-------------:|
|PlayEffect    		| Plays back sound effect. |
|PauseEffect    	| Pauses sound effect. |
|PauseAllEffects	| Pauses all sound effects. |
|ResumeEffect    	| Resumes sound effect. |
|ResumeAllEffects	| Resumes all sound effects. |
|StopEffect 		| Stops sound effect. |
|StopAllEffects		| Stops all sound effects. |
|SetVoiceType 		| Sets voice changing effect. |
|SetKaraokeType 		| Sets karaoke sound effect. |
|GetEffectsVolume	| Obtains the volume of sound effects. |
|SetEffectsVolume 	| Sets the volume of sound effects. |


### Playing sound effect
The API PlayEffect is used to play sound effects. The sound effect ID, which represents an independent playback event, should be managed in the App. The playback can be controlled by this ID. The file supports the m4a, wav, and mp3 formats.

#### Function prototype  
```
ITMGAudioEffectCtrl virtual int PlayEffect(int soundId,  const char* filePath, bool loop, double pitch, double pan, double gain)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| soundId    	|int    		| Sound effect ID |
| filePath    	|char\*     	| Sound effect path						|
| loop    		|bool  	| Whether to repeat playback						|
| pitch    	|double	| Payback frequency. The default value is 1.0. Smaller value means slower playback speed and longer duration. 		|
| pan    		|double	| Sound channel, with values ranging from -1.0 to 1.0. The value -1.0 means only the left channel is enabled. 	|
| gain    		|double	| Gain volume, with values ranging from 0.0 to 1.0. The default value is 1.0.		|

#### Sample code  
```
double pitch = 1.0;
double pan = 0.0;
double gain = 0.0;
//Windows
ITMGContextGetInstance()->GetAudioEffectCtrl()->PlayEffect(soundId,filepath,true,pitch,pan,gain);
//Android
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PlayEffect(soundId,filePath,loop);
//iOS
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PlayEffect:soundId filePath:path loop:isLoop];
```


### Pausing sound effect
The API PauseEffect is used to pause sound effects.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int PauseEffect(int soundId)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| soundId    |int | Sound effect ID|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseEffect(soundId);
```

### Pausing all sound effects
The API PauseAllEffects is used to pause all sound effects.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int PauseAllEffects()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAllEffects();
```

### Resuming sound effect
The API ResumeEffect is used to resume sound effects.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int ResumeEffect(int soundId)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| soundId    |int | Sound effect ID|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeEffect(soundId);
```



### Resuming all sound effects
The API ResumeAllEffects is used to resume all sound effects.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int ResumeAllEffects()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAllEffects();
```


### Stopping sound effect
The API StopEffect is used to stop sound effects.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int StopEffect(int soundId)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| soundId    |int | Sound effect ID|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopEffect(soundId);
```

### Stopping all sound effects
The API StopAllEffects is used to stop all sound effects.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int StopAllEffects()
```


#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAllEffects();
```



### Setting voice changing effect
The API SetVoiceType is used to set voice changing effects.
#### Function prototype  
```
TMGAudioEffectCtrl int setVoiceType(int type)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| type    |int | Indicates the type of local voice changing effect.|



|Type parameter     |Value|Description|
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND  		|0	|Original		|
| ITMG_VOICE_TYPE_LOLITA    				|1	|Lolita			|
| ITMG_VOICE_TYPE_UNCLE  				|2	|Uncle			|
| ITMG_VOICE_TYPE_INTANGIBLE    			|3	|Ethereal			|
| ITMG_VOICE_TYPE_DEAD_FATBOY  			|4	|Fatty			|
| ITMG_VOICE_TYPE_HEAVY_MENTA			|5	|Heavy metal			|
| ITMG_VOICE_TYPE_DIALECT |6|Foreign|
| ITMG_VOICE_TYPE_INFLUENZA 				|7	|Catching cold			|
| ITMG_VOICE_TYPE_CAGED_ANIMAL 			|8	|Animal			|
| ITMG_VOICE_TYPE_HEAVY_MACHINE		|9	|Machine			|
| ITMG_VOICE_TYPE_STRONG_CURRENT		|10	|Strong current			|
| ITMG_VOICE_TYPE_KINDER_GARTEN			|11	|Kid			|
| ITMG_VOICE_TYPE_HUANG |12|Minion|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->setVoiceType(0);
```

### Setting karaoke sound effect
The API SetKaraokeType is used to set karaoke sound effects.
#### Function prototype  
```
TMGAudioEffectCtrl int SetKaraokeType(int type)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| type    |int                    |Indicates the type of local voice changing effect.|


|Type parameter     |Value|Description|
| ------------- |-------------|------------- |
|ITMG_KARAOKE_TYPE_ORIGINAL 		|0	|Original			|
|ITMG_KARAOKE_TYPE_POP 				|1	|Pop		|
|ITMG_KARAOKE_TYPE_ROCK 			|2	|Rock			|
|ITMG_KARAOKE_TYPE_RB 				|3	|Hip-hop			|
|ITMG_KARAOKE_TYPE_DANCE 			|4	|Dance			|
|ITMG_KARAOKE_TYPE_HEAVEN 			|5	|Ethereal			|
|ITMG_KARAOKE_TYPE_TTS 				|6	|Voice synthesis		|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetKaraokeType(0);
```

### Obtaining the volume of sound effects
The API GetEffectsVolume is used to obtain the volume of sound effects. The default value is 100. A value greater than 100 means "volume up", while a value less than 100 means "volume down".
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int GetEffectsVolume()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetEffectsVolume();
```

### Setting the volume of sound effects
The API SetEffectsVolume is used to set the volume of sound effects.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int SetEffectsVolume(int volume)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| volume    |int  | Volume value |

#### Sample code  
```
int volume=1;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetEffectsVolume(volume);
```
