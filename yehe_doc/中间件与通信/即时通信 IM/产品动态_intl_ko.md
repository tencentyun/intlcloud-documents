## 2021년 12월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.8.1696 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 로컬에서 해산된 그룹 세션이나 퇴장한 그룹 대화 읽지 않은 메시지 수가 포함된 경우, 읽지 않은 메시지 비우기 실패가 발생하는 문제 수정</li>
    	<li> TUIKit 메시지 답장 기능 추가 지원</li>
	<li> TUIKit 기본 스킨 변경 및 인터페이스 로직 최적화</li>
	<li> iOS 리소스 파일 로딩 실패 문제 수정</li>
    </ul></td>
    <td> 2021-12-10 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 11월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.8.1672 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 컴플라이언스 요구 충족을 위해 디바이스 정보 수집 로직 최적화</li>
    	<li> 특정 조건에서의 읽지 않은 메시지 수 원클릭 비우기 기능 크래쉬 문제 수정</li>
    </ul></td>
    <td> 2021-11-30 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.8.1668 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 모든 세션의 읽지 않은 메시지 원클릭 비우기 기능 추가</li>
    	<li> 울티메이트 버전 Community 지원 추가(최대 10만명)</li>
    	<li> 울티메이트 버전 활성화 시 AVChatRoom 라이브 그룹 입장 이전의 20개의 메시지 반환 지원</li>
    	<li> 가져온 읽지 않은 총 세션 수에서 수신 옵션이 ‘알림 수신 중지’ 및 ‘메시지 수신 중지’ 세션의 메시지를 자동으로 제거</li>
    	<li> 장기간 연결 암호화 채널에 대한 국비급 지원 추가</li>
    	<li> 그룹 메시지 기록 풀링 시, 종료 플래그의 판단 오류 문제 수정</li>
    	<li> 기본 버전에서 인핸스드 버전으로 업그레이드 시 이전에 입장한 라이브 그룹에 읽지 않은 메시지 수가 발생하는 문제 수정</li>
    	<li> 특수 형식 계정의 읽음 리포트 설정 실패 문제 수정</li>
    	<li> 개인 환경에서 네트워크 연결이 자주 끊겼다가 다시 연결될 때 간헐적으로 연결된 서버가 올바르지 않은 문제 수정</li>
	<li> 업데이트 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">업데이트 로그</a>를 참고하십시오</li>
    </ul></td>
    <td> 2021-11-19 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 09월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.7.1435 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 그룹 프로필 정보 사용자 정의 필드 변경 후 로컬 데이터가 즉시 업데이트 되지 않는 문제를 수정했습니다</li>
    	<li> 상단 고정 대화 수가 너무 많은 경우 발생하는 동기화 문제를 수정했습니다</li>
    	<li> Android 타임아웃 신호에 초대 시 작성한 사용자 정의 데이터가 포함되지 않는 문제를 수정했습니다</li>
    	<li> 친구가 아닌 사용자의 프로필 정보 풀링 시, 네트워크 요청 실패로 인해 빈 정보로 로컬 정보를 덮어쓰기 하는 문제를 수정했습니다</li>
    	<li> 그룹 퇴장 후 다시 입장 시 이전 메시지 기록을 풀링하는 문제를 수정했습니다</li>
    	<li> 친구 삭제 후 onFriendListDeleted를 2번 콜백하는 문제를 수정했습니다</li>
    	<li> 대화의 마지막 메시지에서 친구 설명이 공백으로 나타나는 문제를 수정했습니다</li>
    	<li> IM SDK 초기화 후 로그인하지 않으면 getConversationList 호출 시 콜백이 없는 문제를 수정했습니다</li>
    	<li> 네트워크 연결이 끊겨 그룹 대화에 실패 메시지가 발송된 후, 네트워크 복구 시 해당 대화에서 수신된 첫 번째 메시지에 읽지 않음 수가 표시되지 않는 문제를 수정했습니다</li>
	<li> 업데이트 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">업데이트 로그</a>를 참고하십시오</li>
    </ul></td>
    <td> 2021-09-30 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.66 기본 버전 배포</td>
    <td><ul style="margin:0">
        <li> WiFi 정보를 제거하고 가져오기</li>
    </ul></td>
    <td> 2021-09-22 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.6.1202 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 그룹 퇴장 후 다시 동일한 그룹 입장 시 그룹 퇴장 기간 동안 미수신 메시지도 읽지 않은 메시지 수에 포함되는 문제를 수정했습니다</li>
    	<li> 음소거되어 발송 실패한 그룹 메시지를 삭제할 수 없는 문제를 수정했습니다</li>
    	<li> 메시지 기록 풀링 시, 간혹 메시지 발신자의 대화명 및 프로필 사진을 이전 데이터로 복구하는 문제를 수정했습니다</li>
    	<li> 회의 그룹에 읽지 않음 수 표시 여부를 설정할 수 있습니다</li>
    	<li> 싱가포르, 한국, 독일 3개의 글로벌 포털에서 액세스 가속을 지원합니다</li>
    	<li> 수신된 이미지 메시지에 간혹 형식 오류가 발생하는 문제를 수정했습니다</li>
    	<li> Windows 플랫폼에서 비디오 메시지 발송 시, 썸네일 발송 실패 문제를 수정했습니다</li>
    	<li> 일반 그룹 메시지의 수신 성공률 데이터 리포트를 최적화했습니다</li>
    	<li> 라이브 방송 그룹에서 그룹 구성원 음소거 설정 후 그룹 구성원 프로필 정보에 음소거 시간이 0으로 표시되는 문제를 수정했습니다</li>
    </ul></td>
    <td> 2021-09-10 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 08월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.6.1200 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 로그인 소요 시간을 최적화했습니다</li>
    	<li> 싱가포르, 한국, 독일 글로벌 포털을 지원합니다</li>
    	<li> 상용화 Http DNS를 지원합니다</li>
    	<li> 그룹 속성 로직을 최적화하여 멀티 단말에서 동시에 그룹 속성 수정 시 발생하는 동시성 문제를 해결했습니다</li>
    	<li> 메시지 데이터베이스 쿼리 속도를 최적화했습니다</li>
    	<li> 네트워크 연결 정책을 최적화했습니다</li>
    	<li> 이미지, 비디오, 음성 메시지 검색을 최적화했습니다</li>
    	<li> 대화 리스트 getConversationList 불러오기에 많은 시간이 소요되는 문제를 최적화했습니다</li>
    	<li> 라이브 방송 그룹은 읽음 리포트가 생성되지 않습니다</li>
    	<li> 로그인 오류 코드 통합</li>
    	<li> 친구 검색 콜백 매개변수를 V2TIMFriendInfo에서 V2TIMFriendInfoResult로 변경하여 relationType에 따른 친구 관계 판단을 용이하게 하였습니다</li>
    	<li> 메시지 객체에 오프라인 푸시 설정 가져오기 인터페이스를 추가했습니다</li>
    	<li> 개인 프로필 정보에 간혹 나타나는 데이터베이스 크래쉬 문제를 수정했습니다</li>
        <li> 업데이트 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">업데이트 로그</a>를 참고하십시오</li>
    </ul></td>
    <td> 2021-08-31 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 07월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.5.897 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
	<li> 데이터 리포트 시, 간헐적으로 발생하는 크래쉬 문제를 수정했습니다.</li>
        <li> 통신사 이름 가져오기 콜백 getSimOperatorName()을 제거했습니다.</li>
    </ul></td>
    <td> 2021-07-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.65 기본 버전 배포</td>
    <td><ul style="margin:0">
        <li> 통신사 이름 가져오기 콜백 getSimOperatorName()을 제거했습니다.</li>
    </ul></td>
    <td> 2021-07-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.5.892 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> ‘and’ 또는 ‘or’ 로직 관계의 다중 키워드 메시지 검색 기능을 추가했습니다.</li>
    	<li> 메시지 발신자 계정으로 메시지를 검색하는 기능을 추가했습니다.</li>
    	<li> 메시지 기록 풀링 시, 시간 범위를 설정할 수 있습니다.</li>
    	<li> 그룹 메시지 기록 풀링 시, sequence에 따라 풀링할 수 있습니다.</li>
    	<li> 타사 콜백에 의한 메시지 수정 알림 기능을 추가했습니다.</li>
    	<li> 그룹 프로필에 허용된 최대 그룹 구성원 수를 가져오는 인터페이스를 추가했습니다.</li>
    	<li> App 레이어에서 마지막 메시지가 없는 대화를 정렬할 수 있도록 대화 객체에 orderKey 정렬 필드를 추가했습니다.</li>
    	<li> 라이브 방송 그룹 메시지 수신 딜레이와 백엔드 계정 전환 사전 완료를 최적화했습니다.</li>
    	<li> 인터넷 연결 스케쥴링 프로토콜을 업데이트하고, 중국 본토 외 지역 인터넷 연결 소요 시간을 최적화했습니다.</li>
    	<li> 대화 목록 풀링 로직을 최적화했습니다.</li>
    	<li> 그룹 구성원 리스트 풀링 로직을 최적화하고, 로컬 캐시를 활성화했습니다.</li>
    	<li> ‘로그 레벨이 Debug보다 낮을 때 로그 콜백을 트리거하지 않는 문제’를 수정했습니다.</li>
	<li> ‘그룹 구성원 정보를 가져올 때 친구 설명이 없는 문제’를 수정했습니다.</li>
    	<li> ‘참여한 그룹 리스트를 가져올 때 그룹 소유자 승인 대기 중인 그룹까지 포함하는 문제’를 수정했습니다.</li>
    	<li> 온라인에서 보고된 안정성 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-07-14 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>


## 2021년 06월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.4.666 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 기존 라이트 버전 SDK 이름을 인핸스드 버전 SDK로 변경합니다.</li>
    	<li> 메시지 검색, 그룹 검색, 친구 검색을 지원합니다(울티메이트 버전만 지원).</li>
    	<li> 메시지 발송 시, 대화의 마지막 메시지 업데이트 여부 설정에 사용되는 매개변수를 추가했습니다.</li>
    	<li> 대화를 유지하면서 대화의 로밍 메시지를 지우는 기능이 추가되었습니다.</li>
    	<li> 여러 단말이 동시에 동일 플랫폼에 로그인할 수 있습니다(울티메이트 버전만 지원).</li>
    	<li> 네트워크 연결 및 로그인 소요 시간을 최적화했습니다.</li>
    	<li> 데이터 리포트를 최적화했습니다.</li>
    	<li> 오프라인 푸시 로직을 최적화하였으며, 전역에서 메시지 오프라인 푸시 비활성화를 지원합니다</li>
    	<li> 오프라인 푸시 로직을 최적화하였으며, VIVO 휴대폰 오프라인 푸시 메시지 분류 classification 필드를 지원합니다</li>
    	<li> C2C 대화 읽지 않음 수가 간헐적으로 부정확한 문제를 수정했습니다.</li>
    	<li> 메시지 기록 풀링 속도를 최적화했습니다.</li>
    	<li> 멀티 Element 메시지에 이모티콘 및 위치 추가를 지원합니다.</li>
    	<li> 오프라인 상태에서 그룹 닉네임 수정 후, 다시 로그인 시 해당 대화의 닉네임이 제때에 업데이트되지 않는 문제를 수정했습니다.</li>
    	<li> C2C 대화에 대해 읽음 리포트를 한 후 간혹 20005 오류 코드가 발생하는 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-06-03 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 05월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.3.435 라이트 버전 배포</td>
    <td><ul style="margin:0">
        <li> 대화 로밍 메시지 삭제 인터페이스를 추가했습니다.</li>
    	<li> 일부 안드로이드 휴대폰으로 장시간 인터넷 연결 시, 네트워크 상태 변화 공지를 수신하지 못하는 문제를 수정했습니다.</li>
    	<li> 낯선 사람이 친구 프로필 정보를 요청할 때마다 백엔드에 요청하지 않도록 친구 프로필 정보 풀링 로직을 최적화했습니다.</li>
     	<li> 그룹은 해산하고 대화는 유지하는 시나리오에서 그룹 정보 및 대화 메시지 기록을 가져오지 못하는 문제를 수정했습니다.</li>
	<li> 대화 목록 가져오기 인터페이스에 대화 순서 오류가 발생하는 문제를 수정했습니다.</li>
    	<li> 대화의 읽지 않음 총 수량 가져오기 인터페이스를 추가했습니다.</li>
    	<li> 대화의 읽지 않음 총 수량을 가져올 때 방해 금지를 설정한 그룹 대화를 필터링하는 문제를 수정했습니다.</li>
    	<li> iOS 플랫폼 HTTP 요청에 간헐적으로 발생하는 Crash 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-05-20 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.62 스탠다드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 기존 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-05-20 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 04월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.3.425 라이트 버전 배포</td>
    <td><ul style="margin:0">
        <li> 대화 상단 고정 설정을 지원합니다.</li>
    	<li> 1:1 채팅 메시지 방해 금지 설정을 지원합니다.</li>
    	<li> 읽지 않음 수에 포함되지 않는 메시지 발송을 지원합니다.</li>
     	<li> 네트워크 로그인에 실패하지 않은 상황에서 로컬 대화 및 메시지 데이터 가져오기를 지원합니다.</li>
	<li> iOS 버전에 xcframework를 추가했습니다(Mac Catalyst 지원).</li>
    	<li> 대화의 읽지 않음 총 수량 가져오기 인터페이스를 추가했습니다.</li>
    	<li> 개인 정보에 birthday 필드를 보완했습니다.</li>
    	<li> 기타 구성원이 그룹 @ 메시지를 회수한 후, @ 대상자의 해당 대화에 여전히 그룹 @ 알림이 포함되는 문제를 수정했습니다.</li>
    	<li> 일부 안드로이드 휴대폰으로 지속 연결 시, 초기 인터넷 연결 성공 후 인터넷이 끊겼다가 재연결되는 문제를 해결했습니다.</li>
    	<li> iOS용 SDK에서 그룹을 생성할 때 사용자가 사용자 정의 필드를 설정할 수 없는 문제가 수정되었습니다.</li>
    	<li> 특수 계정 사용자가 findMessage 로컬 메시지를 조회하지 못하는 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-04-19 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.2.212 라이트 버전 배포</td>
    <td><ul style="margin:0">
        <li> iOS: IDFA 관련 키워드를 사용한 SDK 최적화가 App Store에서 거부되는 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-04-06 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.60 스탠다드 버전 배포</td>
    <td><ul style="margin:0">
        <li> iOS: IDFA 관련 키워드를 사용한 SDK 최적화가 App Store에서 거부되는 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-04-06 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 03월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
	<td> SDK 5.2.210 라이트 버전 배포</td>
	<td><ul style="margin:0">
	    <li> 메시지 결합 전달 기능을 지원합니다.</li>
	    <li> 지속 연결 로직을 최적화하여, 중국 본토 외 지역 인터넷 연결 품질을 개선했습니다.</li>
	    <li> 로그인 오류 코드를 세분화하여 로그인 시에 네트워크의 정상 동작 여부를 구분했습니다.</li>
	    <li> cos 업로드 로직을 최적화하여 리치 미디어 메시지 발송 경험이 향상되었습니다.</li>
	    <li> 메시지 기록 가져오기 고급 인터페이스를 추가했습니다.</li>
	    <li> 대화 인터페이스의 일괄 가져오기 기능을 추가했습니다.</li>
		<li> 친구 관계 인터페이스의 일괄 확인 기능을 추가했습니다.</li>
		<li> 업데이트 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.</li>
	</ul></td>
	<td> 2021-03-12 </td>
	<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
	<td> SDK 5.1.56 스탠다드 버전 배포</td>
	<td><ul style="margin:0">
	    <li> Windows SDK에서 새 메시지 콜백이 트리거될 때, 클라이언트 스레드가 SDK 로직 스레드를 차단하는 문제를 수정했습니다.</li>
	    <li> Android SDK에서 신규 로그 컴포넌트 교체 시, 안정성이 향상되었습니다.</li>
	    <li> 지속 연결 로직을 최적화하여, 중국 본토 외 지역 인터넷 연결 품질을 개선했습니다.</li>
	    <li> 데이터 리포트를 최적화하고 네트워크 타임 아웃 관련 오류 코드를 세분화했습니다.</li>
	    <li> iOS SDK 로그 추출 시, 간헐적으로 실패가 발생하는 문제를 수정했습니다.</li>
	    <li> 일부 안정성 문제를 수정했습니다.</li>
	</ul></td>
	<td> 2021-03-03 </td>
	<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 01월
