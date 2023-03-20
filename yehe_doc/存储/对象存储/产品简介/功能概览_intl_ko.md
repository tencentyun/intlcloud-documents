Cloud Object Storage(COS)는 주로 다음과 같은 기능을 제공합니다.

## 작업

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td nowrap="nowrap">버킷 작업</td>
      <td>버킷 생성, 조회, 삭제, 비우기를 지원합니다. 자세한 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/13309">버킷 관리</a> 문서를 참고하십시오.</td>
   </tr>
   <tr>
      <td>객체 작업</td>
      <td>스토리지 유형: 객체의 액세스 빈도 및 재해 복구 정도에 따라 COS에서 제공하는 MAZ(다중AZ)_STANDARD, MAZ_STANDARD_IA, INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE 또는 DEEP ARCHIVE 중에서 스토리지 클래스를 선택할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/30925">스토리지 유형 개요</a>를 참고하십시오. <br>객체/폴더: 업로드, 쿼리, 다운로드, 복사 및 삭제할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/13321">객체 업로드</a>를 참고하십시오.</td>
   </tr>
</table>	 

## 데이터 관리

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td>라이프사이클</td>
      <td>COS를 사용하면 객체 또는 스토리지 클래스 전환에 대한 자동 삭제를 정기적으로 수행하도록 객체에 대한 라이프사이클 규칙을 설정할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/17028">라이프사이클 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>정적 웹 사이트</td>
      <td>버킷을 정적 웹 사이트 호스팅 모드로 설정하고 버킷 도메인을 통해 해당 정적 웹 사이트에 액세스할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/30958">정적 웹 사이트 호스팅</a>을 참고하십시오.</td>
   </tr>
   <tr>
      <td>리스트</td>
      <td>COS는 사용자의 리스트 작업 설정에 따라 매일 또는 매주 정해진 시간에 버킷 내의 지정된 객체 또는 동일한 객체 접두사를 가진 객체를 스캔한 후 리스트 보고서를 출력해 사용자가 지정한 버킷에 CSV 포맷 파일로 저장합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/30622">리스트 기능 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">버킷 태그</td>
      <td>버킷 태그는 버킷을 관리하는 하나의 식별자로, 사용자가 편리하게 버킷을 구분하여 관리할 수 있으며 지정된 버킷의 태그 설정, 조회, 삭제 작업이 가능합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/31509">버킷 태그 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>이벤트 공지</td>
      <td>COS는 SCF(Serverless Cloud Function)와 결합하여 COS 리소스에 변동이 발생하는 경우(예: 신규 파일 업로드, 파일 삭제) 즉시 공지 정보를 받을 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/31648">이벤트 공지</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>데이터 인덱스</td>
      <td>COS Select 기능은 구조화된 쿼리 명령(SQL)으로 COS에 저장되어 있는 객체를 필터링해 객체를 인덱스하고 필요한 데이터를 획득합니다. COS Select 기능을 통해 객체 데이터를 필터링하면 COS 전송 데이터의 양을 줄여 데이터 인덱스에 필요한 비용과 딜레이를 낮출 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/32472">Select 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>로그 관리</td>
      <td>로그 관리 기능은 지정 원본 버킷의 상세 액세스 정보를 기록하고, 해당 정보를 로그 파일 포맷으로 지정 버킷에 저장하여 버킷을 더욱 효율적으로 관리할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/16920">로그 관리 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>객체 태그</td>
      <td>객체 태그 기능은 객체에 키 값 쌍을 형성하는 식별자를 추가하여, 사용자가 버킷에 있는 객체를 그룹화하고 관리하는 데 도움이 되도록 설계되었습니다. 객체 태그는 태그 키(tagKey)와 태그 값(tagValue)이 =로 연결되어 구성되며(예:group = IT), 지정한 객체에 태그를 설정, 조회, 삭제할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/35665">객체 태그 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>스토리지 게이트웨이</td>
      <td>CSG는 Tencent Cloud가 제공하는 하이브리드 클라우드 서비스입니다. 버킷에 CSG를 설정하면 COS의 버킷이 네트워크 폴더 형식으로 사용자의 모든 CVM 서버에 마운트되어 스토리지 디바이스로 사용할 수 있습니다.</td>
   </tr>
