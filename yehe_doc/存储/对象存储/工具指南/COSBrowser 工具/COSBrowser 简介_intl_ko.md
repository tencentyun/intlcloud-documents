COSBrowser는 Tencent Cloud에서 출시한 시각적 인터페이스 툴로 COS 리소스를 보다 쉽고 간단하게 보고, 전송하고, 관리하고, 상호 작용할 수 있습니다. 데이터를 마이그레이션하거나 일괄 업로드하려면 [마이그레이션 서비스 플랫폼(Migration Service Platform, MSP)](https://www.tencentcloud.com/products/msp)을 사용하십시오. 현재 COSBrowser는 데스크톱 및 모바일 장치에서 사용할 수 있습니다. 자세한 내용은 다음을 참고하십시오.

- [데스크톱 버전 사용 설명서](https://intl.cloud.tencent.com/document/product/436/32565)
- [모바일 사용 설명](https://intl.cloud.tencent.com/document/product/436/41616)

## 다운로드 주소

<table>
   <tr>
      <th>COSBrowser 분류</td>
      <th>지원 플랫폼</td>
      <th>시스템 요구사항</td>
      <th>다운로드 주소</td>
   </tr>
   <tr>
      <td rowspan=3>데스크톱 버전</td>
      <td>Windows</td>
      <td>Windows 7 32/64비트 이상, Windows Server 2008 R2 64비트 이상</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe">Windows</a></td>
   </tr>
   <tr>
      <td>macOS</td>
      <td>macOS 10.13 이상</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.dmg">macOS</a></td>
   </tr>
   <tr>
      <td>Linux</td>
      <td>그래픽 인터페이스가 있고 <a href="https://appimage.org">AppImage</a> 포맷을 지원해야 함<br>
          주의사항: CentOS에서 클라이언트 실행 시 단말에서 <code>./cosbrowser.AppImage --no-sandbox</code>를 실행해야 함</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest-linux.zip">Linux</a></td>
   </tr>
   <tr>
      <td rowspan=2>모바일 버전</td>
      <td>Android</td>
      <td>Android 4.4 이상</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.apk">Android</a></td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>iOS 11 이상</td>
      <td><a href="https://apps.apple.com/cn/app/id1469323992">iOS</a></td>
   </tr>
   <tr>
      <td>웹 페이지 버전</td>
      <td>Web</td>
      <td>Chrome/FireFox/Safari/IE10+ 등의 브라우저</td>
      <td><a href="https://cosbrowser.cloud.tencent.com/web">Web</a></td>
   </tr>
   <tr>
      <td>Uploader 플러그 인</td>
      <td>Web</td>
      <td>Chrome 브라우저</td>
      <td><a href="https://chrome.google.com/webstore/detail/cosbrowser-uploader/mggpkimgmmdbdbakdkaebhjhgomcmlnd">애플리케이션 마켓</a>/<a href="https://cos5.cloud.tencent.com/cosbrowser/latest-chrome.zip">오프라인 다운로드</a></td>
   </tr>
</table>

## 데스크톱 버전 기능 리스트

COSBrowser 데스크톱 버전은 주로 리소스 관리에 중점을 두고 있으며, 사용자는 COSBrowser를 통해 데이터를 일괄 업로드 및 다운로드를 진행할 수 있습니다.

> !COSBrowser 데스크톱 버전은 시스템에 설정된 프록시를 이용해 네트워크 연결을 시도합니다. 프록시가 정상적으로 설정되어 있는지 확인하고, 인터넷에 연결할 수 없는 프록시 설정은 사용을 중지하시기 바랍니다.
>
> - Windows 사용자는 운영 체제의 'Internet 선택 항목'에서 조회할 수 있습니다.
> - macOS 사용자는 ‘선호 네트워크 설정’에서 조회할 수 있습니다.
> - Linux 사용자는 시스템 설정>네트워크>네트워크 프록시에서 조회할 수 있습니다.

COSBrowser 데스크톱 버전은 다음과 같은 기능을 지원합니다.

| 기능                                                         | 기능 설명                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [버킷 생성/삭제](https://intl.cloud.tencent.com/document/product/436/32565#createordelete) | 버킷 생성 및 삭제 지원                                         |
| [버킷 상세 정보 조회](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket) | 버킷 기본 정보 조회 지원                                       |
| [통계 데이터 조회](https://intl.cloud.tencent.com/document/product/436/32565#count)           | 버킷의 현재 스토리지 용량 및 객체 총 개수 조회 지원                         |
| [권한 관리](https://intl.cloud.tencent.com/document/product/436/32565#acl) | 버킷, 객체 관련 권한 수정 지원                               |
| [버전 제어 설정](https://intl.cloud.tencent.com/document/product/436/32565#version) | 버킷 버전 제어 활성화 및 일시 중지 지원                                 |
| [액세스 경로 추가](https://intl.cloud.tencent.com/document/product/436/32565#addaccess) | 액세스 경로 추가 지원                                             |
| [파일/폴더 업로드](https://intl.cloud.tencent.com/document/product/436/32565#upload) | 파일/폴더를 버킷에 단일 업로드, 일괄 업로드, 증분 업로드 지원 <br><br>참고: <br>1. 파일 일괄 업로드는 10만개를 초과할 수 없음 <br>2. 체크포인트 재시작 미지원 <br>3. 데이터를 마이그레이션하거나 일괄로 업로드하려면 [마이그레이션 서비스 플랫폼 MSP](https://www.tencentcloud.com/products/msp)를 사용하십시오.     |
| [파일/폴더 다운로드](https://intl.cloud.tencent.com/document/product/436/32565#download) | 파일/폴더를 로컬에 단일 다운로드, 일괄 다운로드, 증분 다운로드 지원 <br><br>참고: <br>1. 파일 일괄 다운로드는 10만개를 초과할 수 없음<br>2. 체크포인트 재시작 미지원           |
| [파일/폴더 삭제](https://intl.cloud.tencent.com/document/product/436/32565#delete) | 버킷에 있는 파일 또는 폴더 단일 삭제, 일괄 삭제 지원                 |
| [파일 동기화](https://intl.cloud.tencent.com/document/product/436/32565#synchronization) | 로컬 파일을 버킷에 실시간 동기화 지원                             |
| [파일 복사 및 붙여넣기](https://intl.cloud.tencent.com/document/product/436/32565#copy) | 한 디렉터리에 있는 파일 또는 폴더를 다른 디렉터리로 단일 복사, 일괄 복사 지원   |
| [파일 이름 변경](https://intl.cloud.tencent.com/document/product/436/32565#rename) | 버킷에 있는 파일 이름 변경 지원                                     |
| [폴더 생성](https://intl.cloud.tencent.com/document/product/436/32565#newfolder) | 버킷에 새 폴더 생성 지원                                     |
| [파일 상세 정보 조회](https://intl.cloud.tencent.com/document/product/436/32565#view) | 버킷에 있는 파일 기본 정보 조회 지원                               |
| [파일 링크 생성](https://intl.cloud.tencent.com/document/product/436/32565#generatelinks) | 임시 서명 요청 방식을 통해 유효 시간이 있는 파일 액세스 링크 생성 지원         |
| [파일/폴더 공유](https://intl.cloud.tencent.com/document/product/436/32565#share) | 파일 및 폴더 공유 지원, 공유 유효 시간 설정 지원         |
| [파일 링크 내보내기](https://intl.cloud.tencent.com/document/product/436/32565#export) | 일괄 내보내기 파일 링크 지원         |
| [파일 미리보기](https://intl.cloud.tencent.com/document/product/436/32565#preview) | 버킷에 있는 미디어 파일(이미지, 비디오, 오디오) 미리보기 지원               |
| [파일 검색](https://intl.cloud.tencent.com/document/product/436/32565#searchfile) | 접두사 검색 방식으로 버킷에 있는 파일 검색 지원                 |
| [버킷 검색](https://intl.cloud.tencent.com/document/product/436/32565#searchbuckete) | 생성한 버킷 검색 지원                                       |
| [이전 버전 또는 불완전한 멀티파트 업로드 보기](https://intl.cloud.tencent.com/document/product/436/32565#viewfiles) | <li>버전 관리가 활성화된 버킷에서 파일의 이전 버전 조회 지원<br><li>버킷에 있는 파일 조각 상세 정보 조회 지원           |
|[파일 비교](https://intl.cloud.tencent.com/document/product/436/32565#compare) |     버킷의 파일과 로컬 파일 비교 지원           |
| [비디오 트랜스 코딩](https://intl.cloud.tencent.com/document/product/436/32565#transcoding)   |  미디어 처리가 활성화된 버킷의 파일 트랜스 코딩 지원  |
|  [인증 코드 생성](https://intl.cloud.tencent.com/document/product/436/32565#authorization)   |   인증 코드를 통한 COSBrowser 클라이언트 임시 로그인   |
|  [이미지 처리](https://intl.cloud.tencent.com/document/product/436/32565#processing)  |  크기 조절, 자르기, 회전 등 기본 이미지 처리 및 텍스트 워터마크, 이미지 워터마크 지원, 생성 처리된 이미지 링크 지원   |
| [네트워크 프록시 설정](https://intl.cloud.tencent.com/document/product/436/32565#sets) | 네트워크 프록시를 설정하여 COS에 액세스 지원                                   |
| [최대 동시 업로드/다운로드 파일 수 설정](https://intl.cloud.tencent.com/document/product/436/32565#sets) | 파일의 업로드 및 다운로드에 대한 동시 전송 수 설정 지원                           |
| [최대 동시 업로드/다운로드 파트 수 설정](https://intl.cloud.tencent.com/document/product/436/32565#sets) | 파일 멀티파트 업로드 및 다운로드의 멀티파트 수 설정 지원                           |
| [업로드/다운로드 실패 시 재시도 횟수 설정](https://intl.cloud.tencent.com/document/product/436/32565#sets) | 파일 업로드 및 다운로드 실패 시 재시도 횟수 설정 지원                       |
| [단일 스레드 업로드/다운로드 속도 제한 설정](https://intl.cloud.tencent.com/document/product/436/32565#sets) | 단일 스레드 업로드 제한 속도 및 단일 스레드 다운로드 제한 속도 설정 지원 |
| [업로드 확인 설정](https://intl.cloud.tencent.com/document/product/436/32565#sets) | 버킷에 업로드하는 파일에 대한 2차 인증 지원                       |
| [로컬 로그 조회](https://intl.cloud.tencent.com/document/product/436/32565#sets) | 사용자의 COSBrowser에 대한 작업 기록을 로컬 로그 형식으로 저장 지원       |

## 모바일 버전 기능 리스트

COSBrowser 모바일은 리소스 조회 및 모니터링에 중점을 두고 있으며 사용자는 언제 어디서나 COS 스토리지 용량, 트래픽 등 데이터를 모니터링할 수 있습니다. COSBrowser의 모바일 지원 기능은 [모바일 버전 기능](https://intl.cloud.tencent.com/document/product/436/41616)을 참고하시기 바랍니다.

## 업데이트 로그

- 데스크톱 버전 업데이트 로그: [changelog](https://github.com/tencentyun/cosbrowser/blob/master/changelog.md).
- 모바일 버전 업데이트 로그: [changelog_mobile](https://github.com/tencentyun/cosbrowser/blob/master/changelog_mobile.md).

## 피드백 및 의견

COSBrowser 사용 중 문의사항 또는 의견이 있는 경우 피드백을 보내주십시오.

- 데스크톱 버전 피드백: [issues](https://github.com/tencentyun/cosbrowser/issues).
- 모바일 버전 피드백: [issues_mobile](https://support.qq.com/embed/phone/67467).
  


