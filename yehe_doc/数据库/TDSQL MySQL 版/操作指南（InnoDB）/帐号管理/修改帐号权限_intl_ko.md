## 개요
콘솔에서 TDSQL for MySQL 계정에 대한 전역/객체 레벨 권한을 부여할 수 있습니다.

## 작업 단계
1. [TDSQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에 로그인합니다. **인스턴스 목록**에서 인스턴스 ID를 클릭하거나 **작업** 열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **계정 관리** 탭을 선택하고 권한을 수정할 계정을 찾아 **권한 수정**을 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XMJs067_1.png)
3. 팝업 창에서 권한을 선택 또는 선택 취소하고 **확인**을 클릭하면 수정이 완료됩니다.
 - 전역 권한: 인스턴스의 모든 데이터베이스에 권한을 부여합니다.
 - 객체 레벨 권한: 인스턴스의 특정 데이터베이스에 권한을 부여합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AzJb007_2.png)

## 관련 API

| API 이름                                                      | 설명     |
| ------------------------------------------------------------ | ------------ |
| [DescribeAccountPrivileges](https://intl.cloud.tencent.com/document/product/1042/34447) | 계정 권한 쿼리 |
| [GrantAccountPrivileges](https://intl.cloud.tencent.com/document/product/1042/34437) | 계정 권한 설정 |