</table>

## 원격 재해 복구

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td>버전 관리</td>
      <td>버전 관리는 동일한 버킷에 동일한 객체의 여러 버전을 저장하는 데 사용합니다. 특정 버킷에 버전 관리 기능을 활성화하면 버전 ID에 따라 버킷에 저장되어 있는 객체를 인덱스, 삭제 또는 복구할 수 있습니다. 이는 사용자가 실수로 삭제하거나 응용 프로그램 장애로 인한 데이터 손실을 복구하는 데 도움이 됩니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/19883">버전 제어 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">버킷 복사</td>
      <td>버킷 복사 규칙을 설정하여 다른 버킷에 자동으로 증분 객체를 비동기 복사해 데이터 재해 복구 및 백업을 실행할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/19237">버킷 복제 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">MAZ(다중AZ) 구성</td>
      <td>MAZ는 COS에서 제공하는 다중 AZ 스토리지 아키텍처를 말하며 데이터에 대한 IDC 레벨의 재해 복구 기능을 제공할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/35208">Overview of Multi-AZ Feature</a>를 참고하십시오.</td>
   </tr>
</table>


## 데이터 보안

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td>암호화</td>
      <td>COS는 데이터센터 내 디스크에 데이터가 입력되기 전, 객체 등급에 애플리케이션 데이터 암호화 보호 정책을 지원하며, 데이터 액세스 시 자동으로 복호화합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/18145">서버 암호화 개요</a> 및 <a href="https://intl.cloud.tencent.com/document/product/436/33457">버킷 암호화 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>링크 도용 방지</td>
      <td>COS는 링크 도용 방지 설정을 지원하며, 사용자는 콘솔의 링크 도용 방지 기능을 통해 블록리스트/얼로우리스트를 설정하여 데이터 리소스를 안전하게 보호할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/32466">링크 도용 방지 사례</a>를 참고하십시오.</td>
   </tr>
</table>

## 액세스 관리

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td>크로스 도메인 액세스</td>
      <td>COS는 HTML5 표준의 크로스 도메인 액세스 설정을 제공하여 크로스 도메인 액세스를 돕습니다. COS는 크로스 도메인 액세스를 위한 OPTIONS 요청 응답을 지원하며, 개발자가 설정한 규칙에 따라 브라우저에 구체적인 설정 규칙을 반환합니다. 자세한 작업 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/13318">CORS 설정</a>을 참고하십시오.</td>
   </tr>
   <tr>
      <td>Origin-pull 기능</td>
      <td>버킷에 Origin-pull 규칙을 설정하면 사용자가 요청하는 객체가 버킷에 존재하지 않거나 특정 요청을 리디렉션해야 하는 경우, Origin-pull 규칙을 통해 COS에서 상응하는 데이터에 액세스합니다. 자세한 작업 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/31508">Origin-pull 설정</a>을 참고하십시오.</td>
   </tr>
   <tr>
      <td>버킷 정책</td>
      <td>버킷에 정책을 추가하여 임의의 계정, IP 출처(또는 IP 대역)의 COS 리소스 액세스를 허용하거나 차단할 수 있습니다. 자세한 작업 방법은 <a href="https://intl.cloud.tencent.com/document/product/436/30927">버킷 정책 추가</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>액세스 제어</td>
      <td>사용자는 버킷 및 객체의 액세스 권한을 관리할 수 있으며, 임의의 리소스 요청 수신 시 COS에서 상응하는 ACL을 검사하여 요청자가 필요한 액세스 권한을 가지고 있는지 여부를 인증합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/30581">액세스 제어 기본 개념</a> 및 <a href="https://intl.cloud.tencent.com/document/product/436/11714">서브 계정에 COS 액세스 권한 부여</a>를 참고하십시오.</td>
   </tr>
