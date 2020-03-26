<style>
table th:nth-of-type(3) {
	width: 585px;
}
</style>
다음은 CDN 내부 상태 코드 설명입니다.

| 상태 코드 | 의미                                         | 처리 권고                                                     |
| ----- | --------------------------------------------------- | ------------------------------------------------------------ |
| 400    | HTTP 요청 구문 오류<br/>서버 분석 불가 |요청 구문이 올바른지 확인하세요.                                  |
| 403    | 요청 거절                             | referer 블랙리스트/화이트리스트, IP 블랙리스트/화이트리스트, 인증 설정 등 액세스 제어 기능 설정 여부를 확인하세요. |
| 413    | POST 길이 제한 초과                    | 클라이언트 POST 내용 크기(기본값 32MB로 제한)를 확인하세요.           |
| 414    | URL 길이 제한 초과                     | URL 기본값 크기는 2KB로 제한됩니다.                                         |
| 423    | 루프 백 요청                             | Origin-pull 301/302 설정 따르기, HTTPS Origin-pull 설정 방식, 원본 서버 rewrite 처리 방식을 확인하세요. |
| 499    | 클라이언트 연결 끊김                   | 클라이언트 상태 또는 시간 초과 설정을 확인하세요.                               |
| 502    | 게이트웨이 오류                             | 비즈니스 원본 서버가 정상인지 확인하세요.                                       |
| 503    | 트리거 COS 빈도 제어                          | 캐시 설정 또는 COS 원본 서버에서 no-cache/no-store를 출력하는지 확인하세요.                 |
| 509    | 트리거 CC 공격 차단                     | [고객센터](https://intl.cloud.tencent.com/support ) 또는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)에서 차단을 해제하세요.                             |
| 514    | IP 액세스 빈도 제한 초과                       | CDN 콘솔의 IP 액세스 빈도 제한 설정을 확인하세요.                                |
| 531    | HTTPS Origin-pull 도메인 리졸브 요청 오류            | Origin-pull 도메인 리졸브 설정을 확인하세요.                                       |
| 532    | HTTPS 원본 서버 Origin-pull 연결 요청 실패              | 원본 서버 443 포트 상태 및 인증서 설정 또는 원본 서버 가용성을 확인하세요.                  |
| 533    | HTTPS 원본 서버 Origin-pull 연결 요청 시간 초과               | 원본 서버 443 포트 상태 및 인증서 설정 또는 원본 서버 가용성을 확인하세요.                  |
| 537    | HTTPS 원본 서버 데이터 수신 요청 시간 초과            | 비즈니스 원본 서버 안정성을 확인하세요.                                         |
| 538    | HTTPS SSL 핸드셰이킹 요청 실패                | 원본 서버 프로토콜과 알고리즘 호환성을 확인하세요.                                 |
| 539    | HTTPS 인증서 검증 요청 실패                 | 원본 서버 인증서가 정상 설정(만료 여부, 인증서 링크 누락 여부)인지 확인하세요.       |
| 540    | HTTPS 인증서 도메인 검증 요청 미통과          | 원본 서버 인증서가 정상 설정인지 확인하세요.                                 |
| 562    | HTTPS 연결 요청 실패                    | [고객센터](https://intl.cloud.tencent.com/support )에서 X-NWS-LOG-UUID 정보 제공 또는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)에서 확인하세요.   |
| 563    | HTTPS 연결 요청 시간 초과                    | [고객센터](https://intl.cloud.tencent.com/support )에서 X-NWS-LOG-UUID 정보 제공 또는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)에서 확인하세요.   |
| 564    | HTTPS Origin-pull 요청 실패                    |HTTP Origin-pull 방식으로 설정한 경우 원본 서버 부하 및 대역폭 사용률 또는 원본 서버 액세스 제한을 확인하세요.</br>프로토콜 따르기 방식으로 설정한 경우 원본 서버 443 포트 상태 및 인증서 설정을 확인하세요.</br>원본 서버에 이상이 없는 경우 [고객센터](https://intl.cloud.tencent.com/support )에서 X-NWS-LOG-UUID 정보 제공 또는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)에서 확인하세요.|












