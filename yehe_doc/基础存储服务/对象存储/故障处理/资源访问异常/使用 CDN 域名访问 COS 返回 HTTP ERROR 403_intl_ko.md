## 현상 설명

Content Delivery Network(CDN) 도메인을 사용해 Cloud Object Storage(COS)에 액세스하는 경우 HTTP ERROR 403 에러 코드 반환


## 예상 원인

CDN 가속 도메인이 비활성화 상태인 경우

## 처리 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 메뉴에서 [버킷 리스트]를 선택해 버킷 관리 페이지로 이동합니다.
3. 작업할 버킷을 찾아 버킷 이름을 클릭하여 버킷 설정 페이지로 이동합니다.
4. 왼쪽 메뉴에서 [도메인 및 전송 관리]>[기본 CDN 가속 도메인]을 선택해 기본 CDN 가속 도메인 페이지로 이동합니다.
5. '기본 CDN 가속 도메인'에서 현재 상태가 비활성화 상태인지 확인합니다.
 - 예. [기본 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31505)를 참조하십시오.
 - 아니요. 다음 단계를 실행합니다.
6. '사용자 정의 CDN 가속 도메인'에서 상태가 런칭으로 되어 있는지 확인합니다.
 - 예. [고객센터](https://intl.cloud.tencent.com/support)로 문의하십시오.
 - 아니요. [사용자 정의 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31506)를 참조하십시오.

