

## 기본 정보 API
| API 이름                   | API 기능                    |
| ------------------------------ | ------------------------------- |
| [BGPIPGetInfo](https://cloud.tencent.com/document/product/1014/31246)             | 지정된 Anti-DDoS Advanced 인스턴스의 세부 정보 가져오기       |
| [BGPIPRename](https://cloud.tencent.com/document/product/1014/31245)                    | 지정된 Anti-DDoS Advanced 인스턴스 이름 수정 |
| [BGPIPSetCCThreshold](https://cloud.tencent.com/document/product/1014/31244)            | 지정된 Anti-DDoS Advanced 인스턴스의 CC 방어 임계값 설정 |
| [BGPIPSetElasticProtectionLimit](https://cloud.tencent.com/document/product/1014/31243) | 지정된 Anti-DDoS Advanced 인스턴스의 엘라스틱 방어 피크값 설정 |
|[ AddCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31242)            | 단일 CC 사용자 지정 전략 추가          |
| [EditCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31241)           | 단일 CC 사용자 지정 전략 편집         |
| [GetCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31240)            | 단일 CC 사용자 지정 전략 정보 가져오기      |
| [GetCustomCCStrategyList](https://cloud.tencent.com/document/product/1014/31239)        | CC 사용자 지정 전략 리스트 가져오기          |
| [RemoveCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31238)         | 단일 CC 사용자 지정 전략 삭제          |
| [SetCustomCCStrategyStatus](https://cloud.tencent.com/document/product/1014/31237)      | 단일 CC 사용자 지정 전략 시작/종료    |
| [OpenDomainCCProtection](https://cloud.tencent.com/document/product/1014/31236)         | 도메인 규칙 CC 방어 시작           |
| [CloseDomainCCProtection](https://cloud.tencent.com/document/product/1014/31235)        | 도메인 규칙 CC 방어 종료           |

## 방어 정보 API
| API 이름                | API 기능                                                    |
| ----------------------- | ----------------------------------------------------------- |
| [BGPIPDDoSGetCounter](https://cloud.tencent.com/document/product/1014/31253)     | 지정된 Anti-DDoS Advanced 인스턴스가 DDoS 공격받은 횟수, 피크값과 엘라스틱 방어 시작 횟수 가져오기 |
| [BGPIPDDoSGetStatistics](https://cloud.tencent.com/document/product/1014/31252)  | 지정된 Anti-DDoS Advanced 인스턴스가 받은 DDoS 공격의 트래픽 통계 가져오기                       |
| [BGPIPDDoSGetDetails](https://cloud.tencent.com/document/product/1014/31251)     | 지정된 Anti-DDoS Advanced 인스턴스가 받은 DDoS 공격 트래픽 세부 정보 가져오기                      |
| [BGPIPCCGetCounter](https://cloud.tencent.com/document/product/1014/31250)       | 지정된 Anti-DDoS Advanced 인스턴스가 CC 공격받은 횟수, 피크값 가져오기                    |
| [BGPIPCCGetStatistics](https://cloud.tencent.com/document/product/1014/31249)    | 지정된 Anti-DDoS Advanced 인스턴스가 받은 CC 공격 트래픽 통계 도표 가져오기                   |
| [BGPIPCCGetDetails](https://cloud.tencent.com/document/product/1014/31248)       | 지정된 Anti-DDoS Advanced 인스턴스가 받은 CC 공격 트래픽 세부 정보 가져오기                        |
| [BGPIPTransGetStatistics](https://cloud.tencent.com/document/product/1014/31247) | 지정된 Anti-DDoS Advanced 인스턴스가 Tencent Cloud 이외의 서버에 트래픽을 포워딩한 통계 도표 가져오기           |

## 서비스 리스트 API
| API 이름                  | 기능 설명                                  |
| ------------------------- | ----------------------------------------- |
| [BGPIPGetServicePacks](https://cloud.tencent.com/document/product/1014/31261)      | 해당 사용자가 보유한 모든 Anti-DDoS Advanced 인스턴스 리스트 가져오기 |
| [BGPIPGetServiceStatistics](https://cloud.tencent.com/document/product/1014/31262) | Anti-DDoS Advanced의 히스토리 사용 일수와 방어 횟수 가져오기 |

## 포워딩 규칙 API
| API이름                 | 기능 설명                                  |
| ------------------------ | ----------------------------------------- |
| [BGPIPAddTransRules](https://cloud.tencent.com/document/product/1014/31270)       | 지정된 Anti-DDoS Advanced 인스턴스에 4계층 포워딩 규칙 추가   |
| [BGPIPEditTransRules](https://cloud.tencent.com/document/product/1014/31269)      | 지정된 Anti-DDoS Advanced 인스턴스의 특정 4계층 포워딩 규칙 편집       |
| [BGPIPGetTransRules](https://cloud.tencent.com/document/product/1014/31268)       | 지정된 Anti-DDoS Advanced 인스턴스의 4계층 포워딩 규칙 리스트 가져오기 |
| [BGPIPDeleteTransRules](https://cloud.tencent.com/document/product/1014/31267)    | 지정된 Anti-DDoS Advanced 인스턴스의 특정 4계층 포워딩 규칙 삭제         |
| [BGPIPAddWadTransRules](https://cloud.tencent.com/document/product/1014/31266)    | 지정된 Anti-DDoS Advanced 인스턴스에 7계층 포워딩 규칙 추가   |
| [BGPIPEditWadTransRules](https://cloud.tencent.com/document/product/1014/31265)   | 지정된 Anti-DDoS Advanced 인스턴스의 특정 7계층 포워딩 규칙 편집             |
| [BGPIPGetWadTransRules](https://cloud.tencent.com/document/product/1014/31263)    | Anti-DDoS Advanced 인스턴스의 7계층 포워딩 규칙 리스트 가져오기   |
| [BGPIPDeleteWadTransRules](https://cloud.tencent.com/document/product/1014/31264) | 지정된 Anti-DDoS Advanced 인스턴스의 특정 7계층 포워딩 규칙 삭제         |

## 화이트리스트 API
| API 이름         | 기능 설명                                      |
| ---------------- | --------------------------------------------- |
| [GetWhiteUrl](https://cloud.tencent.com/document/product/1014/31277)      | 지정된 Anti-DDoS Advanced 인스턴스의 화이트리스트 가져오기         |
| [AddWhiteUrl](https://cloud.tencent.com/document/product/1014/31276)      | 지정된 Anti-DDoS Advanced 인스턴스에 URL 화이트리스트 추가     |
| [RemoveWhiteUrl](https://cloud.tencent.com/document/product/1014/31275)   | 지정된 Anti-DDoS Advanced 인스턴스의 URL 화이트리스트 삭제  |
| [GetSrcWhiteIP](https://cloud.tencent.com/document/product/1014/31274)    | 지정된 Anti-DDoS Advanced 인스턴스의 오리진 IP 화이트리스트 가져오기   |
| [AddSrcWhiteIP](https://cloud.tencent.com/document/product/1014/31273)    | 지정된 Anti-DDoS Advanced 인스턴스에 오리진 IP 화이트리스트 추가    |
| [RemoveSrcWhiteIP](https://cloud.tencent.com/document/product/1014/31272) | 지정된 Anti-DDoS Advanced 인스턴스의 오리진 IP 화이트리스트 삭제|

## 블랙리스트 API
| API 이름         | 기능 설명                                      |
| ---------------- | --------------------------------------------- |
| [AddSrcBlackIP](https://cloud.tencent.com/document/product/1014/31278)    | 지정된 Anti-DDoS Advanced 인스턴스에 오리진 IP 블랙리스트 추가    |
| [RemoveSrcBlackIP](https://cloud.tencent.com/document/product/1014/31279) | 지정된 Anti-DDoS Advanced 인스턴스의 오리진 IP 블랙리스트 삭제 |


