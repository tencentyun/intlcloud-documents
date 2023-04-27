## 개요

COS 콘텐츠 조정 서비스는 이미지, 비디오, 오디오, 텍스트, 문서 및 웹 페이지의 멀티미디어 콘텐츠를 지능적으로 조정합니다. 선정적이고 저속한 콘텐츠, 규정 위반 콘텐츠, 역겹고 반감을 일으키는 콘텐츠와 같은 비준수 콘텐츠를 효과적으로 식별하여 운영 상의 위험을 방지할 수 있습니다. 현재 다음 형식의 파일을 조정할 수 있습니다.

| 파일 유형 | 제한                                                     |
| -------- | ------------------------------------------------------------ |
| 이미지     | <ul  style="margin: 0;"><li>png, jpeg, jpg, bmp, webp 및 gif 형식이 지원됩니다. </li><li>이미지 크기는 5MB를 초과할 수 없습니다. 이미지의 너비와 높이는 20 x 20 픽셀 이상이어야 합니다. </li></ul> |
| 비디오     | <ul  style="margin: 0;"><li>mp4, avi, mkv, wmv, rmvb, flv, m3u8 형식이 지원됩니다. </li><li>동영상 크기는 5GB를 초과할 수 없으며 캡처된 프레임 수는 1만을 초과할 수 없습니다.</li></ul> |
| 오디오     | <ul  style="margin: 0;"><li>mp3, wav, aac, flac, amr, 3gp, m4a, wma, ogg, ape 형식이 지원됩니다. </li><li>오디오 비트 레이트: 128Kbps-256Kbps. <li>오디오 크기: 600MB 미만. 최대 시간: 3시간.</li></ul> |
| 텍스트     | 크기가 1MB 미만인 html 및 txt 파일이 지원됩니다. |
| 라이브 스트림     | <ul  style="margin: 0;"><li>지원되는 라이브 스트리밍 시간: 5시간 이내</li><li>지원되는 라이브 스트리밍 프로토콜: rmtp, hls, http, https 등 주요 프로토콜.</li></ul>     |
| 문서     | 문서 처리 서비스를 통해 조정을 위해 이미지로 변환됩니다. 현재 pdf, ppt, excel 등 수십 개의 문서 형식을 지원합니다. 자세한 내용은 [문서 미리보기 개요](https://intl.cloud.tencent.com/document/product/436/49159)를 참고하십시오. |
| 웹페이지     | 시스템은 딥러닝 기술을 기반으로 웹페이지 파일을 자동으로 감지하고 OCR, 객체 감지(객체, 광고 로고, QR 코드 등), 이미지 인식 차원에서 비준수 콘텐츠를 인식할 수 있습니다. |


>? 콘텐츠 조정은 유료 서비스이며, 요금은 CI에서 청구합니다. 과금 세부 정보는 [콘텐츠 조정 요금](https://cloud.tencent.com/document/product/460/58119)을 참고하십시오. 
>

![](https://qcloudimg.tencent-cloud.cn/raw/f4b075ccd69c4c8e9b056a3c628a7f6e.png)

조정 서비스를 활성화한 후 다음 작업을 수행할 수 있습니다.

- 자동 조정을 구성하여 버킷에 업로드된 데이터를 자동으로 조정하고 비준수 데이터를 차단합니다
- API를 호출하여 타사 데이터를 조정합니다
- 버킷의 기존 데이터에 대해 일회성 일괄 조정을 수행합니다

## 사용 사례

이 기능은 소셜 네트워크, 전자 상거래, 광고, 게임 등 분야에 적합합니다. 상기 유형의 파일에서 음란물, 불법, 광고 콘텐츠를 확인할 수 있습니다.

## 사용 가능한 리전

다음 리전이 지원됩니다.

| 리전 | 코드     |
| :--- | :----------- |
| 베이징 | ap-beijing   |
| 난징 | ap-nanjing   |
| 상하이 | ap-shanghai  |
| 광저우 | ap-guangzhou |
| 청두 | ap-chengdu   |
| 충칭 | ap-chongqing |

다른 리전에서 콘텐츠 조정 기능을 사용하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 문의하십시오.

## 사용 방법

### COS 콘솔 사용

#### 자동 조정

COS 콘솔에서 자동 조정 서비스를 활성화하여 새로 업로드된 이미지, 비디오, 오디오, 파일, 문서 및 웹 페이지를 자동으로 조정할 수 있습니다. 자세한 내용은 [자동 조정](https://cloud.tencent.com/document/product/436/47247)을 참고하십시오.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3YaP402_PRELIM__%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)


#### 기존 데이터 조정

COS 콘솔에서 기록 데이터 조정 서비스를 활성화하여 버킷에 이미 저장된 이미지, 비디오, 오디오, 텍스트, 문서 및 웹 페이지에 대해 일회성 일괄 조정을 수행할 수 있습니다.

### API 사용

API를 사용하여 이미지, 비디오, 오디오, 텍스트, 문서 및 웹 페이지의 콘텐츠를 조정할 수 있습니다. 자세한 내용은 다음 API 문서를 참고하십시오.

- [Single Image Moderation](https://intl.cloud.tencent.com/document/product/436/48537) 
- [Submitting Video Moderation Job](https://intl.cloud.tencent.com/document/product/436/48249) 
- [Submitting Audio Moderation Job](https://intl.cloud.tencent.com/document/product/436/48262)
- [텍스트 조정](https://cloud.tencent.com/document/product/436/56287)
- [문서 조정](https://cloud.tencent.com/document/product/436/59378)
- [웹 페이지 조정](https://cloud.tencent.com/document/product/436/63957)
- [라이브 스트림 조정](https://cloud.tencent.com/document/product/436/76259)

조정 후 민감한 데이터로 확인된 파일의 경우 다음 방법 중 하나를 선택하여 처리하는 것이 좋습니다.
- 사용자가 공중망을 통해 익명으로 액세스하지 못하도록 파일의 액세스 권한을 비공개 읽기로 변경합니다. 자세한 내용은 [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748)을 참고하십시오.
- 파일을 백업 디렉터리로 이동합니다. 원본 파일을 지정된 디렉터리에 복사한 후 원본 파일을 삭제하여 파일을 이동합니다. 자세한 내용은 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) 및 [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)를 참고하십시오.
- 파일을 삭제합니다. 자세한 내용은 [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)를 참고하십시오.

### SDK 사용

또한 다양한 프로그래밍 언어용 SDK를 사용하여 이미지, 비디오, 오디오, 텍스트, 문서 및 웹 페이지의 콘텐츠를 조정할 수 있습니다. 자세한 내용은 다음 SDK 문서를 참고하십시오.

| SDK            | 통합 가이드                                                     |
| :------------- | :----------------------------------------------------------- |
| Android SDK    | [콘텐츠 조정](https://cloud.tencent.com/document/product/436/66151) |
| C SDK          | [콘텐츠 조정](https://cloud.tencent.com/document/product/436/62019) |
| .NET(C#) SDK   | [콘텐츠 조정](https://cloud.tencent.com/document/product/436/55328) |
| Go SDK         | [콘텐츠 조정](https://cloud.tencent.com/document/product/436/55368) |
| iOS SDK        | [콘텐츠 조정](https://cloud.tencent.com/document/product/436/55359) |
| Java SDK       | [콘텐츠 조정](https://cloud.tencent.com/document/product/436/55380) |
| JavaScript SDK | [콘텐츠 조정](https://cloud.tencent.com/document/product/436/74611) |
| PHP SDK        | [콘텐츠 조정](https://cloud.tencent.com/document/product/436/61619) |
| Python SDK     | [콘텐츠 조정](https://cloud.tencent.com/document/product/436/55929) |
