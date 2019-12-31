CDN은 CDN 가속화를 최적화하기 위해 사용자의 비즈니스 요구에 맞게 다양한 사용자 정의를 지원합니다.

## 기본 구성
| 구성 이름                                     | 기능 설명                |
| ---------------------------------------- | ------------------- |
| [기본 정보](https://cloud.tencent.com/doc/product/228/7864) | 도메인 이름 소속 프로젝트, 도메인 이름, 해당 비즈니스 유형 수정 지원 |
| [원본 서버 구성](https://cloud.tencent.com/doc/product/228/6289) | 원본 서버 핫 백업 구성, 원본 서버 수정 , 원본 가져오기 보장 |
| [호스트 헤더 구성](https://cloud.tencent.com/doc/product/228/6293) | CDN이 원본 서버까지 가져오기할 때 방문 도메인 이름 지정 |

## 액세스 제어
| 구성 이름                                     | 기능 설명                      |
| ---------------------------------------- | ------------------------- |
| [필터링 파라미터 구성](https://cloud.tencent.com/doc/product/228/6291) | 사용자의 액세스 URL에서 "?"뒤에 노드가 파라미터를 무시할지 여부를 지정 |
| [링크 도용 방지 구성](https://cloud.tencent.com/doc/product/228/6292) | HTTP referer 블랙리스트/화이트리스트 구성      |
| [IP 블랙리스트/화이트리스트 구성](https://cloud.tencent.com/doc/product/228/6298) | 액세스 제어를 위한 IP 블랙리스트/화이트리스트 설정 지원       |
| [IP 액세스 빈도 제한 구성](https://cloud.tencent.com/doc/product/228/6420) | 단일 IP 노드 액세스 빈도 제한 구성 지원          |
| [비디오 드래그 구성](https://cloud.tencent.com/doc/product/228/8111) | 비디오 드래그 구성 지원                |


## 캐시 만료 설정
| 구성 이름                                     | 기능 설명              |
| ---------------------------------------- | ----------------- |
| [캐시 만료 설정](https://cloud.tencent.com/doc/product/228/6290) | 지정된 리소스 콘텐츠에 대한 캐시 만료 시간 규칙 설정 |
| [상태 코드 캐시 설정](https://intl.cloud.tencent.com/document/product/228/6290) | 404 상태 코드 캐시 시간 설정     |
| [HTTP 헤더 캐시](https://intl.cloud.tencent.com/document/product/228/6290) | 헤드 캐시 정책 설정          |

## 원본 가져오기 구성
| 구성 이름                                     | 기능 설명                 |
| ---------------------------------------- | -------------------- |
| [중간 서버 구성](https://cloud.tencent.com/doc/product/228/6294) | 중간 서버 사용 여부 지정            |
| [Range 원본 가져오기 구성](https://cloud.tencent.com/doc/product/228/7184) | Range 원본 가져오기 기능 켜기/끄기     |
| [302에 따른 원본 가져오기 구성](https://cloud.tencent.com/doc/product/228/7183) | 원본 서버를 302로 반환 켜기/끄기 시, 리디렉션 사용 여부 |

## 보안 구성

| 구성 이름                                     | 기능 설명      |
| ---------------------------------------- | --------- |
| [인증 구성](https://cloud.tencent.com/document/product/228/33115) | URL 인증 구성 |

## 고급 구성

| 구성 이름                               | 기능 설명                             |
| ---------------------------------------- | -------------------------------- |
| [대역폭 상한 구성](https://cloud.tencent.com/doc/product/228/7541) | 도메인 이름에 대한 대역폭 상한 임계 값을 설정합니다. 임계 값을 초과하면 CDN 서비스가 닫히고 원본 서버에 액세스합니다. |
| [HTTPS 구성](https://cloud.tencent.com/doc/product/228/6295) | 보안 가속화를 위한 HTTPS 구성 및 HTTPS 강제 리디렉션을 지원합니다.    |
| [SEO 최적화 구성](https://cloud.tencent.com/doc/product/228/6297) | SEO 최적화 구성을 활성화하여 검색 엔진 가중치 안정성을 보장합니다.      |
| [HTTP Header 구성](https://cloud.tencent.com/doc/product/228/6296) | HTTP Header 구성 추가                |

## 국가간 전용선 구성
| 구성 이름                                     | 기능 설명                        |
| ---------------------------------------- | --------------------------- |
| [국가간 전용선 구성(베타)](https://cloud.tencent.com/doc/product/228/7854) |CDN이 해외에서 가속 될 때 리턴 소스의 품질을 보장하기 위해 국가간 전용선을 켜거나 끕니다. |
