애플리케이션 생성 후 [Application Info]에서 애플리케이션 상세 정보를 조회할 수 있습니다. 애플리케이션 기본 정보, 릴레이 라이브 방송 정보, TRTC 서비스 상태, 애플리케이션 태그 등의 내용이 표시됩니다.

## 애플리케이션 정보
### 애플리케이션 정보 설명
1. TRTC 콘솔로 이동하여 [Application Management](https://console.cloud.tencent.com/trtc/app)를 선택해 애플리케이션 리스트를 조회합니다.
2. 정보를 수정할 애플리케이션을 선택하고 오른쪽 작업 열의 [Application Info]를 클릭합니다.
3. 애플리케이션 상세 페이지에 들어가 [Application Info] 탭의 "Application Info" 모듈을 통해 현재 애플리케이션 기본 정보를 조회할 수 있습니다.
<table>
<tr><th width="18%">정보 항목</th><th>설명</th></tr><tr>
<td>애플리케이션 이름</td>
<td>애플리케이션 생성 시 사용자가 직접 이름을 정의하고 수정할 수 있습니다.</td>
</tr><tr>
<td>SDKAppID</td>
<td>애플리케이션 생성 완료 후 자동으로 생성되는 SDKAppID는 애플리케이션의 고유 식별 번호로, 음성 API 인터페이스 호출 시 해당 매개변수를 제공해야 합니다.</td>
</tr><tr>
<td>생성 시간</td>
<td>애플리케이션 생성 완료 시간</td>
</tr><tr>
<td>애플리케이션 소개</td>
<td>애플리케이션 설명으로, 사용자가 직접 수정할 수 있습니다.</td>
</tr><tr>
<td>애플리케이션 출처</td>
<td>애플리케이션 생성 출처 현황: <ul style="margin:0"><li/><a href="https://intl.cloud.tencent.com/document/product/1047/34540">IM 콘솔에서 Tencent TRTC 서비스를 활성화</a>하면 "애플리케이션 출처" 필드가 나타납니다.<li/>TRTC 콘솔에서 직접 생성할 경우 "애플리케이션 출처" 필드가 나타나지 않습니다.</ul></td>
</tr></table>



### 애플리케이션 정보 수정
1. [Application Management](https://console.cloud.tencent.com/trtc/app)에서 정보를 수정할 애플리케이션을 선택한 후 오른쪽 작업 열에 있는 [Application Info]를 클릭하여 애플리케이션 상세 페이지로 이동합니다.
2. [Application Info] 탭에서 "Application Info" 모듈 오른쪽에 있는 [Edit]을 클릭합니다.
3. 애플리케이션 정보 수정 팝업창에서 **애플리케이션 이름** 및 **애플리케이션 소개** 정보를 수정할 수 있으며 [수정]을 클릭하면 저장됩니다.
> ? 
   > - **애플리케이션 이름* 입력창에는 숫자, 중문, 영문, 언더바만 입력할 수 있으며, 최대 15자까지 입력할 수 있습니다.
   > - **애플리케이션 소개* 입력창에는 숫자, 중문, 영문, 언더바만 입력할 수 있으며, 최대 300자까지 입력할 수 있습니다.



## 릴레이 라이브 방송 정보
릴레이 라이브 방송이란 TRTC가 클라우드에서 릴레이 트랜스 코딩 클러스터를 사용하여 TRTC에 적용된 UDP 프로토콜을 표준화된 라이브 방송 RTMP 프로토콜로 변환하고, TRTC 멀티미디어 데이터를 표준 LVB 시스템에 전송한 뒤 다시 CDN을 경유해 배포하는 형식을 말합니다. [CDN 라이브 방송 보기](https://intl.cloud.tencent.com/document/product/647/35242) 기능 구현이 필요한 경우 해당 링크에서 정보를 확인할 수 있습니다.

## TRTC 서비스 상태
현재 애플리케이션의 TRTC 서비스 상태가 표시되며, "사용 가능", "사용 불가" 두 가지 상태가 표시됩니다.
- **사용 가능**: 패키지를 이미 구매한 경우 바로 TRTC 서비스를 정상적으로 사용할 수 있습니다.
- **사용 불가**: 아직 패키지를 구매하지 않은 경우 TRTC 서비스를 사용할 수 없습니다.

## 태그
[태그](https://intl.cloud.tencent.com/document/product/651/13334)는 Tencent Cloud의 각종 리소스를 식별하고 관리하는 데 사용됩니다. 예를 들어, 기업의 각 비즈니스 부서별로 하나 혹은 여러 개의 TRTC 애플리케이션을 사용하고 있을 경우 태그 추가를 통해 부서별 정보를 표기할 수 있습니다.

### 애플리케이션 태그 추가
1. [Application Management](https://console.cloud.tencent.com/trtc/app)에서 태그 정보를 수정할 애플리케이션을 선택한 후 오른쪽 작업 열에 있는 [Application Info]를 클릭하여 애플리케이션 상세 페이지로 이동합니다.
2. [Application Info] 탭에서 "태그" 모듈 오른쪽에 있는 [Edit]을 클릭합니다.
3. 태그 편집창에서 [태그 관리](https://console.cloud.tencent.com/tag/taglist)에 생성된 **태그 키** 및 **태그 값**을 선택합니다.
>? 
>- 현재 존재하는 태그가 요구에 적합하지 않은 경우 [태그 관리](https://console.cloud.tencent.com/tag/taglist)에서 생성할 수 있습니다.
>- 애플리케이션에 여러 개의 태그를 추가할 수 있으며, [+추가]를 클릭하여 태그 설정창을 새로 생성할 수 있습니다.
5. [확인]을 클릭하여 저장하면 콘솔이 새로고침되면서 팝업창에 수정 성공 여부가 표시됩니다.

### 애플리케이션 태그 삭제
1. [Application Management](https://console.cloud.tencent.com/trtc/app)에서 태그 정보를 수정할 애플리케이션을 선택한 후 오른쪽 작업 열에 있는 [Application Info]를 클릭하여 애플리케이션 상세 페이지로 이동합니다.
2. [Application Info] 탭에서 "태그" 모듈 오른쪽에 있는 [Edit]을 클릭합니다.
3. 태그 편집 팝업창에서 삭제할 태그를 선택하고 오른쪽에 있는 삭제 버튼을 클릭합니다.
5. [확인]을 클릭하여 저장하면 콘솔이 새로고침되면서 팝업창에 수정 성공 여부가 표시됩니다.



## 관련 문서
- 신규 애플리케이션 생성에 대한 자세한 방법은 [애플리케이션 생성](https://intl.cloud.tencent.com/zh/document/product/647/39077)을 참조하십시오.
- 애플리케이션 리스트에서 관련 애플리케이션을 검색하는 자세한 방법은 [애플리케이션 검색](https://intl.cloud.tencent.com/zh/document/product/647/39078)을 참조하십시오.
- 애플리케이션 기능 설정 또는 설정 정보 확인에 대한 자세한 방법은 [기능 설정](https://intl.cloud.tencent.com/zh/document/product/647/39080)을 참조하십시오.
- 클라우드에서 혼합 스트리밍 트랜스 코딩 시 사용자 정의 배경 이미지 설정이 필요한 경우 리소스 관리에서 해당하는 이미지 리소스를 추가할 수 있으며, 자세한 방법은 [리소스 관리](https://intl.cloud.tencent.com/zh/document/product/647/39081)를 참조하십시오.
- 애플리케이션 빠른 실행 관련 Demo 소스 코드에 대한 자세한 내용은 [퀵 스타트](https://intl.cloud.tencent.com/zh/document/product/647/39082)를 참조하십시오.









