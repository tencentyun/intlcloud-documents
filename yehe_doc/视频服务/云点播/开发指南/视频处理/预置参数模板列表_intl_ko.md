VOD는 복잡한 매개변수 세트 대신 매개변수 템플릿을 사용한 비디오 처리 시작을 지원합니다. 다양한 비디오 처리 상황에 대해 VOD는 매개변수 템플릿을 사전 설정합니다.

## 비디오 변환 클래스

비디오 변환 클래스의 사전 설정 매개변수 템플릿에는 다음 유형이 포함됩니다.
- 사전 설정 트랜스 코딩 템플릿
- 사전 설정 리먹싱 템플릿
- 사전 설정 gif 템플릿
- 사전 설정 지정 시점 화면 캡처 템플릿
- 사전 설정 샘플링 화면 캡처 템플릿
- 사전 설정 스프라이트 이미지 템플릿
- 사전 설정 자동 맞춤 전환 코드 스트림 템플릿

[](id:transcoding)
### 사전 설정 트랜스 코딩 템플릿
#### 비디오 트랜스 코딩 포맷

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">사양 레벨</th><th colspan="1" rowspan="2">템플릿 ID</th><th colspan="1" rowspan="2">컨테이너 형식(Format)</th><th colspan="4">비디오 매개변수</th><th colspan="4">오디오 매개변수</th></tr>
<tr><th colspan="1">해상도(Resolution)</th><th colspan="1">비트 레이트(Bitrate)</th><th colspan="1">프레임 레이트(FPS)</th><th colspan="1">코덱(Codec)</th><th colspan="1">비트 레이트(Bitrate)</th><th colspan="1">샘플링 레이트(SampleRate)</th><th colspan="1">오디오 사운드 채널 수(SoundSystem)</th><th colspan="1">코덱(Codec)</th></tr>
<tr><td colspan="1" rowspan="2">FLU</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 360</td><td colspan="1" rowspan="2">400kbps</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64kbps</td><td colspan="1" rowspan="12">44100Hz</td><td colspan="1" rowspan="12">스테레오(Stereo)</td><td colspan="1" rowspan="12">AAC</td></tr>
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

#### 오디오 형식 트랜스코딩[](id:music)

<table>
    <tr>
        <th rowspan=1>
            템플릿 ID                
        </th>
        <th rowspan=1>
            컨테이너 형식(Format)
        </th>
        <th>
            오디오 비트 레이트(Bitrate)
        </th>
        <th>
            코덱(Codec)
        </th>
        <th>
            사운드 채널 수(SoundSystem)
        </th>
        <th>
            샘플링 레이트(SampleRate)
        </th>
    </tr>
 <tr>
        <td>
            1100
        </td>
        <td rowspan="5">
            M4A
        </td>
        <td>
            24kbps
        </td>
        <td rowspan="5">
            AAC
        </td>
        <td rowspan="7">
            스테레오(Stereo)
        </td>
        <td rowspan="7">
            44100Hz
        </td>
    </tr>
 <tr>
        <td>
            1110
        </td>
        <td>
            48kbps
        </td>
    </tr>
    <tr>
        <td>
            1120
        </td>
        <td>
            96kbps
        </td>
    </tr>
     <tr>
        <td>
            1130
        </td>
        <td>
            192kbps
        </td>
    </tr>
    <tr>
        <td>
            1140
        </td>
        <td>
            256kbps
        </td>
    </tr>
    <tr>
        <td>
            1010
        </td>
        <td rowspan="2">
            MP3
        </td>
        <td>
            128kbps
        </td>
        <td rowspan="2">
            MP3
        </td>
    </tr>
    <tr>
        <td>
            1020
        </td>
        <td>
            320kbps
        </td>
    </tr>
</table>


