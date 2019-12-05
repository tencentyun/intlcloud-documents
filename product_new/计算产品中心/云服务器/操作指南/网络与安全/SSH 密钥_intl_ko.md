## 작업 시나리오
비밀번호는 각 클라우드 서버 인스턴스에 대한 고유한 로그인 근거입니다. 인스턴스의 안전성을 보장하기 위해 Tencent Cloud는 다음 두가지 암호화 로그인 방법을 제공합니다.
- [비밀번호 로그인](https://intl.cloud.tencent.com/document/product/213/6093)
- SSH 키 쌍 로그인

본 문서는 SSH 키 쌍 로그인 인스턴스와 관련된 일반적인 작업을 설명합니다.

## 작업 순서

<span id="creatSSH"></span>
### SSH 키 생성
 1. [클라우드 서버 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
 2. 왼쪽 사이드바에서 【[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)】를 클릭하십시오.
 3. SSH 키 관리 페이지에서 [키 생성]을 클릭하십시오.
 4. SSH 키 생성 창에서 키 생성 방법을 선택하고 관련 정보를 입력한 후 [확인]을 클릭하십시오.
  - 생성 방법에서 "키 쌍 새로 생성"을 선택한다면 키 쌍 이름을 입력하십시오.
  - 생성 방법에서 "기존 키 쌍 사용"을 선택하면 키 이름과 기존의 공개키 정보를 입력하십시오.
 4. 팝업 창에서 [다운로드]를 클릭하여 개인키를 다운로드하십시오.
 > Tencent Cloud는 개인키 정보를 저장하지 않음으로 10분 이내에 개인키를 다운로드하여 받으십시오.
 > 

<span id="bindingSSH"></span>
### 키 바인딩/바인딩 해제 클라우드 서버
 1. [클라우드 서버 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
 2. 왼쪽 사이드바에서 【[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)】를 클릭하십시오.
 3. SSH 키 관리 페이지에서 바인딩/바인딩 해제 클라우드 서버의 SSH 키를 선택하고 [바인딩/바인딩 해제 인스턴스]를 클릭하십시오.
 4. 팝업된 인스턴스 바인딩/바인딩 창에서 영역, 클라우드 서버 바인딩/바인딩 해제를 선택한 후 [확인]을 클릭하십시오.


### SSH 키 이름/설명 수정
 1. [클라우드 서버 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
 2. 왼쪽 사이드바에서 【[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)】를 클릭하십시오.
 3. SSH 키 관리 페이지에서 수정할 키를 선택하고 상단의 [수정]을 클릭하십시오.
 4. 키 수정 창에서 새로운 키 이름과 키 설명을 입력하고 [확인]을 클릭하십시오.

### SSH 키 삭제
> SSH 키가 클라우드 서버 또는 사용자 정의 이미지와 연결된 경우 해당 키를 삭제할 수 없습니다.
>
 1. [클라우드 서버 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
 2. 왼쪽 사이드바에서 【[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)】를 클릭하십시오.
 3. SSH 키 관리 페이지에서 삭제해야 하는 모든 SSH 키를 선택하고 [삭제]를 클릭하십시오.
 4. 팝업된 키 삭제 창에서 [확인]을 클릭하십시오.

### SSH 키를 사용해 Linux 클라우드 서버에 로그인

1. [SSH 키 생성](#creatSSH)
2. [SSH 키를 클라우드 서버에 바인딩](#bindingSSH)
3. [SSH를 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)