<table>
<tr>
    <th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr>
<tr>
    <td> SDK 5.1.138 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 로그를 최적화했습니다.</li>
	    <li> 지속 연결 인터넷 연결 정책을 개선하고, 중국 본토 외 지역 인터넷 연결 품질을 최적화했습니다.</li>
	    <li> 1초 내에 여러 개의 C2C 메시지를 받으면 간헐적으로 발생하는 대화의 마지막 메시지가 부정확한 문제를 수정했습니다.</li>
	    <li> 대화 목록 조회 시, 간헐적으로 발생하는 콜백 없음 문제를 수정했습니다.</li>
	    <li> C2C 메시지 발송 시, 간헐적으로 발생하는 메시지 시리얼 넘버가 부정확한 문제를 수정했습니다.</li>
	    <li> Android 플랫폼에서 24MB를 초과하는 비디오 전송 시, 간헐적으로 발생하는 업로딩 진행률에 마이너스 값이 표시되는 문제를 수정했습니다.</li>
	    <li> Android 플랫폼에서 메시지 발송 시, 간헐적으로 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-02-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.50 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            	<li> V2 메시지 객체에 random 필드를 추가했습니다.</li>
	    	<li> 대화에서 lastMsg 메시지 회수를 지원합니다.</li>
		<li> getMessage로 가져온 마지막 메시지 상태에 간헐적으로 오류가 발생하는 문제를 수정했습니다.</li>
		<li> 메시지 수신 후, 사용자 프로필 정보를 자주 풀링하는 경우 메시지 딜레이가 발생하는 문제를 수정했습니다.</li>
		<li> 계정 삭제 시, 그룹 구성원 리스트 풀링에 실패가 발생하는 문제를 수정했습니다.</li>
		<li> insertLocalMessage 이후, findMessage 호출 시, 메시지를 찾을 수 없는 문제를 수정했습니다.</li>
		<li> 대화 삭제 시, 대화 업데이트 콜백이 실행되는 문제를 수정했습니다.</li>
		<li> Android에서 그룹 메시지 기록에 닉네임이 제때에 업데이트 되지 않는 문제를 수정했습니다.</li>
		<li> iOS 데이터베이스 안정성을 개선했습니다.</li>
		<li> 업데이트 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.</li>
        </ul>
    </td>
    <td> 2021-02-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.137 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 사용자가 여러 개의 iOS 또는 Android 디바이스에서 동일 계정으로 반복 로그인할 때, 간헐적으로 발생하는 로그인 인터페이스 콜백 없음 문제를 수정했습니다.</li>
	    <li> 저사양 Android 디바이스로 로그 경로를 가져올 때 간헐적으로 발생하는 crash를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.136 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 API에 로그 콜백 인터페이스를 추가했습니다.</li>
	    <li> 그룹 @ 메시지에 @ 사용자 UserID가 비어있는 문제를 수정했습니다.</li>
	    <li> 간헐적으로 발생하는 라이브 방송 그룹 메시지 수신 불가 문제를 수정했습니다.</li>
	    <li> 네트워크를 빈번하게 연결하면 간혹 로그인 상태 오류가 발생하는 문제를 수정했습니다.</li>
	    <li> 강제 로그아웃 후 다시 로그인 시 간혹 실패가 발생하는 문제를 수정했습니다.</li>
	    <li> DNS 도메인 리졸브 중 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-27 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.132 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 네트워크 모듈에서 과부하 보호를 지원합니다.</li>
	    <li> 표준 버전을 라이트 버전으로 업데이트할 때 간혹 일부 대화가 유실되는 문제를 수정했습니다.</li>
	    <li> 로그인 정보 기간 만료 시, onUserSigExpired 콜백을 수신하지 못하는 문제를 수정했습니다.</li>
	    <li> 그룹 구성원이 그룹에서 강제 퇴장된 후, 다시 그룹에 참여하려고 하면 다시 onMemberKicked 콜백을 받는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-22 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.131 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 단일 메시지 전달 인터페이스를 추가했습니다.</li>
	    <li> 라이브 방송 그룹이 메시지를 수신할 때 메시지 발신자의 닉네임과 프로필을 다시 조회하지 않도록 라이브 방송 그룹 메시지 수신 로직을 최적화했습니다.</li>
	    <li> 대화의 마지막 메시지 삭제 시, 대화 업데이트 알림이 표시되지 않는 문제를 수정했습니다.</li>
	    <li> 로그인 완료 후, C2C 메시지 동기화 시, 간혹 C2C 대화의 읽지 않음 수가 0으로 표시되는 문제를 수정했습니다.</li>
	    <li> 오프라인 상태에서 다시 온라인 상태가 된 후, 대화 목록을 동기화하면 대화의 마지막 메시지를 업데이트하지 않는 문제를 수정했습니다.</li>
	    <li> Android 플랫폼에서 사용자 정의 메시지의 description 필드를 설정할 때, 설정한 개인 프로필 정보 level 및 role 필드가 적용되지 않는 문제를 수정했습니다.</li>
	    <li> Android 플랫폼에서 초기화 해제 시 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-19 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.21 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 글로벌화 지원을 개선하였습니다. 영어 버전에서 일부 문자열이 여전히 중국어로 표시되는 문제를 수정했습니다.</li>
						<li> Android 플랫폼에서 extension 확장 필드의 사용자 정의 메시지를 포함하면 발송 실패하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-15 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.129 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 대화 목록을 가져올 때, 업데이트된 대화가 없어도 대화 업데이트 콜백이 트리거되는 문제를 수정했습니다.</li>
            <li> 대화의 모든 메시지를 삭제할 때, 해당 대화의 마지막 메시지를 삭제하지 않는 문제를 수정했습니다.</li>
            <li> iOS 플랫폼에서 getSignallingInfo 메소드로 비신호 메시지 전달 시, 반환값이 nil이 아닌 문제를 수정했습니다.</li>
            <li> Android 플랫폼에서 JNI 참조 테이블 제한 초과로 인해 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-13 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.125 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 API 메시지 객체에 random 필드를 추가했습니다.</li>
            <li> V2 API 사용자 정의 메시지에 설명 정보 description 및 확장 정보 extension 필드를 추가했습니다.</li>
            <li> V2 API 사용자 프로필 정보 객체에 사용자 역할 role 및 사용자 레벨 level 필드를 추가했습니다.</li>
            <li> 4.8.1 미만 버전을 라이트 버전으로 업데이트할 때 발생하는 데이터베이스 호환성 문제를 수정했습니다.</li>
            <li> 메시지 발송 시, 간혹 사용자가 자신이 보낸 메시지의 콜백을 받는 문제를 수정했습니다.</li>
            <li> 사용자가 아무 그룹에도 참여하지 않은 상태에서, 참여 그룹 리스트 가져오기하면 콜백이 없는 문제를 수정했습니다.</li>
            <li> 그룹 메시지 수신 옵션 설정 시, 대화 업데이트 콜백이 없는 문제를 수정했습니다.</li>
            <li> 대화 동기화 로직에 간혹 종료 콜백이 없는 문제를 수정했습니다.</li>
            <li> 대화 동기화 로직에 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-08 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.20 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 사용자 정의 메시지에 desc 및 ext 필드를 추가했습니다.</li>
            <li> V2 사용자 정보 인터페이스에 role 및 level 필드를 추가했습니다.</li>
            <li> V2 인터페이스에서 로그인 성공 여부와 상관없이, 모두 로컬 대화 목록 데이터 및 로컬 메시지 기록 데이터를 가져올 수 있는 문제를 수정했습니다.</li>
            <li> V2 getHistoryMessageList 인터페이스를 추가하여 클라우드 또는 로컬 메시지 가져오기 및 특정 시간 전후에 전송된 메시지 가져오기를 지원합니다.</li>
            <li> C2C 메시지의 프로필 사진 가져오기 문제를 최적화했습니다.</li>
            <li> 리치 미디어 메시지 파일 업로드의 안전성 문제 및 기간 연장 문제를 최적화했습니다.</li>
            <li> 발송한 리치 미디어 메시지의 로컬 경로가 비어있는 문제를 수정했습니다.</li>
            <li> 그룹에 로컬 메시지를 삽입한 후 로그아웃하고 다시 로그인하면 해당 대화의 lastMessage가 이전 메시지로 표시되는 문제를 수정했습니다.</li>
            <li> 그룹에 로컬 메시지를 삽입한 후 로그아웃하고 다시 로그인하면 해당 대화의 lastMessage가 이전 메시지로 표시되는 문제를 수정했습니다.</li>
            <li> 업데이트 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.</li>
        </ul>
    </td>
    <td> 2021-01-08 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2020년 12월

<table>
<tr>
    <th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr>
<tr>
    <td> SDK 5.1.123 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> Android 버전에서 RESTAPI가 전달한 그룹 사용자 정의 시스템 메시지 수신 불가 문제를 수정했습니다.</li>
            <li> 메시지 random 필드 생성 방법을 최적화했습니다.</li>
            <li> 문제 분석을 위해 로그 출력을 최적화했습니다.</li>
            <li> 네트워크 모듈에 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-31 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.122 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 대화 임시 보관 설정 시, 콜백이 없는 문제를 수정했습니다.</li>
            <li> findMessage 메시지 조회 시, 메시지 발신자 정보가 완료되지 않는 문제를 수정했습니다.</li>
            <li> 로컬 메시지 삽입 후, findMessage로 메시지를 조회하면 실패가 발생하는 문제를 수정했습니다.</li>
            <li> 그룹 메시지 수신 옵션 설정 시, 대화 객체를 업데이트하지 않는 문제를 수정했습니다.</li>
            <li> 개인 또는 그룹 닉네임, 프로필 사진 변경 시, 대화 변경 알림이 표시되지 않는 문제를 수정했습니다.</li>
            <li> 로컬 메시지 삽입 시, 해당 대화의 마지막 메시지를 업데이트하지 않는 문제를 수정했습니다.</li>
            <li> 개인 프로필 정보 업데이트 주기의 클라우드 제어를 활성화했습니다.</li>
            <li> iOS 플랫폼에서 잘못된 사전 및 배열 작업으로 간혹 Crash가 발생하는 문제를 수정했습니다.</li>
            <li> Android 플랫폼에서 메시지를 삭제하면 간혹 Crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-25 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.121 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 라이브 방송 그룹에서 본인의 그룹 구성원 프로필 정보를 풀링할 필요가 없도록, 그룹 정보 풀링 로직을 최적화했습니다.</li>
            <li> 로그 출력을 개선하고 디바이스 유형 필드를 추가했습니다.</li>
            <li> C2C 대화에서 메시지 회수 알림 수신 시, 해당 대화의 마지막 메시지 상태를 업데이트하지 않는 문제를 해결했습니다.</li>
            <li> 라이브 방송 그룹의 long polling 메시지 딜레이가 너무 긴 문제를 수정했습니다.</li>
            <li> 동일 계정으로 중복 로그인한 후 다시 같은 라이브 방송 그룹에 참여하면 메시지 long polling 모듈이 메시지 업데이트 없이 key를 풀링하는 문제를 수정했습니다.</li>
            <li> iOS 플랫폼에 메시지 사용자 정의 필드가 json 배열로 전달될 때, 수신측의 신호 모듈 파싱 중 Crash가 발생하는 문제를 수정했습니다.</li>
            <li> Android 플랫폼에 대화 임시 보관을 설정하면 간혹 Crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-18 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.118 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 메시지 중복 제거 로직을 최적화하여 같은 메시지에 여러 차례 콜백이 발생하는 문제를 수정했습니다.</li>
            <li> 로컬에 C2C 메시지 삽입 인터페이스를 추가했습니다.</li>
            <li> 그룹의 읽지 않은 메시지를 삭제 및 회수해도 읽지 않음 숫자가 줄어들지 않는 문제를 수정했습니다.</li>
            <li> 발송 실패 메시지를 삭제할 수 없는 문제를 수정했습니다.</li>
            <li> 그룹 대화 삭제 시, 그룹에서 탈퇴했거나 해당 그룹이 해산한 경우, 콜백 삭제 실패가 발생하는 문제를 수정했습니다.</li>
            <li> 그룹 메시지 읽음 리포트 시, 그룹에서 탈퇴했거나 해당 그룹이 해산한 경우, 콜백 설정 실패가 발생하는 문제를 수정했습니다.</li>
            <li> 개인 정보 서명 설정 실패 문제를 수정했습니다.</li>
            <li> 친구 블랙리스트 추가에 간혹 크래쉬가 발생하는 문제를 수정했습니다.</li>
            <li> 메시지 발송 시, 반환 메시지 ID를 동기화하지 않는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-11 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.115 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 신호 타임아웃 시간 및 서버 시간 동기화를 최적화했습니다.</li>
            <li> 열악한 네트워크 환경에서 간혹 연결 실패가 발생하는 문제를 수정했습니다.</li>
            <li> iOS API 헤더 파일을 완성했습니다.</li>
            <li> Android JSON을 Gson으로 교체할 때 발생하는 크래쉬 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-04 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.10 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 API에 그룹 사용자 정의 필드 및 메시지 멀티 Element를 추가했습니다.</li>
            <li> V2 API에 로컬에 C2C 메시지를 삽입하는 인터페이스를 추가했습니다.</li>
            <li> 일반 그룹 및 라이브 방송 그룹의 메시지 유실 문제를 최적화했습니다.</li>
            <li> 발송 실패 메시지를 삭제할 수 없는 문제를 수정했습니다.</li>
            <li> C2C 대화에서 발송하는 첫 번째 메시지가 온라인 메시지인 상황에서 읽음 확인을 받지 못하는 문제를 수정했습니다.</li>
            <li> 회수한 메시지가 메시지 기록 풀링 인터페이스를 통해 반환된 후, 메시지 상태가 비정확한 문제를 수정했습니다.</li>
            <li> IOS 플랫폼에서 친구 그룹 인터페이스를 호출하여 빈 그룹명을 입력하면 모든 그룹 정보를 반환하지 않는 문제를 수정했습니다.</li>
            <li> 안정성 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-04 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.111 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 로그 출력을 개선했습니다.</li>
            <li> 일부 안정성 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-01 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>


## 2020년 11월

<table>
<tr>
    <th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr>
<tr>
    <td> SDK 5.1.110 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 API의 모든 인터페이스를 보완했습니다.</li>
            <li> 대화 기능을 보완했습니다.</li>
            <li> 관계망 기능을 보완했습니다</li>
            <li> 그룹@ 기능을 추가했습니다.</li>
            <li> iOS iPhone 및 iPad의 동시 온라인 접속을 지원합니다.</li>
            <li> 메시지 발송 시, 멀티 Element를 지원합니다.</li>
            <li> 그룹 프로필 정보에 사용자 정의 필드를 추가했습니다.</li>
            <li> 일부 안정성 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-11-26 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.2 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> iOS iPhone 및 iPad의 동시 온라인 접속을 지원합니다.</li>
            <li> Mac arm64 아키텍처를 지원합니다.</li>
            <li> android 버전의 안정성 문제를 수정했습니다.</li>
            <li> 표준 TRTC 종속 패키지로 교체했습니다.</li>
        </ul>
    </td>
    <td> 2020-11-12 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.1 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> AVChatRoom 라이브 방송 그룹 온라인 인원 수 가져오기 인터페이스를 추가했습니다.</li>
            <li> 메시지의 유일한 ID로 메시지를 조회하는 인터페이스를 추가했습니다.</li>
            <li> 서버 보정 타임 스탬프 가져오기 인터페이스를 추가했습니다.</li>
            <li> 로그인 속도를 최적화했습니다.</li>
            <li> 그룹 구성원@ 기능에 <code>@전체</code> 기능을 추가했습니다.</li>
            <li> TUIKit 컴포넌트의 글로벌 지원을 강화했습니다.</li>
            <li> 그룹 라이브 방송에 작은 라이브 방송 창을 추가했습니다.</li>
        </ul>
        업데이트에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.
    </td>
    <td> 2020-11-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>


