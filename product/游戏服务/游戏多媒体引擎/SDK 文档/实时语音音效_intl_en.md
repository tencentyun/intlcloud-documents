This document describes the integration for real-time sound effect in details to help developers debug and integrate APIs for Tencent Cloud's Game Multimedia Engine (GME).


## Real-time sound effect APIs
|API     | Description   |
| ------------- |:-------------:|
|PlayEffect    		|Play sound effect|
|PauseEffect    	|Pause sound effect|
|PauseAllEffects	|Pause all sound effects|
|ResumeEffect    	|Resume sound effect|
|ResumeAllEffects	|Resume all sound effects|
|StopEffect 		|Stop sound effect|
|StopAllEffects		|Stop all sound effects|
|SetVoiceType 		|Set voice change effect|
|SetKaraokeType 		|Set karaoke effect|
|GetEffectsVolume	|Obtain volume of sound effect|
|SetEffectsVolume 	|Set volume of sound effect|


### Play sound effect
The PlayEffect API is used to play sound effect. The sound ID, which represents an independent playback event, should be managed in the App. The playback can be controlled by this ID. The file format supports m4a, wav, and mp3.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int PlayEffect(int soundId,  const char* filePath, bool loop, double pitch, double pan, double gain)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| soundId    	|int    		|Sound ID|
| filePath    	|char\*     	|Sound path						|
| loop    		|bool  	|Enable sound loop or not					|
| pitch    	|double	|Playback frequency. The default value is 1.0. Smaller value means slower playback speed and longer time.		|
| pan    		|double	|The channel, with a value ranging from -1.0 to 1.0. -1.0 means that only left channel is enabled.	|
| gain    		|double	|Gain volume, with a value ranging from 0.0 to 1.0,. The default value is 1.0.		|

####  Sample code  
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


### Pause sound effect
The PauseEffect API is used to pause sound effect.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int PauseEffect(int soundId)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| soundId    |int                    |Sound ID|

####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseEffect(soundId);
```

### Pause all sound effects
The PauseAllEffects API is used to pause all sound effects.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int PauseAllEffects()
```
####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAllEffects();
```

### Resume sound effect
The ResumeEffect API is used to resume sound effect.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int ResumeEffect(int soundId)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| soundId    |int                    |Sound ID|

####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeEffect(soundId);
```



### Resume all sound effects
The ResumeAllEffects API is used to resume all sound effects.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int ResumeAllEffects()
```
####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAllEffects();
```

### Stop sound effect
The StopEffect API is used to stop sound effect.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int StopEffect(int soundId)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| soundId    |int                    |Sound ID|

####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopEffect(soundId);
```

### Stop all sound effects
The StopAllEffects API is used to stop all sound effects.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int StopAllEffects()
```


#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAllEffects();
```



### Set voice effect
The SetVoiceType API is used to set voice change effect.
#### Function prototype  
```
TMGAudioEffectCtrl int setVoiceType(int type)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| type    |int                    |Indicates the voice change type of the audio in local end|



|Parameter type     |Value|Description|
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND  		|0	|Original			|
| ITMG_VOICE_TYPE_LOLITA    				|1	|Lolita			|
| ITMG_VOICE_TYPE_UNCLE  				|2	|Uncle			|
| ITMG_VOICE_TYPE_INTANGIBLE    			|3	|Soul			|
| ITMG_VOICE_TYPE_DEAD_FATBOY  			|4	|Homebody			|
| ITMG_VOICE_TYPE_HEAVY_MENTA			|5	|Heavy metal			|
| ITMG_VOICE_TYPE_DIALECT 				|6	|Foreign			|
| ITMG_VOICE_TYPE_INFLUENZA 				|7	|Influenza			|
| ITMG_VOICE_TYPE_CAGED_ANIMAL 			|8	|Animal			|
| ITMG_VOICE_TYPE_HEAVY_MACHINE		|9	|Machine			|
| ITMG_VOICE_TYPE_STRONG_CURRENT		|10	|Strong current			|
| ITMG_VOICE_TYPE_KINDER_GARTEN			|11	|Kid			|
| ITMG_VOICE_TYPE_HUANG 					|12	|Minions			|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->setVoiceType(0);
```

### Set karaoke effect
The SetKaraokeType API is used to set karaoke effect.
####  Function prototype  
```
TMGAudioEffectCtrl int SetKaraokeType(int type)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| type    |int                    |Indicates the voice change type of the audio in local end|


|Parameter type     |Value|Description|
| ------------- |-------------|------------- |
|ITMG_KARAOKE_TYPE_ORIGINAL 		|0	|Original			|
|ITMG_KARAOKE_TYPE_POP 				|1	|Popular			|
|ITMG_KARAOKE_TYPE_ROCK 			|2	|Rock			|
|ITMG_KARAOKE_TYPE_RB 				|3	|Hip hop			|
|ITMG_KARAOKE_TYPE_DANCE 			|4	|Dance			|
|ITMG_KARAOKE_TYPE_HEAVEN 			|5	|Soul			|
|ITMG_KARAOKE_TYPE_TTS 				|6	|Voice synthesis		|

####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetKaraokeType(0);
```

### Obtain volume of sound effect
The GetEffectsVolume API is used to obtain volume of sound effect. It is linear volume with a default value of 100. If the value is greater than 100, the volume is increased; and if the value is less than 100, the volume is decreased.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int GetEffectsVolume()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetEffectsVolume();
```

### Set volume of sound effect
The SetEffectsVolume  API is used to set volume of sound effect.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int SetEffectsVolume(int volume)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| volume    |int                    |Sound effect volume|

#### Sample code  
```
int volume=1;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetEffectsVolume(volume);
```

