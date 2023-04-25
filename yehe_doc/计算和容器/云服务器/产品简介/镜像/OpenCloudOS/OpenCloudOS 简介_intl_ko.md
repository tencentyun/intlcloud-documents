
Tencent가 파트너와 함께 공동으로 시작한 오픈 소스 운영 체제 커뮤니티인 OpenCloudOS는 완전히 중립적이고 개방적이며, 안전하고 안정적인 고성능 운영 체제 및 에코시스템입니다. OpenCloudOS는 소프트웨어 및 오픈 소스 에코시스템에서 많은 벤더의 장점을 축적하고, Tencent의 10년 이상의 운영 체제 및 커널 관련 기술 축적을 계승합니다. 클라우드 네이티브, 안정성, 성능, 하드웨어 지원 측면에서 견고한 지원을 제공하며, 모든 하드웨어 플랫폼을 동등하고 포괄적으로 지원할 수 있습니다.

OpenCloudOS 8.6은 OpenCloudOS 커뮤니티의 첫 번째 공식 릴리스입니다. 기본 라이브러리 및 사용자 모드 컴포넌트는 CentOS 8과 완벽하게 호환되며 커널 수준의 최적화 및 향상을 통해 1000만+노드의 대규모 검증을 거쳐 안정성이 70% 향상되고 특정 시나리오의 성능이 50% 향상되어 사용자에게 CentOS 8보다 더 나은 솔루션을 제공합니다.

## 사용 사례
OpenCloudOS는 클라우드에서 CVM(Cloud Virtual Machine), CBM(Cloud Bare Metal) 등을 포함한 대부분의 프로덕션 인스턴스에 적합합니다.

<dx-alert infotype="notice" title="">
현재 OpenCloudOS에는 사전 설치된 GPU 드라이버가 없습니다. GPU 인스턴스에서 OpenCloudOS를 사용하려면 GPU 드라이버를 수동으로 설치하십시오.
</dx-alert>




## OpenCloudOS 이미지 버전
현재 OpenCloudOS 8(최신 버전 8.6) 이미지는 Tencent Cloud에서 지원됩니다. 이미지는 CentOS 8 사용자 모드와 완벽하게 호환되며 커뮤니티 5.4 LTS 기반의 OpenCloudOS Kernel이 장착되어 있습니다.

## OpenCloudOS 커널
OpenCloudOS Kernel은 커뮤니티 5.4 LTS를 기반으로 구축된 안정적인 고성능 kernel입니다. 커뮤니티의 최신 주요 기능과 다양한 비즈니스 시나리오에 대한 맞춤형 최적화가 포함되어 있습니다. kernel의 안정성을 보장하면서 OpenCloudOS Kernel은 지속적인 기술 업데이트 및 반복을 제공합니다.

## OpenCloudOS 사용
- 인스턴스를 생성하거나 기존 인스턴스의 운영 체제를 재설치할 때 공용 이미지를 선택하고 해당 버전의 OpenCloudOS를 사용하도록 선택할 수 있습니다. 자세한 작업은  [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855) 및 [시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참고하십시오.
- 이미 CentOS 인스턴스가 있는 경우 [CentOS 마이그레이션 가이드](https://docs.opencloudos.org/guide/migrate/)를 참고하여 OpenCloudOS로 마이그레이션할 수도 있습니다.

## OpenCloudOS 가져오기
OpenCloudOS를 가져오려면 [OpenCloudOS 8.6](http://mirrors.tencent.com/opencloudos/8.6/isos/)으로 이동하십시오.

## 업데이트 기록
자세한 내용은 [OpenCloudOS 이미지 업데이트 로그](https://intl.cloud.tencent.com/document/product/213/46208)를 참고하십시오.

## 서비스 및 업데이트
OpenCloudOS 커뮤니티는 최신 kernel 기능, 보안 취약점 수정 및 bug 수정을 포함하여 OpenCloudOS의 각 주요 버전(예시 OpenCloudOS 8)에 대해 최대 10년의 점검 및 업데이트를 제공합니다. yum을 통해 기존 저장 콘텐츠 서버를 업그레이드하여 즉시 취약점 수정을 완료할 수 있습니다.