## 2020년 10월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 5.0.108 라이트 버전 배포</td>
<td>
    <li> iOS 버전 안정성 문제를 수정했습니다.</li>
    <li> Android 버전에서 간혹 메시지 콜백을 하지 않는 문제를 수정했습니다.</li>
</td>
<td> 2020-10-23 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr><tr>
<td> SDK 5.0.10 스탠다드 버전 배포</td>
<td><ul style="margin:0">
    <li> 신호 인터페이스를 최적화하여 온라인 메시지 onlineUserOnly 및 오프라인 푸시 정보 offlinePushInfo 매개변수 설정을 지원합니다.</li>
    <li> 단일 대화 가져오기 인터페이스의 비동기화 콜백을 최적화했습니다.</li>
    <li> 대화 목록에 필터링 표시를 용이하게 하기 위해, 그룹 유형 가져오기 인터페이스를 추가했습니다.</li>
    <li> 그룹 라이브 방송 기능을 추가하여 마이크 연결, 선물하기, 뷰티 필터, 음성 변조 등 기능을 고루 갖추었습니다.</li>
    <li> 라이브 룸을 추가하였으며, 마이크 연결, PK, 좋아요, 선물하기, 뷰티 필터, 댓글 자막, 친구 팔로우 등 기능을 지원합니다.</li>
    <li> 음성 영상 신호 식별 문제를 최적화했습니다.</li>
</ul></td>
<td> 2020-10-15 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>


## 2020년 09월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td> SDK 5.0.106 버전 배포(Android & iOS 라이트 버전)</td>
<td> 기존 안정성 문제를 수정했습니다.</td>
<td> 2020-09-21 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr><tr>
<td> SDK 5.0.6 스탠다드 버전 배포</td>
<td><ul style="margin:0">
    <li>그룹@ 기능을 추가했습니다.</li>
    <li>iOS 및 Android에 deleteMessages 인터페이스를 추가하였습니다. 로컬 및 로밍 메시지를 동시에 삭제할 수 있습니다.</li>
    <li>deleteConversation 인터페이스에서 대화과 로컬 및 로밍 메시지를 동시에 삭제할 수 있습니다.</li>
    <li>API2.0 인터페이스에 사용자 정보, 친구 프로필 정보, 그룹 구성원 프로필 정보의 사용자 정의 필드 설정 및 가져오기 인터페이스를 추가했습니다.</li></ul>
업데이트에 관한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.</td>
<td> 2020-09-18 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr><tr>
<td> SDK 5.0.102 버전 배포(Android & iOS 라이트 버전)</td>
<td><ul style="margin:0">
    <li> Android & iOS 라이트 버전 SDK가 배포되었습니다.</li>
    <li>라이트 버전 SDK는 기존 스탠다드 버전에서 친구 및 대화 기능을 제거하고, 일부 서비스 로직을 최적화하여 실행 효율을 높이고, 설치 패키지 크기를 줄였습니다.</li>
</ul></td>
<td> 2020-09-04 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</td>
</tr>
</table>

## 2020년 07월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.9.1 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>중국 외 지역 로그인 문제를 최적화했습니다.</li>
    <li>일부 중국 외 지역의 파일 업로드 실패 문제를 수정했습니다.</li>
    <li>@부호를 포함한 계정의 파일 업로드 실패 문제를 수정했습니다.</li>
    <li>C2C 읽지 않음 수에 간혹 오류가 발생하는 문제를 수정했습니다.</li>
    <li>대화 showName에 간혹 오류가 표시되는 문제를 수정했습니다.</li>
    <li>파일 유형 메시지에 다운로드 url 가져오기 인터페이스를 추가했습니다.</li>
    <li>iOS의 인터넷 연결이 끊겼을 때 C2C 메시지 가져오기 콜백이 없는 문제를 수정했습니다.</li>
    <li>Android의 신호 파싱 인터페이스에 간혹 크래쉬가 발생하는 문제를 수정했습니다.</li>
    <li>Android 메시지에 오프라인 푸시 정보를 가져올 때, 간혹 크래쉬가 발생하는 문제를 수정했습니다.</li>
    <li>Android의 API2.0 getFriendApplicationList 인터페이스에 데이터가 없으면 콜백하지 않는 문제 및 getGroupMembersInfo 인터페이스 그룹 구성원이 아닌 사람을 입력하면 콜백하지 않는 문제를 수정했습니다.</li>
    <li>Windows에서 참여한 그룹 목록을 가져오기할 때, 그룹의 상세 정보를 추가했습니다.</li>
    <li>Windows 저용량 파일은 발송이 되지 않는 문제를 수정했습니다.</li>
    <li>Windows 로그가 리포트하는 6002 오류를 수정했습니다.</li>
    <li>iOS Demo & Android Demo에 멀티미디어 오프라인 통화 푸시 기능을 추가하였습니다. 수신 화면으로 리디렉션할 수 있습니다.</li>
    <li>iOS 사용자 정의 메시지 삭제, 회수 오류를 최적화했습니다.</li>
    <li>iOS 멀티미디어 코드 swift -> oc, 서드 파티 종속 라이브러리를 대폭 줄였습니다.</li>
    <li>iOS LiteAV_TRTC, LiteAV_Professional 두 종류의 멀티미디어 종속 라이브러리 TUIKit pod 통합을 지원합니다.</li>
    <li>Android의 Demo 오프라인 푸시를 최적화하고 각 벤더의 푸시 SDK 버전을 업데이트했습니다.</li>
</ul></td>
<td>2020-07-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr> </table>


## 2020년 06월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.8.50 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>누군가 라이브 방송 그룹(AVChatRoom)에 입장한 후, onMemberEnter 콜백이 트리거되지 않는 API 2.0 인터페이스 문제를 수정했습니다.</li> 
    <li>API 2.0 인터페이스의 onGroupInfoChanged 및 onMemberInfoChanged 콜백에 groupID 매개변수를 추가했습니다.</li>
    <li>C2C 메시지가 발송된 후 대화 업데이트 콜백이 없는 문제를 수정했습니다.</li>
    <li>계정을 전환하여 동일 라이브 방송 그룹(AVChatRoom)에 참여한 후, 메시지를 수신하지 못하는 문제를 수정했습니다.</li>
    <li>로그인 후, 간혹 읽지 않음 메시지 동기화 콜백 순서에 오류가 발생하는 문제를 수정했습니다.</li>
    <li>신호 인터페이스를 추가했습니다.</li>
    <li>라이브 방송 그룹(AVChatRoom)에 그룹 사용자 정의 속성 인터페이스를 추가했습니다.</li>
    <li>기존 크래쉬 문제를 수정했습니다.</li>
    <li>Android Q 버전 호환을 위해, 로그 기본 스토리지 위치를 /sdcard/Android/data/패키지 이름/files/log/tencent/imsdk으로 수정했습니다.</li>
    <li>Windows 플랫폼에서 그룹 생성 시, 발생하는 그룹 구성원 역할 문제를 수정했습니다.</li>
    <li>TUIKit API 2.0 인터페이스를 교체했습니다.</li>
    <li>TRTC를 통합하여 멀티미디어 통화 기능을 구현했습니다.</li>
    <li>iOS TUIKit에 딥 컬러 모드를 추가했습니다.</li>
    <li>AndroidX를 지원합니다.</li>
</ul></td>
<td>2020-06-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr> </table>

## 2020년 05월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.8 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>iOS & Android에 신규 API 2.0 인터페이스를 배포하였습니다.</li>
    <li>iOS 및 Android에서 IPv6를 지원합니다.</li>
    <li>라이브 방송 그룹(AVChatRoom)그룹 구성원 리스트 동적 업데이트를 지원합니다.</li>
    <li>xlog 로그 크래쉬 문제를 수정했습니다.</li>
    <li>iOS 대용량 파일 발송 실패 문제를 수정했습니다.</li>
    <li>iOS 메시지의 발신자 친구 설명 풀링 오류 문제를 수정했습니다.</li>
    <li>IM SDK는 AndroidX를 지원합니다.</li>
    <li>Android 디바이스에서 네트워크 권한 문제로 발생하는 크래쉬를 수정했습니다.</li>
</ul></td>
<td>2020-05-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr> </table>


## 2020년 03월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 2.6 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0">
    <li>Web의 비디오 메시지 생성 및 발송을 지원하며 최대 100MB까지 가능합니다.</li>
    <li>Message에 <code>nick</code> 및 <code>avatar</code> 속성을 추가하여 AVChatRoom에서 메시지 발신자 닉네임 및 프로필 사진 주소(사전에 updateMyProfile 호출하여 설정)를 표시합니다.</li>
    <li>Web 멀티 인스턴스 로그인 시, C2C 메시지 회수 알림은 각 인스턴스에서 동기화될 수 있습니다.</li>
    <li>updateGroupProfile을 호출하여 그룹 사용자 정의 필드를 수정하면, 그룹 구성원은 그룹 알림 메시지를 받을 수 있고 관련 내용 Message.payload.newGroupProfile.groupCustomField를 가져올 수 있습니다.</li>
    <li>TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED 인터페이스를 폐기하고 MESSAGE_RECEIVED로 대체하였습니다.</li>
    <li>getGroupList 인터페이스 호출 시, 간혹 오류 메시지가 발생하는 문제를 수정했습니다.</li></ul></td>
<td>2020-03-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr><tr>
<td>SDK 4.7 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>로컬 로그 크기를 최적화했습니다.</li>
    <li>로그인 소요 시간을 최적화했습니다.</li>
    <li>멀티 단말에서 읽지 않음 수 동기화 문제를 수정했습니다.</li>
    <li>단일 친구 가져오기 인터페이스 getFriendList를 추가했습니다.</li>
    <li>iOS & Android 두 플랫폼의 오프라인 푸시 알림창에 표시될 메시지 타이틀 및 내용을 각각 설정할 수 있습니다.</li>
</ul></td>
<td>2020-03-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr> </table>

## 2020년 02월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.6 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>파일 업로드 제한을 100MB로 확대했습니다.</li>
    <li>COS 업로드를 최적화했습니다.</li>
    <li>그룹 미결 처리 로직을 최적화했습니다.</li></ul></td>
<td>2020-02-28</td>
<td>-</td>
</tr><tr>
<td>SDK 2.5 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li>네트워크 상태 변경 이벤트 TIM.EVENT.NET_STATE_CHANGE를 추가하여 수신측에서 해당 이벤트에 따라 관련 알림과 가이드를 제공할 수 있습니다.</li>
    <li>WeChat 미니프로그램 플러그인 환경에서 실행할 수 있습니다.</li>
    <li>오류 코드를 줄이고 최적화했습니다.</li>
    <li> 콘솔에서 AVChatRoom을 생성하고 소유자를 지정하면, 소유자가 해당 그룹에 참여한 후 그룹의 다른 구성원이 발송한 정보를 소유자측에 중복해서 표시하는 문제를 수정했습니다.</li>
    <li>콘솔 또는 REST API로 빈번하게 그룹을 폐기하면 SDK에서 TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED 이벤트를 배포하지 않는 문제를 수정했습니다.</li>
    <li>getMessageList에서 간혹 그룹 메시지 리스트 풀링하지 못하는 문제를 수정했습니다.</li></ul></td>
<td>2020-02-28</td>
<td>-</td>
</tr> </table>

## 2020년 01월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 2.4 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li>메시지 회수 인터페이스 revokeMessage를 추가했습니다.</li>
    <li>Message에 isRevoked 속성을 추가했으며 값이 true일 경우 회수된 메시지를 의미합니다.</li>
    <li>메시지가 회수될 때 발생하는 이벤트 알림 TIM.EVENT.MESSAGE_REVOKED를 추가했습니다.</li>
    <li>강제 로그아웃된 이벤트 알림 TIM.EVENT.KICKED_OUT에 ‘다중 디바이스 로그인으로 인한 강제 로그아웃’ 및 ‘UserSig 만료로 인한 강제 로그아웃’ 강제 로그아웃 유형이 추가되었습니다.</li>
    <li>createFileMessage 업로드 파일 크기가 20M에서 100MB로 확대되었습니다.</li>
    <li>그룹 알림 메시지의 msgMemberInfo 및 shutupTime이 폐기될 예정입니다. 대신 memberList 및 muteTime을 사용하십시오.</li>
    <li> 콘솔에 IM 스마트 고객 지원 엔트리를 추가했습니다.</li>
    <li> off 인터페이스를 호출하여 리스닝 이벤트를 취소할 수 없는 문제를 수정했습니다.</li>
    <li> Message의 isRead 속성값 및 유형이 정확하지 않은 문제를 수정했습니다.</li>
    <li> 비디오 메시지, 비디오 파일 발송 시, 최대 크기 제한을 초과하면 표시되는 오류 코드 및 오류 정보가 올바르지 않은 문제를 수정했습니다.</li>
    <li> 사용자 정의 필드를 업데이트한 후 간혹 필드 내용이 정확하지 않은 문제를 수정했습니다.</li>
    <li> 로그인 후 AVChatRoom 유형의 그룹에 참여하면 간혹 발생하는 JOIN_STATUS_ALREADY_IN_GROUP 문제를 수정했습니다.</li>
    <li> core-js로 인한 잠재적 성능 문제를 수정했습니다.</li></ul></td>
<td>2020-01-03</td>
<td>-</td>
</tr> </table>

## 2019년 12월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.6 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>네트워크 연결 품질을 최적화하여 네트워크 품질 변화를 더욱 빠르게 감지합니다.</li>
    <li>AVChatRoom 메시지 처리를 최적화했습니다.</li>
    <li>메시지에 getSenderNickname 동기화 닉네임 반환 인터페이스를 추가했습니다.</li>
    <li>TUIKit/Demo 대화 목록 프로필에 둥근 모서리 설정을 지원합니다.</li></ul></td>
<td>2019-12-23</td>
<td>-</td>
</tr><tr>
<td>SDK 2.3 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li>createImageMessage 및 createFileMessage 인터페이스에 File 객체 입력을 추가했습니다.</li>
    <li>이모티콘 메시지 생성 인터페이스 createFaceMessage를 추가했습니다.</li>
    <li>TIM.TYPES.GRP_AVCHATROOM 유형의 그룹 메시지 알림 효율을 최적화하여 사용자 경험이 대폭 향상되었습니다.</li>
    <li>메시지 발송 실패 시, SDK에서 반환하는 실제 오류 코드 및 오류 정보를 조정했습니다.</li>
    <li>logout 호출 시, 현재 인스턴스 메시지 채널에서만 로그아웃되는 문제를 조정했습니다.</li>
    <li>수신측에서 입력하는 콜백 함수에 안전성 캡슐화를 진행하여 콜백 함수 로직에 오류가 있을 경우 신속하게 문제를 해결할 수 있습니다.</li>
    <li> IM 서버 오류 코드 발생 시, SDK에서 중국어로 오류 정보를 출력합니다.</li>
    <li>WeChat 미니프로그램 환경에서 긴 시간 동안 백그라운드로 전환했다가 다시 포그라운드로 전환하면 간혹 발생하는 메시지 유실 문제를 수정했습니다.</li>
    <li>메시지를 한 번 발송하면 여러 차례 TIM.EVENT.CONVERSATION_LIST_UPDATED가 트리거되는 문제를 수정했습니다.</li>
    <li>registerPlugin을 호출하지 않거나 인터페이스 매개변수 전달이 올바르지 않은 경우 또는 이미지 등 파일 업로드 시, SDK에서 오류 메시지가 발생하는 문제를 수정했습니다.</li>
    <li>TIM.TYPES.GRP_AVCHATROOM 유형의 그룹을 해산하면 long polling이 정지되지 않는 문제를 수정했습니다.</li>
    <li>‘멀티 인스턴스’ 또는 ‘멀티 단말’ 로그인 활성화 시, 하나의 Web 인스턴스에서 로그아웃하면 다른 인스턴스 또는 다른 단말에서 메시지를 수신하지 못하는 문제를 수정했습니다.</li>
    <li>풀링한 대화 목록 구조 문제로 SDK에서 간혹 오류 메시지가 발생하는 수정했습니다.</li></ul></td>
<td>2019-12-13</td>
<td>-</td>
</tr> </table>

