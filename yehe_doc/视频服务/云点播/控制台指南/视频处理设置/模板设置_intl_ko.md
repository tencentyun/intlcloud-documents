[VOD 콘솔]( https://console.cloud.tencent.com/vod/overview)에 로그인하고 왼쪽 사이드바에서 [비디오 처리 설정]>[템플릿 설정]을 선택합니다. 여기에 내장된 템플릿에는 **비디오 트랜스코딩 템플릿**, **TESHD 템플릿**, **오디오 트랜스코딩 템플릿**, **어댑티브 비트레이트 스트리밍 템플릿**, **워터마크 템플릿**, **스크린샷 템플릿**, **애니메이션 이미지 생성 템플릿**, **스마트 인식 템플릿**이 있으며 각각 비디오 처리를 위해 태스크 플로우에 추가할 수 있습니다.


## 비디오 트랜스 코딩 템플릿

비즈니스 니즈에 따라 새 비디오 트랜스코딩 템플릿을 생성하고 사용자 정의 설정을 진행할 수 있습니다. [비디오 트랜스코딩 템플릿]을 선택한 다음 [트랜스코딩 템플릿 생성]을 클릭하여 템플릿 사용자 정의 설정으로 이동합니다.
+ 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
+ 컨테이너 형식: MP4, FLV, HLS
+ 설정 항목: 비디오 매개변수, 오디오 매개변수
+ 비디오 매개변수:
	+ 인코딩 방법: H.264, H.265, AOMedia Video1
	+ 비디오 비트레이트: 128kbps-35000kbps
	+ 해상도: 동영상의 긴 변(동영상 너비)과 동영상의 짧은 변(동영상 높이)은 128px-4096px입니다.
	+ 프레임 레이트: 1-100fps
+ 오디오 매개변수:
	+ 인코딩 표준: AAC, MP3
	+ 샘플링 레이트: 32000Hz, 44100Hz, 48000Hz 3종류의 기본 샘플링 레이트
	+ 오디오 비트레이트: 26kbps-256kbps
	+ 사운드 채널: 싱글 사운드 채널, 듀얼 사운드 채널
+ 자주 사용하는 템플릿: 자주 사용하는 템플릿 설정 여부

생성된 템플릿은 템플릿 리스트에 표시되며, 자주 사용되는 템플릿으로 설정될 수 있고, 템플릿에 대해 보기, 편집, 삭제 등의 관리 작업을 수행할 수 있습니다.

자세한 매개변수는 [매개변수 템플릿 리스트-사전 설정된 트랜스코딩 템플릿](https://intl.cloud.tencent.com/document/product/266/33932#preset-transcoding-templates)을 참고하십시오.

## TESHD 템플릿

비즈니스 니즈에 따라 새 TESHD 템플릿을 생성하고 사용자 정의 설정을 진행할 수 있습니다. [TESHD 템플릿]을 선택하고 [트랜스코딩 템플릿 생성]을 클릭하여 템플릿 사용자 정의 설정으로 이동합니다.
+ 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
+ 컨테이너 형식: MP4, FLV, HLS
+ 설정 항목: 비디오 매개변수, 오디오 매개변수
+ 비디오 매개변수:
	+ 인코딩 방법: H.264, H.265, AOMedia Video1
	+ 평균 비트레이트의 최댓값: 공란 또는 0은 비디오 비트레이트의 최댓값이 없음을 의미합니다.
	+ 해상도: 동영상의 긴 변(동영상 너비)과 동영상의 짧은 변(동영상 높이)이 128px - 4096px입니다.
	+ 프레임 레이트: 1-100fps
+ 오디오 매개변수:
	+ 인코딩 표준: AAC, MP3
	+ 샘플링 레이트: 32000Hz, 44100Hz, 48000Hz 3종류의 기본 샘플링 레이트
	+ 오디오 비트레이트: 26kbps-256kbps
	+ 사운드 채널: 싱글 사운드 채널, 듀얼 사운드 채널
+ 자주 사용하는 템플릿: 자주 사용하는 템플릿 설정 여부

생성된 템플릿은 템플릿 리스트에 표시되며, 자주 사용되는 템플릿으로 설정될 수 있고, 템플릿에 대해 보기, 편집, 삭제 등의 관리 작업을 수행할 수 있습니다.
>?[사전 설정 매개변수 템플릿 리스트 - TESHD 트랜스코딩](https://intl.cloud.tencent.com/document/product/266/33932#preset-teshd-templates)을 참고하십시오.



## 오디오 트랜스코딩 템플릿[](id:yp)
비즈니스 니즈에 따라 새 오디오 트랜스코딩 템플릿을 생성하고 사용자 정의 설정을 진행할 수 있습니다. [오디오 트랜스코딩 템플릿]을 선택한 다음 [오디오 템플릿 생성]를 클릭하여 템플릿 사용자 정의 설정으로 이동합니다.

+ 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
+ 컨테이너 형식: MP3, FLAC, OGG, M4A
+ 오디오 매개변수:
	+ 인코딩 표준: 컨테이너 형식이 MP3인 경우 해당 인코딩 표준은 MP3이며, FLAC 및 OGG인 경우 해당 인코딩 표준은 FLAC이고, M4A인 경우 해당 인코딩 표준은 MP3, AAC, AC3입니다.
	+ 샘플링 레이트: 32000Hz, 44100Hz, 48000Hz 3종류의 기본 샘플링 레이트
	+ 오디오 비트레이트: 26kbps-256kbps
	+ 사운드 채널: 싱글 사운드 채널, 듀얼 사운드 채널
+ 자주 사용하는 템플릿: 자주 사용하는 템플릿 설정 여부

생성된 템플릿은 템플릿 리스트에 표시되며, 자주 사용되는 템플릿으로 설정될 수 있고, 템플릿에 대해 보기, 편집, 삭제 등의 관리 작업을 수행할 수 있습니다.

#### 사전 설정 매개변수 템플릿 리스트

<table>
    <tr>
        <th rowspan=1>
            템플릿 ID                
        </th>
        <th rowspan=1>
            캡슐화 포맷(Format)
        </th>
        <th>
            오디오 비트레이트(Bitrate)
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
        <td>
            M4A
        </td>
        <td>
            24kbps
        </td>
        <td>
            AAC
        </td>
        <td>
            스테레오(Stereo)
        </td>
                <td>
            44100Hz
        </td>
    </tr>
 <tr>
        <td>
            1110
        </td>
        <td>
            M4A
        </td>
        <td>
            48kbps
        </td>
        <td>
            AAC
        </td>
        <td>
            스테레오(Stereo)
        </td>
                <td>
            44100Hz
        </td>
    </tr>
    <tr>
        <td>
            1120
        </td>
        <td>
            M4A
        </td>
        <td>
            96kbps
        </td>
        <td>
            AAC
        </td>
       <td>
            스테레오(Stereo)
        </td>
                <td>
            44100Hz
        </td>
    </tr>
     <tr>
        <td>
            1130
        </td>
        <td>
            M4A
        </td>
        <td>
            192kbps
        </td>
        <td>
            AAC
        </td>
       <td>
            스테레오(Stereo)
        </td>
                <td>
            44100Hz
        </td>
    </tr>
    <tr>
        <td>
            1140
        </td>
        <td>
            M4A
        </td>
        <td>
            256kbps
        </td>
        <td>
            AAC
        </td>
       <td>
            스테레오(Stereo)
        </td>
                <td>
            44100Hz
        </td>
    </tr>
    <tr>
        <td>
            1010
        </td>
        <td>
            MP3
        </td>
        <td>
            128kbps
        </td>
        <td>
            MP3
        </td>
       <td>
            스테레오(Stereo)
        </td>
                <td>
            44100Hz
        </td>
    </tr>
    <tr>
        <td>
            1020
        </td>
        <td>
            MP3
        </td>
        <td>
            320kbps
        </td>
        <td>
            MP3
        </td>
       <td>
            스테레오(Stereo)
        </td>
                <td>
            44100Hz
        </td>
    </tr>
</table>

## 어댑티브 비트레이트 스트리밍 템플릿

시스템 사전 설정 어댑티브 비트레이트 스트리밍 템플릿을 직접 사용하거나 비즈니스 요구 사항에 따라 사용자 정의 템플릿을 만들 수 있습니다.
+ **기본 정보**
	+ 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
	+ 먹싱 형식: HLS, MPEG-DASH
	+ 암호화 유형: 암호화 방식 또는 SimpleAES를 사용하지 마십시오. MPEG-DASH는 SimpleAES를 지원하지 않습니다.
	+ 저해상도에서 고해상도로 전환: 활성화 또는 비활성화
+ **서브 스트림 정보**
	+ 비디오 인코딩 표준: H.264, H.265
	+ 비디오 비트레이트: 128kbps - 35000kbps
	+ 비디오 해상도: 비디오 긴 변 및 짧은 변은 128px - 4096px로 제한됩니다.
	+ 비디오 프레임 레이트: 1-100fps
	+ 오디오 인코딩 표준: AAC, MP3
	+ 오디오 샘플링 레이트: 32000Hz, 44100Hz 및 48000Hz
	+ 오디오 비트레이트: 26kbps-256kbps
	+ 사운드 채널: 싱글 사운드 채널, 듀얼 사운드 채널

생성한 템플릿은 템플릿 리스트에 표시되며, 템플릿 보기, 편집, 삭제 등의 관리 작업을 할 수 있습니다.
>?
>- 템플릿을 생성할 때 최소한 하나의 서브 스트림 정보를 추가해야 합니다.
>- [사전 설정 매개변수 템플릿 리스트 - 어댑티브 비트레이트 스트리밍 템플릿](https://intl.cloud.tencent.com/document/product/266/33932#preset-adaptive-bitrate-streaming-templates)을 참고하십시오.

## 워터마크 템플릿

비즈니스 니즈에 따라 이미지를 업로드하여 워터마크 템플릿을 생성할 수 있으며, 사용자 정의 워터마크를 구성하고 동영상에서의 워터마크의 위치를 ​​설정할 수 있습니다.

+ 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
+ 워터마크 유형: 이미지 워터마크, 텍스트 워터마크, SVG 워터마크
+ 워터마크 글꼴: Simkai는 중국어와 영어를 지원하고 arial은 영어만 지원합니다.
+ 글꼴 크기: 10, 11, 12, 14, 16, 18, 20, 22, 24, 26, 28, 36, 48, 72 지원
+ 글꼴 색상: 해당 색상 선택 지원
+ 투명도: 1-100 사이의 투명도 값
+ 워터마크 이미지: PNG와 APNG 포맷의 이미지를 지원하며, 최적의 시각 효과를 위해 투명 이미지 PNG 포맷 사용을 권장합니다. 이미지 크기 200KB 이하, 사이즈 200px * 200px 범위 이내여야 합니다.
+ 워터마크 위치: 기본값은 왼쪽 위이고, 선택 옵션은 왼쪽 아래, 오른쪽 위, 오른쪽 아래입니다.
+ 수평 오프셋: 수평 오프셋의 백분율은 워터마크와 좌측 상단의 수평 거리 및 수평 폭 간의 비율입니다. 수평 오프셋 백분율을 조정하여 워터마크의 수평 위치를 설정할 수 있습니다.
+ 수직 오프셋: 수직 오프셋의 백분율은 워터마크와 좌측 상단의 수직 거리 및 수직 높이 간의 비율입니다. 수직 오프셋 백분율을 조정하여 워터마크의 수직 위치를 설정할 수 있습니다.
+ 워터마크 사이즈: 백분율(%) 또는 픽셀(px)을 선택하여 사이즈를 조절할 수 있습니다. % 선택 시 원본 사이즈에 따라 백분율로 축소/확대하며, px 선택 시 지정 크기에 따라 워터마크를 축소/확대합니다.

생성된 워터마크 템플릿 관리 목록에서 워터마크 템플릿의 이름, 워터마크 파일 미리보기, 형식, 종류, 워터마크 위치, 크기 등을 볼 수 있으며, 이 워터마크 템플릿을 보기, 편집, 삭제하고 기본 템플릿으로 설정할 수도 있습니다.
>?예를 들어 수평 오프셋: 0%, 수직 오프셋: 0%인 경우 워터마크는 비디오 화면의 왼쪽 상단 모서리에 위치합니다. 수평 오프셋: 90%, 수직 오프셋: 90%인 경우 워터마크는 비디오 파일의 오른쪽 하단 모서리에 위치합니다.


## 스크린샷 템플릿
비즈니스 니즈에 따라 새 스크린샷 템플릿을 생성하고 업로드된 비디오를 다양한 방식으로 캡처할 수 있습니다. 현재 콘솔은 시간대별 스크린샷, 샘플링 스크린샷 및 스프라이트 이미지 스크린샷의 세 가지 스크린샷 방법을 지원합니다.

스크린샷 템플릿에는 템플릿 이름, 스크린샷 유형, 이미지 크기가 표시됩니다. 작업 표시줄에서 스크린샷 템플릿을 조회, 편집 및 삭제할 수 있습니다.

### 시점 스크린샷
스크린샷 유형에서 시간대별 스크린샷을 선택합니다. **샘플링 시점은 스크린샷 작업 설정에서 지정해야 하며 템플릿 설정에서는 스크린샷 유형 설정만 수행할 수 있습니다.** 시간대별 스크린샷 작업 설정은 [태스크 플로우 설명](https://intl.cloud.tencent.com/document/product/266/14058#custom-task-flow)을 참고하십시오.

- 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
- 이미지 포맷: JPG
- 이미지 크기: 128px - 4096px
- 채우기 방식: 검정, 늘이기, 흰색, 가우시안 블러 지원

#### 사전 설정 매개변수 템플릿 리스트

| 템플릿 ID | 출력 형식(Format) | 폭(Width) | 높이(Height) | 채우기 방식(FillType) |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | 원본과 동일          | 원본과 동일           | 늘리기                 |

### 샘플링 스크린샷
스크린샷 유형에서 샘플링 스크린샷를 선택합니다.

- 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
- 이미지 포맷: JPG
- 이미지 크기: 128px - 4096px
- 채우기 방식: 검정, 늘이기, 흰색, 가우시안 블러 지원
- 샘플링 간격: 백분율(최대 100%), 시간(초)

#### 사전 설정 매개변수 템플릿 리스트

| 템플릿 ID | 출력 형식(Format) | 폭(Width) | 높이(Height) | 샘플링 방식(SampleType) | 스크린샷 간격(Interval) | 채우기 방식(FillType) |
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG                | 원본과 동일          | 원본과 동일           | 백분율               | 10%                  | 늘리기                 |



### 스프라이트 이미지 스크린샷
스크린샷 유형에서 스프라이트 이미지 스크린샷를 선택합니다.

- 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
- 이미지 포맷: JPG
- 이미지 크기: 128px - 4096px
- 채우기 방식: 검정, 늘이기, 흰색, 가우시안 블러 지원
- 샘플링 간격: 백분율(최대 100%), 시간(초)
- 작은 이미지 행 수: 자연수로 입력하며, 직은 이미지 행 수에 작은 이미지 열 수를 곱한 값이 100을 초과해서는 안됩니다.
- 작은 이미지 열 수: 자연수로 입력하며, 작은 이미지 행 수에 작은 이미지 열 수를 곱한 값이 100을 초과해서는 안됩니다.



#### 사전 설정 매개변수 템플릿 리스트

| 템플릿 ID | 출력 형식(Format) | 작은 이미지 폭(Width) | 작은 이미지 높이(Height) | 작은 이미지 행 수(Rows) | 작은 이미지 열 수(Columns) | 샘플링 방식(SampleType) | 스크린샷 간격(Interval) |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80                 | 10               | 10                  | 시간 간격             | 10초                 |

## gif 템플릿
비즈니스 니즈에 따라 애니메이션 이미지 템플릿을 생성하고 지정한 시간대에 필요한 애니메이션 이미지를 캡처할 수 있습니다. **애니메이션 이미지의 시간 구간은 태스크 플로우의 애니메이션 이미지 작업 설정에서 지정해야 하며, 템플릿 설정에서는 애니메이션 이미지 유형만 설정되어 있습니다.** 애니메이션 이미지의 작업 설정은 [태스크 플로우 설정](https://intl.cloud.tencent.com/document/product/266/14058#custom-task-flow)을 참고하십시오.

- 이미지 유형: WebP, GIF 지원
- 프레임 레이트: 1fps - 30fps
- 화질: 1 - 100
- 이미지 크기: 128px-4096px

#### 사전 설정 매개변수 템플릿 리스트

| 템플릿 ID | 이미지 형식(Format) | 해상도(Resolution) | 프레임 레이트(FPS) |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | 원본과 동일                 | 2           |
| 20001   | WebP               | 320 x 동일 비율 축소/확대             | 2           |



## 스마트 인식 템플릿
비즈니스 니즈에 따라 새 비디오 스마트 인식 템플릿을 생성하고 사용자 정의 설정을 진행할 수 있습니다. [심사 템플릿 생성]을 클릭하여 템플릿 사용자 정의 설정으로 이동합니다.

- 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(\_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
- 프레임 간격: 스마트 인식 비디오 확인 간격을 의미하며, 프레임 간격은 초 단위이며 기본값은 1이고 최소값은 0.5입니다.
- 스마트 인식 항목: 스마트 인식 선택 옵션은 이미지 인식, 음성 인식, 텍스트 인식이며, 선택된 스마트 인식 서브 항목은 오른쪽의 선택된 열에 나타납니다.
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th >스마트 인식 항목</th>
<th align="center" nowrap="nowrap">스마트 인식 서브 항목</th>
<th align="center">설명</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = 3 nowrap="nowrap">이미지 인식</td>
<td align="center">반감을 일으키는 정보</td>
<td align="center">음란물, 저속한 행위, 선정적 행위, 선정성의 서브 항목에 대한 스마트 인식 포함</td>
</tr>
<tr>
<td align="center">불안감을 일으키는 정보</td>
<td align="center">무장 세력, 무기 및 총, 피가 낭자한 장면, 경찰 부대, 밀집된 군중의 서브 항목에 대한 스마트 인식 포함</td>
</tr>
<tr>
<td align="center">부적절한 정보</td>
<td align="center">관련 인물, 규정 위반 이미지, 연예인, 스포츠 스타의 서브 항목에 대한 스마트 인식 포함</td>
</tr>
<tr>
<td rowspan = 3>음성 인식</td>
<td align="center">반감을 일으키는 정보</td>
<td align="center">음성 메시지에서 반감을 일으키는 정보 키워드 인식</td>
</tr>
<tr>
<td align="center">부적절한 정보</td>
<td align="center">음성 메시지에서 부적절한 정보 키워드 인식</td>
</tr>
<tr>
<td align="center">금지</td>
<td align="center">음성 메시지에서 욕설, 불법 도박 등 내용의 키워드 인식</td>
</tr>
<tr>
<td rowspan = 4>광학 문자 인식</td>
<td align="center">반감을 일으키는 정보</td>
<td align="center">문자 메시지에서 반감을 일으키는 정보 키워드 인식</td>
</tr>
<tr>
<td align="center">부적절한 정보</td>
<td align="center">문자 메시지에서 부적절한 정보 키워드 인식</td>
</tr>
<tr>
<td align="center">불안감을 일으키는 정보</td>
<td align="center">문자 메시지에서 불안감을 일으키는 정보 키워드 인식</td>
</tr>
<tr>
<td align="center">금지</td>
<td align="center">문자 메시지에서 욕설, 불법 도박 등 내용의 키워드 인식</td>
</tr>
</tbody></table>

모든 스마트 인식 서브 항목에 **신뢰도 확인 임계값**과 **신뢰도 의심 임계값**을 설정할 수 있으며, 이는 스마트 인식 강도 조절에 사용됩니다. 입력하지 않으면 VOD 기본값에 따라 작성 및 스마트 인식합니다.
 - 신뢰도 확인 임계값: VOD는 사용자가 업로드한 스마트 인식 비디오를 계산하여 스마트 인식 점수가 사용자가 설정한 값을 초과하면 해당 항목의 스마트 인식 상태를 확인합니다. 특별한 요구 사항이 없는 경우 기본값 사용을 권장하며, 설정 가능한 범위는 0 - 100입니다.
 - 신뢰도 의심 임계값: VOD는 사용자가 업로드한 스마트 인식 비디오를 계산하여 스마트 인식 점수가 사용자가 설정한 값을 초과하면 해당 항목의 스마트 인식 상태를 의심해 비디오 스마트 인식 페이지에서 수동 재심사를 제안합니다. 특별한 요구 사항이 없는 경우 기본값 사용을 권장하며, 설정 가능한 범위는 0 - 100입니다.
 
생성한 템플릿은 템플릿 리스트에 표시되며, 템플릿 보기, 편집, 삭제 등의 관리 작업을 할 수 있습니다.

>?콘솔에서 [스마트 인식 - 사전 설정 매개 변수 템플릿](https://intl.cloud.tencent.com/document/product/266/33932#video-ai)을 볼 수 있습니다.
