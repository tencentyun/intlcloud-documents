

This document describes how to integrate with and debug GME APIs for voice changing effects.


## Overview


![](https://staticintl.cloudcachetci.com/yehe/backend-news/Vst2098_d7d75633180f90d9357650a7d7493f4d.png)

## Prerequisites

- **You have activated the voice chat service**. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- **You have activated the speech-to-text service**. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- **You have integrated the GME SDK**, including core APIs and voice chat APIs. For more information, see [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), and [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545).
- **You have integrated the `libgmesoundtouch` library file of the GME SDK**. Ensure that the project's library files include `libgmesoundtouch`. For more information, see [SDK Version Upgrade Guide](https://intl.cloud.tencent.com/document/product/607/32363).

## Integrating Real-Time Voice Changing

### Voice changing API
After successful room entry and mic enablement, call the `SetVoiceType` API to set the voice changing effect. If the API returns 0, the call is successful, and the local sound heard by users in the room has the voice changing effect. To test the effect, use the in-ear monitoring feature (API: EnableLoopBack).

#### Function prototype  


<dx-codeblock>
::: Android  java
    public static class ITMG_VoiceType {
        public static final int ITMG_VOICE_TYPE_ORIGINAL_SOUND = 0;
        public static final int ITMG_VOICE_TYPE_LOLITA = 1;   
        public static final int ITMG_VOICE_TYPE_UNCLE = 2;  
        public static final int ITMG_VOICE_TYPE_INTANGIBLE = 3; 
        public static final int ITMG_VOICE_TYPE_DEAD_FATBOY = 4; 
        public static final int ITMG_VOICE_TYPE_HEAVY_MENTAL = 5;
        public static final int ITMG_VOICE_TYPE_DIALECT = 6; 
        public static final int ITMG_VOICE_TYPE_INFLUENZA = 7;
        public static final int ITMG_VOICE_TYPE_CAGED_ANIMAL = 8; 
        public static final int ITMG_VOICE_TYPE_HEAVY_MACHINE = 9;
        public static final int ITMG_VOICE_TYPE_STRONG_CURRENT = 10;
        public static final int ITMG_VOICE_TYPE_KINDER_GARTEN = 11; 
        public static final int ITMG_VOICE_TYPE_HUANG = 12;
    };
    public abstract int SetVoiceType(int type);
:::
::: iOS objectc
-(QAVResult)SetVoiceType:(ITMG_VOICE_TYPE) type 
:::
::: Unity C#		
public abstract class ITMGAudioEffectCtrl{
	public static int VOICE_TYPE_ORIGINAL_SOUND = 0;
	public static int VOICE_TYPE_LOLITA = 1;		
	public static int VOICE_TYPE_UNCLE = 2;			
	public static int VOICE_TYPE_INTANGIBLE = 3;	
	public static int VOICE_TYPE_DEAD_FATBOY = 4;	
	public static int VOICE_TYPE_HEAVY_MENTAL = 5;	 
	public static int VOICE_TYPE_DIALECT = 6;		
	public static int VOICE_TYPE_INFLUENZA = 7;		
	public static int VOICE_TYPE_CAGED_ANIMAL = 8;	
	public static int VOICE_TYPE_HEAVY_MACHINE = 9;	
	public static int VOICE_TYPE_STRONG_CURRENT = 10;
	public static int VOICE_TYPE_KINDER_GARTEN = 11;
	public static int VOICE_TYPE_HUANG = 12;
	public abstract int SetVoiceType(int voiceType);
}
:::
::: C++ c++
class ITMGAudioEffectCtrl {
public:
    virtual ~ITMGAudioEffectCtrl(){};
    virtual int SetVoiceType(ITMG_VOICE_TYPE voiceType) = 0;
}
:::
</dx-codeblock>


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
| ITMG_VOICE_TYPE_HUANG |12|Urchin|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->setVoiceType(0);
```


## Integrating Voice Changing for Voice Message

### Process
![](https://qcloudimg.tencent-cloud.cn/raw/490623c6f98fa3d2378a3946d818adc0.png)

Voice changing doesn't affect the original voice message, as the voice changing effect will be reflected only during playback.

#### Voice message playback

Add voice changing parameters when calling the voice message playback API.

<dx-codeblock>
::: Android  java
public abstract int PlayRecordedFile(String filePath,int voicetype);
:::
::: iOS objectc
-(int)PlayRecordedFile:(NSString*)filePath VoiceType:(ITMG_VOICE_TYPE) type
:::
::: Unity c#
ITMGPTT PlayRecordedFile(string filePath,int voiceType);
:::
::: C++ c++
public abstract int PlayRecordedFile(string filePath,int voiceType);
:::
</dx-codeblock>

| Parameter | Type | Description |
| --------- | :----: | ------------------------------------------------------------ |
| filePath | string | Local audio file path |
| voicetype |  int   | Voice changer type |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------- | ------------------------------ |
| 20485 | Playback is not started. | Ensure the existence of the file and the validity of the file path. |