## 2019년 11월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 2.2 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li> 미니프로그램은 비디오 메시지 생성 및 발송을 위해 createVideoMessage를 지원합니다. 비디오 메시지는 플랫폼 간에 동기화될 수 있습니다(최신 버전 TUIKit 및 SDK로 업데이트 필요).</li>
    <li>그룹 구성원 프로필 정보 조회 인터페이스 getGroupMemberProfile을 추가했습니다.</li>
    <li>Native IM v3.x에서 발송한 음성, 파일 메시지를 호환합니다.</li>
    <li>위치 메시지 GeoPayload 수신 지원 기능을 추가했습니다.</li>
    <li>로그아웃 후에도 TIM.TYPES.GRP_AVCHATROOM 유형 그룹의 long polling이 계속 실행되는 문제를 수정했습니다.</li>
    <li>TIM.TYPES.GRP_AVCHATROOM 유형의 그룹 메시지 인스턴스에 그룹 명함 값이 없는 문제를 수정했습니다.</li>
    <li>IE 10 브라우저에서 오류 메시지가 발생하는 문제를 수정했습니다.</li>
    <li>익명으로 그룹에 참여할 수 없는 문제를 수정했습니다.</li></ul></td>
<td>2019-11-21</td>
<td>-</td>
</tr><tr>
<td>SDK 4.6 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>메시지 회수 로밍을 지원합니다.</li>
    <li>iOS/Mac 단말에 OPPOChannelID 설정을 추가하여, Android 8.0 이후 버전을 실행하는 OPPO 휴대폰이 iOS 푸시 메시지를 수신하지 못하는 문제를 해결했습니다.</li>
    <li>iOS/Mac 단말의 getGrouplist 반환 객체 주석을 최적화했습니다.</li>
    <li>OPPO 휴대폰(시스템 8.0 이후 버전)의 오프라인 푸시를 위한 channleID의 콘솔 설정을 지원합니다.</li>
    <li>TUIKit/Demo 영상 통화 기능을 추가했습니다.</li>
    <li>TUIKit/Demo에 그룹 프로필 사진 3x3 그리드 표시를 추가하고, 대화 목록, 주소록 및 채팅 UI를 최적화했습니다.</li></ul></td>
<td>2019-11-13</td>
<td>-</td>
</tr><tr>
<td>메시지 기록 저장 '정찰가' 도입</td>
<td>메시지 기록 저장을 '정찰가'로 변경하여 더욱 간편하고 경제적으로 사용할 수 있습니다.</td>
<td>2019-11-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34350">요금 안내</a></td>
</tr> </table>

## 2019년 10월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>신규 콘솔 출시</td>
<td>IM 콘솔의 신규 버전이 정식 출시되었습니다.</td>
<td>2019-10-22</td>
<td><ul style="margin:0;">
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">애플리케이션 생성 및 업그레이드</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34540">기본 설정</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34419">기능 설정</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34578">그룹 관리</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34520">콜백 설정</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34579">통계 분석</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34580">개발 보조 툴</a></li></ul></td>
</tr><tr>
<td>SDK 4.5 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>파일 유형의 메시지 발송 시 생성되는 URL에 파일 형식 확장자를 추가했습니다.</li>
    <li>그룹 사용자 정의 필드 수정 후, 알림 콜백을 추가했습니다.</li>
    <li>오프라인으로 initStorage 메소드를 호출하면 로컬 사용자 및 그룹 정보를 가져올 수 있습니다.</li>
    <li>Android 단말의 getElementCount 인터페이스의 반환 유형을 최적화했습니다.</li>
    <li>Windows 크로스 플랫폼 라이브러리에 각 플랫폼의 네트워크 재연결 속도를 최적화했습니다.</li>
    <li>Android 환경에서도 JVM을 쉽게 전달할 수 있도록 Windows 크로스 플랫폼 라이브러리에 JVM 구성을 추가했습니다.</li></ul></td>
<td>2019-10-16</td>
<td>-</td>
</tr><tr>
<td>SDK 2.1 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li>오디오 메시지 및 비디오 메시지 수신 기능을 추가했습니다.</li>
    <li>getMessageList 인터페이스 단일 호출로 최대 15건의 메시지 풀링을 지원합니다.</li>
    <li>TIM.TYPES.MSG_SOUND를 폐기하고, TIM.TYPES.MSG_AUDIO로 대체하였습니다.</li>
    <li>getMessageList 인터페이스로 삭제한 그룹 채팅 대화 메시지를 풀링할 수 없는 문제를 수정했습니다.</li>
    <li>그룹 시스템 알림에 그룹 이름이 없는 문제를 수정했습니다.</li>
    <li>새로 생성된 대화의 메시지 수신 시, 프로필 정보가 없는 문제를 수정했습니다.</li></ul></td>
<td>2019-10-16</td>
<td>-</td>
</tr> </table>

## 2019년 09월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 2.0 버전 배포(미니프로그램 및 Web)</td>
<td>신규 IM 미니프로그램용 및 웹용 SDK의 각 모듈 안정성을 최적화하고, 액세스 경험을 개선했으며, 시각화된 Demo를 제공하여, 고객이 편리하게 체험해볼 수 있도록 하였습니다.</td>
<td>2019-09-19</td>
<td>-</td>
</tr><tr>
<td>SDK 4.5 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>Android 단말에 읽음 확인 기능을 추가했습니다.</li>
    <li>네트워크 연결 품질을 최적화했습니다.</li>
    <li>그룹/그룹 구성원 사용자 정의 필드의 풀링 로직을 최적화했습니다.</li></ul></td>
<td>2019-09-18</td>
<td>-</td>
</tr> </table>

## 2019년 08월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.5 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>채팅 메시지 음성 기능에 대한 MotionEvent.ACTION_CANCEL 이벤트 처리를 추가했습니다.</li>
    <li>대화 목록, 채팅 인터페이스, 상세 프로필 정보, 주소록 및 프로필 사진 표시 기능을 추가했습니다.</li>
    <li>개인 프로필 정보의 프로필 사진 수정 기능을 추가했습니다.</li>
    <li>오프라인 푸시 기능 Intent 리디렉션을 추가했습니다.</li>
    <li>1:1 채팅, 그룹 채팅 대화, 랜덤 프로필 사진을 추가했습니다.</li>
    <li>그룹 구성원에 대한 그룹 관리자 역할 부여 및 취소 메시지 알림을 추가했습니다.</li>
    <li>그룹 구성원 음소거 및 음소거 해제 메시지 알림을 추가했습니다.</li>
    <li>읽지 않음 메시지 수를 최적화했습니다.</li>
    <li>로그인 후 최근 대화 목록 로딩 속도를 최적화했습니다.</li>
    <li>로그 정리 기능을 추가했습니다.</li>
    <li>Android 단말에서 com.tencent.imsdk.TIMGroupReceiveMessageOpt 클래스가 통합적으로 사용됩니다.</li>
    <li>TUIKit/Demo에 탭 피드백을 추가하여, 사용자가 TUIKit에서 피드백을 설정 및 사용자 정의할 수 있습니다.</li>
    <li>TUIKit/Demo에 사용자 정의 메시지 발송을 추가했습니다.</li>
    <li>TUIKit/Demo에 C2C 읽음 확인을 추가했습니다.</li>
    <li>TUIKit/Demo에 음성 미재생 시, 빨간 점 표시 기능을 추가했습니다.</li>
    <li>TUIKit/Demo에 프로필 사진을 클릭하면 큰 이미지 보기 기능을 추가했습니다.</li>
    <li>TUIKit/Demo 그룹 채팅에서 작은 회색 막대를 조정하면 사용자 닉네임이 파란색으로 바뀌고, 닉네임을 클릭하면 사용자 정보 인터페이스로 리디렉션됩니다.</li>
    <li>상단 고정 채팅 로직을 최적화하여, 최근 시간 기준으로 정렬 및 표시됩니다.</li>
    <li>Demo의 그룹 닉네임 표시 로직을 최적화했습니다.</li>
    <li>채팅 인터페이스의 프로필 사진 표시 로직을 최적화했습니다.</li>
    <li>읽지 않음 메시지 수를 최적화했습니다.</li>
    <li>로그인 후 최근 대화 목록 로딩 속도를 최적화했습니다.</li>
    <li>중국 외 지역 사용자의 파일 메시지 발송 속도를 최적화했습니다.</li></ul></td>
<td>2019-08-30</td>
<td>-</td>
</tr><tr>
<td>이름을 ‘IM’으로 변경했습니다.</td>
<td>‘Cloud Communication’을 ‘IM’으로 변경했습니다.</td>
<td>2019-08-06</td>
<td>-</td>
</tr> </table>

## 2019년 07월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.4 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>일부 API 인터페이스를 정리 및 통합했습니다.</li>
    <li>친구 추가에 단방향/양방향 옵션를 추가했습니다.</li>
    <li>모든 로컬 스토리지를 비활성화하는 disableStorage 인터페이스를 추가했습니다.</li>
    <li>파일, 비디오, 음성 메시지에 다운로드 URL 가져오기 인터페이스를 추가했습니다.</li>
    <li>로그인 모듈(중복 로그인/빈번한 로그인/빈번한 계정 전환/자동 온라인/강제 로그아웃)을 최적화했습니다.</li>
    <li> 앱이 백그라운드에서 오랜 시간 머물다가 포그라운드로 진입했을 때 메시지 전달 시간이 오래 걸리는 문제를 수정했습니다.</li>
    <li>1:1 채팅 읽지 않음 수를 최적화했습니다.</li></ul></td>
<td>2019-07-16</td>
<td>-</td>
</tr> </table>

## 2019년 06월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.4 버전 및 최신 Demo 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>신규 모바일 클라이언트 UI 디자인의 TUIKit 및 제품 Demo를 출시했습니다.</li>
    <li>Demo 주소록, 그룹 관리, 관계망 등 기능을 개선했습니다.</li>
    <li>캐시를 최적화하여 UI 랙을 줄였습니다.</li>
    <li>메시지 발송 효율을 최적화했습니다.</li>
    <li>크로스 플랫폼 라이브러리 메시지에 메시지의 유일한 ID를 가져오는 JSON key를 추가했습니다.</li></ul></td>
<td>2019-06-27</td>
<td>-</td>
</tr> </table>

## 2019년 05월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
            <td>SDK 4.3 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>TIMFriendshipManager 클래스에 querySelfProfile 및 queryUserProfile 인터페이스(로컬 데이터 읽기)를 추가했습니다.</li>
    <li>친구 프로필 정보 가져오기에 addTime 필드를 추가했습니다.</li>
    <li>x86 및 x86_64 아키텍처 지원을 추가했습니다.</li>
    <li>사용자 정의 필드 데이터 리포트를 추가했습니다.</li>
    <li>메시지 확인 후 바로 사라지는 메시지를 추가했습니다.</li>
    <li>메시지 회수 사용 사례를 추가했습니다.</li>
    <li>친구 검증 인터페이스 checkFriends를 추가했습니다.</li>
    <li>로컬 데이터를 가져오는 queryGroupInfo 인터페이스를 추가했습니다.</li>
    <li>getGroupDetailInfo 및 getGroupPublicInfo 인터페이스를 폐기하고, 통일적으로 getGroupInfo 인터페이스를 사용합니다.</li>
    <li>서버 연결 정책을 최적화했습니다.</li>
    <li>인터넷 재연결 정책을 최적화했습니다.</li>
    <li>서버 과부하 정책을 최적화했습니다.</li>
    <li>하트비트를 최적화하고 불필요한 패킷 발송을 줄였습니다.</li>
    <li>재연결 시 연결 요청을 최적화했습니다.</li>
    <li>다양한 네트워크에서의 첫 연결 및 중국 외 지역 액세스 포인트 품질을 최적화했습니다.</li>
    <li>iOS에서 Wi-Fi로 전환 시, 네트워크 재연결이 느린 문제를 최적화했습니다.</li>
    <li>그룹 메시지 동기화 문제를 최적화했습니다.</li></ul></td>
<td>2019-05-24</td>
<td>-</td>
</tr> </table>

## 2019년 04월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.3 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>친구 블랙리스트 기능, 친구 그룹 기능 및 친구 추가 요청 처리 등 관계망 기능을 추가했습니다.</li>
    <li>읽지 않음 수 관련 문제를 최적화했습니다.</li>
    <li>메시지 읽음 상태 문제를 최적화했습니다.</li>
    <li>REST API에서 발송한C2C 메시지 정렬 오류 문제를 최적화했습니다.</li>
    <li>로밍 메시지 가져오기 시, 간혹 발생하는 중복 문제를 최적화했습니다.</li>
    <li>uniqueId 공란 시 구현 관련 문제를 최적화했습니다.</li>
    <li>TIMMessage가 senderProfile을 통해 사용자 프로필 정보를 가져오지 못하는 문제를 최적화했습니다.</li>
    <li>읽음 확인 콜백 및 상태 문제를 수정했습니다.</li>
    <li>읽지 않은 메시지 동기화 시, 최신 메시지를 콜백하지 않는 문제를 수정했습니다.</li>
    <li>그룹 메시지를 간혹 발송할 수 없는 문제를 수정했습니다.</li>
    <li>IP 연결 및 login 정보 통계 리포트를 추가했습니다.</li></ul></td>
<td>2019-04-24</td>
<td>-</td>
</tr> </table>

## 2019년 03월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.2 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>iOS에 bitcode 2를 지원하는 TUIKit.framework를 추가했습니다.</li>
    <li>iOS에서 pod로 TUIKit.framework를 직접 통합할 수 있습니다.</li>
    <li>Windows에 duilib 라이브러리를 UI 컴포넌트로 하는 IM Demo를 추가했습니다.</li>
    <li>Windows에 /source-charset:.65001 컴파일 옵션을 추가했습니다.</li>
    <li>Web 추가 항목 WEBIM은 .amr 녹음 형식 재생을 지원합니다.</li>
    <li>친구 추가/삭제/조회 로직을 추가했습니다.</li>
    <li>구/신 버전 음성, 파일, 비디오 메시지 통신 문제를 수정했습니다.</li>
    <li>TUIkit 오디오 재생 로직을 최적화했습니다.</li>
    <li>AVChatRoom 방 인원 100명 초과 이후 메시지 수신 오류가 발생하는 문제를 수정했습니다.</li>
    <li>그룹 음소거가 적용되지 않는 문제를 수정했습니다.</li>
    <li>사용자 그룹 내 신분 변경 기능을 수정했습니다.</li>
    <li>그룹 메시지 수신 변경 옵션을 수정했습니다.</li>
    <li>오프라인 푸시 스위치가 적용되지 않는 문제를 수정했습니다.</li>
    <li>사용자 그룹 내 신분 변경 기능을 수정했습니다.</li>
    <li>그룹 미결 및 완결 요청 정보 가져오기에 대한 반환이 정확하지 않은 문제를 수정했습니다.</li>
    <li>클라이언트 백그라운드 이동 시 Crash가 발생하는 문제를 수정했습니다.</li>
    <li>네트워크 재연결 후, 메시지를 받지 못하는 문제를 수정했습니다.</li>
    <li>간혹 메시지 정렬 오류가 발생하는 문제를 수정했습니다.</li>
    <li>간혹 메시지 발송 실패가 발생하는 문제를 수정했습니다.</li>
    <li>백엔드에서 그룹 해산 후 클라이언트가 관련 명령을 받지 못하는 문제를 최적화했습니다.</li></ul></td>
<td>2019-03</td>
<td>-</td>
</tr> </table>

## 2019년 01월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.0 버전 배포(Android, iOS 및 Windows)</td>
<td> 신규 IM 클라이언트 SDK를 배포하여 대규모 네트워크 연결, 메시지 수발신 및 읽지 않음 수 등 문제를 수정하고 네트워크, 메시지 등 중요 기본 모듈의 안정성을 개선했습니다. 또한 오픈소스 TUIKit을 제공하고 고객 액세스 프로세스를 더욱 간소화했습니다.</td>
<td>2019-01-21</td>
<td>-</td>
</tr> </table>

## 2017년 07월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>UGC 쇼트 비디오 지원</td>
<td>UGC 쇼트 비디오 메시지 기능을 지원합니다. 비디오 편집을 통해 콘텐츠 품질 및 사용자 경험을 향상시킬 수 있습니다.</td>
<td>2017-07</td>
<td>-</td>
</tr> </table>

