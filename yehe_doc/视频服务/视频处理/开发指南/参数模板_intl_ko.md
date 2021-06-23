비디오 처리 서비스의 편리한 사용을 위해 자주 사용하는 주요 트랜스 코딩 매개변수를 매개변수 템플릿으로 조합합니다. 각각의 매개변수 템플릿은 이름과 ID로 표시되는데, 자주 사용하는 'FLU', 'SD', 'HD', 'FHD' 등의 경우 트랜스 코딩 템플릿에서 10, 20, 30, 40과 같은 ID로 표시됩니다. 매개변수 템플릿은 작업에 따라 다음과 같은 유형으로 분류됩니다.
- 트랜스 코딩 템플릿
- 리먹싱 템플릿
- gif 템플릿
- 시점 화면 캡처 템플릿
- 샘플링 화면 캡처 템플릿
- 스프라이트 이미지 템플릿
- 자동 맞춤 전환 코드 스트림 템플릿
- 비디오 콘텐츠 스마트 인식 템플릿
- 비디오 콘텐츠 인식 템플릿
- 비디오 콘텐츠 분석 템플릿

비디오 처리에서는 위의 템플릿 유형에 해당하는 자주 사용되는 매개변수 템플릿(사전 설정 매개변수 템플릿)을 제공합니다. 또한 각 유형의 신규 매개변수 템플릿을 생성하고 다양한 매개변수 값을 지정(사용자 정의 매개변수 템플릿)할 수 있습니다. 매개변수 템플릿의 각 매개변수에 대한 자세한 정보는 [매개변수 설명](https://intl.cloud.tencent.com/document/product/1041/33494)을 참조하십시오.

## 사전 설정 매개변수 템플릿

다음은 템플릿 ID, 주요 매개변수 설정 등 비디오 처리에서 사전 설정한 각 유형의 매개변수 템플릿 정보입니다.

[](id:transcoding)
### 사전 설정 트랜스 코딩 템플릿
#### 비디오 트랜스 코딩 포맷

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">사양 레벨</th><th colspan="1" rowspan="2">템플릿 ID</th><th colspan="1" rowspan="2">캡슐화 포맷(Format)</th><th colspan="4">비디오 매개변수</th><th colspan="4">오디오 매개변수</th></tr>
<tr><th colspan="1">해상도(Resolution)</th><th colspan="1">비트 레이트(Bitrate)</th><th colspan="1">프레임 레이트(FPS)</th><th colspan="1">인코딩(Codec)</th><th colspan="1">비트 레이트(Bitrate)</th><th colspan="1">샘플링 레이트(SampleRate)</th><th colspan="1">오디오 사운드 채널 수(SoundSystem)</th><th colspan="1">인코딩(Codec)</th></tr>
<tr><td colspan="1" rowspan="2">원활(FLU)</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 360</td><td colspan="1" rowspan="2">400kbps</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64 kbps</td ><td colspan="1" rowspan="12">44100Hz</td><td colspan="1" rowspan="12">듀얼 사운드 채널(Stereo)</td><td colspan="1" rowspan="12">AAC</td></tr>
<tr><td colspan="1">100210</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">표준 화질(SD)</td><td colspan="1">100020</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 540</td><td colspan="1" rowspan="2">1000kbps</td></tr>
<tr><td colspan="1">100220</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">고화질(HD)</td><td colspan="1">100030</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 720</td><td colspan="1" rowspan="2">1800kbps</td><td colspan="1" rowspan="4">128kbps</td></tr>
<tr><td colspan="1">100230</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">초고화질(FHD)</td><td colspan="1">100040</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 1080</td><td colspan="1" rowspan="2">2500kbps</td></tr>
<tr><td colspan="1">100240</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">2K</td><td colspan="1">100070</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 1440</td><td colspan="1" rowspan="2">3000kbps</td><td colspan="1" rowspan="4">160kbps</td></tr>
<tr><td colspan="1">100270</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">4K</td><td colspan="1">100080</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">비율에 따라 축소/확대 × 2160</td><td colspan="1" rowspan="2">6000kbps</td></tr>
<tr><td colspan="1">100280</td><td colspan="1">HLS</td></tr></tbody></table>

#### 오디오 트랜스 코딩 포맷

<table>
    <tr>
        <th rowspan=1>
            템플릿 ID                
        </th>
        <th rowspan=1>
            캡슐화 포맷(Format)
        </th>
        <th>
            오디오 비트 레이트(Bitrate)
        </th>
        <th>
            인코딩(Codec)
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
            듀얼 사운드 채널(Stereo)
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

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">사양 레벨</th><th colspan="1" rowspan="2">템플릿 ID</th><th colspan="1" rowspan="2">캡슐화 포맷(Format)</th><th colspan="4">비디오 매개변수</th><th colspan="4">오디오 매개변수</th></tr>
<tr><th colspan="1">해상도(Resolution)</th><th colspan="1">최대 비트 레이트(Bitrate)</th><th colspan="1">프레임 레이트(FPS)</th><th colspan="1">인코딩(Codec)</th><th colspan="1">비트 레이트(Bitrate)</th><th colspan="1">샘플링 레이트(SampleRate)</th><th colspan="1">오디오 사운드 채널 수(SoundSystem)</th><th colspan="1">인코딩(Codec)</th></tr>
<tr><td colspan="1">원본과 동일(SAME)</td><td colspan="1" rowspan="">100800</td><td colspan="1" rowspan="5">MP4</td><td colspan="1">원본과 동일</td><td colspan="1" rowspan="5">무제한</td><td colspan="1" rowspan="5">25</td><td colspan="1" rowspan="5">H.264</td><td colspan="1">원본과 동일</td><td colspan="1" rowspan="5">44100Hz</td><td colspan="1" rowspan="5">듀얼 사운드 채널(Stereo)</td><td colspan="1" rowspan="5">AAC</td></tr></tr>
<tr><td colspan="1">원활(FLU)</td><td colspan="1">100810</td><td colspan="1">비율에 따라 축소/확대 × 360</td><td colspan="1" rowspan="2">64 kbps</td></tr>
<tr><td colspan="1">표준 화질(SD)</td><td colspan="1">100820</td><td colspan="1">비율에 따라 축소/확대 × 540</td></tr>
<tr><td colspan="1">고화질(HD)</td><td colspan="1">100830</td><td colspan="1" rowspan="">비율에 따라 축소/확대 × 720</td><td colspan="1" rowspan="2">128kbps</td></tr>
<tr><td colspan="1">초고화질(FHD)</td><td colspan="1">100840</td><td colspan="1">비율에 따라 축소/확대 × 1080</td></tr></tbody></table>


### 사전 설정 리먹싱 템플릿

| 템플릿 ID | 리먹싱 타깃 포맷(Format) |
| ------- | ------------------------ |
| 875       | MP4                      |
| 876       | HLS                      |

[](id:cinemagraph)
### 사전 설정 gif 템플릿

| 템플릿 ID | 이미지 포맷(Format) | 해상도(Resolution) | 프레임 레이트(FPS) |
| ------- | --------- | ----------- | ----------- |
| 20000   | GIF                | 원본과 동일                 | 2           |
| 20001   | WebP               | 원본과 동일                 | 2           |

[](id:screenshot01)
### 사전 설정 지정 시점 화면 캡처 템플릿

| 템플릿 ID | 출력 포맷(Format) | 폭(Width) | 높이(Height) | 채우기 방식(FillType) |
| ------- | --------- | ----- | --------- | -------------- |
| 10      | JPG                | 원본과 동일          | 원본과 동일           | 늘이기   |

[](id:screenshot02)
- 사전 설정 샘플링 화면 캡처 템플릿

| 템플릿 ID &nbsp;| 출력 포맷(Format) | 폭(Width) | 높이(Height) | 샘플링 방식(SampleType) | 화면 캡처 간격(Interval) | 채우기 방식(FillType) |
| ------- | -------- | -- | ----- | ---- | ------- | -------- |
| 10      | JPG    | 원본과 동일   | 원본과 동일     | 백분율  | 10%   | 늘이기     |

[](id:screenshot03)
### 사전 설정 스프라이트 이미지 템플릿

| 템플릿 ID &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 출력 포맷(Format) | 작은 이미지 폭(Width) | 작은 이미지 높이(Height) | 작은 이미지 행 수(Rows) | 작은 이미지 열 수(Columns) | 샘플링 방식(SampleType) | 화면 캡처 간격(Interval) |
| ------- | ----- | ------- | ----- | ---- | ---- | -------- | ------- |
| 10      | JPG   | 142    | 80      | 10       | 10    | 시간 간격   | 10초  |

### 사전 설정 자동 맞춤 전환 코드 스트림 템플릿
#### 템플릿 정보

<table border="0" >
 <tr>
  <th>템플릿 ID</td>
  <th>패키지 유형(PackageType)</td>
  <th>서브 스트림 정보(SubstreamInfo)</td>
  <th >'고해상도 전환' 필터(DisableHigherResolution)</td>
 </tr>
 <tr>
  <td>10</td>
  <td>HLS</td>
  <td >'SD'부터 '4K'까지 총 6개 사양의 서브 스트림 포함</td>
  <td>예</td>
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
  <th >인코딩(Codec)</th>
  <th>비트 레이트(Bitrate)</th>
  <th>샘플링 레이트(SampleRate)</th>
  <th>오디오 사운드 채널 수(SoundSystem)</th>
  <th>인코딩(Codec)</td>
 </tr>
 <tr>
  <td>FLU</td>
  <td>비율에 따라 축소/확대 x 240</td>
  <td>256kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>듀얼 사운드 채널(Stereo)</td>
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
  <td>듀얼 사운드 채널(Stereo)</td>
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
  <td>듀얼 사운드 채널(Stereo)</td>
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
  <td>듀얼 사운드 채널(Stereo)</td>
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
  <td>듀얼 사운드 채널(Stereo)</td>
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
  <td>듀얼 사운드 채널(Stereo)</td>
  <td>AAC</td>
 </tr>
</table>

### 사전 설정 비디오 콘텐츠 스마트 인식 템플릿

[](id:verify)
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

### 사전 설정 비디오 콘텐츠 인식 템플릿

| 템플릿 ID  | 텍스트 전체 인식(OcrFullText) | 텍스트 핵심 키워드 인식(OcrWords) | 음성 전체 인식(AsrFullText) | 음성 핵심 키워드 인식(AsrWords) |
| -- | -- | -- | -- | -- |
| 10  | 아니요 | 아니요 | 아니요 | 아니요 |


### 사전 설정 비디오 콘텐츠 분석 템플릿

| 템플릿 ID | 스마트 분류(Classification) | 스마트 태그(Tag) | 스마트 커버(Cover) | 스마트 프레임 태그(FrameTag) |
| -- | -- | -- | -- | -- |
| 10 | 예 | 예 | 예 | 아니요 |
| 20 | 예 | 예 | 예 | 예 |

## 사용자 정의 매개변수 템플릿
시스템에 사전 설정된 매개변수 템플릿 외에도 필요에 따라 매개변수 템플릿을 사용자 정의할 수 있습니다('사용자 정의 매개변수 템플릿' 생성). 콘솔 또는 API 호출을 통해 각 유형에 해당하는 매개변수 템플릿을 생성할 수 있으며, 해당 템플릿은 사용자 본인만 볼 수 있습니다.

### 콘솔에서 사용자 정의 매개변수 템플릿 생성

콘솔에서 사용자 정의 매개변수 템플릿을 생성하려면 [매개변수 설정](https://intl.cloud.tencent.com/document/product/1041/33486)을 참조하십시오.

### API를 통해 사용자 정의 매개변수 템플릿 생성
다음과 같은 API를 통해 각 유형에 해당하는 사용자 정의 매개변수 템플릿을 생성할 수 있습니다.
- [트랜스 코딩 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/33671)
- [워터마크 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/33670)
- [샘플링 화면 캡처 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/33673)
- [지정 시점 화면 캡처 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/33672)
- [gif 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/33676)
- [스프라이트 이미지 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/33674)
- [자동 맞춤 전환 코드 스트림 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/37469)
- [비디오 콘텐츠 스마트 인식 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/33677)
- [비디오 콘텐츠 인식 템플릿 생성]
- [비디오 콘텐츠 분석 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/37470)
