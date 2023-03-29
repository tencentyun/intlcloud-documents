## 프로필 정보 시스템 소개
IM은 사용자 정보 호스팅 기능을 제공하여 프로필 정보와 관련된 완벽한 솔루션을 지원합니다. 모든 사용자가 자신의 프로필 정보를 보유하고 손쉽게 설정, 풀링할 수 있는 환경을 제공하고 싶다면 IM 프로필 정보 호스팅 서비스를 선택하시기 바랍니다.
- IM은 프로필 정보를 저장하여 데이터에 재해 복구, 크로스 리전 배포 및 오토 스케일링 기능을 부여합니다. 이를 통해 서버 다운, 마스터/슬레이브 멀티 복사 및 확장/축소 등 복잡한 처리 프로세스를 손쉽게 해결할 수 있습니다.
- IM은 업계 범용 비즈니스 처리 프로세스를 제공하므로, 사용자 프로필 정보 로직에 대해 걱정할 필요가 없습니다.
- IM은 전문적인 운영 프로세스 및 운영 팀을 통해 연간 99.99%에 이르는 품질 안정성을 보장하여, 사용자에게 검증받은 안정적인 서비스 제공할 수 있도록 합니다. 
- IM은 손쉽게 사용할 수 있는 서비스 인터페이스와 빠른 액세스 가이드를 제공하여 전 과정에서 최고급 서비스를 선사합니다.

IM 프로필 정보 호스팅 서비스를 통해 다음과 같은 기능을 사용할 수 있습니다. 
- 표준 프로필 정보 필드 저장, 읽기/쓰기 기능.
- 사용자 정의 프로필 정보 필드 저장, 읽기/쓰기 기능.

## 프로필 정보 필드
프로필 정보는 사용자 속성을 설명하는 데이터로 IM 데이터 시스템은 표준 프로필 정보 필드와 사용자 정의 프로필 정보 필드를 지원합니다. 프로필 정보 필드는 다음과 같은 특징이 있습니다. 
- 프로필 정보 필드는 Key-Value로 표시됨.
- Key는 String 유형이며, 이름은 영어 알파벳 대소문자, 숫자, 언더바로 구성.
- Value 유형:
   a. uint32_t 유형의 정수(사용자 정의 프로필 정보 필드 미지원)
   b. uint64_t 유형의 정수(사용자 정의 프로필 정보 필드 미지원)
   c. string 유형의 문자열(string 길이 500 바이트 이하)
   d. bytes 유형의 buffer(buffer 길이 500 바이트 이하)

- 모든 Key의 읽기 권한과 쓰기 권한 설정을 지원합니다. 프로필 정보 필드의 읽기/쓰기 권한은 다음과 같습니다. 

<table style="display:table;width:100%">
		<tbody>
			<tr>
			<th style="width:20%;"> 권한 이름</th>
				<th style="width:30%;"> 권한 유형</th>
				<th> 비고</th>
			</tr>
			<tr>
				<td> 읽기 권한</td>
				<td>
					App 읽기 가능<br>
					App 관리자 읽기 가능<br>
				</td>
				<td> 하나 또는 여러 유형의 읽기 권한 선택 가능</td>
			</tr>
			<tr>
				<td> 쓰기 권한</td>
				<td>
					App 쓰기 가능<br>
					App 관리자 쓰기 가능<br>
				</td>
				<td> 하나 또는 여러 유형의 쓰기 권한 선택 가능</td>
			</tr>
		</tbody>
	</table>

## 표준 프로필 정보 필드

IM은 다음과 같은 표준 프로필 정보 필드를 지원합니다. 