</table>

## 액세스 속도

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td>CDN 가속</td>
      <td>COS는 CDN 가속 서비스와 결합하여 버킷에 있는 콘텐츠를 대량으로 다운로드하거나 배포할 수 있으며, 특히 동일한 콘텐츠를 반복적으로 다운로드하는 시나리오에 유용합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/18669">CDN 가속 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>글로벌 가속</td>
      <td>COS의 글로벌 가속 기능은 전세계 각지의 사용자가 귀하의 버킷에 빠르게 액세스할 수 있도록 도와줌으로써 귀하의 비즈니스 액세스 성공률을 높여 비즈니스의 안정성을 보장하고 사용자 경험을 향상시킵니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/33409">글로벌 가속 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>단일 링크 속도 제한</td>
      <td>COS는 다른 애플리케이션의 네트워크 대역폭을 고려해 파일을 업로드 및 다운로드할 때 발생하는 트래픽을 제어합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/34072">단일 링크 속도 제한</a>을 참고하십시오.</td>
   </tr>
</table>

## 배치 작업

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td nowrap="nowrap">일괄 프로세스</td>
      <td>버킷 내 객체 리스트를 지정하여 지정 작업을 실행할 수 있습니다. 리스트 기능을 통해 지정된 객체 리스트가 될 객체 리스트를 생성하거나, 처리해야 하는 객체를 매니페스트 파일 포맷에 따라 CSV 포맷의 파일에 기록하는 방법이 있으며, 해당 객체 매니페스트 파일에 따라 일괄 처리합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/32958">일괄 프로세스 개요</a>를 참고하십시오.</td>
   </tr>
</table>

## 데이터 모니터링

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td>모니터링 및 알람</td>
      <td>COS의 읽기/쓰기 요청량, 트래픽 등의 데이터는 <a href="https://www.tencentcloud.com/document/product/248">Cloud Monitor</a>를 기반으로 통계 및 표시합니다. 클라우드 모니터 <a href="https://console.cloud.tencent.com/monitor/product/COS">콘솔</a>에서 COS의 읽기/쓰기 요청량, 트래픽 등 자세한 모니터링 데이터를 확인할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/31649">모니터링 및 알람</a>을 참고하십시오.</td>
   </tr>
   <tr>
      <td>데이터 조회 개요</td>
      <td>COS는 저장 데이터에 대한 모니터링 능력을 제공하며, 데이터 모니터링 창에서 시간대별로 스토리지 유형에 따른 데이터 양과 추세를 확인할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/36542">데이터 개요 조회</a> 및 <a href="https://intl.cloud.tencent.com/document/product/436/31634">데이터 모니터링 조회</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>모니터링 알람 설정</td>
      <td>Cloud Monitoring의 알람 정책을 통해 COS 모니터링 지표의 임계값 알람을 설정할 수 있습니다. 알람 정책에는 정책 이름, 정책 유형, 알람 트리거 조건, 알람 객체, 알람 공지 템플릿의 다섯 가지 필수 구성이 포함되어 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/39104">모니터링 알람 설정</a>을 참고하십시오.</td>
   </tr>
</table>

