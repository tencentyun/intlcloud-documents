본문은 CSS 콘솔에서 타임 시프트 세부 정보를 보고 타임 시프트 재생을 구성하는 방법을 보여줍니다.

## 전제 조건
- CSS 콘솔에 로그인되어 있습니다.
- [타임 시프트 템플릿](https://cloud.tencent.com/document/product/267/85686)을 생성하여 푸시 도메인에 바인딩하고 성공적으로 스트림을 푸시했습니다.

## 작업 단계
1. 왼쪽 사이드바에서 **기능 구성** > **타임 시프트**를 클릭하고 > [타임 시프트 세부 정보](https://console.cloud.tencent.com/live/config/time-shift/meta) 탭을 선택합니다.
2. 도메인 또는 스트림 ID 검색을 지원합니다. 쿼리 기간 범위는 24시간을 지원합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/98a84c68da571dbe3e8c1fa96e80c47d.png)
3. **세부 사항**을 클릭하여 세부 정보 페이지로 들어갑니다.
4. 기본 정보 영역에서 푸시 URL 및 스트림 유형을 봅니다.
5. 인덱스 세부 정보 영역에서 타임라인을 마우스로 가리키면 타임스탬프가 표시됩니다.
6. 타임라인을 클릭하여 특정 시점의 비디오를 미리보기하고 해당 지점을 표시할 수 있습니다.

>! 타임 시프트 콘텐츠를 미리보기 하려면 재생에 사용되는 도메인에 HTTPS 인증서가 있어야 합니다. 재생 도메인에 아직 HTTPS 인증서가 없는 경우 **도메인 관리** >[인증서 관리](https://console.cloud.tencent.com/live/domainmanage/certificate)에서 인증서를 추가하십시오. 타임 시프트 기능을 사용하면 재생 트래픽/대역폭 요금이 발생합니다.

7. 다음과 같이 타임 시프트 재생을 구성합니다.

<table>
   <thead><tr><th width="20%" colspan=2>구성 항목</th><th>설명</th></tr></thead>
   <tbody><tr>
   <tr>
   <td rowspan=2 width="10%">타임 시프트 모드</td>
   <td width="30%">오프셋</td> 
   <td>이 모드에서는 재생 지연 시간을 지정하여 타임 시프트 재생을 구성합니다. 진행 중인 라이브 스트림에 적합합니다.</ul></td>
   </tr><tr>
   <td>기간</td>
   <td>이 모드에서는 재생 시작 및 종료 시간을 지정합니다(6시간 이내의 타임 시프트 콘텐츠 선택 가능). 이미 종료된 라이브 스트림에 적합합니다.</td>
   </tr><tr>
   <td colspan=2>재생 도메인</td>
   <td>CSS에 추가된 재생 도메인을 선택합니다.</td>
   </tr><tr>
 <td colspan=2>타임 시프트 재생 URL 생성</td>
   <td>주소 생성을 클릭하여 타임 시프트 재생 URL을 생성하고 복사합니다.</td>
   </tr><tr>  
</tbody></table>

![](https://qcloudimg.tencent-cloud.cn/raw/55aa01d9fc5c2a8aabf1db3b6dcf92f8.png)