## 개요
사용자는 정적 리소스(정적 스크립트, 오디오 및 비디오, 이미지, 첨부 파일 등)를 모두 Tencent Cloud COS의 표준 스토리지에 호스팅할 수 있으며, 무제한 용량, 고빈도 읽기 및 쓰기 특징을 이용하여 정적 리소스에 확장 가능하고 신뢰할 수 있는 스토리지를 제공하여 리소스 서버의 부담을 줄일 수 있습니다. COS의 정적 리소스가 CDN 서비스에 액세스하여 CDN에서 글로벌 가속을 수행하고 사용자 클라이언트에 배포할 수 있습니다.

## 과금 설명
COS가 CDN 원본 서버인 경우 CDN 과금(가속)과 COS 과금(원본 서버)의 두 가지 과금이 포함됩니다.

### CDN 과금
CDN이 가속 서비스를 수행하는 경우 CDN 노드에서 리소스를 가져와 사용자 클라이언트에 배포할 때 소모한 용량은 CDN에서 과금을 진행합니다. 자세한 과금 설명은 [CDN 과금 설명](https://intl.cloud.tencent.com/document/product/228/2949)을 참조하십시오.

### COS 과금
CDN Origin-pull인 경우 COS 원본 서버에서 리소스를 가져오고 사용한 용량은 COS에서 과금을 진행합니다. 자세한 과금 설명은 [COS 과금 설명](https://intl.cloud.tencent.com/document/product/436/16871)을 참조하십시오.
![](https://main.qcloudimg.com/raw/794db40485325436ec6f52e32f0df117.jpg)



