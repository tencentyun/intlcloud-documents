## 작업 배경
CentOS 6은 2020년 11월 30일에 EOL(단종)되었으며 Linux 커뮤니티에서 더 이상 유지 관리하지 않습니다. 따라서 CentOS 6 소스는 `http://mirror.centos.org/centos-6/` 및 타사 이미지 사이트에서 사용할 수 없습니다. Tencent Cloud 사이트 `http://mirrors.tencent.com/` 및 `http://mirrors.tencentyun.com/`에서는 CentOS 6 소스를 얻을 수 없습니다. Tencent Cloud에 구성된 기본 CentOS 6 소스를 계속 사용하면 오류가 발생할 수 있습니다.

<dx-alert infotype="explain" title="">
운영 체제를 CentOS 7 이상 버전으로 업그레이드하는 것이 좋습니다. 여전히 CentOS 6 종속성을 사용해야 하는 경우 아래 안내에 따라 CentOS 6 소스를 전환합니다.
</dx-alert>


## 작업 단계
1. [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436). 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수 있습니다.
	- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
	- [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)
2. 아래 명령어를 실행하여 현재 운영 체제 CentOS의 버전을 조회합니다.
```shellsession
cat /etc/centos-release
```
반환된 결과가 아래 이미지와 같을 경우 현재 운영 체제 버전은 CentOS 6.9입니다.
![](https://main.qcloudimg.com/raw/de65529a43dc5bfee695c08d5f7bff80.png)
3. 다음 명령어를 실행하여 `CentOS-Base.repo` 파일을 편집합니다.
```shellsession
vim /etc/yum.repos.d/CentOS-Base.repo 
```
4. **i**를 클릭해 편집 모드로 전환한 뒤, CentOS 버전 및 네트워크 환경에 따라 baseurl을 수정합니다.
<dx-alert infotype="explain" title="">
[인트라넷 서비스](https://intl.cloud.tencent.com/document/product/213/5225)와 [공용망 서비스](https://intl.cloud.tencent.com/document/product/213/5224)를 참고하여 인스턴스에 필요한 소스를 결정합니다.
- 사설망 액세스 소스: `http://mirrors.tencentyun.com/centos-vault/6.x/`
- 공중망 액세스 소스: `https://mirrors.cloud.tencent.com/centos-vault/6.x/`
</dx-alert>
여기에서는 CentOS 6.9를 인스턴스 운영 체제로 내부 네트워크 액세스를 예로 들어 설명합니다. 수정 완료 후 <code>CentOS-Base.repo</code> 파일은 아래 그림과 같습니다:
<img src="https://main.qcloudimg.com/raw/1d2485a9be0df6d5f7c46151fc50d73b.png"/>
설정은 다음과 같으며 필요에 따라 얻을 수 있습니다.
```plaintext
[extras]
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/centos/RPM-GPG-KEY-CentOS-6
enabled=1
baseurl=http://mirrors.tencentyun.com/centos-vault/6.9/extras/$basearch/
name=Qcloud centos extras - $basearch
[os]
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/centos/RPM-GPG-KEY-CentOS-6
enabled=1
baseurl=http://mirrors.tencentyun.com/centos-vault/6.9/os/$basearch/
name=Qcloud centos os - $basearch
[updates]
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/centos/RPM-GPG-KEY-CentOS-6
enabled=1
baseurl=http://mirrors.tencentyun.com/centos-vault/6.9/updates/$basearch/
name=Qcloud centos updates - $basearch
```
5. **ESC**를 클릭해 **:wq**를 입력한 뒤, **Enter**를 눌러 수정 내용을 저장합니다.
6. 다음 명령어를 실행하여 `CentOS-Epel.repo` 파일을 수정합니다.
```shellsession
vim /etc/yum.repos.d/CentOS-Epel.repo 
```
7. **i**를 클릭해 편집 모드로 전환한 뒤, 인스턴스 및 네트워크 환경에 따라 baseurl을 수정합니다.
여기에서는 내부 네트워크 액세스를 예로 들어 설명하고 있습니다. 즉, `baseurl=http://mirrors.tencentyun.com/epel/$releasever/$basearch/`를 `baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/`로 수정하면 됩니다. 수정 완료 후는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/9c4b3eaf65d005b3d6819f013037443d.png)
설정은 다음과 같으며 필요에 따라 얻을 수 있습니다.
```plaintext
[epel]
name=epel for redhat/centos $releasever - $basearch
failovermethod=priority
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/epel/RPM-GPG-KEY-EPEL-6
enabled=1
baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/
```
8. **ESC**를 클릭해 **:wq**를 입력한 뒤, **Enter**를 눌러 수정 내용을 저장합니다.
9. 이제 YUM 발신자 주소 전환이 완료되어 `yum install` 명령을 사용해 필요한 소프트웨어를 설치할 수 있습니다.