## 2017년 05월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 3.0 버전 배포</td>
<td> 더 많은 기능, 더 작은 크기, 최적화된 코드 구조를 통해 고객 통합 효율성 및 다운로드 경험을 개선하였습니다.</td>
<td>2017-05</td>
<td>-</td>
</tr> </table>

## 2016년 12월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>다중 인스턴스 강제 오프라인 기능 지원</td>
<td>Web 다중 인스턴스 강제 오프라인 및 Web 클라이언트 고객 서비스 등 시나리오에 대한 요구 사항을 충족합니다.</td>
<td>2016-12</td>
<td>-</td>
</tr> </table>

## 2016년 08월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>브로드캐스트 메시지 기능 지원</td>
<td>전 구성원 브로드캐스트 메시지 푸시를 지원하여, 메시지 전파 효율을 높이고 푸시에 대한 고객의 요구를 충족시킵니다.</td>
<td>2016-08</td>
<td>-</td>
</tr><tr>
<td>멀티 단말 동시 로그인 지원</td>
<td>멀티 단말 동시 로그인을 지원하여, 휴대폰과 PC를 동시에 사용 가능합니다. 이를 통해 사용자 경험을 크게 향상시켰습니다.</td>
<td>2016-08</td>
<td>-</td>
</tr> </table>

## 2016년 05월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>라이브 방송 채팅방 출시</td>
<td>라이브 방송 시나리오에 대해 인원수에 제한이 없는 라이브 방송 채팅방 및 메시지 빈도 제한, 사용자 정의 메시지 등 시나리오에 맞춤형 지원이 가능합니다.</td>
<td>2016-05</td>
<td>-</td>
</tr> </table>

## 2016년 03월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>메시지 푸시 기능 지원</td>
<td>Android 및 iOS 오프라인 푸시 기능을 지원하여, 확실한 메시지 전달과 더 나은 사용자 경험을 보장합니다.</td>
<td>2016-03</td>
<td>-</td>
</tr> </table>

## 2015년 12월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>쇼트 비디오 메시지 유형 지원</td>
<td>쇼트 비디오 메시지 유형을 지원하여, 풍부한 메시지 콘텐츠를 제공합니다.</td>
<td>2015-12</td>
<td>-</td>
</tr> </table>

## 2015년 08월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>Web 플랫폼 지원</td>   
<td>Web 플랫폼의 IM 클라우드 서비스를 지원합니다. 사용자 정의 이모티콘 등 메시지 유형을 추가했습니다.</td>
<td>2015-08</td>
<td>-</td>
</tr> </table>

## 2015년 07월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>Windows 플랫폼 지원</td>
<td>Windows 플랫폼의 IM 클라우드 서비스를 지원합니다. 지리적 위치, 음성 등 메시지 유형을 추가했습니다.</td>
<td>2015-07</td>
<td>-</td>
</tr> </table>

## 2015년 05월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>IM(기존 명칭: Cloud Communication) 출시</td>
<td>Android 및 iOS IM 클라우드 서비스를 지원합니다. 이미지, 텍스트, 이모티콘 등 다양한 메시지 유형을 지원합니다.</td>
<td>2015-05</td>
<td>-</td>
</tr> </table>




## 2021년 07월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.5.897 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
	<li> 데이터 리포트 시, 간헐적으로 발생하는 크래쉬 문제를 수정했습니다.</li>
        <li> 통신사 이름 가져오기 콜백 getSimOperatorName()을 제거했습니다.</li>
    </ul></td>
    <td> 2021-07-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.65 기본 버전 배포</td>
    <td><ul style="margin:0">
        <li> 통신사 이름 가져오기 콜백 getSimOperatorName()을 제거했습니다.</li>
    </ul></td>
    <td> 2021-07-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.5.892 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> ‘and’ 또는 ‘or’ 로직 관계의 다중 키워드 메시지 검색 기능을 추가했습니다.</li>
    	<li> 메시지 발신자 계정으로 메시지를 검색하는 기능을 추가했습니다.</li>
    	<li> 메시지 기록 풀링 시, 시간 범위를 설정할 수 있습니다.</li>
    	<li> 그룹 메시지 기록 풀링 시, sequence에 따라 풀링할 수 있습니다.</li>
    	<li> 타사 콜백에 의한 메시지 수정 알림 기능을 추가했습니다.</li>
    	<li> 그룹 프로필에 허용된 최대 그룹 구성원 수를 가져오는 인터페이스를 추가했습니다.</li>
    	<li> App 레이어에서 마지막 메시지가 없는 대화를 정렬할 수 있도록 대화 객체에 orderKey 정렬 필드를 추가했습니다.</li>
    	<li> 라이브 방송 그룹 메시지 수신 딜레이와 백엔드 계정 전환 사전 완료를 최적화했습니다.</li>
    	<li> 인터넷 연결 스케쥴링 프로토콜을 업데이트하고, 중국 본토 외 지역 인터넷 연결 소요 시간을 최적화했습니다.</li>
    	<li> 대화 목록 풀링 로직을 최적화했습니다.</li>
    	<li> 그룹 구성원 리스트 풀링 로직을 최적화하고, 로컬 캐시를 활성화했습니다.</li>
    	<li> ‘로그 레벨이 Debug보다 낮을 때 로그 콜백을 트리거하지 않는 문제’를 수정했습니다.</li>
	<li> ‘그룹 구성원 정보를 가져올 때 친구 설명이 없는 문제’를 수정했습니다.</li>
    	<li> ‘참여한 그룹 리스트를 가져올 때 그룹 소유자 승인 대기 중인 그룹까지 포함하는 문제’를 수정했습니다.</li>
    	<li> 온라인에서 보고된 안정성 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-07-14 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>


## 2021년 06월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.4.666 인핸스드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 기존 라이트 버전 SDK 이름을 인핸스드 버전 SDK로 변경합니다.</li>
    	<li> 메시지 검색, 그룹 검색, 친구 검색을 지원합니다(울티메이트 버전만 지원).</li>
    	<li> 메시지 발송 시, 대화의 마지막 메시지 업데이트 여부 설정에 사용되는 매개변수를 추가했습니다.</li>
    	<li> 대화를 유지하면서 대화의 로밍 메시지를 지우는 기능이 추가되었습니다.</li>
    	<li> 여러 단말이 동시에 동일 플랫폼에 로그인할 수 있습니다(울티메이트 버전만 지원).</li>
    	<li> 네트워크 연결 및 로그인 소요 시간을 최적화했습니다.</li>
    	<li> 데이터 리포트를 최적화했습니다.</li>
    	<li> 오프라인 푸시 로직을 최적화하였으며, 전역에서 메시지 오프라인 푸시 비활성화를 지원합니다</li>
    	<li> 오프라인 푸시 로직을 최적화하였으며, VIVO 휴대폰 오프라인 푸시 메시지 분류 classification 필드를 지원합니다</li>
    	<li> C2C 대화 읽지 않음 수가 간헐적으로 부정확한 문제를 수정했습니다.</li>
    	<li> 메시지 기록 풀링 속도를 최적화했습니다.</li>
    	<li> 멀티 Element 메시지에 이모티콘 및 위치 추가를 지원합니다.</li>
    	<li> 오프라인 상태에서 그룹 닉네임 수정 후, 다시 로그인 시 해당 대화의 닉네임이 제때에 업데이트되지 않는 문제를 수정했습니다.</li>
    	<li> C2C 대화에 대해 읽음 리포트를 한 후 간혹 20005 오류 코드가 발생하는 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-06-03 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 05월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.3.435 라이트 버전 배포</td>
    <td><ul style="margin:0">
        <li> 대화 로밍 메시지 삭제 인터페이스를 추가했습니다.</li>
    	<li> 일부 안드로이드 휴대폰으로 장시간 인터넷 연결 시, 네트워크 상태 변화 공지를 수신하지 못하는 문제를 수정했습니다.</li>
    	<li> 낯선 사람이 친구 프로필 정보를 요청할 때마다 백엔드에 요청하지 않도록 친구 프로필 정보 풀링 로직을 최적화했습니다.</li>
     	<li> 그룹은 해산하고 대화는 유지하는 시나리오에서 그룹 정보 및 대화 메시지 기록을 가져오지 못하는 문제를 수정했습니다.</li>
	<li> 대화 목록 가져오기 인터페이스에 대화 순서 오류가 발생하는 문제를 수정했습니다.</li>
    	<li> 대화의 읽지 않음 총 수량 가져오기 인터페이스를 추가했습니다.</li>
    	<li> 대화의 읽지 않음 총 수량을 가져올 때 방해 금지를 설정한 그룹 대화를 필터링하는 문제를 수정했습니다.</li>
    	<li> iOS 플랫폼 HTTP 요청에 간헐적으로 발생하는 Crash 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-05-20 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.62 스탠다드 버전 배포</td>
    <td><ul style="margin:0">
        <li> 기존 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-05-20 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 04월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
    <td> SDK 5.3.425 라이트 버전 배포</td>
    <td><ul style="margin:0">
        <li> 대화 상단 고정 설정을 지원합니다.</li>
    	<li> 1:1 채팅 메시지 방해 금지 설정을 지원합니다.</li>
    	<li> 읽지 않음 수에 포함되지 않는 메시지 발송을 지원합니다.</li>
     	<li> 네트워크 로그인에 실패하지 않은 상황에서 로컬 대화 및 메시지 데이터 가져오기를 지원합니다.</li>
	<li> iOS 버전에 xcframework를 추가했습니다(Mac Catalyst 지원).</li>
    	<li> 대화의 읽지 않음 총 수량 가져오기 인터페이스를 추가했습니다.</li>
    	<li> 개인 정보에 birthday 필드를 보완했습니다.</li>
    	<li> 기타 구성원이 그룹 @ 메시지를 회수한 후, @ 대상자의 해당 대화에 여전히 그룹 @ 알림이 포함되는 문제를 수정했습니다.</li>
    	<li> 일부 안드로이드 휴대폰으로 지속 연결 시, 초기 인터넷 연결 성공 후 인터넷이 끊겼다가 재연결되는 문제를 해결했습니다.</li>
    	<li> iOS용 SDK에서 그룹을 생성할 때 사용자가 사용자 정의 필드를 설정할 수 없는 문제가 수정되었습니다.</li>
    	<li> 특수 계정 사용자가 findMessage 로컬 메시지를 조회하지 못하는 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-04-19 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.2.212 라이트 버전 배포</td>
    <td><ul style="margin:0">
        <li> iOS: IDFA 관련 키워드를 사용한 SDK 최적화가 App Store에서 거부되는 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-04-06 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.60 스탠다드 버전 배포</td>
    <td><ul style="margin:0">
        <li> iOS: IDFA 관련 키워드를 사용한 SDK 최적화가 App Store에서 거부되는 문제를 수정했습니다.</li>
    </ul></td>
    <td> 2021-04-06 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 03월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> 
<tr>
	<td> SDK 5.2.210 라이트 버전 배포</td>
	<td><ul style="margin:0">
	    <li> 메시지 결합 전달 기능을 지원합니다.</li>
	    <li> 지속 연결 로직을 최적화하여, 중국 본토 외 지역 인터넷 연결 품질을 개선했습니다.</li>
	    <li> 로그인 오류 코드를 세분화하여 로그인 시에 네트워크의 정상 동작 여부를 구분했습니다.</li>
	    <li> cos 업로드 로직을 최적화하여 리치 미디어 메시지 발송 경험이 향상되었습니다.</li>
	    <li> 메시지 기록 가져오기 고급 인터페이스를 추가했습니다.</li>
	    <li> 대화 인터페이스의 일괄 가져오기 기능을 추가했습니다.</li>
		<li> 친구 관계 인터페이스의 일괄 확인 기능을 추가했습니다.</li>
		<li> 업데이트 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.</li>
	</ul></td>
	<td> 2021-03-12 </td>
	<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
	<td> SDK 5.1.56 스탠다드 버전 배포</td>
	<td><ul style="margin:0">
	    <li> Windows SDK에서 새 메시지 콜백이 트리거될 때, 클라이언트 스레드가 SDK 로직 스레드를 차단하는 문제를 수정했습니다.</li>
	    <li> Android SDK에서 신규 로그 컴포넌트 교체 시, 안정성이 향상되었습니다.</li>
	    <li> 지속 연결 로직을 최적화하여, 중국 본토 외 지역 인터넷 연결 품질을 개선했습니다.</li>
	    <li> 데이터 리포트를 최적화하고 네트워크 타임 아웃 관련 오류 코드를 세분화했습니다.</li>
	    <li> iOS SDK 로그 추출 시, 간헐적으로 실패가 발생하는 문제를 수정했습니다.</li>
	    <li> 일부 안정성 문제를 수정했습니다.</li>
	</ul></td>
	<td> 2021-03-03 </td>
	<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 01월
<table>
<tr>
    <th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr>
