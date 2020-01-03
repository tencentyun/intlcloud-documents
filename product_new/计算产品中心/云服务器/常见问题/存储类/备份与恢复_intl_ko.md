### CVM의 데이터 백업은 어떻게 진행합니까?

- CVM을 CBS로 호스팅할 경우, 시스템 디스크의 사용자 정의 이미지 및 데이터 디스크의 스냅샷 생성을 통해 서비스 데이터를 백업할 수 있습니다. 
  - 사용자 정의 이미지 생성이 필요할 경우, [사용자 정의 이미지 생성 방법](https://intl.cloud.tencent.com/document/product/213/4942)을 참조하십시오.
  - 스냅샷 생성이 필요할 경우, [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755)을 참조하십시오.
- CVM를 로컬 디스크로 호스팅할 경우, 사용자 정의 이미지를 생성하는 방식을 통해 시스템 디스크를 백업할 수 있습니다. 그러나 데이터 디스크의 서비스 데이터는 사용자 정의 백업 정책에 따라 직접 진행해야 합니다. 
  보통 FTP 방식을 사용해 클라우드 서버의 데이터를 다른 곳으로 백업할 수 있으며, 구체적인 FTP 배포 방식은 아래를 참조하십시오. 
  - Windows 운영 체제: [Windows 인스턴스의 FTP 구축 서비스](https://cloud.tencent.com/document/product/213/10414)
  - Linux 운영 체제: [Linux 인스턴스의 FTP 구축 서비스](https://intl.cloud.tencent.com/document/product/213/10912) 
- 이외에도, 데이터 보안성을 더 높이고 싶을 경우 전문적인 3rd party 백업 서비스를 구매할 수 있습니다.
자세한 정보는 [클라우드 마켓 >>](https://market.cloud.tencent.com/)을 액세스하십시오.

### 범용적인 데이터의 백업과 복원 방안에는 무엇이 있습니까?

응용 시나리오와 서비스 상황에 따라 적합한 데이터 백업과 복원 방안도 다릅니다. Tecent가 제공하는 아래의 일부 범용적인 제안을 실제 상황에 따라 선택해 사용하십시오.
- [CBS 스냅샷](https://cloud.tencent.com/doc/product/362/5754) 기능을 정기적으로 사용해 인스턴스를 백업하십시오.
- 여러 가용존에 애플리케이션의 주요 구성 요소를 배포하여 적절한 위치에 데이터를 복제하십시오.
- [EIP](https://cloud.tencent.com/doc/product/213/5733)를 사용한 도메인 매핑을 CVM에서 허용하지 않을 경우, 서비스 IP를 신속하게 다른 CVM 인스턴스로 다시 지정할 수 있습니다.
- 모니터링 데이터가 적절한 알람으로 설정되어 있는지 정기적으로 조회하십시오. 자세한 정보는 [클라우드 모니터링](http://cloud.tencent.com/doc/product/248)을 참조하십시오.
- Auto Scaling을 사용해 돌발적 요청을 처리하십시오. 자세한 정보는 [Auto Scaling](https://cloud.tencent.com/doc/product/377)을 참조하십시오.

### CVM 파일은 어떻게 복구합니까?

CVM 파일 복구는 [클라우드 마켓](https://market.cloud.tencent.com/)을 통해 관련된 무료 또는 유료 서비스를 사용할 수 있습니다.
