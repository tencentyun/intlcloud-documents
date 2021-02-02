COS에서는 다음과 같은 주요 기능을 제공합니다.

<table>
   <tr>
      <th colspan=2>기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td rowspan=2>작업</td>
      <td nowrap="nowrap">버킷 작업</td>
      <td>버킷 생성, 조회, 삭제, 비우기를 제공하며, 자세한 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/13309">버킷 관리</a> 디렉터리 문서를 참조하십시오.</td>
   </tr>
   <tr>
      <td>객체 작업</td>
      <td>다양한 스토리지 유형: COS는 액세스 빈도 수에 따라 INTELLIGENT TIERING 스토리지, 표준 스토리지, 표준IA 스토리지, CAS, DEEP ARCHIVE를 포함한 다양한 객체 스토리지 유형을 제공합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/30925">스토리지 유형</a>을 참조하십시오.<br>객체/폴더 업로드, 조회, 다운로드, 복사, 삭제 작업에 대한 자세한 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/13321">객체 관리</a> 디렉터리 문서를 참조하십시오.</td>
   </tr>
   <tr>
      <td rowspan=8>데이터 관리</td>
      <td>라이프사이클</td>
      <td>COS는 사용자가 규칙을 설정할 수 있으며, 지정한 객체를 일정 시간(일) 경과 후 자동으로 삭제하거나 스토리지 유형을 전환할 수 있습니다. 자세한 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/17028">라이프사이클 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>정적 웹사이트</td>
      <td>버킷을 정적 웹사이트 호스팅 모드로 설정할 수 있으며 버킷 도메인을 통해 해당 정적 웹사이트를 액세스할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/30958">정적 웹사이트 호스팅</a>을 참조하십시오.</td>
   </tr>
   <tr>
      <td>인벤토리</td>
      <td>COS는 사용자의 인벤토리 작업 설정에 따라 매일 또는 매주 일정 주기로 사용자 버킷 내의 지정한 객체 또는 동일한 접두사를 가지고 있는 객체를 스캔하여 인벤토리 보고서를 작성해 CSV 포맷 파일로 사용자가 지정한 버킷에 저장할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/30622">인벤토리 기능 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">버킷 태그</td>
      <td>버킷 태그는 버킷을 관리할 수 있는 일종의 표식으로 사용자가 편리하게 버킷을 구분하여 관리할 수 있습니다. 지정한 버킷에 태그를 설정, 조회, 삭제할 수 있으며, 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/31509">버킷 태그 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>이벤트 알림</td>
      <td>COS와 클라우드 함수(Serverless Cloud Function, SCF)를 결합하여 COS 리소스가 변경(예: 신규 파일 업로드, 파일 삭제)될 때 사용자가 즉시 알림을 받을 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/31648">이벤트 알림</a>을 참조하십시오.</td>
   </tr>
   <tr>
      <td>데이터 인덱스</td>
      <td>COS Select 기능은 쿼리 명령(SQL)을 구조화하여 COS에 저장되어 있는 객체를 필터링해 객체를 인덱스하고 사용자가 필요한 데이터를 획득할 수 있습니다. COS Select 기능을 이용해 객체 데이터를 필터링하면 COS 데이터 전송량을 줄일 수 있어 해당 데이터를 인덱스하는 데 필요한 자본과 딜레이를 절감할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/32472">Select 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>로그 관리</td>
      <td>로그 관리 기능은 버킷을 더 편리하게 관리할 수 있도록 지정한 원본 버킷의 액세스 상세 정보를 기록하고 해당 정보를 로그 파일 포맷으로 지정할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/16920">로그 관리 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>객체 태그</td>
      <td>객체 태그 기능은 객체에 키 값 쌍 형식의 표식을 추가하여 사용자가 버킷에 있는 객체를 분할 관리할 수 있도록 도와줍니다. 객체 태그는 태그 키(tagKey)와 태그 값(tagValue)이 =으로 연결되어 구성되며(예: group = IT), 지정한 객체의 태그를 설정, 조회, 삭제할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/35665">객체 태그 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td rowspan=3>원격 재해 복구</td>
      <td>버전 제어</td>
      <td>버전 제어는 동일한 버킷에 동일한 객체의 여러 버전을 저장하는 데 사용합니다. 버킷에 버전 제어 기능을 활성화한 후 버전 ID에 따라 버킷에 있는 객체를 인덱스, 삭제하거나 복구할 수 있으며, 이는 사용자가 잘못 삭제하거나 응용 프로그램 장애로 손실된 데이터를 복구하는 데 도움이 됩니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/19883">버전 제어 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">버킷 복제</td>
      <td>버킷 복제 규칙을 설정하여 각각의 버킷에 자동 및 비동기화 방식으로 증분 객체를 복제해 데이터 재해 복구와 백업을 실현할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/19237">버킷 복제 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
   <tr>
      <td rowspan=2>데이터 보안</td>
      <td>암호화</td>
      <td>COS는 데이터센터 내 디스크에 데이터를 입력하기 전 객체 등급별로 애플리케이션 데이터를 암호화하는 보안 정책을 지원하며, 데이터 액세스 시 자동으로 복호화합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/18145">서버 암호화 개요</a> 및 <a href="https://intl.cloud.tencent.com/document/product/436/33457">버킷 암호화 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>링크 도용 방지</td>
      <td>COS는 링크 도용 방지 설정을 제공합니다. 콘솔의 링크 도용 방지 기능에서 블랙리스트/화이트리스트를 설정하여 데이터 리소스를 안전하게 보호할 수 있으며, 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/32466">링크 도용 방지 사례</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td rowspan=4>Cloud Access Management(CAM)</td>
      <td>크로스 도메인 액세스</td>
      <td>COS는 HTML5 표준 크로스 도메인 액세스 설정을 제공하여 크로스 도메인 액세스를 실현하는 데 도움을 줍니다. 크로스 도메인 액세스는 COS에서 OPTIONS 요청에 응답하여 개발자가 설정한 규칙에 따라 구체적으로 설정된 규칙을 브라우저에 리턴합니다. 자세한 작업 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/13318">크로스 도메인 액세스 설정</a>을 참조하십시오.</td>
   </tr>
   <tr>
      <td>원본 가져오기 기능</td>
      <td>버킷에 원본 가져오기 규칙을 설정하면 사용자가 요청한 객체가 버킷에 존재하지 않거나 특정 요청이 필요하여 리디렉션하는 경우, 원본 가져오기 규칙을 통해 COS에서 상응하는 데이터에 액세스합니다. 자세한 작업 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/31508">원본 가져오기 설정</a>을 참조하십시오.</td>
   </tr>
   <tr>
      <td>버킷 정책</td>
      <td>버킷에 정책을 추가하여 특정 계정, IP 출처(또는 IP측)에서의 COS 리소스 액세스를 허용하거나 차단할 수 있으며, 자세한 작업 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/30927">버킷 정책 추가</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>액세스 제어</td>
      <td>버킷 및 객체의 액세스 권한을 관리할 수 있으며, 리소스 요청 수신 시 COS에서 상응하는 ACL을 조회하여 요청자가 필요한 액세스 권한을 가지고 있는지 검증합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/30581">액세스 제어의 기본 개념</a> 및 <a href="https://intl.cloud.tencent.com/document/product/436/11714">서브 계정에 COS 액세스 권한 부여</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td rowspan=3>액세스 속도</td>
      <td>CDN 가속</td>
      <td>COS에 CDN 가속 서비스를 결합하여 버킷에 있는 콘텐츠를 광범위하게 다운로드, 배포할 수 있으며, 특히 동일한 콘텐츠를 반복적으로 다운로드하는 사용 시나리오에 적용할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/18669">CDN 가속 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>글로벌 가속</td>
      <td>Tencent Cloud COS의 글로벌 가속 기능은 전세계 각지의 사용자가 귀하의 버킷에 빠르게 액세스할 수 있도록 도와줍니다. 귀하의 비즈니스 액세스 성공률을 향상시켜 비즈니스 안정성을 보장하고 비즈니스에 대한 경험을 향상시킵니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/33409">글로벌 가속 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>링크별 속도 제한</td>
      <td>COS는 파일 업로드 및 다운로드 시의 트래픽을 제어하여 다른 애플리케이션의 네트워크 대역폭을 보장합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/34072">링크별 속도 제한</a>을 참조하십시오.</td>
   </tr>
   <tr>
      <td>배치 작업</td>
      <td nowrap="nowrap">배치 처리</td>
      <td>버킷 내 객체 리스트를 지정하여 지정 작업을 실행할 수 있습니다. 인벤토리 기능을 통해 객체 인벤토리를 생성해 객체 리스트를 지정하는 방법, 또는 처리해야 하는 객체를 매니페스트 파일 포맷에 따라 CSV 포맷의 파일에 기록하는 방법이 있으며, 해당 객체 매니페스트 파일에 따라 배치 처리합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/32958">배치 처리 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td rowspan=2>데이터 모니터링</td>
      <td>모니터링 및 알람</td>
      <td>COS의 읽기/쓰기 요청량, 트래픽 등의 데이터는 <a href="https://intl.cloud.tencent.com/doc/product/248">클라우드 모니터링</a>을 기반으로 통계 및 표시합니다. 클라우드 모니터링 <a href="https://console.cloud.tencent.com/monitor/product/COS">콘솔</a>에서 COS의 읽기/쓰기 요청량, 트래픽 등 자세한 모니터링 데이터를 확인할 수 있으며, 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/31649">모니터링 및 알람</a>을 참조하십시오.</td>
   </tr>
   <tr>
      <td>데이터 조회 개요</td>
      <td>COS는 저장 데이터에 대한 모니터링 능력을 제공하며, 데이터 모니터링 창에서 시간대별로 스토리지 유형에 따른 데이터 양과 추세를 확인할 수 있습니다. 자세한 내용은 데이터 모니터링 조회 및 <a href="https://intl.cloud.tencent.com/document/product/436/36542">데이터 조회 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td rowspan=3>데이터 처리</td>
      <td nowrap="nowrap">이미지 처리</td>
      <td>Tencent Cloud COS는 Cloud Infinite(CI)를 통합하는 전문적인 미디어 통합 솔루션을 제공하며, 이미지 처리 및 심사, 식별 등의 기능이 포함되어 있습니다. COS의 업로드 및 처리 인터페이스를 통해 미디어 데이터를 처리할 수 있으며, 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/35280">이미지 처리 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>파일 압축 해제</td>
      <td>파일 압축 해제 기능은 Tencent Cloud COS가 SCF를 기반으로 사용자에게 제공하는 데이터 처리 솔루션입니다. 파일 압축 해제 기능 추가 후, COS에 압축 파일을 업로드하면 COS에서 자동으로 설정해 놓은 SCF를 트리거하여 파일을 버킷 디렉터리에 압축 해제합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/35663">파일 압축 해제</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>CDN 캐시 퍼지</td>
      <td>CDN 캐시 퍼지는 Tencent Cloud COS가 SCF를 기반으로 사용자에게 제공하는 데이터 퍼지 기능입니다. 자동으로 CDN 엣지 노드 상의 캐시 데이터를 퍼지하며, 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/37273"> CDN 캐시 퍼지</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>툴</td>
      <td nowrap="nowrap">다양한 관리 툴</td>
      <td>COS는 편리한 데이터 관리 또는 데이터 마이그레이션을 위해 COSBrowser, COSCMD, COS Migration 등의 다양하고 실용적인 툴을 제공합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/6242">툴 개요</a>를 참조하십시오.</td>
   </tr>
   <tr>
      <td>API/SDK</td>
      <td nowrap="nowrap">다양한 API 및 SDK</td>
      <td><li>API: COS는 기능 인터페이스의 사용 방법 및 매개변수를 포함해 다양한 API 인터페이스와 요청 사례, 응답 사례, 에러 코드 소개를 제공합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/10111">작업 리스트</a>를 참조하십시오. <br><li>COS에서는 Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, 미니프로그램 SDK의 다양한 개발 언어를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK 개요</a>를 참조하십시오.</td>
   </tr>
</table>
