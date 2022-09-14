TDSQL for MySQL은 데이터베이스 감사 기능을 제공하여, 데이터베이스 액세스 및 SQL 명령 실행 상황을 기록하고 기업의 리스크 관리와 데이터 보안 등급 향상을 지원합니다.  
>?데이터베이스 감사 기능은 현재 베타 테스트 중입니다. 이 기능을 사용하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청할 수 있습니다.

## SQL 감사 서비스 활성화
1. [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에 로그인하여 왼쪽 사이드바에서 **데이터베이스 감사**를 선택하고 상단에서 리전을 선택합니다. **감사 인스턴스** 탭을 클릭하고 **비활성화**를 클릭하여 감사가 비활성화된 인스턴스를 필터링합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/023dce8aca92a5f71f96edf4276810ef.png)
>?또는 **감사 로그** 탭의 **감사 인스턴스**에서 감사가 미활성화된 인스턴스를 직접 검색한 다음 감사를 활성화합니다.
>![](https://qcloudimg.tencent-cloud.cn/raw/0b388e192adf91a00891d4c64d5c5225.png)
2. **감사 인스턴스** 탭에서 대상 인스턴스의 ID를 클릭하여 활성화 페이지로 이동하고 계약에 대한 동의를 표시한 후 **다음 단계**를 클릭합니다.
3. **SQL 감사 서비스 설정** 페이지에서 감사 로그 저장 기간을 선택하고 **활성화**를 클릭합니다.
>?
>- 감사 로그의 보관 기간은 7일, 30일, 3개월, 6개월, 1년, 3년, 5년 중에서 선택할 수 있습니다. 감사를 활성화한 후 콘솔에서 수정할 수도 있습니다. 자세한 내용은 [Modifying Log Retention Period](https://intl.cloud.tencent.com/document/product/1042/48429)를 참고하십시오.
>- SQL 로그 저장 기간에 대한 보안 컴플라이언스 요구 사항을 충족하기 위해, 180일 이상으로 선택하는 것이 좋습니다.

## 감사 로그 조회
감사를 활성화한 후 **감사 로그** 탭에서 SQL 감사 로그를 볼 수 있습니다. 자세한 내용은 [Viewing Audit Logs](https://intl.cloud.tencent.com/document/product/1042/48428)를 참고하십시오.