## 데이터 처리

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td nowrap="nowrap">이미지 처리</td>
      <td>COS는 전문 통합 미디어 솔루션인 Cloud Infinite(CI)를 통합하여 이미지 처리, 조정, 식별 등 다양한 서비스를 수행합니다. COS 업로드 및 처리 API를 사용하여 미디어 데이터를 처리할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/35280">이미지 처리 개요</a>를 참고하십시오. 또한 이미지 고급 압축 및 블라인드 워터마크 기능도 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/40115">이미지 압축 개요</a> 및 <a href="https://intl.cloud.tencent.com/document/product/436/46325">블라인드 워터마크 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>미디어 처리</td>
      <td>미디어 처리는 COS에서 CI 기반으로 제공하는 멀티미디어 파일 처리 서비스로서, 오디오/비디오 트랜스코딩, 비디오 프레임 캡처, 오디오/비디오 스플라이싱, 비디오 gif 변환, 비디오 메타데이터 수집 등 비디오 처리 서비스를 포함합니다. Tencent Cloud의 최첨단 AI 기술을 결합한 스마트 썸네일 고급 처리 서비스도 제공합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/48303">미디어 처리 개요</a> 및 <a href="https://intl.cloud.tencent.com/document/product/436/46387">Data Workflow Overview</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>파일 처리</td>
      <td>파일 처리는 CI 기반의 COS에서 제공하는 모든 형식의 파일 처리 서비스입니다. 현재 파일 해시 계산, 파일 압축 해제 및 다중 파일 압축 기능을 제공합니다.</td>
   </tr>
   <tr>
      <td>파일 미리보기</td>
      <td>파일 미리보기는 CI를 기반으로 합니다. 활성화되면 버킷의 문서 파일을 다운로드하지 않고 온라인으로 직접 미리 볼 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/49159">문서 미리보기 개요</a>를 참고하십시오.</td>
   </tr>
   <tr>
      <td>스마트 오디오</td>
      <td>스마트 오디오는 CI를 기반으로 합니다. 활성화되면 텍스트 음성 변환, 음성 인식 및 오디오 노이즈 감소와 같은 작업을 수행할 수 있습니다.</td>
   </tr>

   <tr>
      <td>함수 계산</td>
      <td>COS를 사용하면 지정된 버킷에 대한 파일 압축 해제 및 CDN 캐시 퍼지를 설정할 수 있습니다.</td>
   </tr>
	 
	 
</table>

## 데이터 조정

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td>콘텐츠 조정</td>
      <td>COS 콘텐츠 조정 서비스는 이미지, 비디오, 음성, 텍스트, 문서 및 웹 페이지 등의 멀티미디어 콘텐츠를 지능적으로 조정합니다. 음란물, 저속, 폭력, 테러리스트, 불법, 저속하고 공격적인 정보와 같은 비준수 콘텐츠를 효과적으로 식별하여 운영상의 위험을 방지할 수 있습니다.</td>
   </tr>
</table>

## 애플리케이션 통합

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td nowrap="nowrap">다른 Tencent Cloud 서비스와 통합</td>
      <td>COS는 SCF(Serverless Cloud Function)를 기반으로 데이터베이스 백업, 메시지 백업, 로그 백업, 로그 분석, 파일 압축 해제, 데이터 내보내기 기능을 제공합니다. 자세한 내용은 <a href="https://www.tencentcloud.com/document/product/436/39924">애플리케이션 통합</a>을 참고하십시오.</td>
   </tr>
</table>

## 툴

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td nowrap="nowrap">다양한 관리 툴</td>
      <td>COS는 COSBrowser, COSCMD, COSCLI 및 COS Migration과 같은 툴 세트를 제공하여 데이터 관리 및/또는 마이그레이션을 돕습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/6242">툴 개요</a>를 참고하십시오.</td>
   </tr>
</table>

## API/SDK

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td nowrap="nowrap">다양한 API 및 SDK</td>
      <td><ul  style="margin: 0;"><li>API: COS는 기능 인터페이스의 사용 방법 및 매개변수를 포함해 다양한 API 인터페이스와 요청 사례, 응답 사례, 에러 코드 소개를 제공합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/10111">Operation List</a>를 참고하십시오. </li><li>COS에서는 Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, 미니프로그램 SDK의 다양한 개발 언어를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK 개요</a>를 참고하십시오.</li></ul></td>
   </tr>
</table>

## 프로토콜 지원

<table>
   <tr>
      <th style="width: 18%;">기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td>다양한 프로토콜</td>
      <td>COS는 HTTP1.0 및 HTTP1.1 전송 프로토콜과 TLS1.0, TLS1.1 및 TLS1.2 암호화 프로토콜을 지원합니다.</td>
   </tr>
</table>


