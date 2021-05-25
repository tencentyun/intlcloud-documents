## 현상 설명

파일 액세스 시 파일을 찾지 못하거나 파일이 표시되지 않고 404 NoSuchKey 에러 코드를 반환합니다.
![](https://main.qcloudimg.com/raw/0974c1635f7a0d9189008b4543b59d4e.png)

## 예상 원인

- 액세스하는 파일 경로 입력 오류
- 액세스하는 파일 경로의 대소문자 불일치

## 처리 순서

액세스하는 파일 경로 및 대소문자가 정확한지 확인합니다.
 - 예. [고객센터](https://intl.cloud.tencent.com/support)로 문의하십시오.
 - 아니요. 파일 경로를 수정하십시오. 객체(Object)의 이름 생성 규칙은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오.