<tr>
    <td> SDK 5.1.138 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 로그를 최적화했습니다.</li>
	    <li> 지속 연결 인터넷 연결 정책을 개선하고, 중국 본토 외 지역 인터넷 연결 품질을 최적화했습니다.</li>
	    <li> 1초 내에 여러 개의 C2C 메시지를 받으면 간헐적으로 발생하는 대화의 마지막 메시지가 부정확한 문제를 수정했습니다.</li>
	    <li> 대화 목록 조회 시, 간헐적으로 발생하는 콜백 없음 문제를 수정했습니다.</li>
	    <li> C2C 메시지 발송 시, 간헐적으로 발생하는 메시지 시리얼 넘버가 부정확한 문제를 수정했습니다.</li>
	    <li> Android 플랫폼에서 24MB를 초과하는 비디오 전송 시, 간헐적으로 발생하는 업로딩 진행률에 마이너스 값이 표시되는 문제를 수정했습니다.</li>
	    <li> Android 플랫폼에서 메시지 발송 시, 간헐적으로 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-02-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.50 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            	<li> V2 메시지 객체에 random 필드를 추가했습니다.</li>
	    	<li> 대화에서 lastMsg 메시지 회수를 지원합니다.</li>
		<li> getMessage로 가져온 마지막 메시지 상태에 간헐적으로 오류가 발생하는 문제를 수정했습니다.</li>
		<li> 메시지 수신 후, 사용자 프로필 정보를 자주 풀링하는 경우 메시지 딜레이가 발생하는 문제를 수정했습니다.</li>
		<li> 계정 삭제 시, 그룹 구성원 리스트 풀링에 실패가 발생하는 문제를 수정했습니다.</li>
		<li> insertLocalMessage 이후, findMessage 호출 시, 메시지를 찾을 수 없는 문제를 수정했습니다.</li>
		<li> 대화 삭제 시, 대화 업데이트 콜백이 실행되는 문제를 수정했습니다.</li>
		<li> Android에서 그룹 메시지 기록에 닉네임이 제때에 업데이트 되지 않는 문제를 수정했습니다.</li>
		<li> iOS 데이터베이스 안정성을 개선했습니다.</li>
		<li> 업데이트 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.</li>
        </ul>
    </td>
    <td> 2021-02-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.137 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 사용자가 여러 개의 iOS 또는 Android 디바이스에서 동일 계정으로 반복 로그인할 때, 간헐적으로 발생하는 로그인 인터페이스 콜백 없음 문제를 수정했습니다.</li>
	    <li> 저사양 Android 디바이스로 로그 경로를 가져올 때 간헐적으로 발생하는 crash를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.136 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 API에 로그 콜백 인터페이스를 추가했습니다.</li>
	    <li> 그룹 @ 메시지에 @ 사용자 UserID가 비어있는 문제를 수정했습니다.</li>
	    <li> 간헐적으로 발생하는 라이브 방송 그룹 메시지 수신 불가 문제를 수정했습니다.</li>
	    <li> 네트워크를 빈번하게 연결하면 간혹 로그인 상태 오류가 발생하는 문제를 수정했습니다.</li>
	    <li> 강제 로그아웃 후 다시 로그인 시 간혹 실패가 발생하는 문제를 수정했습니다.</li>
	    <li> DNS 도메인 리졸브 중 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-27 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.132 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 네트워크 모듈에서 과부하 보호를 지원합니다.</li>
	    <li> 표준 버전을 라이트 버전으로 업데이트할 때 간혹 일부 대화가 유실되는 문제를 수정했습니다.</li>
	    <li> 로그인 정보 기간 만료 시, onUserSigExpired 콜백을 수신하지 못하는 문제를 수정했습니다.</li>
	    <li> 그룹 구성원이 그룹에서 강제 퇴장된 후, 다시 그룹에 참여하려고 하면 다시 onMemberKicked 콜백을 받는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-22 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.131 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 단일 메시지 전달 인터페이스를 추가했습니다.</li>
	    <li> 라이브 방송 그룹이 메시지를 수신할 때 메시지 발신자의 닉네임과 프로필을 다시 조회하지 않도록 라이브 방송 그룹 메시지 수신 로직을 최적화했습니다.</li>
	    <li> 대화의 마지막 메시지 삭제 시, 대화 업데이트 알림이 표시되지 않는 문제를 수정했습니다.</li>
	    <li> 로그인 완료 후, C2C 메시지 동기화 시, 간혹 C2C 대화의 읽지 않음 수가 0으로 표시되는 문제를 수정했습니다.</li>
	    <li> 오프라인 상태에서 다시 온라인 상태가 된 후, 대화 목록을 동기화하면 대화의 마지막 메시지를 업데이트하지 않는 문제를 수정했습니다.</li>
	    <li> Android 플랫폼에서 사용자 정의 메시지의 description 필드를 설정할 때, 설정한 개인 프로필 정보 level 및 role 필드가 적용되지 않는 문제를 수정했습니다.</li>
	    <li> Android 플랫폼에서 초기화 해제 시 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-19 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.21 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 글로벌화 지원을 개선하였습니다. 영어 버전에서 일부 문자열이 여전히 중국어로 표시되는 문제를 수정했습니다.</li>
						<li> Android 플랫폼에서 extension 확장 필드의 사용자 정의 메시지를 포함하면 발송 실패하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-15 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.129 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 대화 목록을 가져올 때, 업데이트된 대화가 없어도 대화 업데이트 콜백이 트리거되는 문제를 수정했습니다.</li>
            <li> 대화의 모든 메시지를 삭제할 때, 해당 대화의 마지막 메시지를 삭제하지 않는 문제를 수정했습니다.</li>
            <li> iOS 플랫폼에서 getSignallingInfo 메소드로 비신호 메시지 전달 시, 반환값이 nil이 아닌 문제를 수정했습니다.</li>
            <li> Android 플랫폼에서 JNI 참조 테이블 제한 초과로 인해 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-13 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.125 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 API 메시지 객체에 random 필드를 추가했습니다.</li>
            <li> V2 API 사용자 정의 메시지에 설명 정보 description 및 확장 정보 extension 필드를 추가했습니다.</li>
            <li> V2 API 사용자 프로필 정보 객체에 사용자 역할 role 및 사용자 레벨 level 필드를 추가했습니다.</li>
            <li> 4.8.1 미만 버전을 라이트 버전으로 업데이트할 때 발생하는 데이터베이스 호환성 문제를 수정했습니다.</li>
            <li> 메시지 발송 시, 간혹 사용자가 자신이 보낸 메시지의 콜백을 받는 문제를 수정했습니다.</li>
            <li> 사용자가 아무 그룹에도 참여하지 않은 상태에서, 참여 그룹 리스트 가져오기하면 콜백이 없는 문제를 수정했습니다.</li>
            <li> 그룹 메시지 수신 옵션 설정 시, 대화 업데이트 콜백이 없는 문제를 수정했습니다.</li>
            <li> 대화 동기화 로직에 간혹 종료 콜백이 없는 문제를 수정했습니다.</li>
            <li> 대화 동기화 로직에 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2021-01-08 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.20 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 사용자 정의 메시지에 desc 및 ext 필드를 추가했습니다.</li>
            <li> V2 사용자 정보 인터페이스에 role 및 level 필드를 추가했습니다.</li>
            <li> V2 인터페이스에서 로그인 성공 여부와 상관없이, 모두 로컬 대화 목록 데이터 및 로컬 메시지 기록 데이터를 가져올 수 있는 문제를 수정했습니다.</li>
            <li> V2 getHistoryMessageList 인터페이스를 추가하여 클라우드 또는 로컬 메시지 가져오기 및 특정 시간 전후에 전송된 메시지 가져오기를 지원합니다.</li>
            <li> C2C 메시지의 프로필 사진 가져오기 문제를 최적화했습니다.</li>
            <li> 리치 미디어 메시지 파일 업로드의 안전성 문제 및 기간 연장 문제를 최적화했습니다.</li>
            <li> 발송한 리치 미디어 메시지의 로컬 경로가 비어있는 문제를 수정했습니다.</li>
            <li> 그룹에 로컬 메시지를 삽입한 후 로그아웃하고 다시 로그인하면 해당 대화의 lastMessage가 이전 메시지로 표시되는 문제를 수정했습니다.</li>
            <li> 그룹에 로컬 메시지를 삽입한 후 로그아웃하고 다시 로그인하면 해당 대화의 lastMessage가 이전 메시지로 표시되는 문제를 수정했습니다.</li>
            <li> 업데이트 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.</li>
        </ul>
    </td>
    <td> 2021-01-08 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>

## 2020년 12월

<table>
<tr>
    <th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr>
<tr>
    <td> SDK 5.1.123 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> Android 버전에서 RESTAPI가 전달한 그룹 사용자 정의 시스템 메시지 수신 불가 문제를 수정했습니다.</li>
            <li> 메시지 random 필드 생성 방법을 최적화했습니다.</li>
            <li> 문제 분석을 위해 로그 출력을 최적화했습니다.</li>
            <li> 네트워크 모듈에 간혹 crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-31 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.122 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 대화 임시 보관 설정 시, 콜백이 없는 문제를 수정했습니다.</li>
            <li> findMessage 메시지 조회 시, 메시지 발신자 정보가 완료되지 않는 문제를 수정했습니다.</li>
            <li> 로컬 메시지 삽입 후, findMessage로 메시지를 조회하면 실패가 발생하는 문제를 수정했습니다.</li>
            <li> 그룹 메시지 수신 옵션 설정 시, 대화 객체를 업데이트하지 않는 문제를 수정했습니다.</li>
            <li> 개인 또는 그룹 닉네임, 프로필 사진 변경 시, 대화 변경 알림이 표시되지 않는 문제를 수정했습니다.</li>
            <li> 로컬 메시지 삽입 시, 해당 대화의 마지막 메시지를 업데이트하지 않는 문제를 수정했습니다.</li>
            <li> 개인 프로필 정보 업데이트 주기의 클라우드 제어를 활성화했습니다.</li>
            <li> iOS 플랫폼에서 잘못된 사전 및 배열 작업으로 간혹 Crash가 발생하는 문제를 수정했습니다.</li>
            <li> Android 플랫폼에서 메시지를 삭제하면 간혹 Crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-25 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.121 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 라이브 방송 그룹에서 본인의 그룹 구성원 프로필 정보를 풀링할 필요가 없도록, 그룹 정보 풀링 로직을 최적화했습니다.</li>
            <li> 로그 출력을 개선하고 디바이스 유형 필드를 추가했습니다.</li>
            <li> C2C 대화에서 메시지 회수 알림 수신 시, 해당 대화의 마지막 메시지 상태를 업데이트하지 않는 문제를 해결했습니다.</li>
            <li> 라이브 방송 그룹의 long polling 메시지 딜레이가 너무 긴 문제를 수정했습니다.</li>
            <li> 동일 계정으로 중복 로그인한 후 다시 같은 라이브 방송 그룹에 참여하면 메시지 long polling 모듈이 메시지 업데이트 없이 key를 풀링하는 문제를 수정했습니다.</li>
            <li> iOS 플랫폼에 메시지 사용자 정의 필드가 json 배열로 전달될 때, 수신측의 신호 모듈 파싱 중 Crash가 발생하는 문제를 수정했습니다.</li>
            <li> Android 플랫폼에 대화 임시 보관을 설정하면 간혹 Crash가 발생하는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-18 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.118 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 메시지 중복 제거 로직을 최적화하여 같은 메시지에 여러 차례 콜백이 발생하는 문제를 수정했습니다.</li>
            <li> 로컬에 C2C 메시지 삽입 인터페이스를 추가했습니다.</li>
            <li> 그룹의 읽지 않은 메시지를 삭제 및 회수해도 읽지 않음 숫자가 줄어들지 않는 문제를 수정했습니다.</li>
            <li> 발송 실패 메시지를 삭제할 수 없는 문제를 수정했습니다.</li>
            <li> 그룹 대화 삭제 시, 그룹에서 탈퇴했거나 해당 그룹이 해산한 경우, 콜백 삭제 실패가 발생하는 문제를 수정했습니다.</li>
            <li> 그룹 메시지 읽음 리포트 시, 그룹에서 탈퇴했거나 해당 그룹이 해산한 경우, 콜백 설정 실패가 발생하는 문제를 수정했습니다.</li>
            <li> 개인 정보 서명 설정 실패 문제를 수정했습니다.</li>
            <li> 친구 블랙리스트 추가에 간혹 크래쉬가 발생하는 문제를 수정했습니다.</li>
            <li> 메시지 발송 시, 반환 메시지 ID를 동기화하지 않는 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-11 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.115 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 신호 타임아웃 시간 및 서버 시간 동기화를 최적화했습니다.</li>
            <li> 열악한 네트워크 환경에서 간혹 연결 실패가 발생하는 문제를 수정했습니다.</li>
            <li> iOS API 헤더 파일을 완성했습니다.</li>
            <li> Android JSON을 Gson으로 교체할 때 발생하는 크래쉬 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-04 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.10 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 API에 그룹 사용자 정의 필드 및 메시지 멀티 Element를 추가했습니다.</li>
            <li> V2 API에 로컬에 C2C 메시지를 삽입하는 인터페이스를 추가했습니다.</li>
            <li> 일반 그룹 및 라이브 방송 그룹의 메시지 유실 문제를 최적화했습니다.</li>
            <li> 발송 실패 메시지를 삭제할 수 없는 문제를 수정했습니다.</li>
            <li> C2C 대화에서 발송하는 첫 번째 메시지가 온라인 메시지인 상황에서 읽음 확인을 받지 못하는 문제를 수정했습니다.</li>
            <li> 회수한 메시지가 메시지 기록 풀링 인터페이스를 통해 반환된 후, 메시지 상태가 비정확한 문제를 수정했습니다.</li>
            <li> IOS 플랫폼에서 친구 그룹 인터페이스를 호출하여 빈 그룹명을 입력하면 모든 그룹 정보를 반환하지 않는 문제를 수정했습니다.</li>
            <li> 안정성 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-04 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.111 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> 로그 출력을 개선했습니다.</li>
            <li> 일부 안정성 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-12-01 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>


## 2020년 11월

<table>
<tr>
    <th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr>
<tr>
    <td> SDK 5.1.110 라이트 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> V2 API의 모든 인터페이스를 보완했습니다.</li>
            <li> 대화 기능을 보완했습니다.</li>
            <li> 관계망 기능을 보완했습니다</li>
            <li> 그룹@ 기능을 추가했습니다.</li>
            <li> iOS iPhone 및 iPad의 동시 온라인 접속을 지원합니다.</li>
            <li> 메시지 발송 시, 멀티 Element를 지원합니다.</li>
            <li> 그룹 프로필 정보에 사용자 정의 필드를 추가했습니다.</li>
            <li> 일부 안정성 문제를 수정했습니다.</li>
        </ul>
    </td>
    <td> 2020-11-26 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.2 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> iOS iPhone 및 iPad의 동시 온라인 접속을 지원합니다.</li>
            <li> Mac arm64 아키텍처를 지원합니다.</li>
            <li> android 버전의 안정성 문제를 수정했습니다.</li>
            <li> 표준 TRTC 종속 패키지로 교체했습니다.</li>
        </ul>
    </td>
    <td> 2020-11-12 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
<tr>
    <td> SDK 5.1.1 스탠다드 버전 배포</td>
    <td>
        <ul style="margin:0">
            <li> AVChatRoom 라이브 방송 그룹 온라인 인원 수 가져오기 인터페이스를 추가했습니다.</li>
            <li> 메시지의 유일한 ID로 메시지를 조회하는 인터페이스를 추가했습니다.</li>
            <li> 서버 보정 타임 스탬프 가져오기 인터페이스를 추가했습니다.</li>
            <li> 로그인 속도를 최적화했습니다.</li>
            <li> 그룹 구성원@ 기능에 <code>@전체</code> 기능을 추가했습니다.</li>
            <li> TUIKit 컴포넌트의 글로벌 지원을 강화했습니다.</li>
            <li> 그룹 라이브 방송에 작은 라이브 방송 창을 추가했습니다.</li>
        </ul>
        업데이트에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.
    </td>
    <td> 2020-11-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>


## 2020년 10월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 5.0.108 라이트 버전 배포</td>
<td>
    <li> iOS 버전 안정성 문제를 수정했습니다.</li>
    <li> Android 버전에서 간혹 메시지 콜백을 하지 않는 문제를 수정했습니다.</li>
</td>
<td> 2020-10-23 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr><tr>
<td> SDK 5.0.10 스탠다드 버전 배포</td>
<td><ul style="margin:0">
    <li> 신호 인터페이스를 최적화하여 온라인 메시지 onlineUserOnly 및 오프라인 푸시 정보 offlinePushInfo 매개변수 설정을 지원합니다.</li>
    <li> 단일 대화 가져오기 인터페이스의 비동기화 콜백을 최적화했습니다.</li>
    <li> 대화 목록에 필터링 표시를 용이하게 하기 위해, 그룹 유형 가져오기 인터페이스를 추가했습니다.</li>
    <li> 그룹 라이브 방송 기능을 추가하여 마이크 연결, 선물하기, 뷰티 필터, 음성 변조 등 기능을 고루 갖추었습니다.</li>
    <li> 라이브 룸을 추가하였으며, 마이크 연결, PK, 좋아요, 선물하기, 뷰티 필터, 댓글 자막, 친구 팔로우 등 기능을 지원합니다.</li>
    <li> 음성 영상 신호 식별 문제를 최적화했습니다.</li>
</ul></td>
<td> 2020-10-15 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr>
</table>


## 2020년 09월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td> SDK 5.0.106 버전 배포(Android & iOS 라이트 버전)</td>
<td> 기존 안정성 문제를 수정했습니다.</td>
<td> 2020-09-21 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr><tr>
<td> SDK 5.0.6 스탠다드 버전 배포</td>
<td><ul style="margin:0">
    <li>그룹@ 기능을 추가했습니다.</li>
    <li>iOS 및 Android에 deleteMessages 인터페이스를 추가하였습니다. 로컬 및 로밍 메시지를 동시에 삭제할 수 있습니다.</li>
    <li>deleteConversation 인터페이스에서 대화과 로컬 및 로밍 메시지를 동시에 삭제할 수 있습니다.</li>
    <li>API2.0 인터페이스에 사용자 정보, 친구 프로필 정보, 그룹 구성원 프로필 정보의 사용자 정의 필드 설정 및 가져오기 인터페이스를 추가했습니다.</li></ul>
업데이트에 관한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">로그 업데이트</a>를 참고하십시오.</td>
<td> 2020-09-18 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr><tr>
<td> SDK 5.0.102 버전 배포(Android & iOS 라이트 버전)</td>
<td><ul style="margin:0">
    <li> Android & iOS 라이트 버전 SDK가 배포되었습니다.</li>
    <li>라이트 버전 SDK는 기존 스탠다드 버전에서 친구 및 대화 기능을 제거하고, 일부 서비스 로직을 최적화하여 실행 효율을 높이고, 설치 패키지 크기를 줄였습니다.</li>
</ul></td>
<td> 2020-09-04 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</td>
</tr>
</table>

