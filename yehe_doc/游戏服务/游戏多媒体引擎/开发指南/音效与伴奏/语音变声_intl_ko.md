

이 문서는 음성 변조 효과를 위해 GME(Game Multimedia Engine) API와 통합하고 디버깅하는 방법을 설명합니다.


## 시나리오


![](https://qcloudimg.tencent-cloud.cn/raw/d7d75633180f90d9357650a7d7493f4d.png)

## 전제 조건

- **음성 채팅 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **음성-텍스트 변환 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME SDK 통합**: 핵심 API 및 음성 채팅 API를 포함합니다. 자세한 내용은 [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.
- **GME SDK의 libgmesoundtouch 라이브러리 파일 통합**: 프로젝트의 라이브러리 파일에 libgmesoundtouch가 포함되어 있는지 확인하십시오. 자세한 내용은 [Library files' corresponding features](https://intl.cloud.tencent.com/document/product/607/32363)를 참고하십시오.

## 실시간 음성 변조 통합

### 음성 변조 API
성공적인 방 입장 및 마이크 활성화 후, SetVoiceType API를 호출하여 음성 변조 효과를 설정합니다. API가 0을 반환하면 호출이 성공한 것이고 방에 있는 사용자에게 들리는 로컬 사운드가 음성 변조 효과를 갖습니다. 음성 변조 효과를 테스트하려면 인이어 모니터링 기능(API: EnableLoopBack)을 사용하십시오.

#### 함수 프로토타입  


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


|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| type    |int                    |로컬 음성 변조 효과의 종류를 나타냅니다|


|유형 매개변수     |값|설명|
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND  |0|오리지널|
| ITMG_VOICE_TYPE_LOLITA    |1|로리타|
| ITMG_VOICE_TYPE_UNCLE  |2|삼촌|
| ITMG_VOICE_TYPE_INTANGIBLE    |3|오묘한|
| ITMG_VOICE_TYPE_DEAD_FATBOY  |4|통통이|
| ITMG_VOICE_TYPE_HEAVY_MENTA|5|헤비메탈|
| ITMG_VOICE_TYPE_DIALECT |6|외국인|
| ITMG_VOICE_TYPE_INFLUENZA |7|감기|
| ITMG_VOICE_TYPE_CAGED_ANIMAL |8|동물|
| ITMG_VOICE_TYPE_HEAVY_MACHINE|9|기계|
| ITMG_VOICE_TYPE_STRONG_CURRENT|10|강한 전류|
| ITMG_VOICE_TYPE_KINDER_GARTEN|11|유치원|
| ITMG_VOICE_TYPE_HUANG |12|미니언|

#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->setVoiceType(0);
```


## 음성 메시지에 대한 음성 변조 통합

### 음성 메시지에 대한 음성 변조 프로세스
![](https://qcloudimg.tencent-cloud.cn/raw/490623c6f98fa3d2378a3946d818adc0.png)

음성 변조 효과는 재생 중에만 반영되므로 음성 변조는 원본 음성 메시지에는 영향을 미치지 않습니다.

#### 음성 메시지 재생

음성 메시지 재생 API 호출 시 음성 변조 매개변수를 추가합니다.

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

| 매개변수      |  유형  | 설명                                                         |
| --------- | :----: | ------------------------------------------------------------ |
| filePath  | string | 로컬 오디오 파일 경로                                           |
| voicetype |  int   | 음성 변조 유형 |

#### 오류 코드

| 오류 코드 값 | 원인       | 솔루션 제안                       |
| -------- | ---------- | ------------------------------ |
| 20485    | 재생이 시작되지 않습니다 | 파일의 존재와 파일 경로의 유효성을 확인하십시오 |
