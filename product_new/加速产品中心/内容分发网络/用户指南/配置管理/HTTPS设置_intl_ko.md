HTTPS는 HTTP 프로토콜을 기반으로 전송 암호화를 위한 보안 프로토콜인 하이퍼 텍스트 전송 프로토콜 보안 (Hypertext Transfer Protocol Secure)을 나타내며 데이터 전송 보안을 효과적으로 보장할 수 있습니다. HTTPS를 구성할 때, 도메인 이름에 해당하는 인증서를 제공하고 전체 네트워크에 CDN 노드를 배포하여 전체 네트워크에서 데이터 암호화 및 전송을 구현합니다.

>- **오브젝트 스토리지** 또는 **Cloud Infinite** CDN 가속 서비스 후, 기본`.file.myqcloud.com` 접미사 도메인 또는`.image.myqcloud.com` 접미사 도메인 이름을 인증서 없이 HTTPS 요청을 직접 지원할 수 있습니다.
> - Tencent Cloud CDN 현재 HTTP2.0 프로토콜 지원에 대한 테스트가 완료되었으며, 바로 사용할 수 있습니다.

## 구성 안내
Tencent Cloud CDN은 인증서를 배포하는 두 가지 방법을 지원합니다.
- 자체 인증서: 배포를 위해 자체 인증서 및 개인키 콘텐츠를 CDN에 업로드하고 전체 프로세스를 암호화하고 전송하면 인증서의 보안을 보장합니다.
- Tencent Cloud 호스팅 인증서: [SSL 인증서 관리](https://console.cloud.tencent.com/ssl)를 사용하여 여러 클라우드 제품의 기존 인증서를 Tencent Cloud에 호스팅할 수 있습니다. 플랫폼에서 Trust Asia가 무료로 제공한 타사 인증서를 신청하여 CDN에 직접 배포하십시오.


1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 왼쪽 디렉터리 [도메인 관리]를 클릭합니다. 관리 페이지로 이동하여 목록에서 편집해야 하는 도메인 이름을 찾아 작업표시줄에서 [관리]를 클릭하십시오.
![img](https://mc.qcloudimg.com/static/img/f92d2ef7e4be2b69185ab43228f025ef/1.png)
2. [고급 구성]을 클릭하여 **HTTPS 구성** 모듈을 찾으십시오. [구성하기]를 클릭하여 **인증서 관리 ** 페이지로 이동하여 인증서를 구성하십시오. 구성 프로세스는 [인증서 관리](https://intl.cloud.tencent.com/document/product/228/6303)를 참조하십시오.
![img](https://mc.qcloudimg.com/static/img/df38d5d35b266e96c99f4ab67732cfd8/2.png)
3. 인증서 ** 구성이 성공하면 88후, [HTTPS 강제 리디렉션]창이 나타나며, 기본적으로 HTTPS가 비활성화 상태로 강제 리디렉션됩니다.
![img](https://mc.qcloudimg.com/static/img/22b01df16d9b4d50397b612b60252cfa/3.png)
4. [HTTPS 리디렉션]이 활성화된 경우, 사용자가 HTTP 요청을 시작하더라도 강제 리디렉션되어 HTTPS 요청에 액세스해야 합니다. 기본적으로 리디렉션 모드는 302입니다.
리디렉션 모드를 수정하려면 [편집]을 클릭하십시오.


## HTTP2.0 구성

도메인 이름에 대한 HTTPS 인증서를 성공적으로 구성한 다음 HTTP2.0을 활성화할 수 있습니다.
![img](https://mc.qcloudimg.com/static/img/72d122326ad99bb23f1ba66690bae91c/4.png)
HTTP 2.0 관련 기능에 대한 자세한 내용은 [HTTP 2.0의 새로운 기능](https://cloud.tencent.com/community/article/541321)을 참조하십시오.

>  `.myqcloud.com` 백그라운드 가속 도메인 이름은 Http2.0을 지원하지 않습니다.

## OCSP 고정 구성
**기능 설명**
OCSP 고정(OCSP Stapling, TLS 인증서 상태 쿼리 확장). OCSP Stapling 서버는 TLS 핸드 쉐이크시 이미 저장된 OCSP 쿼리 결과를 클라이언트에게 전송하여, 클라이언트가 요청을 CA로 보내지 않고도 확인할 수 있도록 합니다. OCSP 고정은 TLS 핸드 쉐이크 효율성을 크게 향상해 사용자 인증 시간을 절약합니다.

도메인 이름에 대한 HTTPS 인증서를 성공적으로 구성한 후 OCSP 고정을 활성화할 수 있습니다.


## HTTPS 원본 가져오기 지원 알고리즘

현재 HTTPS 원본 서버에서 지원되는 알고리즘은 다음 표에 나와 있습니다(순서 구분 없음).

| ECDHE-RSA-AES256-SHA   | ECDHE-RSA-AES256-SHA384   | ECDHE-RSA-AES256-GCM-SHA384   |
| ---------------------- | ------------------------- | ----------------------------- |
| ECDHE-ECDSA-AES256-SHA | ECDHE-ECDSA-AES256-SHA384 | ECDHE-ECDSA-AES256-GCM-SHA384 |
| SRP-AES-256-CBC-SHA    | SRP-RSA-AES-256-CBC-SHA   | SRP-DSS-AES-256-CBC-SHA       |
| DH-RSA-AES256-SHA      | DH-RSA-AES256-SHA256      | DH-RSA-AES256-GCM-SHA384      |
| DH-DSS-AES256-SHA      | DH-DSS-AES256-SHA256      | DH-DSS-AES256-GCM-SHA384      |
| DHE-RSA-AES256-SHA     | DHE-RSA-AES256-SHA256     | DHE-RSA-AES256-GCM-SHA384     |
| DHE-DSS-AES256-SHA     | DHE-DSS-AES256-SHA256     | DHE-DSS-AES256-GCM-SHA384     |
| CAMELLIA256-SHA        | DH-RSA-CAMELLIA256-SHA    | DHE-RSA-CAMELLIA256-SHA       |
| PSK-3DES-EDE-CBC-SHA   | DH-DSS-CAMELLIA256-SHA    | DHE-DSS-CAMELLIA256-SHA       |
| ECDH-RSA-AES256-SHA    | ECDH-RSA-AES256-SHA384    | ECDH-RSA-AES256-GCM-SHA384    |
| ECDH-ECDSA-AES256-SHA  | ECDH-ECDSA-AES256-SHA384  | ECDH-ECDSA-AES256-GCM-SHA384  |
| AES256-SHA             | AES256-SHA256             | AES256-GCM-SHA384             |
| ECDHE-RSA-AES128-SHA   | ECDHE-RSA-AES128-SHA256   | ECDHE-RSA-AES128-GCM-SHA256   |
| ECDHE-ECDSA-AES128-SHA | ECDHE-ECDSA-AES128-SHA256 | ECDHE-ECDSA-AES128-GCM-SHA256 |
| SRP-AES-128-CBC-SHA    | SRP-RSA-AES-128-CBC-SHA   | SRP-DSS-AES-128-CBC-SHA       |
| DH-RSA-AES128-SHA      | DH-RSA-AES128-SHA256      | DH-RSA-AES128-GCM-SHA256      |
| DH-DSS-AES128-SHA      | DH-DSS-AES128-SHA256      | DH-DSS-AES128-GCM-SHA256      |
| DHE-RSA-AES128-SHA     | DHE-RSA-AES128-SHA256     | DHE-RSA-AES128-GCM-SHA256     |
| DHE-DSS-AES128-SHA     | DHE-DSS-AES128-SHA256     | DHE-DSS-AES128-GCM-SHA256     |
| ECDH-RSA-AES128-SHA    | ECDH-RSA-AES128-SHA256    | ECDH-RSA-AES128-GCM-SHA256    |
| ECDH-ECDSA-AES128-SHA  | ECDH-ECDSA-AES128-SHA256  | ECDH-ECDSA-AES128-GCM-SHA256  |
| CAMELLIA128-SHA        | DH-RSA-CAMELLIA128-SHA    | DHE-RSA-CAMELLIA128-SHA       |
| PSK-RC4-SHA            | DH-DSS-CAMELLIA128-SHA    | DHE-DSS-CAMELLIA128-SHA       |
| AES128-SHA             | AES128-SHA256             | AES128-GCM-SHA256             |
| SEED-SHA               | DH-RSA-SEED-SHA           | DH-DSS-SEED-SHA               |
| DES-CBC3-SHA           | DHE-RSA-SEED-SHA          | DHE-DSS-SEED-SHA              |
| IDEA-CBC-SHA           | PSK-AES256-CBC-SHA        | PSK-AES128-CBC-SHA            |
| EDH-RSA-DES-CBC3-SHA   | ECDH-RSA-DES-CBC3-SHA     | ECDHE-RSA-DES-CBC3-SHA        |
| EDH-DSS-DES-CBC3-SHA   | ECDH-ECDSA-DES-CBC3-SHA   | ECDHE-ECDSA-DES-CBC3-SHA      |
| RC4-SHA                | ECDH-RSA-RC4-SHA          | ECDHE-RSA-RC4-SHA             |
| RC4-MD5                | ECDH-ECDSA-RC4-SHA        | ECDHE-ECDSA-RC4-SHA           |
| SRP-3DES-EDE-CBC-SHA   | SRP-RSA-3DES-EDE-CBC-SHA  | SRP-DSS-3DES-EDE-CBC-SHA      |
| DH-DSS-DES-CBC3-SHA    | DH-RSA-DES-CBC3-SHA       | -                             |

