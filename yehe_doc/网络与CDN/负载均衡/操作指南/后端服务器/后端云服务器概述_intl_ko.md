## 리얼 서버란?
리얼 서버는 생성된 CLB 인스턴스에 바인딩되어 요청을 처리하는 [CVM 인스턴스](https://intl.cloud.tencent.com/doc/product/213)입니다. [CLB Listener](https://intl.cloud.tencent.com/document/product/214/6151)를 구성할 때 CVM 인스턴스를 리얼 서버로 바인딩해야 합니다. CLB는 다양한 [Round-Robin Methods](https://intl.cloud.tencent.com/document/product/214/6153)를 통해 요청을 리얼 서버로 포워딩하여 애플리케이션의 안정성과 신뢰성을 보장합니다. CLB 인스턴스가 있는 리전의 하나 이상의 가용존에서 CVM 인스턴스를 바인딩하여 애플리케이션 견고성을 향상하고 단일 실패 지점을 차단할 수 있습니다.

## 주의 사항
리얼 서버를 추가할 때 다음을 수행하는 것이 좋습니다.
- CLB 인스턴스에 바인딩할 모든 CVM 인스턴스에 Web 서버(예: Apache 또는 IIS)를 설치하고 애플리케이션 일관성을 보장합니다.
- CLB가 여러 요청에서 재사용할 수 있도록 더 긴 TCP 연결을 유지할 수 있도록 [Session Persistence](https://intl.cloud.tencent.com/document/product/214/6154)를 활성화하여 Web 서버의 부하를 줄이고 CLB 처리량을 개선하는 것이 좋습니다.
- 실제 인스턴스의 보안 그룹에 CLB 리스너 포트 및 상태 확인 포트에 대한 인바운드 규칙이 있는지 확인하십시오. 자세한 내용은 [Configuring CVM Security Groups](https://intl.cloud.tencent.com/document/product/214/6157)를 참고하십시오.
