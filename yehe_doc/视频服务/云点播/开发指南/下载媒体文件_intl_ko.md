VOD에 저장된 미디어 파일을 다운로드하여 로컬 디스크 또는 다른 위치에 저장할 수 있습니다.

### 미디어 파일
VOD는 업로드한 원본 파일과 트랜스코딩 파일, 스크린샷, 썸네일 등 VOD 서비스를 사용하면서 생성된 파일을 포함한 다양한 유형의 다운로드용 미디어 파일을 제공합니다.

* 오디오/비디오
  * 원본 오디오/비디오 파일: VOD로 업로드한 오디오/비디오 파일입니다.
  * 처리된 오디오/비디오 파일: 트랜스코딩 파일 및 어댑티브 비트레이트 파일과 같은 미디어 처리 작업으로 생성된 오디오/비디오 파일입니다.
* 이미지
  * 원본 이미지 파일: VOD에 업로드한 이미지 파일입니다.
  * 처리된 이미지 파일: 스크린샷, 이미지 스프라이트, 애니메이션 이미지 등 미디어 처리 작업으로 생성된 이미지 파일입니다.

### 콘솔에서 다운로드 URL 가져오기
* [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인합니다. 왼쪽 사이드바에서 **미디어 자산**을 선택하고 **오디오/비디오 관리** 또는 **이미지 관리**를 클릭합니다. 대상 파일을 찾아 오른쪽 **관리**를 클릭하여 파일의 다운로드 URL을 가져옵니다. 자세한 내용은 [오디오/비디오 보기](https://intl.cloud.tencent.com/document/product/266/33895) 또는 [이미지 관리](https://intl.cloud.tencent.com/document/product/266/37903)를 참고하십시오.
* [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인하고 왼쪽 사이드바에서 **미디어 자산**>**오디오/비디오 관리**를 선택합니다. 오른쪽 상단 모서리에 있는 **더 많은 일괄 작업**에서 모든 파일의 다운로드 URL을 내보냅니다. 자세한 내용은 [오디오/비디오 내보내기](https://intl.cloud.tencent.com/document/product/266/38534)를 참고하십시오.

### API를 사용하여 다운로드 URL 가져오기
다음 API를 사용하여 미디어 파일의 다운로드 URL을 가져올 수도 있습니다.
- [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181)
- [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179)

### 다운로드한 파일 이름 지정
일반적으로 브라우저에서 미디어 파일의 URL을 열면 파일을 다운로드하는 대신 브라우저에서 파일을 엽니다. 예를 들어 브라우저로 비디오의 URL을 열면 브라우저가 비디오 재생을 시작합니다. 파일을 다운로드하려면 QueryString에 `download_name` 매개변수를 추가하면 됩니다. 이렇게 하면 다운로드한 파일의 이름을 지정할 수도 있습니다. 다음은 예입니다.
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?download_name=[download_name]
```

>!
>- 링크 도용 방지를 활성화하면 Referer 얼로우리스트/블록리스트 또는 URL 만료 시간과 같은 제한 사항이 다운로드에 적용될 수 있습니다. 자세한 내용은 [링크 도용 방지 개요](https://intl.cloud.tencent.com/document/product/266/33984)를 참고하십시오.
>- 동영상이 암호화된 경우 다운로드하는 트랜스코딩 파일도 암호화됩니다. 동영상을 재생하려면 먼저 파일의 암호를 해독해야 합니다. 자세한 내용은 [암호화된 동영상 재생](https://intl.cloud.tencent.com/document/product/266/38294)을 참고하십시오.
>- HLS 파일의 경우 인덱스 파일과 세그먼트 파일을 모두 다운로드해야 합니다. 이를 방지하기 위해 HLS 파일을 MP4로 트랜스코딩할 수 있습니다.