## 2020년 07월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.9.1 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>중국 외 지역 로그인 문제를 최적화했습니다.</li>
    <li>일부 중국 외 지역의 파일 업로드 실패 문제를 수정했습니다.</li>
    <li>@부호를 포함한 계정의 파일 업로드 실패 문제를 수정했습니다.</li>
    <li>C2C 읽지 않음 수에 간혹 오류가 발생하는 문제를 수정했습니다.</li>
    <li>대화 showName에 간혹 오류가 표시되는 문제를 수정했습니다.</li>
    <li>파일 유형 메시지에 다운로드 url 가져오기 인터페이스를 추가했습니다.</li>
    <li>iOS의 인터넷 연결이 끊겼을 때 C2C 메시지 가져오기 콜백이 없는 문제를 수정했습니다.</li>
    <li>Android의 신호 파싱 인터페이스에 간혹 크래쉬가 발생하는 문제를 수정했습니다.</li>
    <li>Android 메시지에 오프라인 푸시 정보를 가져올 때, 간혹 크래쉬가 발생하는 문제를 수정했습니다.</li>
    <li>Android의 API2.0 getFriendApplicationList 인터페이스에 데이터가 없으면 콜백하지 않는 문제 및 getGroupMembersInfo 인터페이스 그룹 구성원이 아닌 사람을 입력하면 콜백하지 않는 문제를 수정했습니다.</li>
    <li>Windows에서 참여한 그룹 목록을 가져오기할 때, 그룹의 상세 정보를 추가했습니다.</li>
    <li>Windows 저용량 파일은 발송이 되지 않는 문제를 수정했습니다.</li>
    <li>Windows 로그가 리포트하는 6002 오류를 수정했습니다.</li>
    <li>iOS Demo & Android Demo에 멀티미디어 오프라인 통화 푸시 기능을 추가하였습니다. 수신 화면으로 리디렉션할 수 있습니다.</li>
    <li>iOS 사용자 정의 메시지 삭제, 회수 오류를 최적화했습니다.</li>
    <li>iOS 멀티미디어 코드 swift -> oc, 서드 파티 종속 라이브러리를 대폭 줄였습니다.</li>
    <li>iOS LiteAV_TRTC, LiteAV_Professional 두 종류의 멀티미디어 종속 라이브러리 TUIKit pod 통합을 지원합니다.</li>
    <li>Android의 Demo 오프라인 푸시를 최적화하고 각 벤더의 푸시 SDK 버전을 업데이트했습니다.</li>
</ul></td>
<td>2020-07-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr> </table>


## 2020년 06월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.8.50 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>누군가 라이브 방송 그룹(AVChatRoom)에 입장한 후, onMemberEnter 콜백이 트리거되지 않는 API 2.0 인터페이스 문제를 수정했습니다.</li> 
    <li>API 2.0 인터페이스의 onGroupInfoChanged 및 onMemberInfoChanged 콜백에 groupID 매개변수를 추가했습니다.</li>
    <li>C2C 메시지가 발송된 후 대화 업데이트 콜백이 없는 문제를 수정했습니다.</li>
    <li>계정을 전환하여 동일 라이브 방송 그룹(AVChatRoom)에 참여한 후, 메시지를 수신하지 못하는 문제를 수정했습니다.</li>
    <li>로그인 후, 간혹 읽지 않음 메시지 동기화 콜백 순서에 오류가 발생하는 문제를 수정했습니다.</li>
    <li>신호 인터페이스를 추가했습니다.</li>
    <li>라이브 방송 그룹(AVChatRoom)에 그룹 사용자 정의 속성 인터페이스를 추가했습니다.</li>
    <li>기존 크래쉬 문제를 수정했습니다.</li>
    <li>Android Q 버전 호환을 위해, 로그 기본 스토리지 위치를 /sdcard/Android/data/패키지 이름/files/log/tencent/imsdk으로 수정했습니다.</li>
    <li>Windows 플랫폼에서 그룹 생성 시, 발생하는 그룹 구성원 역할 문제를 수정했습니다.</li>
    <li>TUIKit API 2.0 인터페이스를 교체했습니다.</li>
    <li>TRTC를 통합하여 멀티미디어 통화 기능을 구현했습니다.</li>
    <li>iOS TUIKit에 딥 컬러 모드를 추가했습니다.</li>
    <li>AndroidX를 지원합니다.</li>
</ul></td>
<td>2020-06-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr> </table>

## 2020년 05월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.8 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>iOS & Android에 신규 API 2.0 인터페이스를 배포하였습니다.</li>
    <li>iOS 및 Android에서 IPv6를 지원합니다.</li>
    <li>라이브 방송 그룹(AVChatRoom)그룹 구성원 리스트 동적 업데이트를 지원합니다.</li>
    <li>xlog 로그 크래쉬 문제를 수정했습니다.</li>
    <li>iOS 대용량 파일 발송 실패 문제를 수정했습니다.</li>
    <li>iOS 메시지의 발신자 친구 설명 풀링 오류 문제를 수정했습니다.</li>
    <li>IM SDK는 AndroidX를 지원합니다.</li>
    <li>Android 디바이스에서 네트워크 권한 문제로 발생하는 크래쉬를 수정했습니다.</li>
</ul></td>
<td>2020-05-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr> </table>


## 2020년 03월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 2.6 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0">
    <li>Web의 비디오 메시지 생성 및 발송을 지원하며 최대 100MB까지 가능합니다.</li>
    <li>Message에 <code>nick</code> 및 <code>avatar</code> 속성을 추가하여 AVChatRoom에서 메시지 발신자 닉네임 및 프로필 사진 주소(사전에 updateMyProfile 호출하여 설정)를 표시합니다.</li>
    <li>Web 멀티 인스턴스 로그인 시, C2C 메시지 회수 알림은 각 인스턴스에서 동기화될 수 있습니다.</li>
    <li>updateGroupProfile을 호출하여 그룹 사용자 정의 필드를 수정하면, 그룹 구성원은 그룹 알림 메시지를 받을 수 있고 관련 내용 Message.payload.newGroupProfile.groupCustomField를 가져올 수 있습니다.</li>
    <li>TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED 인터페이스를 폐기하고 MESSAGE_RECEIVED로 대체하였습니다.</li>
    <li>getGroupList 인터페이스 호출 시, 간혹 오류 메시지가 발생하는 문제를 수정했습니다.</li></ul></td>
<td>2020-03-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr><tr>
<td>SDK 4.7 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>로컬 로그 크기를 최적화했습니다.</li>
    <li>로그인 소요 시간을 최적화했습니다.</li>
    <li>멀티 단말에서 읽지 않음 수 동기화 문제를 수정했습니다.</li>
    <li>단일 친구 가져오기 인터페이스 getFriendList를 추가했습니다.</li>
    <li>iOS & Android 두 플랫폼의 오프라인 푸시 알림창에 표시될 메시지 타이틀 및 내용을 각각 설정할 수 있습니다.</li>
</ul></td>
<td>2020-03-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK 다운로드</a></td>
</tr> </table>

## 2020년 02월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.6 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>파일 업로드 제한을 100MB로 확대했습니다.</li>
    <li>COS 업로드를 최적화했습니다.</li>
    <li>그룹 미결 처리 로직을 최적화했습니다.</li></ul></td>
<td>2020-02-28</td>
<td>-</td>
</tr><tr>
<td>SDK 2.5 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li>네트워크 상태 변경 이벤트 TIM.EVENT.NET_STATE_CHANGE를 추가하여 수신측에서 해당 이벤트에 따라 관련 알림과 가이드를 제공할 수 있습니다.</li>
    <li>WeChat 미니프로그램 플러그인 환경에서 실행할 수 있습니다.</li>
    <li>오류 코드를 줄이고 최적화했습니다.</li>
    <li> 콘솔에서 AVChatRoom을 생성하고 소유자를 지정하면, 소유자가 해당 그룹에 참여한 후 그룹의 다른 구성원이 발송한 정보를 소유자측에 중복해서 표시하는 문제를 수정했습니다.</li>
    <li>콘솔 또는 REST API로 빈번하게 그룹을 폐기하면 SDK에서 TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED 이벤트를 배포하지 않는 문제를 수정했습니다.</li>
    <li>getMessageList에서 간혹 그룹 메시지 리스트 풀링하지 못하는 문제를 수정했습니다.</li></ul></td>
<td>2020-02-28</td>
<td>-</td>
</tr> </table>

## 2020년 01월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 2.4 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li>메시지 회수 인터페이스 revokeMessage를 추가했습니다.</li>
    <li>Message에 isRevoked 속성을 추가했으며 값이 true일 경우 회수된 메시지를 의미합니다.</li>
    <li>메시지가 회수될 때 발생하는 이벤트 알림 TIM.EVENT.MESSAGE_REVOKED를 추가했습니다.</li>
    <li>강제 로그아웃된 이벤트 알림 TIM.EVENT.KICKED_OUT에 ‘다중 디바이스 로그인으로 인한 강제 로그아웃’ 및 ‘UserSig 만료로 인한 강제 로그아웃’ 강제 로그아웃 유형이 추가되었습니다.</li>
    <li>createFileMessage 업로드 파일 크기가 20M에서 100MB로 확대되었습니다.</li>
    <li>그룹 알림 메시지의 msgMemberInfo 및 shutupTime이 폐기될 예정입니다. 대신 memberList 및 muteTime을 사용하십시오.</li>
    <li> 콘솔에 IM 스마트 고객 지원 엔트리를 추가했습니다.</li>
    <li> off 인터페이스를 호출하여 리스닝 이벤트를 취소할 수 없는 문제를 수정했습니다.</li>
    <li> Message의 isRead 속성값 및 유형이 정확하지 않은 문제를 수정했습니다.</li>
    <li> 비디오 메시지, 비디오 파일 발송 시, 최대 크기 제한을 초과하면 표시되는 오류 코드 및 오류 정보가 올바르지 않은 문제를 수정했습니다.</li>
    <li> 사용자 정의 필드를 업데이트한 후 간혹 필드 내용이 정확하지 않은 문제를 수정했습니다.</li>
    <li> 로그인 후 AVChatRoom 유형의 그룹에 참여하면 간혹 발생하는 JOIN_STATUS_ALREADY_IN_GROUP 문제를 수정했습니다.</li>
    <li> core-js로 인한 잠재적 성능 문제를 수정했습니다.</li></ul></td>
<td>2020-01-03</td>
<td>-</td>
</tr> </table>

## 2019년 12월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.6 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>네트워크 연결 품질을 최적화하여 네트워크 품질 변화를 더욱 빠르게 감지합니다.</li>
    <li>AVChatRoom 메시지 처리를 최적화했습니다.</li>
    <li>메시지에 getSenderNickname 동기화 닉네임 반환 인터페이스를 추가했습니다.</li>
    <li>TUIKit/Demo 대화 목록 프로필에 둥근 모서리 설정을 지원합니다.</li></ul></td>
<td>2019-12-23</td>
<td>-</td>
</tr><tr>
<td>SDK 2.3 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li>createImageMessage 및 createFileMessage 인터페이스에 File 객체 입력을 추가했습니다.</li>
    <li>이모티콘 메시지 생성 인터페이스 createFaceMessage를 추가했습니다.</li>
    <li>TIM.TYPES.GRP_AVCHATROOM 유형의 그룹 메시지 알림 효율을 최적화하여 사용자 경험이 대폭 향상되었습니다.</li>
    <li>메시지 발송 실패 시, SDK에서 반환하는 실제 오류 코드 및 오류 정보를 조정했습니다.</li>
    <li>logout 호출 시, 현재 인스턴스 메시지 채널에서만 로그아웃되는 문제를 조정했습니다.</li>
    <li>수신측에서 입력하는 콜백 함수에 안전성 캡슐화를 진행하여 콜백 함수 로직에 오류가 있을 경우 신속하게 문제를 해결할 수 있습니다.</li>
    <li> IM 서버 오류 코드 발생 시, SDK에서 중국어로 오류 정보를 출력합니다.</li>
    <li>WeChat 미니프로그램 환경에서 긴 시간 동안 백그라운드로 전환했다가 다시 포그라운드로 전환하면 간혹 발생하는 메시지 유실 문제를 수정했습니다.</li>
    <li>메시지를 한 번 발송하면 여러 차례 TIM.EVENT.CONVERSATION_LIST_UPDATED가 트리거되는 문제를 수정했습니다.</li>
    <li>registerPlugin을 호출하지 않거나 인터페이스 매개변수 전달이 올바르지 않은 경우 또는 이미지 등 파일 업로드 시, SDK에서 오류 메시지가 발생하는 문제를 수정했습니다.</li>
    <li>TIM.TYPES.GRP_AVCHATROOM 유형의 그룹을 해산하면 long polling이 정지되지 않는 문제를 수정했습니다.</li>
    <li>‘멀티 인스턴스’ 또는 ‘멀티 단말’ 로그인 활성화 시, 하나의 Web 인스턴스에서 로그아웃하면 다른 인스턴스 또는 다른 단말에서 메시지를 수신하지 못하는 문제를 수정했습니다.</li>
    <li>풀링한 대화 목록 구조 문제로 SDK에서 간혹 오류 메시지가 발생하는 수정했습니다.</li></ul></td>
<td>2019-12-13</td>
<td>-</td>
</tr> </table>

## 2019년 11월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 2.2 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li> 미니프로그램은 비디오 메시지 생성 및 발송을 위해 createVideoMessage를 지원합니다. 비디오 메시지는 플랫폼 간에 동기화될 수 있습니다(최신 버전 TUIKit 및 SDK로 업데이트 필요).</li>
    <li>그룹 구성원 프로필 정보 조회 인터페이스 getGroupMemberProfile을 추가했습니다.</li>
    <li>Native IM v3.x에서 발송한 음성, 파일 메시지를 호환합니다.</li>
    <li>위치 메시지 GeoPayload 수신 지원 기능을 추가했습니다.</li>
    <li>로그아웃 후에도 TIM.TYPES.GRP_AVCHATROOM 유형 그룹의 long polling이 계속 실행되는 문제를 수정했습니다.</li>
    <li>TIM.TYPES.GRP_AVCHATROOM 유형의 그룹 메시지 인스턴스에 그룹 명함 값이 없는 문제를 수정했습니다.</li>
    <li>IE 10 브라우저에서 오류 메시지가 발생하는 문제를 수정했습니다.</li>
    <li>익명으로 그룹에 참여할 수 없는 문제를 수정했습니다.</li></ul></td>
<td>2019-11-21</td>
<td>-</td>
</tr><tr>
<td>SDK 4.6 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>메시지 회수 로밍을 지원합니다.</li>
    <li>iOS/Mac 단말에 OPPOChannelID 설정을 추가하여, Android 8.0 이후 버전을 실행하는 OPPO 휴대폰이 iOS 푸시 메시지를 수신하지 못하는 문제를 해결했습니다.</li>
    <li>iOS/Mac 단말의 getGrouplist 반환 객체 주석을 최적화했습니다.</li>
    <li>OPPO 휴대폰(시스템 8.0 이후 버전)의 오프라인 푸시를 위한 channleID의 콘솔 설정을 지원합니다.</li>
    <li>TUIKit/Demo 영상 통화 기능을 추가했습니다.</li>
    <li>TUIKit/Demo에 그룹 프로필 사진 3x3 그리드 표시를 추가하고, 대화 목록, 주소록 및 채팅 UI를 최적화했습니다.</li></ul></td>
<td>2019-11-13</td>
<td>-</td>
</tr><tr>
<td>메시지 기록 저장 '정찰가' 도입</td>
<td>메시지 기록 저장을 '정찰가'로 변경하여 더욱 간편하고 경제적으로 사용할 수 있습니다.</td>
<td>2019-11-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34350">요금 안내</a></td>
</tr> </table>

## 2019년 10월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>신규 콘솔 출시</td>
<td>IM 콘솔의 신규 버전이 정식 출시되었습니다.</td>
<td>2019-10-22</td>
<td><ul style="margin:0;">
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">애플리케이션 생성 및 업그레이드</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34540">기본 설정</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34419">기능 설정</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34578">그룹 관리</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34520">콜백 설정</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34579">통계 분석</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34580">개발 보조 툴</a></li></ul></td>
</tr><tr>
<td>SDK 4.5 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>파일 유형의 메시지 발송 시 생성되는 URL에 파일 형식 확장자를 추가했습니다.</li>
    <li>그룹 사용자 정의 필드 수정 후, 알림 콜백을 추가했습니다.</li>
    <li>오프라인으로 initStorage 메소드를 호출하면 로컬 사용자 및 그룹 정보를 가져올 수 있습니다.</li>
    <li>Android 단말의 getElementCount 인터페이스의 반환 유형을 최적화했습니다.</li>
    <li>Windows 크로스 플랫폼 라이브러리에 각 플랫폼의 네트워크 재연결 속도를 최적화했습니다.</li>
    <li>Android 환경에서도 JVM을 쉽게 전달할 수 있도록 Windows 크로스 플랫폼 라이브러리에 JVM 구성을 추가했습니다.</li></ul></td>
