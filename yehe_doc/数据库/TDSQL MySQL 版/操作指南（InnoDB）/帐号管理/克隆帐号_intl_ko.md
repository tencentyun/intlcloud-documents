## 개요
TDSQL for MySQL 콘솔에서 데이터베이스 계정을 복제하고 원본 계정 암호를 유지하여 각기 다른 권한을 제공할 수 있습니다.

## 작업 단계
1. [TDSQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에 로그인합니다. **인스턴스 목록**에서 인스턴스 ID를 클릭하거나 **작업** 열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 데이터베이스 관리 페이지에서 **계정 관리** 탭을 선택하고 비밀번호를 재설정할 계정을 찾은 후 **계정 클론**을 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZcNv667_3.png)
3. 팝업 창에 원본 서버 IP, 계정 이름, 비밀번호(원래 계정과 동일할 수 있음)를 입력하고 **확인, 다음 단계**를 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xHeX802_4.png)
4. 복제된 계정을 보려면 계정 관리 페이지로 돌아갑니다.

## 관련 API

| API 이름                                                      | 설명     |
| ------------------------------------------------------------ | ------------ |
| [CloneAccount](https://intl.cloud.tencent.com/document/product/1042/34452) | 계정 클론 |

