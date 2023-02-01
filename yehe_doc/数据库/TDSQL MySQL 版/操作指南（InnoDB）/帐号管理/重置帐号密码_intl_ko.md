## 개요
TDSQL for MySQL을 사용하는 동안 데이터베이스 계정 비밀번호를 잊어버렸거나 변경해야 하는 경우 콘솔에서 재설정할 수 있습니다.

>?데이터 보안을 위해 최소 3개월에 한 번은 정기적으로 비밀번호를 재설정할 것을 권장합니다.

## 작업 단계
1. [TDSQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에 로그인합니다. 인스턴스 목록에서 인스턴스 ID를 클릭하거나 **작업** 열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **계정 관리** 탭을 선택하고 비밀번호를 재설정할 계정을 찾은 후 **더보기** > **비밀번호 재설정**을 선택합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yk5M998_11.png)
3. 팝업 창에서 새 비밀번호를 입력하고 비밀번호를 확인한 다음 **확인**을 클릭합니다.
>?계정 정보의 생성, 수정, 삭제로 인한 위험을 방지하기 위해 [액세스 관리](https://intl.cloud.tencent.com/document/product/1042/33343)를 설정하고, 비밀번호 재설정에 주의를 기울이는 것이 좋습니다.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/z4ky065_12.png)

## 관련 API

| API 이름                                                      | 설명     |
| ------------------------------------------------------------ | ------------ |
| [ResetAccountPassword](https://intl.cloud.tencent.com/document/product/1042/34430) | 계정 비밀번호 재설정 |