### 사전 설정 초고속 고화질 템플릿

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">사양 레벨</th><th colspan="1" rowspan="2">템플릿 ID</th><th colspan="1" rowspan="2">컨테이너 형식(Format)</th><th colspan="4">비디오 매개변수</th><th colspan="4">오디오 매개변수</th></tr>
<tr><th colspan="1">해상도(Resolution)</th><th colspan="1">최대 비트 레이트(Bitrate)</th><th colspan="1">프레임 레이트(FPS)</th><th colspan="1">코덱(Codec)</th><th colspan="1">비트 레이트(Bitrate)</th><th colspan="1">샘플링 레이트(SampleRate)</th><th colspan="1">오디오 사운드 채널 수(SoundSystem)</th><th colspan="1">코덱(Codec)</th></tr>
<tr><td colspan="1">원본과 동일(SAME)</td><td colspan="1" rowspan="">100800</td><td colspan="1" rowspan="5">MP4</td><td colspan="1">원본과 동일</td><td colspan="1" rowspan="5">무제한</td><td colspan="1" rowspan="5">25</td><td colspan="1" rowspan="5">H.264</td><td colspan="1">원본과 동일</td><td colspan="1" rowspan="5">44100Hz</td><td colspan="1" rowspan="5">스테레오(Stereo)</td><td colspan="1" rowspan="5">AAC</td></tr></tr>
<tr><td colspan="1">FLU</td><td colspan="1">100810</td><td colspan="1">비율에 따라 축소/확대 × 360</td><td colspan="1" rowspan="2">64 kbps</td></tr>
<tr><td colspan="1">SD</td><td colspan="1">100820</td><td colspan="1">비율에 따라 축소/확대 × 540</td></tr>
<tr><td colspan="1">HD</td><td colspan="1">100830</td><td colspan="1" rowspan="">비율에 따라 축소/확대 × 720</td><td colspan="1" rowspan="2">128kbps</td></tr>
<tr><td colspan="1">FHD</td><td colspan="1">100840</td><td colspan="1">비율에 따라 축소/확대 × 1080</td></tr></tbody></table>


### 사전 설정 리먹싱 템플릿

| 템플릿 ID | 리먹싱 타깃 포맷(Format) |
| ------- | ------------------------ |
| 875       | MP4                      |
| 876       | HLS                      |

[](id:cinemagraph)
### 사전 설정 gif 템플릿

| 템플릿 ID | 이미지 형식(Format) | 해상도(Resolution) | 프레임 레이트(FPS) |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | 원본과 동일                 | 2           |
| 20001   | WEBP               | 원본과 동일                 | 2           |

[](id:screenshot01)
### 사전 설정 지정 시점 화면 캡처 템플릿

| 템플릿 ID | 출력 형식(Format) | 폭(Width) | 높이(Height) | 채우기 방식(FillType) |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | 원본과 동일          | 원본과 동일           | 늘리기                 |

[](id:screenshot02)
### 사전 설정 샘플링 화면 캡처 템플릿

| 템플릿 ID | 출력 형식(Format) | 폭(Width) | 높이(Height) | 샘플링 방식(SampleType) | 화면 캡처 간격(Interval) | 채우기 방식(FillType) |
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG                | 원본과 동일          | 원본과 동일           | 백분율               | 10%                  | 늘리기                 |

[](id:screenshot03)
### 사전 설정 스프라이트 이미지 템플릿

| 템플릿 ID | 출력 형식(Format) | 작은 이미지 폭(Width) | 작은 이미지 높이(Height) | 작은 이미지 행 수(Rows) | 작은 이미지 열 수(Columns) | 샘플링 방식(SampleType) | 화면 캡처 간격(Interval) |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80                 | 10               | 10                  | 시간 간격             | 10초                 |

### 사전 설정 자동 맞춤 전환 코드 스트림 템플릿
#### 템플릿 정보

<table border="0" >
 <tr>
  <th>템플릿 ID</td>
  <th>패키지 유형(PackageType)</td>
  <th>암호화 유형(EncryptionType)</td>
  <th>서브 스트림 정보(SubstreamInfo)</td>
  <th >'고해상도 전환' 필터(DisableHigherResolution)</td>
 </tr>
 <tr>
  <td>10</td>
  <td>HLS</td>
  <td >암호화되지 않음</td>
  <td >'FLU'부터 '4K'까지 총 6개 사양의 서브 스트림 포함</td>
  <td>예</td>
 </tr>
 <tr>
  <td>12</td>
  <td>HLS</td>
  <td>SimpleAES</td>
  <td >'FLU'부터 '4K'까지 총 6개 사양의 서브 스트림 포함</td>
  <td>예</td>
 </tr>
  <tr>
  <td>20</td>
  <td>MPEG-DASH</td>
  <td>암호화되지 않음</td>
  <td >'FLU'부터 '4K'까지 총 6개 사양의 서브 스트림 포함</td>
  <td>아니오</td>
 </tr>
