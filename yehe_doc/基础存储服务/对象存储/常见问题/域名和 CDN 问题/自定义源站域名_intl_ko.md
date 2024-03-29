### 자체 도메인을 사용해 객체에 액세스할 수 있나요?

사용자 정의 도메인 바인딩을 통해 구현할 수 있습니다. 자세한 내용은 [사용자 정의 원본 서버 도메인 활성화하기](https://intl.cloud.tencent.com/document/product/436/31507)를 참고하십시오.

### 사용자 정의 도메인을 사용하려면 반드시 Tencent Cloud ICP비안을 받아야 하나요?

사용자의 상황에 따라 판단합니다.

- 도메인이 중국 내 CDN에 액세스하는 경우 ICP비안이 필요합니다. 그러나 반드시 Tencent Cloud ICP비안을 받을 필요는 없으며, ICP비안이 등록된 액세스 도메인이면 됩니다.
- 도메인이 해외 CDN에 액세스하는 경우 ICP비안이 필요 없습니다.

### COS의 사용자 정의 도메인은 HTTPS를 지원하나요?

사용자 지정 COS 도메인 이름에 대해 HTTPS를 구성하는 기능은 현재 업그레이드 중입니다. 현재 인증서 호스팅은 중국 본토와 싱가포르 및 실리콘 밸리의 퍼블릭 클라우드 리전에서 지원되며 더 많은 리전이 추가될 예정입니다. 다른 리전의 경우 [사용자 지정 엔드포인트에 대한 HTTPS 지원](https://intl.cloud.tencent.com/document/product/436/11142) 문서를 참고해 도메인 이름에 대한 역방향 프록시를 구성할 수 있습니다.

### COS에서 파일을 업로드한 후 사용자 정의 도메인의 액세스 링크를 어떻게 반환하나요?

COS는 현재 파일 업로드 후 사용자 도메인 액세스 링크 반환을 지원하지 않습니다. 도메인 접합을 통해 이를 구현할 수 있으며, [기본 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 사용자 정의 도메인으로 변경하면 됩니다.

### 사용자 정의 도메인을 사용하여 COS에 액세스하려면 CDN을 활성화해야 하나요?

사용자 정의 도메인을 사용해 COS에 액세스하는 경우 CDN을 활성화할 필요가 없습니다. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하여 사용자 정의 원본 서버 도메인을 설정하면 됩니다. 자세한 작업 방법은 [사용자 정의 원본 서버 도메인 활성화하기](https://intl.cloud.tencent.com/document/product/436/31507) 문서를 참고하십시오.

### CDN 콘솔에서 원본 서버를 변경하면 COS 콘솔에서 기존의 사용자 정의 도메인이 사라지는 이유가 무엇인가요?

**V5 버전 콘솔을 사용하면 JSON 버전 도메인 설정이 따라오며, COS V5 콘솔은 신규 도메인을 표시할 수 없습니다.** 버킷에 JSON 도메인이 설정되어 있는지 확인하시고, JSON 버전 도메인을 XML 도메인으로 변경하십시오.

### 사용자 정의 도메인을 COS 버킷에 바인딩하려면 먼저 경량급 서버의 리졸브를 삭제해야 하나요?

도메인 1개당 하나의 CNAME 기록을 설정할 수 있습니다. 따라서 먼저 경량급 서버의 리졸브 관계를 삭제한 후, 다시 리졸브 관계를 COS 버킷에 바인딩해야 합니다.


### 리졸브 또는 CNAME이 적용되지 않았다고 표시됩니다. 어떻게 처리해야 하나요?

리졸브 또는 CNAME 설정은 적용하는 데 몇 분의 시간이 소요됩니다. 잠시 기다렸다가 사용자 정의 원본 서버 도메인을 사용해 버킷에 액세스해 보시기 바랍니다. 계속해서 적용되지 않는 경우 DNS 콘솔에 로그인하여 리졸브 관계가 정확하게 설정되어 있는지 확인합니다.

