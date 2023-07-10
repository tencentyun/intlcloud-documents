## 소개

본 문서에서는 로컬 데이터를 클라우드에 업로드하여 백업하는 방법을 개략적으로 소개합니다. Tencent Cloud COS는 로컬 데이터를 COS 버킷으로 편리하게 백업할 수 있는 다음 세 가지 백업 방법을 지원합니다.

- COSBrowser 파일 동기화 백업
- COS Migration 온라인 마이그레이션 백업
- CDM 오프라인 마이그레이션 백업

## 파일 동기화 백업

COSBrowser는 Tencent Cloud COS가 출시한 클라우드 파일 관리용 시각화 인터페이스 툴로, COS 리소스 조회, 전송, 관리를 간편하고 인터랙티브하게 실현할 수 있습니다. 현재 COSBrowser는 데스크톱 버전 및 모바일 버전의 두 버전을 제공하며, 자세한 내용은 [COSBrowser 소개](https://intl.cloud.tencent.com/document/product/436/11366)를 참조하십시오.

COSBrowser의 데스크톱 버전은 파일 동기화 기능을 통합하여 로컬 폴더와 버킷을 연결함으로써 로컬 파일을 클라우드로 동기화하여 실시간 업로드할 수 있습니다.

<img src="https://main.qcloudimg.com/raw/fc3160ec43b732936152ccf4f5f107c8.png" style="zoom:60%;" />

#### 사용 방법

[파일 동기화 사용 설명](https://intl.cloud.tencent.com/document/product/436/32565#synchronization)을 참조하십시오.

## 온라인 마이그레이션 방안

COS Migration은 COS의 데이터 마이그레이션 기능을 결합한 통합형 툴입니다. 간단한 설정만으로도 데이터를 COS로 빠르게 마이그레이션할 수 있습니다.

#### 적용 시나리오

로컬 IDC를 보유한 사용자는 COS Migration을 통해 로컬 IDC의 대용량 데이터를 빠르게 COS로 마이그레이션할 수 있습니다.

#### 사용 방법

[COS 마이그레이션](https://intl.cloud.tencent.com/document/product/436/32974#cos)을 참조하십시오.

## 오프라인 마이그레이션 방안

CDM은 Tencent Cloud가 제공하는 오프라인 마이그레이션 전용 디바이스로 사용자가 로컬 데이터를 클라우드로 마이그레이션하도록 돕습니다. 네트워크 전송을 통해 로컬 데이터센터에서 클라우드로 마이그레이션할 때보다 시간, 비용, 보안성 면에서 우수한 성능을 구현합니다.

데이터 마이그레이션 규모, IDC 출력 대역폭, IDC 유휴 서버 리소스, 마이그레이션 실행 시 제한 시간 등 요소를 감안하여 마이그레이션 방법을 선택할 수 있습니다. 아래 이미지는 온라인 마이그레이션 실행 시 예상 소요 시간입니다. 마이그레이션 주기가 10일이 넘거나 마이그레이션 데이터양이 50TB가 넘으면 [CDM](https://intl.cloud.tencent.com/document/product/436/32974#cdm)을 선택하여 오프라인으로 마이그레이션을 실행할 것을 권장합니다.

![](https://main.qcloudimg.com/raw/321d9e3f6a0a1f812da5f87792621093.png)

#### 사용 방법

[CDM](https://intl.cloud.tencent.com/document/product/436/32974#cdm)을 참조하십시오.

