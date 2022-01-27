<style>
table th:nth-of-type(3) {
	width: 586px;
}
</style>
다음은 CDN 내부 상태 코드 관련 설명입니다. 

| 상태 코드 | 의미                                         | 권장 해결 방법                                                     |
| ----- | --------------------------------------------------- | ------------------------------------------------------------ |
| 0|요청 응답 상태 코드를 가져오기 전에 요청 종료|클라이언트의 조기 요청 연결 해제 여부 또는 Origin-pull 실패 여부를 확인하십시오.|
| 400    | HTTP 요청 구문 오류<br/>서버 분석 불가 |요청 구문이 올바른지 확인하십시오.                                  |
| 403 | 요청 거절    | referer 블록리스트/얼로우리스트, IP 블록리스트/얼로우리스트, 인증 설정 등 액세스 제어 설정 여부를 확인하십시오. |
| 413    | POST 길이 제한 초과                    | 클라이언트 POST 내용 크기(기본값 32MB로 제한)를 확인하십시오.           |
| 414    | URL 길이 제한 초과                     | URL 기본값 크기는 2KB로 제한됩니다.                                         |
| 423    | 루프 백 요청                             | Origin-pull 301/302 설정 따르기, HTTPS Origin-pull 설정 방식, 원본 서버 rewrite 처리 방식을 확인하십시오. |
| 499    | 클라이언트 연결 끊김                   | 클라이언트 상태 또는 시간 초과 설정을 확인하십시오.                               |
| 502    | 게이트웨이 오류                             | 비즈니스 원본 서버가 정상인지 확인하십시오.                                       |
| 503    | 트리거 COS 빈도 제어                          | 캐시 설정 또는 COS 원본 서버에서 no-cache/no-store를 출력하는지 확인하십시오.                 |
| 504    | 게이트웨이 시간 초과                          | 공식 홈페이지로 연락주십시오.              |
| 509    | 트리거 CC 공격 차단                     | [문의하기](https://intl.cloud.tencent.com/contact-sales) 또는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 차단을 해제하십시오.                             |
| 514    | IP 액세스 빈도 제한 초과                       | CDN 콘솔의 IP 액세스 빈도 제한 설정을 확인하십시오.                                |
| 531    | HTTPS Origin-pull 도메인 리졸브 요청 오류            | Origin-pull 도메인 리졸브 설정을 확인하십시오.                                       |
| 532    | HTTPS 원본 서버 Origin-pull 연결 요청 실패              | 원본 서버 443 포트 상태 및 인증서 설정 또는 원본 서버 가용성을 확인하십시오.                  |
| 533    | HTTPS 원본 서버 Origin-pull 연결 요청 시간 초과               | 원본 서버 443 포트 상태 및 인증서 설정 또는 원본 서버 가용성을 확인하십시오.                  |
| 537    | HTTPS 원본 서버 데이터 수신 요청 시간 초과            | 비즈니스 원본 서버 안정성을 확인하십시오.                                         |
| 538    | HTTPS SSL 핸드셰이킹 요청 실패                | 원본 서버 프로토콜과 알고리즘 호환성을 확인하십시오.                                 |
| 539    | HTTPS 인증서 검증 요청 실패                 | 원본 서버 인증서가 정상 설정(만료 여부, 인증서 링크 누락 여부)인지 확인하십시오.       |
| 540    | HTTPS 인증서 도메인 검증 요청 미통과          | 원본 서버 인증서가 정상 설정인지 확인하십시오.                                 |
| 562    | HTTPS 요청 연결 실패                    | [문의하기](https://intl.cloud.tencent.com/contact-sales)를 통해 X-NWS-LOG-UUID 정보를 제공하거나 또는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하시기 바랍니다.   |
| 563    | HTTPS 요청 연결 시간 초과                    | [문의하기](https://intl.cloud.tencent.com/contact-sales)를 통해 X-NWS-LOG-UUID 정보를 제공하거나 또는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하시기 바랍니다.   |
| 564    | HTTPS 요청 Origin-pull 실패                    |HTTP Origin-pull 방식으로 설정한 경우 원본 서버 부하 및 대역폭 사용률 또는 원본 서버 액세스 제한을 확인하십시오.</br>Follow Protocol 방식으로 설정한 경우 원본 서버 443 포트 상태 및 인증서 설정을 확인하십시오.</br>원본 서버에 이상이 없는 경우 [문의하기](https://intl.cloud.tencent.com/contact-sales)를 통해 X-NWS-LOG-UUID 정보를 제공하거나 또는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하시기 바랍니다.   |












