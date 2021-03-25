## 1. CVM에 익숙해지기 위한 기본 지식
- [CVM은 어떤 작업입니까?](https://intl.cloud.tencent.com/document/product/213/495)
- [Tencent Cloud CVM을 선택해야 하는 이유](https://intl.cloud.tencent.com/document/product/213/3036)
- [Tencent Cloud CVM 사용 시 제한 사항](https://intl.cloud.tencent.com/document/product/213/15379)
- [CVM의 일반적 개념](https://intl.cloud.tencent.com/zh/document/product/213/38678)


## 2. CVM의 과금 방식
Tencent Cloud CVM의 과금 방식에는 종량제 방식과 스팟 인스턴스 방식이 있습니다. CVM 과금 방식을 완벽히 이해하고 최적화된 과금 방식을 선택하시기 바랍니다. 자세한 내용은 [과금 방식](https://intl.cloud.tencent.com/document/product/213/2180)을 참조하십시오.

## 3. 신규 사용자
#### 3.1 가입 및 인증
Tencent Cloud CVM 사용 전 [Tencent Cloud 계정 가입](https://intl.cloud.tencent.com/register)과 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료해야 합니다.

#### 3.2 CVM 구매
가입 및 실명 인증 완료 후, [CVM 구매 페이지](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.91351132.770173325.1571651505)에서 실제 비즈니스 수요에 적합한 CVM 소재 리전, 모델, 이미지, 공용 네트워크 대역폭, 구매 수량, 구매 시간을 유연하게 선택할 수 있습니다. 자세한 내용은 다음을 참조하십시오. 

- [사용자 정의 Linux CVM 구성](https://intl.cloud.tencent.com/document/product/213/10517)

- [사용자 정의 Windows CVM 구성](https://intl.cloud.tencent.com/document/product/213/10516)

#### 3.3 CVM 로그인 및 사용
구매 완료 후 CVM에 로그인하여 로컬 파일을 CVM에 저장할 수 있으며, CVM을 개인 가상 컴퓨터 또는 사이트 구축 서버로 사용할 수 있습니다.
- CVM 로그인 방법에 대한 자세한 내용은 다음을 참조하십시오.
 - [Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5436)
 - [Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5435)
- 로컬 파일을 CVM에 저장하는 자세한 방법은 [로컬 파일 CVM에 복사하기](https://intl.cloud.tencent.com/document/product/213/34821)를 참조하십시오.
-사이트 구축 관련 작업에 대한 자세한 방법은 [웹 사이트 구축하기](https://intl.cloud.tencent.com/document/product/213/34815)를 참조하십시오.


## 4. 콘솔 인터페이스
CVM 콘솔 총람 페이지:
![](https://main.qcloudimg.com/raw/98a624ab6b2e13beb8d69b966d1e12d4.png)

## 5. 콘솔 기능 개요

| 필요한 기능 | 참조 페이지 |
|---------|---------|
| CVM 인스턴스 생성 | [인스턴스 생성 가이드](https://intl.cloud.tencent.com/document/product/213/36302) |
|인스턴스 명칭/호스트명에 일정한 규칙성 부여 | [대량 연속 이름 생성 또는 지정 스트링 패턴 이름 생성](https://intl.cloud.tencent.com/document/product/213/32020) |
| CVM 인스턴스 구성 향상 또는 하향 조정 | [인스턴스 구성 조정](https://intl.cloud.tencent.com/document/product/213/2178) |
| CVM 암호화 로그인 방식으로 SSH 키 사용 및 관리 | [SSH 키 관리](https://intl.cloud.tencent.com/document/product/213/16691) |
|인스턴스 로그인 비밀번호 수정 또는 재설정 | [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566) |
| CVM 인스턴스 폐기, 릴리스, 반환 | [인스턴스 폐기/반환](https://intl.cloud.tencent.com/document/product/213/4930) |
| 리전의 CVM 인스턴스 정보 | [인스턴스 내보내기](https://intl.cloud.tencent.com/document/product/213/16563) |
| CVM 인스턴스 및 관련 리소스 검색 | 리전 간 검색|
| 이후 이미지를 사용해 기존 인스턴스와 동일한 사용자 정의 페이지를 가진 신규 인스턴스를 더 많이 생성하기 위한 신규 사용자 정의 이미지 생성 | [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) |
| 다른 사용자에게서 공유 이미지 획득 및 해당 이미지에서 필요한 구성 요소를 획득하고 사용자 정의 컨텐츠 추가하기 | [사용자 정의 이미지 공유](https://intl.cloud.tencent.com/document/product/213/4944) |
| 로컬 또는 기타 플랫폼 서버 시스템 디스크 상의 이미지 파일을 CVM 사용자 정의 이미지로 가져오기 | [이미지 가져오기 개요](https://intl.cloud.tencent.com/document/product/213/4945) |
| Linux 이미지 생성 및 내보내기 | [Linux 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17814) |
| Windows 이미지 생성 및 내보내기 | [Windows 이미지 생성](https://intl.cloud.tencent.com/document/product/213/17815) |
| 원본 서버 상의 시스템, 응용 프로그램 등을 자체구축 데이터 센터(IDC) 또는 클라우드 플랫폼 등 기존 환경에서 Tencent Cloud로 마이그레이션 | [온라인 마이그레이션 개요](https://intl.cloud.tencent.com/document/product/213/35639) |
| 저장 공간 추가를 위한 클라우드 디스크 크기 확장 | [CBS 확장](https://intl.cloud.tencent.com/document/product/213/32377) |
|일반 공인 IP를 EIP로 전환하여 인스턴스 장애 차단 | [EIP](https://intl.cloud.tencent.com/document/product/213/16586) |
| IPv6 CIDR을 가진 CVM 구축 및 ENI에서 IPv6을 활성화하기 위한 IPv6 내외부 네트워크 통신 실현하기 | [IPv6 주소 설정](https://intl.cloud.tencent.com/document/product/213/34836) |
| 실제 시나리오에 따른 보안 그룹 설정 | [보안 그룹 응용 사례](https://intl.cloud.tencent.com/document/product/213/32369) |
| 다양한 각도(예: 비즈니스, 용도, 책임자 등)에서의 CVM 리소스 분류 관리 | [태그를 사용한 인스턴스 관리](https://intl.cloud.tencent.com/document/product/213/19548) |
| CVM 인스턴스의 CPU, 메모리, 네트워크 대역폭, 디스크 등 모니터링 데이터 조회 | [인스턴스 모니터링 데이터 획득하기](https://intl.cloud.tencent.com/document/product/213/5178) |

## 6. 신규 사용자 FAQ

#### 리전 및 가용존 관련
- [이미 구매한 CVM의 리전 변경이 가능합니까?](https://intl.cloud.tencent.com/document/product/213/17276)
- [중국 외 리전에서 구매한 인스턴스는 Linux 및 Windows와 호환 가능합니까?](https://intl.cloud.tencent.com/document/product/213/17276)

#### 인스턴스 과금 문제
- [종량제 CMV 구매 시 어떤 제한이 존재합니까?](https://intl.cloud.tencent.com/document/product/213/17283)
- [비즈니스에 적합한 CVM 인스턴스 선택 방법은 무엇입니까?](https://intl.cloud.tencent.com/document/product/213/36781)
- [인스턴스 구매 결제를 완료하였는데 인스턴스가 생성되지 않습니다.](https://intl.cloud.tencent.com/document/product/213/36781)

#### 인스턴스 로그인 및 연결 문제
- [Ubuntu에서 root 사용자로 인스턴스에 로그인하는 방법은 무엇입니까?](https://intl.cloud.tencent.com/document/product/213/17278)
- [CVM 인스턴스 원격 연결 시 인스턴스 연결 시간 초과가 안내됩니다.](https://intl.cloud.tencent.com/document/product/213/17278)
- [Linux 인스턴스에 연결할 수 없습니다.](https://intl.cloud.tencent.com/document/product/213/17278)
- [Windows 인스턴스에 연결할 수 없습니다.](https://intl.cloud.tencent.com/document/product/213/17278)

#### CBS 사용 문제
- [Windows를 Linux로 재설치한 후 기존 NTFS 유형 데이터 디스크 읽기 및 쓰기](https://intl.cloud.tencent.com/document/product/213/37890)
- [Linux를 Windows로 재설치한 후 기존 EXT 유형 데이터 디스크 읽기](https://intl.cloud.tencent.com/document/product/213/37890)

#### 비밀번호 문제
- [CVM 초기 비밀번호는 어떻게 획득합니까?](https://intl.cloud.tencent.com/document/product/213/36779)
- [CVM 기본 사용자 이름과 비밀번호는 무엇입니까?](https://intl.cloud.tencent.com/document/product/213/36779)
- [비밀번호 재설정에 실패했습니다.](https://intl.cloud.tencent.com/document/product/213/36779)

#### 포트 문제
- [인스턴스 로그인 전 어떤 포트를 개방해야 합니까?](https://intl.cloud.tencent.com/document/product/213/2502)
- [CVM 상용 포트에는 어떤 것이 있습니까?](https://intl.cloud.tencent.com/document/product/213/12451)
- [25 포트는 어떻게 차단을 해제합니까?](https://intl.cloud.tencent.com/document/product/213/34833)

## 7. 피드백 및 의견
Tencent Cloud CVM 제품 및 서비스 사용 중 문제 또는 의견이 있는 경우 다음 채널을 통해 피드백을 보내주십시오. 전문가가 귀하의 문제를 해결해 드립니다.
- 링크, 내용, API 오류 등 제품 문서에 문제가 발생하는 경우 문서 페이지 오른쪽 [문서 피드백]을 클릭하거나 문제가 있는 내용을 선택하여 피드백을 보낼 수 있습니다.
- 제품 관련 문제가 발생하는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 도움을 요청할 수 있습니다.


