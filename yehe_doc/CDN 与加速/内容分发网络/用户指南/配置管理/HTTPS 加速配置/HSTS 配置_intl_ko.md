

## 설정 시나리오

HSTS(HTTP Strict Transport Security)는 IETE(Institution of Electronics and Telecommunication Engineers)에서 보급한 웹 보안 프로토콜로써, 강제적으로 클라이언트(브라우저 등)에서 HTTPS로 서버에 연결하게 하며, 웹 사이트를 전역 암호화하는 기능입니다.

## 설정 제한

- expireTime은 0~365일로 제한되며, 설정 시 단위는 초입니다.
- 서브 도메인 포함 여부를 선택하여, includeSubDomain 매개변수를 조절할 수 있습니다.
- HSTS 설정을 활성화하려면 먼저 HTTPS 가속이 설정되어 있어야 합니다.

## 설정 가이드

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴에서 [도메인 관리]를 선택하고 도메인 오른쪽의 [관리]를 클릭하면, 도메인 설정 페이지의 네 번째 메뉴인 [HTTPS 설정]에서 HSTS 설정 모듈을 확인할 수 있으며, 비활성화 상태로 기본 설정되어 있습니다.
![](https://main.qcloudimg.com/raw/f9c2e5d2796fc254ae316bd560bcf2c3.png)
클릭하여 활성화하면 관련 사항을 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/cdcc8afd16cb9fe284eb307db8022fa7.png)
[확인]을 클릭하고 설정한 내용에 따라 응답 헤더 값을 정한 다음, [편집]을 클릭해 수정합니다.
![](https://main.qcloudimg.com/raw/4c6fbedf2f0f7b40cccc8a094af5bca3.png)

## 설정 예시

도메인 `cloud.tencent.com`의 HSTS Configuration은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/4c6fbedf2f0f7b40cccc8a094af5bca3.png)
액세스 시의 응답 헤더(Response Header)는 아래와 같습니다.
![](https://main.qcloudimg.com/raw/910e57e5abdedba4a33b4e4748a81318.png)

