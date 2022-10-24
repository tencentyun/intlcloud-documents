## 오디오/비디오 트랜스 코딩 템플릿[](id:vtrans)

### 일반 비디오 트랜스 코딩[](id:nvtrans)
MPS(Media Processing Service)는 스킴에 직접 추가할 수 있는 사전 설정된 오디오/비디오 트랜스 코딩 템플릿을 제공합니다. **템플릿 생성**을 클릭하여 자신만의 오디오/비디오 트랜스 코딩 템플릿을 사용자 지정할 수도 있습니다.

|  설정 항목| 설명 |
| --- | ----|
|    템플릿 이름    | 중국어, 영어, 숫자, 스페이스, 언더바(\_), 붙임표(-), 마침표(.)만 지원하며, 최대 64자까지 입력할 수 있습니다.    |  
|    컨테이너 형식    |    MP4, FLV, HLS    |  
|    설정 항목    |    비디오 매개변수, 오디오 매개변수    |  
|    비디오 코덱    |    ​​H.264, H.265, AV1    |  
|    비디오 비트 레이트    |  0 또는 [128, 35000]. 0은 원본 비디오 비트 레이트를 사용한다는 의미입니다    |  
|    비디오 해상도(px)    | 각 차원에 대해 0 또는 [128, 4096]. 0은 원본 해상도를 사용한다는 의미입니다  |  
|    프레임 레이트(fps)    | [0, 100]. 0은 원본 프레임 레이트를 사용하는 것을 의미합니다   |  
|    오디오 매개변수 인코딩 표준    |    AAC, MP3    |  
|    오디오 매개변수 샘플링 레이트    |    32000Hz, 44100Hz 및 48000Hz 의 기본 설정 샘플링 레이트        |  
|    오디오 매개변수 비트 레이트    |    0 또는 26kbps – 256kbps(0인 경우 원본 오디오의 비트 레이트 유지)    |  
|    오디오 매개변수 사운드 채널    |    싱글 사운드 채널, 듀얼 사운드 채널    |  

생성한 템플릿은 템플릿 리스트에 표시되며, 사용자 정의 템플릿을 조회, 편집, 삭제할 수 있습니다. 시스템 사전 설정 템플릿은 조회만 가능하며 편집 및 삭제는 지원하지 않습니다.

>? 컨테이너 형식이 MP4, FLV 또는 HLS로 설정된 경우 비디오 매개변수는 필수이고, 오디오 매개변수는 선택 사항입니다.

#### 사전 설정 템플릿

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">사양 레벨</th><th colspan="1" rowspan="2">템플릿 ID</th><th colspan="1" rowspan="2">컨테이너 형식(Format)</th><th colspan="4">비디오 매개변수</th><th colspan="4">오디오 매개변수</th></tr>
<tr><th colspan="1">해상도(Resolution)</th><th colspan="1">비트 레이트(Bitrate)</th><th colspan="1">프레임 레이트(FPS)</th><th colspan="1">코덱(Codec)</th><th colspan="1">비트 레이트(Bitrate)</th><th colspan="1">샘플링 레이트(SampleRate)</th><th colspan="1">오디오 사운드 채널 수(SoundSystem)</th><th colspan="1">코덱(Codec)</th></tr>
<tr><td colspan="1" rowspan="2">원활(FLU)</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 360</td><td colspan="1" rowspan="2">400kbps</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64kbps</td><td colspan="1" rowspan="12">44100Hz</td><td colspan="1" rowspan="12">스테레오(Stereo)</td><td colspan="1" rowspan="12">AAC</td></tr>
<tr><td colspan="1">100210</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">SD</td><td colspan="1">100020</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 540</td><td colspan="1" rowspan="2">1000kbps</td></tr>
<tr><td colspan="1">100220</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">HD</td><td colspan="1">100030</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 720</td><td colspan="1" rowspan="2">1800kbps</td><td colspan="1" rowspan="4">128kbps</td></tr>
<tr><td colspan="1">100230</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">FHD</td><td colspan="1">100040</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 1080</td><td colspan="1" rowspan="2">2500kbps</td></tr>
<tr><td colspan="1">100240</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">2K</td><td colspan="1">100070</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 1440</td><td colspan="1" rowspan="2">3000kbps</td><td colspan="1" rowspan="4">160kbps</td></tr>
<tr><td colspan="1">100270</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">4K</td><td colspan="1">100080</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 2160</td><td colspan="1" rowspan="2">6000kbps</td></tr>
<tr><td colspan="1">100280</td><td colspan="1">HLS</td></tr></tbody></table>

### TESHD 트랜스 코딩[](id:svtrans)
MPS는 스킴에 직접 추가할 수 있는 사전 설정된 Tencent Extreme Speed High Definition(TESHD) 템플릿을 제공합니다. **템플릿 생성**을 클릭하여 자신만의 TESHD 템플릿을 사용자 지정할 수도 있습니다.

