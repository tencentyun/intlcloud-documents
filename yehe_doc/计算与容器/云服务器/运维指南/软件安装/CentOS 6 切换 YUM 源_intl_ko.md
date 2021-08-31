## 작업 배경
CentOS 6 운영 체제 버전 라이프 사이클(EOL)은 2020년 11월 30일로 종료되며, Linux 커뮤니티는 해당 운영 체제 버전에 대한 유지보수를 중단합니다. 커뮤니티 규정에 따라 CentOS 6의 발신지 주소 `http://mirror.centos.org/centos-6/`의 컨텐츠는 이미 삭제되었으며, 현재 타사의 미러 이미지 사이트에서도 CentOS 6의 발신지 주소가 삭제되었습니다. Tencent Cloud의 발신지 주소 `http://mirrors.cloud.tencent.com/ 및 http://mirrors.tencentyun.com/`는 CentOS 6의 발신지 주소와 동기화할 수 없습니다. Tencent Cloud에서 디폴트 설정된 CentOS 6의 발신지 주소를 계속 사용하면 오류가 보고됩니다.



>?  운영 체제를 CentOS 7나 그 이상의 버전으로 업그레이드 할 것을 권장합니다. 업무 전환기에 CentOS 6 운영체제의 일부 설치 패키지를 계속 사용해야 할 경우, 본 문서의 안내에 따라 CentOS 6의 발신자 주소를 전환하십시오.



## 작업 순서
1. [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436). 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수 있습니다.
	- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
	- [SSH를 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)
2. 아래 명령어를 실행하여 현재 운영 체제 CentOS의 버전을 조회합니다.
```
cat /etc/centos-release
```
반환된 결과가 아래 이미지와 같을 경우 현재 운영 체제 버전은 CentOS 6.9입니다.
![](https://main.qcloudimg.com/raw/de65529a43dc5bfee695c08d5f7bff80.png)
3. 다음 명령어를 실행하여 `CentOS-Base.repo` 파일을 편집합니다.
```
vim /etc/yum.repos.d/CentOS-Base.repo 
```
4. **I**을 클릭해 편집 모드로 전환한 뒤, CentOS 버전 및 네트워크 환경에 따라 baseurl을 수정합니다.
>?
>[내부 네트워크 서비스](https://intl.cloud.tencent.com/document/product/213/5225)와 [공용 네트워크 서비스](https://intl.cloud.tencent.com/document/product/213/5224)를 참조하여 인스턴스에 사용할 발신자 주소를 결정할 수 있습니다.
>
>- 내부 네트워크 액세스 주소를 `http://mirrors.tencentyun.com/centos-vault/6.x/`로 전환합니다. 
>- 공용 네트워크 액세스 주소를 `https://mirrors.cloud.tencent.com/centos-vault/6.x/`로 전환합니다.

여기에서는 CentOS 6.9를 인스턴스 운영 체제로 내부 네트워크 액세스를 예로 들어 설명합니다. 수정 완료 후 <code>CentOS-Base.repo</code> 파일은 아래 그림과 같습니다:
<img src="https://main.qcloudimg.com/raw/1d2485a9be0df6d5f7c46151fc50d73b.png"/>
5. **ESC**를 클릭해 **:wq**를 입력한 뒤, **Enter**를 눌러 수정 내용을 저장합니다. 
6. 다음 명령어를 실행하여 `CentOS-Epel.repo` 파일을 수정합니다.
```
vim /etc/yum.repos.d/CentOS-Epel.repo 
```
6. **I**을 클릭해 편집 모드로 전환한 뒤, 인스턴스 및 네트워크 환경에 따라 baseurl을 수정합니다.
여기에서는 내부 네트워크 액세스를 예로 들어 설명하고 있습니다. 즉, `baseurl=http://mirrors.tencentyun.com/epel/$releasever/$basearch/`를 `baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/`로 수정하면 됩니다. 수정 완료 후는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/9c4b3eaf65d005b3d6819f013037443d.png)
7. **ESC**를 클릭해 **:wq**를 입력한 뒤, **Enter**를 눌러 수정 내용을 저장합니다. 
8. 이제 YUM 발신자 주소 전환이 완료되어 `yum install` 명령을 사용해 필요한 소프트웨어를 설치할 수 있습니다.
