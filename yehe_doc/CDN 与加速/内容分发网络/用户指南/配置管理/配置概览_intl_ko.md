<style> table th:first-of-type { width: 200px; } </style>

CDN은 다양한 사용자 정의 설정을 지원합니다. 비즈니스 니즈에 맞게 설정하여 최적화된 CDN 가속 효과를 볼 수 있습니다.

## 기본 설정
| 설정 이름                                     | 기능 설명              |
| ---------------------------------------- | ------------------- |
| [기본 정보](https://intl.cloud.tencent.com/document/product/228/7864) | 도메인 서브 프로젝트, 서비스 리전 및 서비스 유형 변경 지원. |
| [원본 서버 설정](https://intl.cloud.tencent.com/document/product/228/6289) | 도메인 원본 서버 설정: 원본 서버의 기본 정보, 원본 요청 프로토콜, 호스트 헤더 및 핫 백업 원본 서버 설정 가능, 원본 요청 보장. 중국 내/외를 다르게 설정 가능.  |


## 액세스 제어
| 설정 이름                                     | 기능 설명                      |
| ---------------------------------------- | ------------------------- |
| [필터링 매개변수 설정](https://intl.cloud.tencent.com/document/product/228/35316) | 노드의 사용자 액세스 URL 무시 여부 중 "?" 뒤의 매개변수 지정. |
| [링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/228/6292) | HTTP referer 블랙리스트/화이트리스트 설정. 중국 내/외를 다르게 설정 가능.      |
| [IP 블랙리스트/화이트리스트 설정](https://intl.cloud.tencent.com/document/product/228/6298) | IP 블랙리스트/화이트리스트 설정으로 액세스 제어 가능.       |
| [IP 액세스 빈도 제한 설정](https://intl.cloud.tencent.com/document/product/228/6420) | 단일 IP 단일 노드 액세스 빈도 제한 설정 지원.          |
| [비디오 드래그 설정](https://intl.cloud.tencent.com/document/product/228/8111) | 비디오 드래그 설정 지원.                |
| [인증 설정](https://intl.cloud.tencent.com/document/product/228/35237) | URL 인증 설정. 중국 내/외를 다르게 설정 가능. |


## 캐시 만료 설정
| 설정 이름                                     | 기능 설명              |
| ---------------------------------------- | ----------------- |
| [캐시 만료 설정](https://intl.cloud.tencent.com/document/product/228/35317) | 지정된 리소스 콘텐츠의 캐시 만료 시간 규칙 설정. |
| [상태 코드 캐시 설정](https://intl.cloud.tencent.com/document/product/228/35318) | 403 및 404 상태 코드의 캐시 시간 설정.     |
| [HTTP 헤더 캐시](https://intl.cloud.tencent.com/document/product/228/35319) | 헤더 캐시 정책 설정.          |

#원본 가져오기 구성
| 설정 이름                                     | 기능 설명                 |
| ---------------------------------------- | -------------------- |
| [Range 원본 가져오기 구성](https://intl.cloud.tencent.com/document/product/228/7184) | Range 샤드 원본 요청 활성화/비활성화.     |
| [원본 요청 301/302 따르기 설정](https://intl.cloud.tencent.com/document/product/228/7183) |원본 서버 301/302 리턴 시 리디렉션 따르기 여부 활성화/비활성화 |
| [원본 요청 타임아웃 시간 설정](https://intl.cloud.tencent.com/document/product/228/35227) | 원본 요청 TCP 연결 타임아웃 시간과 원본 요청 데이터 로딩 타임아웃 시간을 설정해 정상적인 원본 요청 보장. |


## 고급 설정

| 설정 이름                                     | 기능 설명                             |
| ---------------------------------------- | -------------------------------- |
| [대역폭 상한 설정](https://intl.cloud.tencent.com/document/product/228/7541) |도메인의 대역폭 상한 임계 값을 설정하여 임계 값 초과 시 CDN 서비스 종료 및 원본 서버에 액세스. 중국 내/외를 다르게 설정 가능. |
| [HTTPS 설정](https://intl.cloud.tencent.com/document/product/228/35212) | HTTPS 설정으로 보안 가속 구현. HTTPS 강제 리디렉션, HTTP2.0 액세스 및 OCSP 고정 활성화/비활성화 지원.    |
| [SEO 최적화 설정](https://intl.cloud.tencent.com/document/product/228/35219) | SEO 최적화 설정을 활성화하여 검색 엔진의 가중치 안정성 보장.          |
| [HTTP Header 설정](https://intl.cloud.tencent.com/document/product/228/35320) | HTTP Header 설정 추가                |


