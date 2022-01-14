### VOD 업로드를 지원하는 미디어 파일 형식은 무엇입니까?

지원되는 VOD 파일 형식:
- 비디오: WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WEBM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, OGG.
- 오디오: MP3, M4A, FLAC, OGG, WAV, RA, AAC, AMR.
- 썸네일: JPG, JPEG, PNG, GIF, BMP, TIFF, AI, CDR, EPS, TIF.

### VOD에 파일을 업로드하려면 어떻게 해야 합니까? 체크포인트 재시작이 지원됩니까?
파일은 [콘솔에서 업로드](https://intl.cloud.tencent.com/document/product/266/33890), [서버에서 업로드](https://intl.cloud.tencent.com/document/product/266/33912), [클라이언트에서 업로드](https://intl.cloud.tencent.com/document/product/266/33921)의 방법으로 VOD에 업로드할 수 있습니다. 그 중 클라이언트에서 업로드는 체크포인트 재시작을 지원합니다.

### 콘솔에서 VOD에 동영상을 업로드하려면 어떻게 합니까?
자세한 내용은 [비디오 업로드](https://intl.cloud.tencent.com/document/product/266/33890)를 참고하십시오.


### VOD로 업로드 진행 상황을 확인하려면 어떻게 해야 하나요?

업로드 진행 상황은 가져올 수 없습니다.

### 업로드 후 동영상은 언제 볼 수 있나요?
동영상 길이와 트랜스코딩 비트 레이트에 따라 다릅니다.

### VOD는 App이나 웹 페이지에서 동영상 업로드를 허용합니까?

VOD를 사용하면 최종 사용자가 직접 파일을 업로드할 수 있습니다. 자세한 내용은 [클라이언트 업로드 가이드](https://intl.cloud.tencent.com/document/product/266/33921)를 참고하십시오.

### VOD 백엔드의 업로드 디렉터리는 무엇입니까?
현재 VOD는 업로드 디렉터리를 제공하지 않습니다. 카테고리 구조를 디렉터리로 사용하고 해당 카테고리에 파일을 업로드할 수 있습니다. 자세한 내용은 [비디오 카테고리 수정](https://intl.cloud.tencent.com/document/product/266/33893)을 참고하십시오.

### 업로드한 비디오를 압축할 수 있습니까?
현재 비디오 압축은 지원되지 않습니다.

### 많은 수량의 비디오 파일을 VOD에 업로드하려면 어떻게 해야 하나요?
VOD는 대기열 업로드 방식을 사용하여 비디오 파일의 순차적 업로드를 보장합니다. 특별한 요구 사항이 있는 경우(예: TB에서 PB 단위로 파일을 업로드해야 하는 경우) [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 하시기 바랍니다.

### 업로드 반환 URL이 HTTP입니다. HTTPS로 설정하려면 어떻게 해야 합니까?
자세한 내용은 [기본 배포 설정](https://intl.cloud.tencent.com/document/product/266/35768)을 참고하십시오.

### VOD의 Web 업로드 SDK에 필요한 개발 환경은 무엇입니까?
- 브라우저가 HTML5를 지원해야 합니다.
- App 서버는 클라이언트에서 업로드할 서명을 배포해야 합니다. 서명을 생성하는 방법은 [간단한 동영상 업로드](https://intl.cloud.tencent.com/document/product/266/33924)를 참고하십시오.

### VOD는 모바일 장치에 어떤 업로드 SDK를 제공합니까?

현재 VOD는 모바일용 Android SDK와 iOS SDK를 제공하고 있습니다.
비디오 업로드 API 외에도 모바일 SDK는 다양한 비디오 편집 API를 제공하여 고객의 니즈를 충족시킵니다. 비디오 클리핑, 스플라이싱, 필터링에서 자막에 이르기까지 다양합니다.

### 비디오 업로드 서명에 암호화된 트랜스코딩 템플릿을 지정할 수 있습니까?
현재 지원되지 않습니다. 이 기능은 개발 중이며 추후 지원 예정입니다.

### VOD의 비디오 업로드 API는 Go, PHP, .NET을 지원합니까?
TencentCloud API 3.0은 Go, PHP 및 .NET용 SDK를 지원합니다. 자세한 내용은 [인터페이스 업로드 신청 문서](https://intl.cloud.tencent.com/document/product/266/34120)를 참고하십시오.



### 동영상을 성공적으로 업로드한 후 링크를 공유하려면 어떻게 합니까?
아래 단계에 따라 링크를 공유할 수 있습니다.
1. 콘솔에서 배포를 신청합니다.
2. 신청이 승인되면 공유 가능한 링크가 반환됩니다.
3. 링크를 사용하여 비디오를 공유합니다.

자세한 내용은 [비디오 배포](https://intl.cloud.tencent.com/document/product/266/33896)를 참고하십시오.

### VOD에 업로드된 동영상의 커버를 자동으로 생성할 수 있습니까?

할 수 있습니다. 비디오가 업로드되면 VOD는 첫 번째 프레임을 커버로 사용하거나 동영상에서 커버를 가져옵니다.


### VOD 동영상 풀링은 M3U8 파일을 지원합니까?

현재 M3U8 파일을 가져올 수 없습니다.
