## 기능 소개
CDN 상에서 배포한 콘텐츠는 기본적으로 공개 리소스이며, Tencent Cloud CDN은 악의적인 사용자가 콘텐츠를 도용해 이익을 취할 수 없도록 URL 인증 설정을 지원합니다.

## 알고리즘 설명
### TypeA
- 액세스 URL 형식: `http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`
- 알고리즘 설명:
  - timestamp: 10진법(UNIX 타임스탬프).
  - rand: 랜덤 문자열, 0~100자리의 랜덤 문자열, 대소문자 및 숫자로 구성됩니다.
  - uid: 0
  - md5hash: MD5(파일 경로-timestamp-rand-uid- 사용자 지정 키).

> !초기 요청 URL이 `http://www.test.com/test/1.jpg`인 경우 MD5 계산 시의 파일 경로는 `/test/1.jpg`입니다.

### TypeB
- 액세스 URL 형식: `http://DomainName/timestamp/md5hash/FileName`
- 알고리즘 설명:
  - timestamp: 타임스탬프. 형식은 YYYYMMDDHHMM입니다.
  - md5hash: MD5(사용자 지정 키 + timestamp + 파일 경로).

> !초기 요청 URL이 `http://www.test.com/test/1.jpg`인 경우 MD5 계산 시의 파일 경로는 `/test/1.jpg`입니다.

### TypeC
- 액세스 URL 형식: `http://DomainName/md5hash/timestamp/FileName`
- 알고리즘 설명:
  - timestamp: 16진법(UNIX 타임스탬프).
  - md5hash: MD5(사용자 지정 키 + 파일 경로 + timestamp).

> !초기 요청 URL이 `http://www.test.com/test/1.jpg`인 경우 MD5 계산 시의 파일 경로는 `/test/1.jpg`입니다.

### TypeD
- 액세스 URL 형식: `http://DomainName/FileName?sign=md5hash&t=timestamp`
- 알고리즘 설명:
  - timestamp: 10진법/16진법(UNIX 타임스탬프) 선택 가능.
  - md5hash: MD5(사용자 지정 키 + 파일 경로 + timestamp).

> !초기 요청 URL이 `http://www.test.com/test/1.jpg`인 경우 MD5 계산 시의 파일 경로는 `/test/1.jpg`입니다.

## 설정 가이드
1. [CDN Console](https://console.cloud.tencent.com/cdn)에 로그인하여 왼쪽 메뉴에서 [Domain Management]를 클릭해 관리 페이지로 이동합니다. 목록에서 편집할 도메인이 있는 행을 찾아 작업칸의 [관리]를 클릭하십시오.
![img](https://main.qcloudimg.com/raw/dec7f22ef91890a5d39b969d01437361.png)
2. [보안 설정]을 클릭하면 **인증 설정** 모듈이 나타나며 기본적으로 비활성화 상태입니다.
![image](https://main.qcloudimg.com/raw/7704e3f764d2e99ed61504783bb36b42.png)
3. **인증 설정** 모듈에서 [인증 설정]을 클릭해서 이동합니다. 현재 3가지 유형의 모드를 제공합니다.
> !TypeB 업그레이드 중, 현재 선택 불가.
> 
![img](https://main.qcloudimg.com/raw/e011bc76fafa307013956f9b4f1e3b4c.png)
4. 유형을 선택한 다음 인증 매개변수를 설정할 수 있습니다(**TypeA**).
   - 인증 키: 작업 상황에 따라 문자열을 인증 키로 지정할 수 있습니다.
   - 서명 매개변수: 서명 문자열이 있는 매개변수 명을 설정합니다. 기본값은 **sign**이며 다른 매개변수명으로 지정할 수 있습니다.
   - 유효 시간: 서버 단에서 서명 분석을 통해 나온 **timestamp**에 유효 시간을 더하고 현재 시간과 대조하여 서명이 유효한지 판단합니다.

<img src="https://main.qcloudimg.com/raw/95253c212fcd2028d37d8e2f5f828c41.png"  style="margin: 0px 0px 0px 30px;">

5. 인증 매개변수 설정을 완료한 다음 인증 범위 및 객체를 지정해야 합니다.
![img](https://main.qcloudimg.com/raw/4c89dd4fc8aab848a3ada068794c2977.png)

## 인증 계산기
> ?인증 계산기를 사용하여 요청 경로, 서명의 계산이 정확한지 검사할 수 있습니다.
> 
**인증 설정** 모듈에서 [인증 계산기]를 클릭합니다. 현재 3가지 유형의 모드 제공하며 유형을 선택하고 인증 매개변수를 선택한 후 인증 URL(**TypeA**)을 계산할 수 있습니다.
![img](https://main.qcloudimg.com/raw/8d090ea7b5358120a1e233245e06f885.png)
> !
> - TypeB 업그레이드 중, 현재 선택 불가.
> - 액세스 경로에 중국어 URL이 포함된 경우 먼저 URL 코드를 변환한 다음 인증 설정을 진행해야 합니다.