</table>

#### 서브 스트림 정보

<table border="0" >
 <tr>
  <th rowspan="2" >서브 스트림 사양</td>
  <th colspan="4" >비디오 매개변수</td>
  <th colspan="4" >오디오 매개변수</td>
 </tr>
 <tr>
  <th>해상도(Resolution)</th>
  <th>비트 레이트(Bitrate)</th>
  <th >프레임 레이트(FPS)</th>
  <th >코덱(Codec)</th>
  <th>비트 레이트(Bitrate)</th>
  <th>샘플링 레이트(SampleRate)</th>
  <th>오디오 사운드 채널 수(SoundSystem)</th>
  <th>코덱(Codec)</td>
 </tr>
 <tr>
  <td>FLU</td>
  <td>비율에 따라 축소/확대 x 240</td>
  <td>256kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>스테레오(Stereo)</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>SD</td>
  <td>비율에 따라 축소/확대 x 480</td>
  <td>512kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>스테레오(Stereo)</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>HD</td>
  <td>비율에 따라 축소/확대 x 720</td>
  <td>512kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>스테레오(Stereo)</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>FHD</td>
  <td>비율에 따라 축소/확대 x 1080</td>
  <td>1024kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>스테레오(Stereo)</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>2K</td>
  <td>비율에 따라 축소/확대 x 1440</td>
  <td>3072kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>스테레오(Stereo)</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>4K</td>
  <td>비율에 따라 축소/확대 x 2160</td>
  <td>6144kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>스테레오(Stereo)</td>
  <td>AAC</td>
 </tr>
</table>


## 비디오 AI 클래스

비디오 AI 클래스의 사전 설정 매개변수 템플릿에는 다음 유형이 포함됩니다.

* 사전 설정 비디오 콘텐츠 심사 템플릿
* 사전 설정 비디오 콘텐츠 분석 템플릿
* 사전 설정 비디오 콘텐츠 인식 템플릿

### 사전 설정 비디오 심사 템플릿[](id:verify)


<table>
    <tr>
        <th rowspan=2>
            템플릿 ID                
        </th>
        <th colspan=3>
            비디오 화면
        </th>
        <th colspan=2>
            ASR 문자
        </th>
        <th colspan=2>
            OCR 문자
        </th>
    </tr>
 <tr>
        <th>
            자극적인 정보(Porn)
        </th>
        <th>
            위험한 정보(Terrorism)
        </th>
        <th>
            부적절한 정보(Political)
        </th>
        <th>
            자극적인 정보(Asr.Porn)
        </th>
        <th>
            부적절한 정보(Asr.Political)
        </th>
        <th>
            자극적인 정보(Ocr.Porn)
        </th>
        <th>
            부적절한 정보(Ocr.Political)
        </th>
    </tr>
    <tr>
        <td>
            10
        </td>
        <td>
            예
        </td>
        <td>
            예
        </td>
        <td>
            예
        </td>
        <td>
            아니요
        </td>
        <td>
            아니요
        </td>
        <td>
            아니요
        </td>
        <td>
            아니요
        </td>
    </tr>
    <tr>
        <td>
            20
        </td>
        <td>
            예
        </td>
        <td>
            예
        </td>
        <td>
            예
        </td>
        <td>
            예
        </td>
        <td>
            예
        </td>
        <td>
            예
        </td>
        <td>
            예
        </td>
    </tr>
</table>

### 사전 설정 비디오 콘텐츠 분석 템플릿

| 템플릿 ID | 스마트 분류(Classification) | 스마트 태그(Tag) | 스마트 커버(Cover) | 스마트 프레임 태그(FrameTag) |
| -- | -- | -- | -- | -- |
| 10 | 예 | 예 | 예 | 아니요 |
| 20 | 예 | 예 | 예 | 예 |

### 사전 설정 비디오 콘텐츠 인식 템플릿

