## 작업 시나리오
본 문서에서는 SSH 키 생성, 바인딩 및 바인딩 해제, 수정 및 삭제 등 SSH 키 쌍을 사용한 인스턴스 로그인과 관련된 일반적인 작업에 대해 소개합니다.

<dx-alert infotype="notice" title="">
SSH 키를 인스턴스에 바인딩하거나 바인딩을 해제하려면 먼저 인스턴스를 종료합니다. [인스턴스 셧다운](https://intl.cloud.tencent.com/document/product/213/4929)을 참고하십시오.
</dx-alert>

## 작업 단계

### SSH 키 생성[](id:creatSSH)
1. CVM 콘솔에 로그인한 뒤, 왼쪽 사이드바에서 **[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)** 를 선택합니다.
2. ‘SSH 키’ 페이지에서 **키 생성**을 클릭합니다.
3. ‘SSH 키 생성’ 팝업 창에서 키를 구성합니다. 다음 이미지 참고:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4dCL899_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421162143.png)
 - **생성 방법**:
    - **새 키 쌍 생성**을 선택하고, 키 이름을 입력합니다.
    - **기존 공개키 가져오기**를 선택하고, 키 이름과 기존의 공개키 정보를 입력합니다.
<dx-alert infotype="notice" title="">
자체 비밀번호가 없는 공개키를 사용해야 합니다. 그렇지 않으면 콘솔을 통해 인스턴스에 로그인할 수 없습니다.
</dx-alert>
 - **키 이름**: 사용자 정의 이름입니다.
 - **태그(옵션)**: 리소스의 분류, 검색 및 취합을 위해 필요에 따라 키에 태그를 추가할 수 있습니다. 자세한 내용은 [Overview](https://intl.cloud.tencent.com/document/product/651/13334)를 참고하십시오.
4. **확인**을 클릭하여 생성을 완료합니다.
<dx-alert infotype="notice" title="">
**확인**을 클릭하면 개인키가 자동으로 다운로드됩니다. Tencent Cloud는 사용자의 개인키 정보를 보관하지 않습니다. 개인키 파일을 분실하면 다시 생성하고 인스턴스에 다시 바인딩해야 합니다. 개인키를 안전한 곳에 잘 보관하십시오.
</dx-alert>

### 인스턴스에 키 바인딩[](id:bindingSSH)
1. CVM 콘솔에 로그인한 뒤, 왼쪽 사이드바에서 **[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)** 를 선택합니다.
2. **SSH 키** 페이지에서 대상 SSH 키 우측의 **인스턴스 바인딩**을 클릭합니다. 다음 이미지 참고:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wQxy755_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421163951.png)
3. 팝업 창에서 대상 리전과 인스턴스를 선택하고 **바인딩**을 클릭합니다.


### 인스턴스에서 키 바인딩 해제
1. CVM 콘솔에 로그인한 뒤, 왼쪽 사이드바에서 **[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)** 를 선택합니다.
2. ‘SSH 키’ 페이지에서 대상 SSH 키 우측의 **인스턴스 바인딩 해제**를 클릭합니다. 다음 이미지 참고:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vvPz605_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421164006.png)
3. 팝업 창에서 키에서 바인딩 해제할 리전과 인스턴스를 선택하고 **바인딩 해제**를 클릭합니다.


### SSH 키 이름 또는 설명 수정
1. CVM 콘솔에 로그인한 뒤, 왼쪽 사이드바에서 **[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)** 를 선택합니다.
2. ‘SSH 키’ 페이지에서 키 이름 우측의 <img  style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/9db81482f9242417d94a04f314b42b19.png"/>을(를) 선택합니다. 다음 이미지 참고:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/JIYj454_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421164231.png)
3. ‘키 수정’ 팝업 창에서 새 키 이름 또는 키 설명을 입력하고 **확인**을 클릭합니다.

### SSH 키 삭제

<dx-alert infotype="notice" title="">
SSH 키는 CVM 인스턴스 또는 사용자 지정 이미지와 바인딩된 경우 삭제할 수 없습니다.
</dx-alert>

1. CVM 콘솔에 로그인한 뒤, 왼쪽 사이드바에서 **[SSH 키](https://console.cloud.tencent.com/cvm/sshkey)** 를 선택합니다.
2. ‘SSH 키’ 페이지에서 필요에 따라 단일 또는 여러 SSH 키를 삭제할 수 있습니다.
<dx-tabs>
::: 단일 키 삭제
    1. 삭제할 SSH 키 우측의 **삭제**를 클릭합니다. 다음 이미지 참고:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wj58904_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421164021.png)
    2. 키 삭제 팝업 창에서 **확인**을 클릭합니다.
   

:::
::: 키 일괄 삭제
    1. 삭제할 SSH 키를 선택하고 목록 위의 **삭제**를 클릭하여 일괄 삭제합니다.
        2. 키 삭제 팝업 창에서 **확인**을 클릭합니다. 다음 이미지 참고:
        선택한 보안키 쌍에 삭제할 수 없는 키 쌍이 포함되어 있는 경우, 삭제가 가능한 키 쌍만 삭제됩니다.
![](https://main.qcloudimg.com/raw/bfcdfb401f8906834b02372d3e50dbe0.png)
		
:::
</dx-tabs>

## 관련 작업

### SSH 키를 사용해 Linux CVM에 로그인

1. [SSH 키 생성](#creatSSH)
2. [SSH 키를 CVM 인스턴스에 바인딩](#bindingSSH)
3. [SSH를 사용하여 Linux 인스턴스에 로그인
](https://intl.cloud.tencent.com/document/product/213/32501).

### 키 태그 편집

SSH 키에 태그 추가, 수정 또는 삭제 작업을 진행하려면 다음 단계를 참고하십시오. 태그에 대한 자세한 내용은 [Overview](https://intl.cloud.tencent.com/document/product/651/13334)를 참고하십시오. 

1. ‘SSH 키’ 페이지에서 키 우측의 **태그 편집**을 클릭합니다. 다음 이미지 참고:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nwtQ886_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421163834.png)
2. ‘태그 편집’ 팝업 창에서 필요에 따라 작업을 수행합니다.
3. 조정 후 **확인**을 클릭합니다.

