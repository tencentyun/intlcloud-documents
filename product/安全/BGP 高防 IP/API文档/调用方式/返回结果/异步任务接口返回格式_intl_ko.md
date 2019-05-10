

새로운 버전의 API(현재는 CVM과 같은 부분 비즈니스에만 사용 가능)에는 비동기 작업 API에 대한 개념 정의가 존재하지 않습니다. 구체적인 사용 방법은 각 Action 문서에서 더 자세하게 다룰 예정입니다.

## 일반 비동기작업 API의 반환결과 형식
1회 요청은 1개 리소스의 비동기 작업 API를 조작할 수 있습니다(예를 들어 로드밸런서 생성, 서버 운영 체제 리셋 등).

<table>
   <tr>
      <th>이름</th>
      <th>유형</th>
      <th>설명</th>
      <th>필수 여부</th>
   </tr>
   <tr>
      <td>code</td>
      <td>Int</td>
      <td>반환 결과의 오류 코드, 0은 성공, 기타 값은 실패를 의미합니다.</td>
      <td>네</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>반환 결과의 오류 정보</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td>requestId</td>
      <td>String</td>
      <td>작업 번호</td>
      <td>네</td>
   </tr>
</table>

## 배치 비동기작업 API의 반환결과 형식
1회 요청은 여러 개의 리소스 비동기 작업 API를 조작할 수 있습니다(예를 들어 비밀번호 수정, 기기 부팅, 기기 정지 등).

<table>
   <tr>
      <th>이름</th>
      <th>유형</th>
      <th>설명</th>
      <th>필수 여부</th>
   </tr>
   <tr>
      <td>code</td>
      <td>Int</td>
      <td>반환 결과의 오류 코드, 0은 성공, 기타 값은 실패를 의미합니다.</td>
      <td>네</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>반환 결과의 오류 정보</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td>detail</td>
      <td>Array</td>
      <td>리소스 ID를 key로 사용하여, 해당 리소스에 대해 조작한 code, message, requestId를 반환됩니다.</td>
      <td>네</td>
   </tr>
</table>

예:

```
{
	"code": 0,
	"message": "success",
	"detail": {
		"qcvm6a456b0d8f01d4b2b1f5073d3fb8ccc0": {
			"code": 0,
			"message": "",
			"requestId": "1231231231231"
		}
	}
}
```
>
>- 리소스 전체 조작 성공, 가장 바깥쪽 code는 0입니다.
>- 리소스 전체 조작 실패, 가장 바깥쪽 code가 5100을 반환합니다.
>- 리소스 부분 조작 실패, 가장 바깥쪽 code가 5400을 반환합니다. 이런 상황에서 터미널은 detail을 통해 실패한 조작에 대한 정보를 얻을 수 있습니다.

