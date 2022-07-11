Tencent Cloud는 TencentDB for MySQL 데이터베이스 감사 기능을 제공하여 데이터베이스 액세스 및 SQL 명령어 실행 상황을 기록하고, 기업의 리스크 관리와 데이터 보안 등급 향상에 이바지합니다.  

>!데이터베이스 감사는 현재 TencentDB for MySQL 5.6, 5.7 및 8.0(2노드 및 3노드) 인스턴스를 지원하지만 TencentDB for MySQL 5.5 또는 단일 노드 인스턴스는 지원하지 않습니다.

## [감사 규칙 생성](id:cjsjgz)
1. [MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql) 로그인 후, 왼쪽 사이드바에서 **데이터베이스 감사**를 선택하고, 상단의 리전 선택 후, **감사 규칙** 탭을 클릭합니다.
2. 감사 규칙 페이지에서 **규칙 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/687766a51c68c1b5ee483716c6097bac.png)
3. 감사 규칙 생성 페이지에서 규칙 명칭, 설명 기입 후, **다음 단계**를 클릭합니다.
4. 매개변수 설정 페이지에서 감사 방식 및 매개변수 선택 후, **저장**을 클릭합니다.
>!
>- 규칙 생성 완료 후, 감사 정책과 연결해야 규칙이 적용됩니다.
>- SQL 감사 규칙에 대한 자세한 사용 설명은 [SQL 감사 규칙](https://intl.cloud.tencent.com/document/product/1102/47770)을 참고하십시오.

## SQL 감사 서비스 활성화
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql)에 로그인하여 왼쪽 사이드바에서 **데이터베이스 감사**를 선택하고 상단에서 리전을 선택한 후 **감사 인스턴스** 탭에서 **미활성화**를 클릭하여 감사가 비활성화된 인스턴스를 필터링합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c64c25e2c28775636390079ba2971c91.png)
>?또는 **감사 로그** 탭의 **감사 인스턴스**에서 감사가 미활성화된 인스턴스를 직접 검색한 다음 감사를 활성화합니다.
>![](https://qcloudimg.tencent-cloud.cn/raw/8c8ed0771f0c0e81babe362e8d98c663.png)
2. **감사 인스턴스** 탭에서 대상 인스턴스의 ID를 클릭하여 활성화 페이지로 이동하고 계약에 대한 동의를 표시한 후 **다음 단계**를 클릭합니다.
3. **SQL 감사 서비스 설정** 페이지에서 감사 저장 기간 선택 후, **다음 단계**를 클릭합니다.
>?
>- 감사 로그의 보관 기간은 7일, 30일, 3개월, 6개월, 1년, 3년, 5년 중에서 선택할 수 있습니다. 감사를 활성화한 후 콘솔에서 수정할 수도 있습니다. 자세한 내용은 [로그 저장 기간 수정](https://intl.cloud.tencent.com/document/product/1102/47771)을 참고하십시오.
>- SQL 로그 저장 기간에 대한 보안 컴플라이언스 요구 사항을 충족하기 위해, 180일 이상으로 선택하는 것이 좋습니다.
4. **정책 생성** 페이지에서 정책 이름을 설정하고 생성된 [감사 규칙](https://intl.cloud.tencent.com/document/product/1102/47770)을 선택한 후 **정책 생성**을 클릭합니다.

## 감사 정책 생성
1. [MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql) 로그인 후, 왼쪽 사이드바에서 **데이터베이스 감사**를 선택하고, 상단의 리전 선택 후, **감사 정책** 탭을 클릭합니다.
2. **감사 정책** 탭에서 **정책 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d5260ffd47d4318825a3ef152385dddd.png)
3. 팝업 창에서 정책 이름을 설정하고 생성된 [감사 규칙](https://intl.cloud.tencent.com/document/product/1102/47770)을 선택한 후 **확인**을 클릭합니다.

## 감사 로그 조회
감사를 활성화한 후 **감사 로그** 탭에서 SQL 감사 로그를 볼 수 있습니다. 자세한 내용은 [감사 로그](https://intl.cloud.tencent.com/document/product/1102/47772)를 참고하십시오.

