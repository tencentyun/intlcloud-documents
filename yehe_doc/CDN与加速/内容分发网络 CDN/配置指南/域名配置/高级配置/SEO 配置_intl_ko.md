## 설정 시나리오
SEO 최적화 설정은 CDN에 도메인을 액세스한 후 CDN이 IP를 자주 변경하여 도메인 검색 결과에 가중치를 부여하는 문제를 해결하는 기능입니다.액세스 IP가 검색 엔진에 속하는지 식별함으로써, 사용자는 리소스에 직접 Origin-pull 액세스하여 검색 엔진 가중치의 안정성을 보장할 수 있습니다.


> !
> - 검색 엔진 IP가 자주 업데이트되므로 Tencent Cloud CDN은 대다수의 검색 엔진 IP 인식만 보장할 수 있습니다.
> - SEO 설정 기능은 도메인 원본 서버 유형이 [외부 원본](https://intl.cloud.tencent.com/document/product/228/6289)인 경우에만 사용할 수 있습니다.SEO 최적화 설정 기능 활성화 후 만약 도메인에 여러 원본 서버 주소가 있는 경우 기본 Origin-pull 주소는 추가된 첫 번째 원본 서버 주소입니다.
> - 중국 외 지역에서는 지원되지 않습니다.도메인의 가속 리전이 중국 외 지역인 경우 SEO 설정이 지원되지 않습니다.도메인의 가속 리전이 글로벌인 경우 SEO 설정 활성화 후 중국 내에만 적용됩니다.
## 설정 가이드

### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [도메인 이름 관리]를 선택한 뒤 도메인 오른쪽의 [관리]를 클릭하면 도메인 설정 페이지로 이동하여 [고급 설정]에서 SEO 설정을 확인할 수 있습니다. 비활성화 상태로 기본 설정되어 있습니다.
![](https://main.qcloudimg.com/raw/44f35a715f922cda12191d50e1cfc723.png)

### 설정 수정
SEO 설정 스위치를 통해 직접 서비스를 활성화 또는 비활성화할 수 있습니다.
![](https://main.qcloudimg.com/raw/8ea737dbd456397286f3ef8ff965aaf2.png)


