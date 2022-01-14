

## 사용 수칙

### 내용 소개

이 문서에서는 VOD로 동영상을 트랜스코딩하고 트랜스코딩 출력 결과를 얻는 방법을 설명합니다.

### 요금

이 문서에 제공된 코드는 오픈 소스이며 무료이지만 사용 중 다음과 같은 비용이 발생할 수 있습니다.

- TencentCloud API 요청 스크립트를 실행하기 위한 Tencent Cloud CVM 인스턴스 구입 요금입니다. 자세한 내용은 [CVM 과금](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.
- 업로드된 동영상이 차지하는 VOD 저장 공간. 자세한 내용은 [비디오 스토리지 가격](https://intl.cloud.tencent.com/document/product/266/14666)을 참고하십시오.
- VOD 트랜스코딩 서비스 사용 시간. 자세한 내용은 [비디오 트랜스코딩 가격](https://intl.cloud.tencent.com/document/product/266/14666)을 참고하십시오.
- 동영상 재생에 사용된 VOD 트래픽. 자세한 내용은 [트래픽 과금](https://intl.cloud.tencent.com/document/product/266/14666)을 참고하십시오.

### 매개변수 소개
Tencent Cloud VOD 동영상 트랜스코딩은 현재 다음 형식을 지원합니다.
<table>
   <tr>
      <th width="0px" style="text-align:center">매개변수</td>
      <th width="0px" style="text-align:center">유형</td>
      <th width="0px"  style="text-align:center">상세 설명</td>
   </tr>
   <tr>
      <td rowspan='2' style="text-align:center">입력 포맷</td>
      <td>컨테이너 형식</td>
      <td>WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WEBM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, OGG</td>
   </tr>
   <tr>
      <td>동영상 인코딩 형식</td>
      <td>AV1, AVS2, H.264/AVC, H.263, H.263+, H.265, MPEG-1, MPEG-2, MPEG-4, MJPEG, VP8, VP9, Quicktime, RealVideo, Windows Media Video</td>
   </tr>
   <tr>
      <td rowspan='4' style="text-align:center">출력 포맷</td>
      <td rowspan='3'>컨테이너 형식</td>
      <td>동영상: FLV, MP4, HLS(m3u8+ts)</td>
   </tr>
   <tr>
      <td>오디오: MP3, MP4, OGG, FLAC, m4a</td>
   </tr>
   <tr>
      <td>이미지: GIF, WEBP</td>
   </tr>
   <tr>
      <td>동영상 인코딩 형식</td>
      <td>H.264/AVC, H.265/HEVC, AV1</td>
   </tr>
</table>

트랜스코딩의 타깃 사양에는 인코딩 포맷, 해상도 및 비트 레이트 등과 같은 매개변수가 포함됩니다. VOD는 트랜스코딩 템플릿을 사용하여 트랜스코딩 매개변수 집합을 나타냅니다. 트랜스코딩 템플릿을 통해 다음과 같은 트랜스코딩 관련 매개변수를 지정할 수 있습니다. 자세한 내용은 [비디오 처리 개요](https://intl.cloud.tencent.com/document/product/266/33930)를 참고하십시오.
<table>
   <tr>
      <th width="108px" style="text-align:center">카테고리</td>
      <th width="200px" style="text-align:center">매개변수</td>
      <th width="0px"  style="text-align:center">설명</td>
   </tr>
   <tr>
      <td rowspan='7' width="0px" style="text-align:center">동영상 인코딩</td>
      <td>인코딩 방식(Codec)</td>
      <td>H.264, H.265 및 AV1 인코딩 포맷 지원</td>
   </tr>
	  <tr>
      <td>비트 레이트(Bitrate)</td>
      <td>동영상 비트 레이트 지원 범위: 10kbps-35Mbps</td>
   </tr>
	    <tr>
      <td>프레임 레이트(Frame Rate)</td>
      <td>지원되는 프레임 레이트 범위: 1fps-60fps, 일반적인 프레임 레이트 24fps, 25fps 및 30fps</td>
   </tr>
	    <tr>
      <td>해상도(Resolution)</td>
      <td><li>폭 지원 범위: 128px - 4096px</li><br><li>높이 지원 범위: 128px - 4096px</li><br></td>
   </tr>
	    <tr>
      <td>GOP 길이</td>
      <td>GOP 길이 지원 범위: 1초 - 10초</td>
   </tr>
	    <tr>
      <td>프로파일(Profile)</td>
      <td><li>동영상 인코딩 방식이 H.264인 경우 Baseline, Main 및 High의 인코딩 등급이 지원됩니다.</li><br><li>동영상 인코딩 방식이 H.265인 경우 Main의 인코딩 등급이 지원됩니다.</li><br></td>
   </tr>
	    <tr>
      <td>색 공간(Color Space)</td>
      <td>YUV420P 지원</td>
   </tr>
</table>

>?
>- **인코딩 방식**: 특정 압축 기술을 통해 동영상을 다른 형식의 파일로 변환하는 방식을 말합니다. H.264와 비교하여 H.265는 코드 변환을 위해 보다 발전된 인코딩 방법을 사용하여 비트 레이트를 크게 줄이고, 원본 이미지 품질을 유지하면서 재생 대역폭을 절감합니다.
>- **비트 레이트**: 인코더가 초당 컴파일하는 데이터 크기(kbps)입니다. 예를 들어 800kbps는 인코더가 초당 800kb의 데이터를 생성한다는 의미입니다.
>- **프레임 레이트(FPS)**: 초당 프레임 수를 나타냅니다.
>- **해상도**: 단위 인치에 포함된 픽셀 수입니다.
>- **GOP**: 일반적으로 두 I-프레임 사이의 간격을 나타냅니다.

일반 트랜스코딩 및 다른 해상도의 경우 권장 비트 레이트, 해상도 및 설정 간격은 다음 표와 같습니다.

| **선명도** | **권장 비트 레이트** | **권장 해상도** | **해상도 범위**            |
| ------- | -------- | --------- | -------------------- |
| SD      | 600      | 640x480   | SD(짧은 변 ≤ 480px)    |
| HD      | 2000     | 1280x720  | HD(짧은 변 ≤ 720px)    |
| FHD     | 4000     | 1920x1080 | FHD(짧은 변 ≤ 1080px) |
| 2K      | 6000     | 2560x1440 | 2K(짧은 변 ≤ 1440px)      |
| 4K      | 8000     | 3840x2160 | 4K(짧은 변 ≤ 2160px)      |

Tencent Cloud의 고유한 TESHD는 이미지 품질 복원 및 향상, 콘텐츠 어댑티브 매개변수 선택, V265 인코더와 같은 동영상 처리 솔루션를 통합합니다. 동영상을 더 작고 선명하게 만드는 트랜스코딩 방법을 제공하여 네트워크 리소스를 적게 소비함과 동시에 사용자에게 더 나은 시각적 경험을 제공합니다. 다양한 선명도가 VOD에 대해 사전 설정되어 있으며 특정 매개변수는 다음과 같습니다.

| **선명도** | **권장 비트 레이트** | **권장 해상도** | **해상도 범위**            |
| ------- | -------- | --------- | -------------------- |
| SD      | 350 또는 미설정   | 640x480   | SD(짧은 변 ≤ 480px)    |
| HD      | 1350 또는 미설정  | 1280x720  | HD(짧은 변 ≤ 720px)    |
| FHD     | 2700 또는 미설정  | 1920x1080 | FHD(짧은 변 ≤ 1080px) |
| 2K      | 3500 또는 미설정  | 2560x1440 | 2K(짧은 변 ≤ 1440px)      |
| 4K      | 7500 또는 미설정  | 3840x2160 | 4K(짧은 변 ≤ 2160px)      |

>?미설정 시 TESHD는 동영상 소스를 지능적으로 분석하고 동영상의 최저 비트 레이트를 지능적으로 설정합니다.

## 콘솔에서 트랜스코딩 시작

### 1단계: VOD 활성화[](id:p11)

[시작하기 - 1단계](https://intl.cloud.tencent.com/document/product/266/8757)를 참고하여 VOD 서비스를 활성화합니다.

### 2단계: 동영상 업로드[](id:p12)

[시작하기 - 2단계](https://intl.cloud.tencent.com/document/product/266/8757)를 참고하여 테스트 동영상을 업로드합니다. Demo에 사용된 테스트 동영상을 보려면 [여기](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4)를 클릭합니다. 해당 FileId는 아래와 같이 8602268010602075659입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9d10415aff42613a6b9899c552d053d2.png)
>?트랜스코딩에 너무 많은 시간이 소요되지 않도록 테스트에 짧은 동영상 파일(지속 시간 수십 초)을 사용하는 것이 좋습니다.

### 3단계: 트랜스코딩 시작[](id:p13)

콘솔의 [비디오 관리](https://console.cloud.tencent.com/vod/media) 페이지에서 업로드된 테스트 동영상을 확인하고 [비디오 처리]를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9d10415aff42613a6b9899c552d053d2.png)
팝업 창에서 [트랜스코딩] 처리 유형을 선택하고 [트랜스코딩 템플릿]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bb552a5454fe649f2b61edf2d5fe50fa.png)
원하는 트랜스코딩 템플릿을 선택하고 [확인]을 클릭합니다. 이 Demo에서는 사전 설정 템플릿 STD-H264-MP4-360P(템플릿 ID 100010) 및 STD-H264-MP4-540P(템플릿 ID 100020)를 예시로 사용합니다. 사용자 정의 트랜스코딩 템플릿을 사용하려면 [템플릿 설정 문서](https://intl.cloud.tencent.com/document/product/266/14059)를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/d26764d535ee63e216969e21ee7e6e46.png)
[확인]을 클릭하여 트랜스코딩을 시작합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e370f7ee3ae245e5b97d47fa383e2be8.png)
‘비디오 관리’ 페이지에서 테스트 동영상 상태가 ‘처리 중’임을 확인할 수 있으며 이는 동영상이 트랜스코딩되고 있음을 나타냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9c329fbf018cd251c2280d2df453f041.png)

### 4단계: 트랜스코딩 결과 조회[](id:p14)

콘솔의 [비디오 관리](https://console.cloud.tencent.com/vod/media) 페이지에서 트랜스코딩이 완료되어 테스트 동영상 상태가 ‘정상’으로 바뀔 때까지 대기합니다. 그런 다음 테스트 동영상 오른쪽에 있는 [관리]를 클릭하여 동영상 관리 페이지로 들어갑니다.
![](https://qcloudimg.tencent-cloud.cn/raw/be5fa72994d786fa6737bf3590d4324f.png)
‘기본 정보’ 탭의 [표준 트랜스코딩 목록]에서 STD-H264-MP4-360P 및 STD-H264-MP4-540P 사양의 동영상이 출력됩니다. 오른쪽에 있는 [미리보기]를 클릭하면 해당 영상을 바로 볼 수 있습니다. [주소 복사]를 클릭하여 해당 출력 동영상의 URL을 복사하고 다른 채널을 통해 시청자에게 게시할 수도 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/48867ad69971690bc6a528cf9f14473c.png)

## TencentCloud API를 호출하여 트랜스코딩 시작

### 1단계: Tencent Cloud CVM 준비[](id:p21)

TencentCloud API 요청 스크립트는 다음 요구 사항을 충족하는 CVM 인스턴스에서 실행해야 합니다.

- 리전: 랜덤.
- 모델: 공식 웹 사이트의 최저 사양(1코어 1GB).
- 공용 네트워크: 공용 IP를 보유해야 하며 대역폭은 1Mbps 이상.
- 운영 체제: 공식 웹 사이트의 공용 이미지 `Ubuntu Server 16.04.1 LTS 64비트` 또는 `Ubuntu Server 18.04.1 LTS 64비트`.

CVM 구매 방법은 [운영 가이드 - 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오. 시스템 재설치 방법은 [운영 가이드 - 시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참고하십시오.

>!상기 조건에 부합하는 Tencent Cloud CVM이 없을 경우, 다른 공인 네트워크의 Linux(예: CentOS, Debian 등) 또는 Mac 디바이스에서도 스크립트를 실행할 수 있으나 운영 체제에 따라 스크립트의 개별 명령을 수정해야 합니다. 자세한 수정 방법은 개발자가 직접 검색하시기 바랍니다.

### 2단계: API Keys 가져오기[](id:p22)

TencentCloud API 요청에는 API 키(예: SecretId 및 SecretKey)가 필요합니다. 아직 API 키를 생성하지 않았다면 [보안키 생성 파일](https://intl.cloud.tencent.com/document/product/598/34228)을 참고하여 새로운 API 키를 생성합니다. 이미 키를 생성했다면 [보안키 파일 조회](https://intl.cloud.tencent.com/document/product/598/34228)을 참고하여 API 키를 가져옵니다.

### 3단계: VOD 활성화[](id:p23)

[시작하기 - 1단계](https://intl.cloud.tencent.com/document/product/266/8757)를 참고하여 VOD 서비스를 활성화합니다.

### 4단계: 동영상 업로드[](id:p24)
[시작하기 - 2단계](https://intl.cloud.tencent.com/document/product/266/8757)를 참고하여 테스트 동영상을 업로드합니다. 데모에 사용된 테스트 동영상을 보려면 [여기](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4)를 클릭합니다. 해당 FileId는 아래와 같이 5285890804162014755입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fb2ac8243834a909cee60aaf19426bea.png)
>?트랜스코딩에 너무 많은 시간이 소요되지 않도록 테스트에 짧은 동영상 파일(지속 시간 수십 초)을 사용하는 것이 좋습니다.


### 5단계: 트랜스코딩 시작[](id:p25)

[1단계](#p21)에서 준비한 CVM(로그인 방식은 [운영 가이드 - Linux 로그인](https://intl.cloud.tencent.com/document/product/213/5436)참고)에 로그인하여, 원격 터미널에 다음 명령어를 입력하고 실행합니다.
```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/transcode_api.sh
```
>?[2단계](#p22)에서 얻은 해당 값을 명령어의 SECRET_ID와 SECRET_KEY에 할당합니다.

해당 명령은 Github로부터 Demo 소스 코드를 다운로드하고 설치 스크립트를 자동 실행합니다. 설치 프로세스는 수 분(실제 시간은 CVM 네트워크 상태에 따라 다름)이 소요되며, 원격 터미널에서 다음과 같은 정보를 인쇄합니다.
```
  [2020-06-15 20:39:56] pip3 설치 시작.
  [2020-06-15 20:40:06]pip3 설치 성공.
  [2020-06-15 20:40:06]Cloud API Python SDK 설치 시작.
  [2020-06-15 20:40:07]Cloud API Python SDK 설치 완료.
  [2020-06-15 20:40:07]API 매개변수 설정 시작.
  [2020-06-15 20:40:07]API 매개변수 설정 완료.
```
‘process_media.py’ 스크립트를 실행하여 트랜스코딩을 시작합니다.
```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/transcode_api/; python3 process_media.py 5285890804162014755
```
>?명령의 5285890804162014755를 [4단계](#p24)에서 얻은 실제 FileId로 바꾸십시오.

이 명령은 5285890804162014755 동영상에 대한 [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) 요청을 시작하여 두 VOD [사전 설정 트랜스코딩 템플릿](https://intl.cloud.tencent.com/document/product/266/33932) 사양 100010 및 100020 으로 트랜스코딩하고 요청 응답 콘텐츠를 출력합니다.
```
{"TaskId": "1400329073-procedurev2-f6bf6f01612369b6db30f2224792a2aft0", "RequestId": "809918fb-791c-4937-b684-5027ba6bc5f0"}
```

### 6단계: 트랜스코딩 결과 조회[](id:p14)

‘비디오 관리’ 페이지에서 테스트 동영상 상태가 ‘처리 중’임을 확인할 수 있으며 이는 동영상이 트랜스코딩되고 있음을 나타냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5fcd99f766d6587f1644daac23c10d4d.png)
테스트 동영상 트랜스코딩이 완료되어 ‘정상’ 상태로 바뀔 때까지 기다립니다. 그런 다음 테스트 동영상 오른쪽에 있는 [관리]를 클릭하여 동영상 관리 페이지로 들어갑니다.
![](https://qcloudimg.tencent-cloud.cn/raw/be5fa72994d786fa6737bf3590d4324f.png)
‘기본 정보’ 탭의 [표준 트랜스코딩 목록]에서 해당 사양의 동영상이 출력됩니다. 오른쪽에 있는 [미리보기]를 클릭하면 해당 영상을 바로 볼 수 있습니다. [주소 복사]를 클릭하여 해당 출력 동영상의 URL을 복사하고 다른 채널을 통해 시청자에게 게시할 수도 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9067b71ebcac7658c58222499f47fcf0.png)

## 동영상 업로드 후 자동 트랜스코딩(태스크 플로우)

VOD는 콘솔을 통한 업로드, 서버에서 업로드, 클라이언트에서 업로드, URL에서 가져오기(자세한 내용은 [미디어 업로드 개요](https://intl.cloud.tencent.com/document/product/266/9760)참고)와 같은 다양한 동영상 업로드 방법을 제공합니다. 모든 업로드 방법을 사용하면 업로드가 완료된 후 자동으로 트랜스코딩을 트리거할 수 있는 [태스크 플로우](https://intl.cloud.tencent.com/document/product/266/33931)를 지정할 수 있습니다.

## 동영상 업로드 후 자동 트랜스코딩 (이벤트 알림)

동영상 업로드 또는 트랜스코딩 작업이 완료된 후 VOD 백엔드는 [이벤트 알림](https://intl.cloud.tencent.com/document/product/266/33948) 요청을 시작합니다. 이벤트 알림 메커니즘을 사용하여 새로 업로드된 동영상에 대한 트랜스코딩을 시작하고 이벤트 알림을 통해 트랜스코딩 결과를 자동으로 얻을 수 있습니다(상기에서 설명한 방법은 콘솔에서 트랜스코딩 결과를 수동으로 조회하는 것입니다). 자세한 내용은 모범 사례의 [이벤트 알림 수신](https://intl.cloud.tencent.com/document/product/266/37542) 방법을 참고하십시오.