<td>2019-10-16</td>
<td>-</td>
</tr><tr>
<td>SDK 2.1 버전 배포(미니프로그램 및 Web)</td>
<td><ul style="margin:0;">
    <li>오디오 메시지 및 비디오 메시지 수신 기능을 추가했습니다.</li>
    <li>getMessageList 인터페이스 단일 호출로 최대 15건의 메시지 풀링을 지원합니다.</li>
    <li>TIM.TYPES.MSG_SOUND를 폐기하고, TIM.TYPES.MSG_AUDIO로 대체하였습니다.</li>
    <li>getMessageList 인터페이스로 삭제한 그룹 채팅 대화 메시지를 풀링할 수 없는 문제를 수정했습니다.</li>
    <li>그룹 시스템 알림에 그룹 이름이 없는 문제를 수정했습니다.</li>
    <li>새로 생성된 대화의 메시지 수신 시, 프로필 정보가 없는 문제를 수정했습니다.</li></ul></td>
<td>2019-10-16</td>
<td>-</td>
</tr> </table>

## 2019년 09월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 2.0 버전 배포(미니프로그램 및 Web)</td>
<td>신규 IM 미니프로그램용 및 웹용 SDK의 각 모듈 안정성을 최적화하고, 액세스 경험을 개선했으며, 시각화된 Demo를 제공하여, 고객이 편리하게 체험해볼 수 있도록 하였습니다.</td>
<td>2019-09-19</td>
<td>-</td>
</tr><tr>
<td>SDK 4.5 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>Android 단말에 읽음 확인 기능을 추가했습니다.</li>
    <li>네트워크 연결 품질을 최적화했습니다.</li>
    <li>그룹/그룹 구성원 사용자 정의 필드의 풀링 로직을 최적화했습니다.</li></ul></td>
<td>2019-09-18</td>
<td>-</td>
</tr> </table>

## 2019년 08월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.5 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>채팅 메시지 음성 기능에 대한 MotionEvent.ACTION_CANCEL 이벤트 처리를 추가했습니다.</li>
    <li>대화 목록, 채팅 인터페이스, 상세 프로필 정보, 주소록 및 프로필 사진 표시 기능을 추가했습니다.</li>
    <li>개인 프로필 정보의 프로필 사진 수정 기능을 추가했습니다.</li>
    <li>오프라인 푸시 기능 Intent 리디렉션을 추가했습니다.</li>
    <li>1:1 채팅, 그룹 채팅 대화, 랜덤 프로필 사진을 추가했습니다.</li>
    <li>그룹 구성원에 대한 그룹 관리자 역할 부여 및 취소 메시지 알림을 추가했습니다.</li>
    <li>그룹 구성원 음소거 및 음소거 해제 메시지 알림을 추가했습니다.</li>
    <li>읽지 않음 메시지 수를 최적화했습니다.</li>
    <li>로그인 후 최근 대화 목록 로딩 속도를 최적화했습니다.</li>
    <li>로그 정리 기능을 추가했습니다.</li>
    <li>Android 단말에서 com.tencent.imsdk.TIMGroupReceiveMessageOpt 클래스가 통합적으로 사용됩니다.</li>
    <li>TUIKit/Demo에 탭 피드백을 추가하여, 사용자가 TUIKit에서 피드백을 설정 및 사용자 정의할 수 있습니다.</li>
    <li>TUIKit/Demo에 사용자 정의 메시지 발송을 추가했습니다.</li>
    <li>TUIKit/Demo에 C2C 읽음 확인을 추가했습니다.</li>
    <li>TUIKit/Demo에 음성 미재생 시, 빨간 점 표시 기능을 추가했습니다.</li>
    <li>TUIKit/Demo에 프로필 사진을 클릭하면 큰 이미지 보기 기능을 추가했습니다.</li>
    <li>TUIKit/Demo 그룹 채팅에서 작은 회색 막대를 조정하면 사용자 닉네임이 파란색으로 바뀌고, 닉네임을 클릭하면 사용자 정보 인터페이스로 리디렉션됩니다.</li>
    <li>상단 고정 채팅 로직을 최적화하여, 최근 시간 기준으로 정렬 및 표시됩니다.</li>
    <li>Demo의 그룹 닉네임 표시 로직을 최적화했습니다.</li>
    <li>채팅 인터페이스의 프로필 사진 표시 로직을 최적화했습니다.</li>
    <li>읽지 않음 메시지 수를 최적화했습니다.</li>
    <li>로그인 후 최근 대화 목록 로딩 속도를 최적화했습니다.</li>
    <li>중국 외 지역 사용자의 파일 메시지 발송 속도를 최적화했습니다.</li></ul></td>
<td>2019-08-30</td>
<td>-</td>
</tr><tr>
<td>이름을 ‘IM’으로 변경했습니다.</td>
<td>‘Cloud Communication’을 ‘IM’으로 변경했습니다.</td>
<td>2019-08-06</td>
<td>-</td>
</tr> </table>

## 2019년 07월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.4 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>일부 API 인터페이스를 정리 및 통합했습니다.</li>
    <li>친구 추가에 단방향/양방향 옵션를 추가했습니다.</li>
    <li>모든 로컬 스토리지를 비활성화하는 disableStorage 인터페이스를 추가했습니다.</li>
    <li>파일, 비디오, 음성 메시지에 다운로드 URL 가져오기 인터페이스를 추가했습니다.</li>
    <li>로그인 모듈(중복 로그인/빈번한 로그인/빈번한 계정 전환/자동 온라인/강제 로그아웃)을 최적화했습니다.</li>
    <li> 앱이 백그라운드에서 오랜 시간 머물다가 포그라운드로 진입했을 때 메시지 전달 시간이 오래 걸리는 문제를 수정했습니다.</li>
    <li>1:1 채팅 읽지 않음 수를 최적화했습니다.</li></ul></td>
<td>2019-07-16</td>
<td>-</td>
</tr> </table>

## 2019년 06월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.4 버전 및 최신 Demo 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>신규 모바일 클라이언트 UI 디자인의 TUIKit 및 제품 Demo를 출시했습니다.</li>
    <li>Demo 주소록, 그룹 관리, 관계망 등 기능을 개선했습니다.</li>
    <li>캐시를 최적화하여 UI 랙을 줄였습니다.</li>
    <li>메시지 발송 효율을 최적화했습니다.</li>
    <li>크로스 플랫폼 라이브러리 메시지에 메시지의 유일한 ID를 가져오는 JSON key를 추가했습니다.</li></ul></td>
<td>2019-06-27</td>
<td>-</td>
</tr> </table>

## 2019년 05월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
            <td>SDK 4.3 버전 지속적인 최적화(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>TIMFriendshipManager 클래스에 querySelfProfile 및 queryUserProfile 인터페이스(로컬 데이터 읽기)를 추가했습니다.</li>
    <li>친구 프로필 정보 가져오기에 addTime 필드를 추가했습니다.</li>
    <li>x86 및 x86_64 아키텍처 지원을 추가했습니다.</li>
    <li>사용자 정의 필드 데이터 리포트를 추가했습니다.</li>
    <li>메시지 확인 후 바로 사라지는 메시지를 추가했습니다.</li>
    <li>메시지 회수 사용 사례를 추가했습니다.</li>
    <li>친구 검증 인터페이스 checkFriends를 추가했습니다.</li>
    <li>로컬 데이터를 가져오는 queryGroupInfo 인터페이스를 추가했습니다.</li>
    <li>getGroupDetailInfo 및 getGroupPublicInfo 인터페이스를 폐기하고, 통일적으로 getGroupInfo 인터페이스를 사용합니다.</li>
    <li>서버 연결 정책을 최적화했습니다.</li>
    <li>인터넷 재연결 정책을 최적화했습니다.</li>
    <li>서버 과부하 정책을 최적화했습니다.</li>
    <li>하트비트를 최적화하고 불필요한 패킷 발송을 줄였습니다.</li>
    <li>재연결 시 연결 요청을 최적화했습니다.</li>
    <li>다양한 네트워크에서의 첫 연결 및 중국 외 지역 액세스 포인트 품질을 최적화했습니다.</li>
    <li>iOS에서 Wi-Fi로 전환 시, 네트워크 재연결이 느린 문제를 최적화했습니다.</li>
    <li>그룹 메시지 동기화 문제를 최적화했습니다.</li></ul></td>
<td>2019-05-24</td>
<td>-</td>
</tr> </table>

## 2019년 04월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.3 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>친구 블랙리스트 기능, 친구 그룹 기능 및 친구 추가 요청 처리 등 관계망 기능을 추가했습니다.</li>
    <li>읽지 않음 수 관련 문제를 최적화했습니다.</li>
    <li>메시지 읽음 상태 문제를 최적화했습니다.</li>
    <li>REST API에서 발송한C2C 메시지 정렬 오류 문제를 최적화했습니다.</li>
    <li>로밍 메시지 가져오기 시, 간혹 발생하는 중복 문제를 최적화했습니다.</li>
    <li>uniqueId 공란 시 구현 관련 문제를 최적화했습니다.</li>
    <li>TIMMessage가 senderProfile을 통해 사용자 프로필 정보를 가져오지 못하는 문제를 최적화했습니다.</li>
    <li>읽음 확인 콜백 및 상태 문제를 수정했습니다.</li>
    <li>읽지 않은 메시지 동기화 시, 최신 메시지를 콜백하지 않는 문제를 수정했습니다.</li>
    <li>그룹 메시지를 간혹 발송할 수 없는 문제를 수정했습니다.</li>
    <li>IP 연결 및 login 정보 통계 리포트를 추가했습니다.</li></ul></td>
<td>2019-04-24</td>
<td>-</td>
</tr> </table>

## 2019년 03월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.2 버전 배포(Android, iOS 및 Windows)</td>
<td><ul style="margin:0;">
    <li>iOS에 bitcode 2를 지원하는 TUIKit.framework를 추가했습니다.</li>
    <li>iOS에서 pod로 TUIKit.framework를 직접 통합할 수 있습니다.</li>
    <li>Windows에 duilib 라이브러리를 UI 컴포넌트로 하는 IM Demo를 추가했습니다.</li>
    <li>Windows에 /source-charset:.65001 컴파일 옵션을 추가했습니다.</li>
    <li>Web 추가 항목 WEBIM은 .amr 녹음 형식 재생을 지원합니다.</li>
    <li>친구 추가/삭제/조회 로직을 추가했습니다.</li>
    <li>구/신 버전 음성, 파일, 비디오 메시지 통신 문제를 수정했습니다.</li>
    <li>TUIkit 오디오 재생 로직을 최적화했습니다.</li>
    <li>AVChatRoom 방 인원 100명 초과 이후 메시지 수신 오류가 발생하는 문제를 수정했습니다.</li>
    <li>그룹 음소거가 적용되지 않는 문제를 수정했습니다.</li>
    <li>사용자 그룹 내 신분 변경 기능을 수정했습니다.</li>
    <li>그룹 메시지 수신 변경 옵션을 수정했습니다.</li>
    <li>오프라인 푸시 스위치가 적용되지 않는 문제를 수정했습니다.</li>
    <li>사용자 그룹 내 신분 변경 기능을 수정했습니다.</li>
    <li>그룹 미결 및 완결 요청 정보 가져오기에 대한 반환이 정확하지 않은 문제를 수정했습니다.</li>
    <li>클라이언트 백그라운드 이동 시 Crash가 발생하는 문제를 수정했습니다.</li>
    <li>네트워크 재연결 후, 메시지를 받지 못하는 문제를 수정했습니다.</li>
    <li>간혹 메시지 정렬 오류가 발생하는 문제를 수정했습니다.</li>
    <li>간혹 메시지 발송 실패가 발생하는 문제를 수정했습니다.</li>
    <li>백엔드에서 그룹 해산 후 클라이언트가 관련 명령을 받지 못하는 문제를 최적화했습니다.</li></ul></td>
<td>2019-03</td>
<td>-</td>
</tr> </table>

## 2019년 01월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 4.0 버전 배포(Android, iOS 및 Windows)</td>
<td> 신규 IM 클라이언트 SDK를 배포하여 대규모 네트워크 연결, 메시지 수발신 및 읽지 않음 수 등 문제를 수정하고 네트워크, 메시지 등 중요 기본 모듈의 안정성을 개선했습니다. 또한 오픈소스 TUIKit을 제공하고 고객 액세스 프로세스를 더욱 간소화했습니다.</td>
<td>2019-01-21</td>
<td>-</td>
</tr> </table>

## 2017년 07월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>UGC 쇼트 비디오 지원</td>
<td>UGC 쇼트 비디오 메시지 기능을 지원합니다. 비디오 편집을 통해 콘텐츠 품질 및 사용자 경험을 향상시킬 수 있습니다.</td>
<td>2017-07</td>
<td>-</td>
</tr> </table>

## 2017년 05월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>SDK 3.0 버전 배포</td>
<td> 더 많은 기능, 더 작은 크기, 최적화된 코드 구조를 통해 고객 통합 효율성 및 다운로드 경험을 개선하였습니다.</td>
<td>2017-05</td>
<td>-</td>
</tr> </table>

## 2016년 12월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>다중 인스턴스 강제 오프라인 기능 지원</td>
<td>Web 다중 인스턴스 강제 오프라인 및 Web 클라이언트 고객 서비스 등 시나리오에 대한 요구 사항을 충족합니다.</td>
<td>2016-12</td>
<td>-</td>
</tr> </table>

## 2016년 08월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>브로드캐스트 메시지 기능 지원</td>
<td>전 구성원 브로드캐스트 메시지 푸시를 지원하여, 메시지 전파 효율을 높이고 푸시에 대한 고객의 요구를 충족시킵니다.</td>
<td>2016-08</td>
<td>-</td>
</tr><tr>
<td>멀티 단말 동시 로그인 지원</td>
<td>멀티 단말 동시 로그인을 지원하여, 휴대폰과 PC를 동시에 사용 가능합니다. 이를 통해 사용자 경험을 크게 향상시켰습니다.</td>
<td>2016-08</td>
<td>-</td>
</tr> </table>

## 2016년 05월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>라이브 방송 채팅방 출시</td>
<td>라이브 방송 시나리오에 대해 인원수에 제한이 없는 라이브 방송 채팅방 및 메시지 빈도 제한, 사용자 정의 메시지 등 시나리오에 맞춤형 지원이 가능합니다.</td>
<td>2016-05</td>
<td>-</td>
</tr> </table>

## 2016년 03월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>메시지 푸시 기능 지원</td>
<td>Android 및 iOS 오프라인 푸시 기능을 지원하여, 확실한 메시지 전달과 더 나은 사용자 경험을 보장합니다.</td>
<td>2016-03</td>
<td>-</td>
</tr> </table>

## 2015년 12월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>쇼트 비디오 메시지 유형 지원</td>
<td>쇼트 비디오 메시지 유형을 지원하여, 풍부한 메시지 콘텐츠를 제공합니다.</td>
<td>2015-12</td>
<td>-</td>
</tr> </table>

## 2015년 08월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>Web 플랫폼 지원</td>   
<td>Web 플랫폼의 IM 클라우드 서비스를 지원합니다. 사용자 정의 이모티콘 등 메시지 유형을 추가했습니다.</td>
<td>2015-08</td>
<td>-</td>
</tr> </table>

## 2015년 07월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>Windows 플랫폼 지원</td>
<td>Windows 플랫폼의 IM 클라우드 서비스를 지원합니다. 지리적 위치, 음성 등 메시지 유형을 추가했습니다.</td>
<td>2015-07</td>
<td>-</td>
</tr> </table>

## 2015년 05월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th>
</tr> <tr>
<td>IM(기존 명칭: Cloud Communication) 출시</td>
<td>Android 및 iOS IM 클라우드 서비스를 지원합니다. 이미지, 텍스트, 이모티콘 등 다양한 메시지 유형을 지원합니다.</td>
<td>2015-05</td>
<td>-</td>
</tr> </table>