|  설정 항목| 설명 |
| --- | ----|
|  템플릿 이름    |  중국어, 영어, 숫자, 스페이스, 언더바(\_), 붙임표(-), 마침표(.)만 지원하며, 최대 64자까지 입력할 수 있습니다.    |  
|  컨테이너 형식    |  MP4, FLV, HLS    |  
|  설정 항목    |  비디오 매개변수(필수), 오디오 매개변수(옵션)    |  
|  비디오 코덱    |  ​​H.264, H.265, AV1   |  
|  평균 비트 레이트 상한    |  이 매개변수를 비워두거나 0으로 설정하면 비트 레이트에 상한이 설정되지 않았음을 의미합니다    |  
|  비디오 해상도    |  각 차원에 대해 0 또는 [128, 4096]. 0은 원본 해상도를 사용한다는 의미입니다   |  
|  프레임 레이트    |  [0, 100]. 0은 원본 프레임 레이트를 사용하는 것을 의미합니다  |  
|  오디오 코덱    |  AAC, MP3    |  
|  오디오 샘플링 레이트    |  32000Hz, 44100Hz, 48000Hz의 기본 샘플링 레이트    |  
|  오디오 비트 레이트    |  0 또는 26kbps - 256kbps，0은 원본 비트 레이트를 사용하는 것을 의미합니다    |  
|  사운드 채널    |  모노 사운드 채널, 듀얼 사운드 채널    |  



>?
> - [MPS - 템플릿 설정](https://console.cloud.tencent.com/mps/templates?tab=tehd)에서 **사전 설정**된 TESHD 트랜스 코딩 템플릿을 볼 수 있습니다.
> - MP4, FLV, HLS의 컨테이너 형식 선택 시 비디오 매개변수를 반드시 설정해야 합니다.

생성한 템플릿은 템플릿 리스트에 표시되며, 사용자 정의 템플릿을 필터링 조회, 편집, 삭제할 수 있습니다. 시스템 사전 설정 템플릿은 조회만 가능하며 편집 및 삭제는 지원하지 않습니다.


### 오디오 트랜스 코딩[](id:atrans)
MPS는 스킴에 직접 추가할 수 있는 사전 설정된 오디오 트랜스 코딩 템플릿을 제공합니다. **템플릿 생성**을 클릭하여 나만의 오디오 트랜스 코딩 템플릿을 사용자 지정할 수도 있습니다.

|  설정 항목| 설명 |
| --- | ----|
| 템플릿 이름   | 중국어, 영어, 숫자, 스페이스, 언더바(\_), 붙임표(-), 마침표(.)만 지원하며, 최대 64자까지 입력할 수 있습니다.   |      
| 컨테이너 형식   | MP3, FLAC, OGG, M4A   |      
| 오디오 코덱   | <li>코덱은 컨테이너 형식이 MP3인 경우 MP3여야 하고 <li>컨테이너 형식이 FLAC 또는 OGG인 경우 FLAC이어야 하며 <li>컨테이너 형식이 M4A인 경우 MP3, AAC 또는 AC3일 수 있습니다   |      
| 샘플링 레이트   | 32000Hz, 44100Hz, 48000Hz의 기본 샘플링 레이트   |      
| 오디오 비트 레이트   | 0 또는 26kbps |    256kbps (0인 경우 원본 오디오의 비트 레이트 유지)   |      
| 사운드 채널   | 모노 사운드 채널, 듀얼 사운드 채널    |      

생성한 템플릿은 템플릿 리스트에 표시되며, 사용자 정의 템플릿을 조회, 편집, 삭제할 수 있습니다. 시스템 사전 설정 템플릿은 조회만 가능하며 편집 및 삭제는 지원하지 않습니다.

#### 사전 설정 템플릿
 
| 템플릿 ID | 컨테이너 형식(Format) | 오디오 비트 레이트(Bitrate) | 코덱(Codec) | 사운드 채널(SoundSystem) | 오디오 샘플링 레이트(SampleRate) |
| :------ | :----------------- | :------------------ | :------------ | :-------------------- | :--------------------- |
| 1100    | M4A                | 24kbps              | AAC           | 스테레오(Stereo)      | 44100Hz                |
| 1110    | M4A                | 48kbps              | AAC           | 스테레오(Stereo)      | 44100Hz                |
| 1120    | M4A                | 96kbps              | AAC           | 스테레오(Stereo)      | 44100Hz                |
| 1130    | M4A                | 192kbps             | AAC           | 스테레오(Stereo)      | 44100Hz                |
| 1140    | M4A                | 256kbps             | AAC           | 스테레오(Stereo)      | 44100Hz                |
| 1010    | MP3                | 128kbps             | MP3           | 스테레오(Stereo)      | 44100Hz                |
| 1020    | MP3                | 320kbps             | MP3           | 스테레오(Stereo)      | 44100Hz                |

