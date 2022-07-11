
### 감사는 어떻게 비용을 책정하나요?
데이터베이스 감사는 감사 로그 스토리지 양에 따라 청구됩니다. 요금은 매 시간마다 청구되며 1시간 미만의 사용 시간은 1시간으로 계산됩니다. 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/1102/41313)을 참고하십시오.

### 활성화된 감사 기능은 어떻게 비활성화 하나요?
[MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql/policy), [TDSQL-C MySQL 콘솔](https://console.cloud.tencent.com/dls/cynosdb/instance) 및 [MongoDB 콘솔](https://console.cloud.tencent.com/dls/mongodb)에 로그인하고 감사 로그 페이지에서 **서비스 구성**을 클릭한 후 **서비스 비활성화**를 선택합니다.
>!서비스 비활성화 후, 해당 인스턴스에 적용되던 감사 정책, 로그, 파일은 삭제되며 복구가 불가능합니다. 로그와 파일을 미리 저장하시기 바랍니다.

### 감사 데이터는 얼마 동안 보관할 수 있나요?
감사 데이터는 7일에서 5년 동안 보관할 수 있습니다. [MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql/policy), [TDSQL-C MySQL 콘솔](https://console.cloud.tencent.com/dls/cynosdb/instance), [MongoDB 콘솔](https://console.cloud.tencent.com/dls/mongodb)에서 감사 활성화 시 보관 기간을 설정할 수 있습니다. 감사를 활성화한 후 감사 로그 페이지에서 **서비스 구성**을 클릭하여 변경할 수도 있습니다.
