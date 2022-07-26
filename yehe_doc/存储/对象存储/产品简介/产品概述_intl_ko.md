

Cloud Object Storage(COS)는 Tencent Cloud가 제공하는 대량 파일 저장용 분산형 스토리지 서비스로, 사용자는 네트워크를 통해 언제든지 데이터를 저장 및 조회할 수 있습니다. Tencent Cloud COS는 높은 확장성, 저렴한 가격, 높은 신뢰성 및 보안성을 갖춘 데이터 스토리지 서비스를 제공합니다.

콘솔, API, SDK, 툴 등 다양한 방법으로 간편하고 빠르게 액세스할 수 있으며, 대량의 데이터를 저장하고 관리할 수 있습니다. COS를 사용하면 모든 포맷의 파일에 대한 업로드, 다운로드, 관리가 가능합니다. Tencent Cloud는 직관적인 Web 관리 인터페이스를 제공하며, 중국 전역에 분포되어 있는 CDN 노드에서 파일 다운로드를 가속할 수 있습니다.



## 제품 기능

COS는 대기업 및 개인 사용자에게 다양한 시나리오가 포함된 데이터 관리, 원격 재해 복구, 데이터 액세스 가속, 데이터 처리 등의 기능을 제공합니다. 자세한 내용은 [기능 개요](https://intl.cloud.tencent.com/document/product/436/8186) 문서를 참고하십시오.

## 기본 개념

이 섹션에서는 Tencent Cloud COS를 더 잘 이해하는 데 도움이 되는 주요 개념을 설명합니다.

- [버킷(bucket)](https://intl.cloud.tencent.com/document/product/436/13312): 객체 저장 수단으로 객체를 저장하는 '컨테이너'의 기능을 하며, 하나의 버킷에는 무수한 객체를 저장할 수 있습니다.
- [객체(Object)](https://intl.cloud.tencent.com/document/product/436/13324): COS의 기본 단위로 이미지, 문서, 멀티미디어 파일 등 다양한 포맷의 데이터를 의미합니다.
- [리전(Region)](https://intl.cloud.tencent.com/document/product/436/6224): Tencent Cloud의 호스팅 데이터 센터가 분포된 지역으로 COS 데이터를 리전의 버킷에 저장합니다.
- [액세스 도메인(Endpoint)](https://intl.cloud.tencent.com/document/product/436/6224): 객체가 버킷에 저장되면 사용자가 액세스 도메인을 통해 객체에 액세스하여 다운로드할 수 있습니다.
- [스토리지 유형(StorageClass)](https://intl.cloud.tencent.com/document/product/436/30925): COS는 INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE 및 DEEP ARCHIVE와 같은 객체 스토리지 클래스를 제공합니다. COS에서 객체가 얼마나 활성 상태인지 나타내며 액세스 빈도, 내구성, 가용성, 대기 시간 등이 서로 다릅니다. 사용 사례에 따라 데이터를 업로드할 스토리지 클래스를 선택할 수 있습니다. COS 스토리지 클래스 간의 비교는 [스토리지 클래스 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오.



## COS는 어떻게 사용하나요?

### 신규 사용자 가이드

COS는 COS를 더 잘 이해하고 사용하는 데 도움이 되는 관련 툴 및 영상 가이드와 함께 다양한 학습 경로를 제공합니다.


### 사용 방법

COS는 사용자에게 다양한 사용 방식을 제공합니다. 자세한 사항은 다음 표를 참고하십시오.

<table>
<thead>
<tr>
<th align="left" width="30%">시작 방법</th>
<th align="left" width="70%">기능 설명</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/32955">콘솔</a></td>
<td align="left" width="70%">COS 콘솔은 사용자의 편의를 위해 제공되는 간편하고 손쉬운 COS 사용 수단입니다. 코딩 또는 실행 프로그램 없이 COS 콘솔을 통해 COS 서비스를 바로 이용할 수 있습니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowser 툴</a></td>
<td align="left" width="70%">해당 툴은 데이터 업로드, 다운로드, 액세스 링크 생성 등의 작업을 보다 쉽게 하기 위한 시각화 인터페이스를 지원합니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/10976">COSCMD 툴</a></td>
<td align="left" width="70%">해당 툴은 객체 대량 업로드, 다운로드, 삭제 등의 작업을 위해 간단한 명령 라인을 사용한 명령을 지원합니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">API 방식</a></td>
<td align="left" width="70%">COS는 미연결 상태의 경량급 인터페이스인 XML API를 사용합니다. 이 인터페이스를 호출하면 HTTP/HTTPS를 통한 요청 발송 및 응답 수신으로 Tencent Cloud COS 백그라운드와의 인터랙티브 작업이 가능합니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK 방식</a></td>
<td align="left" width="70%">Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, 미니프로그램 SDK 등 다양한 주요 개발 언어를 지원합니다.</td>
</tr>
</tbody></table>





## COS는 어떻게 과금되나요?

COS는 기본적으로 종량제(후불)로 과금됩니다. 자세한 내용은 [과금 개요](https://intl.cloud.tencent.com/document/product/436/16871) 문서를 참고하십시오.

## 관련 문서

기타 안내 문서는 [개발자 가이드](https://www.tencentcloud.com/document/product/436/14102)를 참고하십시오.