<table style="display:table;width:100%">
		<tbody>
			<tr>
			<th style="width:15%;"> 필드 이름</th>
				<th style="width:5%;"> 유형</th>
				<th style="width:10%;"> 설명</th>
				<th style="width:19%;"> 업데이트 Push</th>
				<th> 비고</th>
			</tr>
			<tr>
				<td> Tag_Profile_IM_Nick</td>
				<td> string</td>
				<td> 닉네임</td>
				<td> 있음</td>
				<td> 최대 길이: 500 바이트</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_Gender</td>
				<td> string</td>
				<td> 성별</td>
				<td> 있음</td>
				<td>
					Gender_Type_Unknown: 성별 미설정<br>
					Gender_Type_Female: 여성<br>
					Gender_Type_Male: 남성<br>
				</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_BirthDay</td>
				<td> uint32</td>
				<td> 생일</td>
				<td> 있음</td>
				<td>권장 형식: 20190419</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_Location</td>
				<td> string</td>
				<td> 소재지</td>
				<td> 있음</td>
				<td>
					최대 길이: 16 바이트. 권장 사용 방법:<br>
					App의 숫자 세트-지명 간의 매핑 관계 로컬 정의<br>
					백엔드에서 4개의 uint32_t 숫자 저장<br>
					첫 번째 uint32_t는 ‘국가’를 표시<br>
					두 번째 uint32_t는 ‘도’ 또는 ‘지역’을 표시<br>
					세 번째 uint32_t는 ‘시’를 표시<br>
					네 번째 uint32_t는 ‘군’, ‘구’를 표시<br>
				</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_SelfSignature</td>
				<td> string</td>
				<td> 개인 서명</td>
				<td> 있음</td>
				<td> 최대 길이: 500 바이트</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_AllowType</td>
				<td> string</td>
				<td> 친구 추가 인증 방식</td>
				<td> 있음</td>
				<td>
					AllowType_Type_NeedConfirm: 친구 요청 수동 승인 후 친구 추가<br>
					AllowType_Type_AllowAny: 모든 친구 요청 자동 승인<br>
					AllowType_Type_DenyAny: 모든 친구 요청 거부<br>
				</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_Language</td>
				<td> uint32</td>
				<td> 언어</td>
				<td> 있음</td>
				<td> App 로컬에서 숫자와 언어의 매핑 관계를 정의합니다. App 로컬에서 언어에 해당 숫자를 문자로 변환해야 함</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_Image</td>
				<td> string</td>
				<td> 프로필 사진 URL</td>
				<td> 있음</td>
				<td> 최대 길이: 500 바이트</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_AdminForbidType</td>
				<td> string</td>
				<td> 관리자가 친구 추가 태그 지정을 금지함</td>
				<td> 있음</td>
				<td>
					AdminForbid_Type_None: 기본값, 친구 추가 요청 발송 허용<br>
					AdminForbid_Type_SendOut: 친구 추가 요청 발송 금지<br>
				</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_Level</td>
				<td> uint32</td>
				<td> 레벨</td>
				<td> 있음</td>
				<td> 일반적으로 한 개의 UINT-8 데이터는 한 레벨의 정보 저장 가능. <br>분할 저장을 통해 레벨의 여러 역할 정보 저장 가능</td>
			</tr>
			<tr>
				<td> Tag_Profile_IM_Role</td>
				<td> uint32</td>
				<td> 역할</td>
				<td> 있음</td>
				<td> 일반적으로 한 개의 UINT-8 데이터는 한 개의 역할 정보 저장 가능. <br>분할 저장을 통해 여러 역할 정보 저장 가능</td>
			</tr>
		</tbody>
	</table>

## 사용자 정의 프로필 정보 필드
사용자 정의 프로필 정보 필드는 App이 비즈니스 니즈에 따라 설정한 사용자 데이터입니다. App은 사용자 프로필 정보에 부가 데이터를 추가하고, 기존 인터페이스를 통해 읽기/쓰기 작업을 할 수 있습니다. 

### 사용자 정의 프로필 정보 필드 신청
App 관리자는 IM [콘솔](https://console.cloud.tencent.com/im)>**애플리케이션 설정**>**기능 설정**을 통해 사용자 정의 프로필 필드를 신청할 수 있으며 신청 제출 후 5분 내에 적용됩니다. 
사용자 정의 프로필 정보 필드 신청 시, 모든 사용자 정의 프로필 정보 필드는 다음 정보를 제출해야 합니다. 
- 사용자 정의 프로필 필드 이름(Key). 자세한 내용은 [사용자 정의 프로필 정보 필드 이름 생성 규칙](#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5.E7.9A.84.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83)을 참고하십시오.
- 사용자 정의 프로필 필드 유형(Value). 자세한 내용은 [프로필 정보 필드](#.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5)를 참고하십시오.
- 사용자 정의 프로필 정보 필드 읽기 및 쓰기 권한. 자세한 내용은 [프로필 정보 필드](#.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5)를 참고하십시오.

### 사용자 정의 프로필 정보 필드의 이름 생성 규칙
사용자 정의 프로필 정보 필드의 이름 생성 규칙은 다음과 같습니다. 
- 사용자 정의 프로필 정보 필드 이름 구성: 접두사, 키워드.
- 사용자 정의 프로필 정보 필드의 접두사: Tag_Profile_Custom. 
- 키워드: 8바이트 이하의 영어 알파벳으로 구성하며, 영어 단어 또는 약자 사용 권장.
- 예시: App에서 신청하려는 사용자 정의 필드의 키워드가 Test일 경우, 사용자 정의 프로필 정보 필드 이름은 Tag_Profile_Custom_Test가 됨.



