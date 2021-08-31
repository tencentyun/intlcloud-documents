## 개요
사용자는 모든 정적 리소스(정적 스크립트, 멀티미디어, 이미지, 첨부 파일 등)를 Tencent Cloud COS의 표준 스토리지에서 호스팅할 수 있으며, 그 특징인 무제한 용량 및 고빈도 읽기 및 쓰기로 확장 가능하고 신뢰할 수 있는 스토리지를 정적 리소스에 제공함으로써, 리소스 서버의 부담을 줄일 수 있습니다. COS 내의 정적 리소스를 CDN 서비스에 연결하여 CDN의 글로벌 가속을 통해 사용자 클라이언트로 배포할 수 있습니다.

## 과금 설명
COS가 CDN 원본 서버일 때에는, CDN 과금(가속)과 COS 과금(Origin-pull) 두 가지 과금으로 구분됩니다.

### CDN 과금
CDN 가속 서비스를 수행하는 경우, CDN 노드에서 리소스를 가져와 사용자 클라이언트에 배포할 때 사용한 용량은 CDN에서 과금합니다. 자세한 과금 설명은 [CDN 과금 설명](https://intl.cloud.tencent.com/document/product/228/2949)을 참조 바랍니다.

### COS 과금
CDN Origin-pull의 경우, COS 원본 서버에서 리소스를 가져올 때 사용한 용량은 COS에서 과금합니다. 자세한 과금 설명은 [COS 과금 설명](https://intl.cloud.tencent.com/document/product/436/16871)을 참조 바랍니다.
![](https://main.qcloudimg.com/raw/64557185ea11d642a939f2c0cb650e50.png)



