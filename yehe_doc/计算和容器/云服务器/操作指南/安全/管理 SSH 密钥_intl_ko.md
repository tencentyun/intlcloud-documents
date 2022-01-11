## 작업 시나리오
본 문서에서는 SSH 키 생성, 바인딩 및 바인딩 해제, 수정 및 삭제 등 SSH 키 쌍을 사용한 인스턴스 로그인과 관련된 일반적인 작업에 대해 소개합니다.
>!CVM 종료 후 보안키 바인딩 및 바인딩 해제가 가능합니다. [인스턴스 종료](https://intl.cloud.tencent.com/document/product/213/4929)를 참조하여 CVM을 종료하십시오.
>

## 작업 순서

<span id="creatSSH"></span>
### SSH 키 생성
 1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
 2. 왼쪽 메뉴에서 [[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)]를 클릭하십시오.
 3. SSH 키 관리 페이지에서 [보안키 생성]을 클릭하십시오.
>! [확인]을 클릭하면 자동으로 개인키를 다운로드합니다. Tencent Cloud는 사용자의 개인키 정보를 보관하지 않으므로 개인키를 안전한 곳에 잘 보관하십시오.
 > 
![](https://main.qcloudimg.com/raw/a6675ade459e6bf236ff7301995a35f2.png)
  - 생성 방식에서 ‘신규 키 쌍 생성’을 선택한 경우, 보안키 이름을 입력하십시오.
  - 생성 방식에서 ‘기존 공개키 가져오기’를 선택한 경우, 보안키 이름과 기존의 공개키 정보를 입력하십시오.


<span id="bindingSSH"></span>
### 보안키 바인딩 인스턴스
 1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
 2. 왼쪽 메뉴에서 [[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)]를 클릭하십시오.
 3. SSH 키 관리 페이지에서 CVM과 바인딩 할 SSH 키를 선택하고 [인스턴스 바인딩]을 클릭하십시오.
![](https://main.qcloudimg.com/raw/7419df720863aa9463e0dcf478580bbd.png)
 4. 바인딩 인스턴스 팝업창에서 리전을 선택하고 바인딩 할 CVM을 선택한 뒤, [확인]을 클릭하십시오.


### 보안키 바인딩 해제 인스턴스
 1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
 2. 왼쪽 메뉴에서 [[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)]를 클릭하십시오.
 3. SSH 키 관리 페이지에서 CVM과 바인딩을 해제 할 SSH 키를 선택하고 [바인딩 해제 인스턴스]를 클릭하십시오.
![](https://main.qcloudimg.com/raw/263f344c4bea3cdff4e422996821cb5d.png)
 4. 바인딩 해제 인스턴스 팝업창에서 리전을 선택하고 바인딩을 해제 할 CVM을 선택한 뒤, [확인]을 클릭하십시오.


### SSH 키 이름/설명 수정
 1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
 2. 왼쪽 메뉴에서 [[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)]를 클릭하십시오.
 3. SSH 키 관리 페이지에서 보안키 이름 우측의 <img  style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/9db81482f9242417d94a04f314b42b19.png"/>를 선택합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/e4c46354bafa78daa7efa24064eafea9.png)
 4. 보안키 수정 팝업창에 새로운 키 이름과 키 설명을 입력하고 [확인]을 클릭하십시오.

### SSH 키 삭제
>!  SSH 키가 CVM 또는 사용자 정의 이미지와 연결된 경우 해당 키를 삭제할 수 없습니다.
>
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 왼쪽 메뉴에서 [[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)]를 클릭하십시오. 필요에 따라 보안키를 개별 삭제하거나 일괄 삭제할 수 있습니다.
 - **보안키 개별 삭제**
    1. SSH 키 관리 페이지에서 삭제할 SSH 키가 있는 행 우측의 [삭제]를 클릭합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/96d57d5beb3d73c0978cc1464bc73c7e.png)
    2. 보안키 삭제 팝업창에서 [확인]을 클릭합니다.
 - **보안키 일괄 삭제**
    1. SSH 키 관리 페이지에서 삭제할 보안키에 체크하고 페이지 상단의 [삭제]를 클릭하면 보안키를 일괄 삭제합니다.
    2. 보안키 삭제 팝업창에서 [확인]을 클릭합니다. 다음 이미지를 참고하십시오.
    선택한 보안키 쌍에 삭제할 수 없는 키 쌍이 포함되어 있는 경우, 삭제가 가능한 키 쌍만 삭제됩니다.
		![](https://main.qcloudimg.com/raw/bfcdfb401f8906834b02372d3e50dbe0.png)


### SSH 키를 사용한 Linux CVM 로그인

1. [SSH 키 생성](#creatSSH).
2. [SSH 키를 CVM에 바인딩](#bindingSSH).
3. [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501).
