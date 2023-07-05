

다음은 CDN 내부 상태 코드를 설명합니다. 

| 상태 코드 | 의미                                         | 권장 해결 방안                                                     |
| :----- | :------------------------------- | :----------------------------------------------------------- |
| 400    | HTTP 요청 구문 오류 및 서버 파싱 불가  |요청 구문이 올바른지 확인합니다.                                  |
| 403    | 요청 거절                             | referer 블랙리스트/화이트리스트, IP 블랙리스트/화이트리스트, 인증 설정 등 액세스 제어 설정 여부를 확인합니다. |
| 404    | 서버에서 정확한 정보 반환 불가          | 원본 서버 정상 여부 또는 원본 서버 정보, 호스트 헤더 구성에 변경이 발생하지 않았는지 확인합니다. |
| 413    | POST 길이 제한 초과                    | 클라이언트 POST 콘텐츠 크기(기본 제한: 32MB)를 확인합니다.           |
| 414    | URL 길이 제한 초과                     | URL 기본 크기 제한은 2KB입니다.                                         |
| 423    | 루핑 요청                             | 301/302 설정, HTTPS Origin-pull 설정, 원본 서버의 rewrite 처리 방식을 확인합니다. |
| 499    | 클라이언트의 연결 중단                   | 클라이언트 상태 또는 타임 아웃 설정을 확인합니다.                               |
| 502    | 게이트웨이 오류                             | 비즈니스 원본 서버가 정상인지 확인합니다.                                       |
| 503    | COS 빈도 제어 트리거                          | 캐시 설정 또는 COS 원본 서버에서 no-cache/no-store를 반환하는지 확인합니다.                 |
| 509    | CC 공격 차단 트리거                     | [문의하기](https://intl.cloud.tencent.com/contact-sales) 또는 [Tencent Cloud Support Plan](https://intl.cloud.tencent.com/support)를 통해 차단을 해제합니다.                             |
| 514    | IP 액세스 빈도 제한 초과                       | CDN 콘솔의 IP 액세스 빈도 제한 설정을 확인합니다.                                |
| 531    | HTTPS 요청의 Origin-pull 도메인 리졸브 오류            | 원본 서버의 도메인 리졸브 설정을 확인합니다.                                       |
| 532    | HTTPS 요청의 원본 서버 연결 실패              | 원본 서버 443 포트 상태 및 인증서 설정 또는 원본 서버 가용성을 확인합니다.                  |
| 533    | HTTPS 요청의 Origin-pull 연결 시간 초과                | 원본 서버 443 포트 상태 및 인증서 설정 또는 원본 서버 가용성을 확인합니다.                  |
| 537    | HTTPS 요청의 원본 서버 데이터 수신 시간 초과            | 비즈니스 원본 서버 안정성을 확인합니다.                                         |
| 538    | HTTPS 요청의 SSL 핸드셰이크 실패                | 원본 서버 프로토콜과 알고리즘 호환성을 확인합니다.                                 |
| 539    | HTTPS 요청의 인증서 유효성 검사 실패                 | 원본 서버의 인증서가 올바르게 구성되었는지 확인합니다(인증서 체인의 유효 기간 및 완성도).       |
| 540    | HTTPS 요청의 인증서 도메인 이름 유효성 검사 실패          | 원본 서버 인증서가 정상적으로 설정되었는지 확인합니다.                                 |
| 562    | HTTPS 요청의 연결 구축 실패                    | [문의하기](https://intl.cloud.tencent.com/contact-sales)를 통해 X-NWS-LOG-UUID 정보를 제공하거나 [Tencent Cloud Support Plan](https://intl.cloud.tencent.com/support)을 통해 문제를 진단합니다.   |
| 563    | HTTPS 요청의 연결 시간 초과                    | [문의하기](https://intl.cloud.tencent.com/contact-sales)를 통해 X-NWS-LOG-UUID 정보를 제공하거나 [Tencent Cloud Support Plan](https://intl.cloud.tencent.com/support)을 통해 문제를 진단합니다.   |
| 564    | HTTPS Origin-pull 요청 실패                    | HTTP가 원본 요청 프로토콜로 설정된 경우 원본 서버의 부하 및 대역폭 사용률 또는 액세스 제한을 확인합니다. 프로토콜이 Follow Request로 설정되어 있으면 원본 서버의 443 포트 상태 및 인증서 설정을 확인합니다. 원본 서버에서 오류가 발견되지 않으면, [문의하기](https://intl.cloud.tencent.com/contact-sales)를 통해 X-NWS-LOG-UUID 정보를 제공하거나 [Tencent Cloud Support Plan](https://intl.cloud.tencent.com/support)을 통해 문제를 진단합니다. |











