

COS(Cloud Object Storage)는 저렴한 비용과 높은 확장성, 안정성 및 보안을 특징으로 하는 강력한 Tencent Cloud 분산 스토리지 서비스입니다. 대량의 파일을 저장하고 언제든지 클라우드에서 볼 수 있습니다.

대규모 데이터를 저장하고 관리하기 위해 콘솔, API, SDK 또는 툴을 통해 쉽고 빠르게 COS에 액세스할 수 있습니다. COS의 사용자 친화적인 Web 관리 인터페이스를 활용하여 다양한 형식의 파일을 업로드, 다운로드 및 관리할 수 있습니다. 전 세계에 배포된 CDN 노드로 파일 다운로드 속도를 높입니다.



## 제품 기능

COS는 대기업 및 개인 사용자에게 다양한 시나리오가 포함된 데이터 관리, 원격 재해 복구, 데이터 액세스 가속, 데이터 처리 등의 기능을 제공합니다. 자세한 내용은 [기능 개요](https://intl.cloud.tencent.com/document/product/436/8186) 문서를 참고하십시오.

## 기본 개념

이 섹션에서는 Tencent Cloud COS를 더 잘 이해하는 데 도움이 되는 주요 개념을 설명합니다.

- [버킷(bucket)](https://intl.cloud.tencent.com/document/product/436/13312): 객체 저장 수단으로 객체를 저장하는 '컨테이너'의 기능을 하며, 하나의 버킷에는 무수한 객체를 저장할 수 있습니다.
- [객체(Object)](https://intl.cloud.tencent.com/document/product/436/13324): COS의 기본 단위로 이미지, 문서, 멀티미디어 파일 등 다양한 포맷의 데이터를 의미합니다.
- [리전(Region)](https://intl.cloud.tencent.com/document/product/436/6224): Tencent Cloud의 호스팅 데이터 센터가 분포된 지역으로 COS 데이터를 리전의 버킷에 저장합니다.
- [액세스 도메인(Endpoint)](https://intl.cloud.tencent.com/document/product/436/6224): 객체가 버킷에 저장되면 사용자가 액세스 도메인을 통해 객체에 액세스하여 다운로드할 수 있습니다.
- [스토리지 유형(StorageClass)](https://intl.cloud.tencent.com/document/product/436/30925): COS는 STANDARD(다중 AZ), 활성 객체가 COS에 있는 방법을 나타내는 스토리지 레벨입니다. COS는 MAZ_STANDARD, MAZ_STANDARD_IA, MAZ_INTELLIGENT TIERING, STANDARD, STANDARD_IA, INTELLIGENT TIERING, ARCHIVE 및 DEEP ARCHIVE를 비롯한 여러 스토리지 클래스를 제공합니다. 서로 다른 스토리지 클래스는 서로 다른 사용 사례에 적합하며 객체 액세스 빈도 및 액세스 대기 시간과 같은 서로 다른 속성을 가집니다.



## COS 시작하기

### 시작하기

COS는 서비스를 더 잘 이해하고 사용하는 데 도움이 되는 다양한 툴과 비디오 튜토리얼을 제공합니다. 자세한 내용은 [Cloud Object Storage](https://www.tencentcloud.com/products/cos)를 참고하십시오.


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
<td align="left" width="30%"><a href="https://cloud.tencent.com/doc/product/436/10976">COSCMD 툴</a></td>
<td align="left" width="70%">해당 툴은 객체 대량 업로드, 다운로드, 삭제 등의 작업을 위해 간단한 명령 라인을 사용한 명령을 지원합니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">API 방식</a></td>
<td align="left" width="70%">COS는 경량, 비연결형 및 상태 비저장 XML API를 채택합니다. XML API를 호출하면 HTTP/HTTPS를 통해 직접 COS에 요청을 보내고 COS로부터 응답을 받을 수 있습니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK 방식</a></td>
<td align="left" width="70%">Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, 미니프로그램 SDK 등 다양한 주요 개발 언어를 지원합니다.</td>
</tr>
</tbody></table>





## COS는 어떻게 과금되나요?

COS는 기본적으로 종량제(후불)로 청구됩니다. 또한 일부 과금 항목의 사용량도 할인된 리소스 패키지(선불)로 차감할 수 있습니다. 자세한 내용은 [과금 개요](https://intl.cloud.tencent.com/document/product/436/16871)를 참고하십시오.