| 템플릿 ID  | 얼굴 인식(Face) | 텍스트 핵심 키워드 인식(OcrWords) | 음성 전체 인식(AsrFullText) | 음성 핵심 키워드 인식(AsrWords) | 
| -- | -- | -- | -- | -- | -- |
| 10 | 예(기본 얼굴 라이브러리 사용) | 아니오 | 아니오 | 아니오 |아니오 |




## 이전 트랜스코딩 클래스

### 이전 사전 설정 트랜스코딩 템플릿

#### 비디오 트랜스 코딩 포맷

<table>
    <tr>
        <th rowspan=2>
            사양 등급                
        </th>
        <th rowspan=2>
            템플릿 ID                
        </th>
        <th rowspan=2>
            컨테이너 형식(Format)
        </th>
        <th colspan=4>    
            비디오 매개변수
        </th>
        <th colspan=1>    
            오디오 매개변수
        </th>
    </tr>
    <tr>
        <th>
            해상도(Resolution)
        </th>
        <th>
            비트 레이트(Bitrate)
        </th>
        <th>
            프레임 레이트(FPS)
        </th>
        <th>
            코덱(Codec)
        </th>
        <th>
            코덱(Codec)
        </th>
    </tr>
    <tr>
        <td rowspan=6>
            FLU
        </td>
        <td>
            10
        </td>
        <td>
            MP4
        </td>
        <td>
            320 × 비율에 따라 조정
        </td>
        <td>
            256kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            510
        </td>
        <td>
            MP4
        </td>
        <td>
            비율에 따라 조정 × 240
        </td>
        <td>
            250kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            210
        </td>
        <td>
            HLS
        </td>
        <td>
            320 × 비율에 따라 조정
        </td>
        <td>
            256kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            610
        </td>
        <td>
            HLS
        </td>
        <td>
            비율에 따라 조정 × 240
        </td>
        <td>
            250kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10046
        </td>
        <td>
            FLV
        </td>
        <td>
            320 × 비율에 따라 조정
        </td>
        <td>
            256kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            710
        </td>
        <td>
            FLV
        </td>
        <td>
            비율에 따라 조정 × 240
        </td>
        <td>
            250kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td rowspan=6>
            SD
        </td>
        <td>
            20
        </td>
        <td>
            MP4
        </td>
        <td>
            640 × 비율에 따라 조정
        </td>
        <td>
            512kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            520
        </td>
        <td>
            MP4
        </td>
        <td>
            비율에 따라 조정 × 480
        </td>
        <td>
            600kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            220
        </td>
        <td>
            HLS
        </td>
        <td>
            640 × 비율에 따라 조정
        </td>
        <td>
            512kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            620
        </td>
        <td>
            HLS
        </td>
        <td>
            비율에 따라 조정 × 480
        </td>
        <td>
            600kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10047
        </td>
        <td>
            FLV
        </td>
        <td>
            640 × 비율에 따라 조정
        </td>
        <td>
            512kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            720
        </td>
        <td>
            FLV
        </td>
        <td>
            비율에 따라 조정 × 480
        </td>
        <td>
            600kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td rowspan=6>
            HD
        </td>
        <td>
            30
        </td>
        <td>
            MP4
        </td>
        <td>
            1280 × 비율에 따라 조정
        </td>
        <td>
            1024kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            530
        </td>
        <td>
            MP4
        </td>
        <td>
            비율에 따라 조정 × 720
        </td>
        <td>
            800kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            230
        </td>
        <td>
            HLS
        </td>
        <td>
            1280 × 비율에 따라 조정
        </td>
        <td>
            1024kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            630
        </td>
        <td>
            HLS
        </td>
        <td>
            비율에 따라 조정 × 720
        </td>
        <td>
            800kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10048
        </td>
        <td>
            FLV
        </td>
        <td>
            1280 × 비율에 따라 조정
        </td>
        <td>
            1024kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            730
        </td>
        <td>
            FLV
        </td>
        <td>
            비율에 따라 조정 × 720
        </td>
        <td>
            800kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            FHD
        </td>
        <td>
            40
        </td>
        <td>
            MP4
        </td>
        <td>
            1920 × 비율에 따라 조정
        </td>
        <td>
            2500kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            540
        </td>
        <td>
            MP4
        </td>
        <td>
            비율에 따라 조정 × 1080
        </td>
        <td>
            1400kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            240
        </td>
        <td>
            HLS
        </td>
        <td>
            1920 × 비율에 따라 조정
        </td>
        <td>
            2500kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            640
        </td>
        <td>
            HLS
        </td>
        <td>
            비율에 따라 조정 × 1080
        </td>
        <td>
            1400kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10049
        </td>
        <td>
            FLV
        </td>
        <td>
            1920 × 비율에 따라 조정
        </td>
        <td>
            2500kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            740
        </td>
        <td>
            FLV
        </td>
        <td>
            비율에 따라 조정 × 1080
        </td>
        <td>
            1400kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            2K
        </td>
        <td>
            70
        </td>
        <td>
            MP4
        </td>
        <td>
            비율에 따라 조정 × 1440
        </td>
        <td>
            3072kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            570
        </td>
        <td>
            MP4
        </td>
        <td>
            비율에 따라 조정 × 1440
        </td>
        <td>
            2048kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            270
        </td>
        <td>
            HLS
        </td>
        <td>
            비율에 따라 조정 × 1440
        </td>
        <td>
            3072kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            670
        </td>
        <td>
            HLS
        </td>
        <td>
            비율에 따라 조정 × 1440
        </td>
        <td>
            2048kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            370
        </td>
        <td>
            FLV
        </td>
        <td>
            비율에 따라 조정 × 1440
        </td>
        <td>
            3072kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            770
        </td>
        <td>
            FLV
        </td>
        <td>
            비율에 따라 조정 × 1440
        </td>
        <td>
            2048kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            4K
        </td>
        <td>
            80
        </td>
        <td>
            MP4
        </td>
        <td>
            비율에 따라 조정 × 2160
        </td>
        <td>
            6144kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            580
        </td>
        <td>
            MP4
        </td>
        <td>
            비율에 따라 조정 × 2160
        </td>
        <td>
            4096kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            280
        </td>
        <td>
            HLS
        </td>
        <td>
            비율에 따라 조정 × 2160
        </td>
        <td>
            6144kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            680
        </td>
        <td>
            HLS
        </td>
        <td>
            비율에 따라 조정 × 2160
        </td>
        <td>
            4096kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            380
        </td>
        <td>
            FLV
        </td>
        <td>
            비율에 따라 조정 × 2160
        </td>
        <td>
            6144kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            780
        </td>
        <td>
            FLV
        </td>
        <td>
            비율에 따라 조정 × 2160
        </td>
        <td>
            4096kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
