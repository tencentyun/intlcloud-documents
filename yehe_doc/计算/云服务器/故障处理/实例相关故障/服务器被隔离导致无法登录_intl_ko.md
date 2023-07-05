본 문서는 CVM의 외부 네트워크가 격리되어 로그인할 수 없는 문제에 대한 솔루션을 소개합니다.

## 장애 현상
CVM 격리는 해당 서버가 현재 법률 법규를 위반한 것일 수 있습니다. 아래 방식을 통해 해당 서버의 격리 상태 여부를 조회할 수 있습니다.
- CVM 외부 네트워크가 격리될 경우, [콘솔 내부 메시지](https://console.cloud.tencent.com/message) 또는 SMS 발송 방식을 통해 규정 위반 격리 안내를 사용자에게 공지합니다.
 
- [CVM 콘솔](https://console.cloud.tencent.com/cvm/index) 의 "Monitorinig/Status" 표시줄에 해당 CVM 상태: 격리 중이라고 표시됩니다.


## 문제 원인
CVM에 규정 위반 사항 또는 위험 사항을 발견할 경우, 규정을 위반한 기기에 대해 일부 격리 작업(내부 네트워크의 22, 36000, 3389 로그인 포트를 제외한 나머지 네트워크 액세스가 전부 격리되며, 개발자는 점프 서버 방식으로 서버에 로그인할 수 있음)을 시행합니다.
자세한 내용은 [클라우드 보안 규정 위반 사항의 등급 구분 및 처벌 설명]을 참조 바랍니다.

## 솔루션

 1. 내부 메시지 또는 SMS 알림에 따라 규정 위반 내용을 처리합니다. 보안 취약점을 처리하고, 필요에 따라 시스템을 재설치합니다.
 2. 사용자 개인 행위로 인한 규정 위반이 아닌 경우, 서버에 악성 침입이 있을 가능성이 있습니다. 솔루션은 [HS](https://intl.cloud.tencent.com/document/product/296)를 참조 바랍니다.
 3. 보안 취약점을 제거하거나 규정 위반을 중단한 후 [Submit Ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM)을 통해 고객서비스에 문의하여 격리를 해제하시기 바랍니다.

