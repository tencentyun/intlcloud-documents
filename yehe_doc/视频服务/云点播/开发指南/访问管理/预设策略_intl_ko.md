>!본 문서는 **VOD** CAM 기능에 대한 내용을 소개합니다. 기타 제품의 CAM 관련 내용은 [CAM 지원 제품](https://intl.cloud.tencent.com/document/product/598/10588)을 참고하십시오.

CAM은 기본적으로 서브 계정을 정책과 바인딩하거나 정책을 서브 계정에 부여하는 것입니다. 개발자는 콘솔에서 사전 설정된 정책을 직접 사용하여 간단한 권한 작업을 구현할 수 있으며, 복잡한 권한 작업은 [사용자 정의 정책](https://intl.cloud.tencent.com/document/product/266/33972)을 참고하십시오.

현재 VOD는 다음과 같은 사전 설정 정책을 제공합니다.

|        정책 이름         |       정책 설명       |
| :---------------------: | :------------------: |
|   QcloudVODFullAccess   | VOD에 대한 전체 액세스 |
| QcloudVODReadonlyAccess |  VOD에 대한 읽기 전용 액세스  |

## 사전 설정 정책 사용 예시


### VOD에 대한 전체 액세스 권한이 있는 서브 계정 생성

1. [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [[사용자 리스트]](https://console.cloud.tencent.com/cam) 페이지에 액세스하고 [사용자 생성]을 클릭합니다.
   ![](https://main.qcloudimg.com/raw/e700947b468ef25d4bf70ad1fecc6348.png)
2. ‘사용자 생성’ 페이지에서 서브 계정 아래의 [사용자 정의]을 클릭하여 ‘서브 계정 생성’ 페이지로 들어갑니다.
   ![](https://main.qcloudimg.com/raw/b8351b38a1df79df1836cb62268ecc74.png)
3. [다음]을 클릭하고 사용자 정보를 입력합니다.
   - 사용자 이름을 입력하고 [프로그래밍 액세스] 및 [Tencent Cloud 콘솔 액세스]를 선택한 다음 필요에 따라 다른 옵션을 구성합니다.
   - [다음]을 클릭하고 안내에 따라 실명 인증을 완료합니다.
     ![](https://main.qcloudimg.com/raw/19b98c0b2dde4824d5eeaa52304ea3df.png)
4. 사용자 권한을 설정합니다.
   - 사전 설정 정책 ‘QcloudVODFullAccess’를 검색 및 선택합니다.
   - [다음]을 클릭합니다.
		<img src="https://main.qcloudimg.com/raw/0bd65772428242306300e315537853cd.png" width="704">
5. ‘정보 및 권한 검토’ 열 아래의 [완료]를 클릭합니다. 사용자가 성공적으로 생성되면 아래와 같이 로그인 링크와 보안 자격 증명을 다운로드하여 안전하게 보관하십시오.
   ![](https://main.qcloudimg.com/raw/cc223f380730f8dbfe81caa799be2dfc.png)
<table>
     <tr>
         <th nowrap="nowrap">정보</th>  
         <th nowrap="nowrap">출처</th>  
         <th nowrap="nowrap">기능</th>  
         <th nowrap="nowrap">필수 저장 여부</th>  
     </tr>
	 <tr>      
         <td>로그인 링크</td>   
	     <td>페이지에 복사</td>   
	     <td nowrap="nowrap">루트 계정 입력이 필요없는 편리한 콘솔 로그인</td>   
	     <td>No</td>
     </tr> 
	 <tr>      
         <td nowrap="nowrap">사용자 이름 </td>   
	     <td>CSV 형식의 보안 자격 증명 파일</td>   
	     <td>콘솔 로그인 시 입력</td>   
	     <td>Yes</td>
     </tr> 
	 <tr>      
         <td>비밀번호</td>   
	     <td>CSV 형식의 보안 자격 증명 파일 </td>   
	     <td >콘솔 로그인 시 입력</td>   
	     <td >Yes</td>
     </tr> 
		  <tr>      
         <td>SecretId</td>   
	     <td>CSV 형식의 보안 자격 증명 파일</td>   
	     <td >서버 API 호출에 필요합니다. 자세한 내용은 다음을 참고하십시오: <a href="https://intl.cloud.tencent.com/document/product/598/32675">액세스 키</a></td>   
	     <td >Yes</td>
     </tr> 
	     <tr>      
         <td>SecretKey</td>   
	     <td>CSV 형식의 보안 자격 증명 파일</td>   
	     <td >서버 API 호출에 필요합니다. 자세한 내용은 다음을 참고하십시오: <a href="https://intl.cloud.tencent.com/document/product/598/32675">액세스 키</td>   
	     <td >Yes</td>
     </tr> 
</table>

상기 로그인 링크와 보안 자격 증명을 VOD 사용자에게 제공합니다. 후자는 이 서브 계정을 통해 VOD에서 모든 작업(예: VOD 콘솔 액세스 및 VOD 서버 API 호출)을 수행할 수 있습니다.
>?서브 계정를 만드는 방법에 대한 자세한 내용은 CAM의 [서브 계정 생성](https://intl.cloud.tencent.com/document/product/598/13674) 문서를 참고하십시오.

<span id="p2"></span>
### 기존 서브 계정에 VOD의 전체 권한 부여

1. [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [[사용자 리스트]](https://console.cloud.tencent.com/cam)에 액세스하고 대상 서브 계정을 클릭합니다.
   ![](https://main.qcloudimg.com/raw/86a75ce62dde0ba4c061975181186974.png)
2. 아래와 같이 ‘사용자 세부 정보’ 페이지의 권한 열에서 [정책 추가]를 클릭합니다(실제로 이 페이지에 표시되는 정보는 서브 계정의 기존 권한에 따라 다를 수 있습니다. 서브 계정의 권한이 비어 있지 않으면 [정책 연결]을 클릭하십시오).
   ![](https://main.qcloudimg.com/raw/e775e39eec0292f31a78d5a2332d6d09.png)
3. [정책 목록에서 연결할 정책 선택]을 클릭하고 사전 설정된 정책 `QcloudVODFullAccess`를 검색하여 확인하고 안내에 따라 권한 부여를 완료합니다.

### VOD에 대한 서브 계정 전체 액세스 권한 취소

1. [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [[사용자 리스트]](https://console.cloud.tencent.com/cam)에 액세스하고 대상 서브 계정을 클릭합니다.
   ![](https://main.qcloudimg.com/raw/86a75ce62dde0ba4c061975181186974.png)
2. 사용자 ‘세부 정보’ 페이지의 권한 열에서 사전 설정된 정책 `QcloudVODFullAccess`를 찾아 오른쪽에서 [연결 해제]를 클릭하고 안내에 따라 권한 취소를 완료합니다.
   ![](https://main.qcloudimg.com/raw/4d221c52efe40913031355c877f28a47.png)