</table>

상기 비디오 전송 템플릿에 명시되지 않은 매개변수는 모두 동일합니다. 즉:

<table>
    <tr>
        <th style="width:18%">
            분류               
        </th>
        <th style="width:22%">
            매개변수/능력 항목
        </th>
        <th>
            설명
        </th>
    </tr>
    <tr>
        <td rowspan=4>
            비디오 매개변수
        </td>
        <td>
            코덱 등급
        </td>
        <td>
				    <ul>
				       <li>H.264 코덱 사용 시 코덱 등급: High</li>
						   <li>H.265 코덱 사용 시 코덱 등급: Main</li>
				    </ul>
        </td>
    </tr>
    <tr>
        <td>
            GOP 길이
        </td>
        <td>
            240프레임
        </td>
    </tr>
    <tr>
        <td>
            색 공간
        </td>
        <td>
            YUV420P
        </td>
    </tr>
    <tr>
        <td>
            비트 레이트 제어 방법
        </td>
        <td>
            가변 비트레이트(VBR)
        </td>
    </tr>
    <tr>
        <td rowspan=3>
            오디오 매개변수
        </td>
        <td>
            샘플링 레이트
        </td>
        <td>
            44100Hz
        </td>
    </tr>
    <tr>
        <td>
            비트 레이트
        </td>
        <td>
            48kbps
        </td>
    </tr>
    <tr>
        <td>
            사운드 채널 수
        </td>
        <td>
            스테레오(Stereo)
        </td>
    </tr>
</table>
