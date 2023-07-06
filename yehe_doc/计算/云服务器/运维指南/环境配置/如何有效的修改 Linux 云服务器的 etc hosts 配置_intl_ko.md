## 작업 시나리오

2018년 3월 1일부터 Tencent Cloud에서 제공하는 Linux 공개 이미지에는 오픈 소스 툴 Cloud-Init이 사전 설치되어 있으며, 인스턴스의 모든 초기화 작업은 Cloud-Init을 통해 수행되므로, 인스턴스 내부의 작업이 더 투명해집니다. 자세한 내용은 [Init 및 Cloudbase-init](https://intl.cloud.tencent.com/document/product/213/19670)을 참고하십시오.
Cloud-Init은 **시작할 때마다** `/etc/cloud/templates/hosts.${os_type}.tmpl` 템플릿에 따라 새 `/etc/hosts` 파일을 생성하고 관련된 인스턴스의 기존 `/etc/hosts` 파일을 덮어씁니다. 따라서 인스턴스의 내부 `/etc/hosts` 구성을 수동으로 수정하고 다시 시작하면 `/etc/hosts` 구성이 원래 기본 구성으로 돌아갑니다.

## 전제 조건
Tencent Cloud는 **2018년 9월 이후 공용 이미지를 사용**하여 생성된 인스턴스에 대해 이 문제를 수정했으며 `/etc/hosts` 구성을 덮어쓰지 않습니다.
**2018년 9월 이전**에 생성된 인스턴스의 경우 아래 단계에 따라 수정하십시오.

## 작업 단계

### 솔루션1 
1. Linux CVM에 로그인합니다.
2. 다음 명령을 실행하여 `/etc/cloud/cloud.cfg` 구성 파일의 `- update_etc_hosts`를 `- ['update-etc-hosts', 'once-per-instance']`로 변경합니다.
```shellsession
sed -i "/update_etc_hosts/c \ - ['update_etc_hosts', 'once-per-instance']" /etc/cloud/cloud.cfg
```
3. 다음 명령을 실행하여 `/var/lib/cloud/instance/sem/` 경로 아래에 `config_update_etc_hosts` 파일을 생성합니다.
```shellsession
touch /var/lib/cloud/instance/sem/config_update_etc_hosts
```

### 솔루션2


<dx-alert infotype="explain" title="">
이 솔루션은 CentOS 7.2 운영 체제를 예로 들어 설명합니다.
</dx-alert>


#### hosts 템플릿 파일 경로 가져오기
1. Linux CVM에 로그인합니다.
2. 다음 명령을 실행하여 시스템 hosts 템플릿 파일을 봅니다.
```shellsession
cat /etc/hosts
```
hosts 템플릿 파일은 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/f51f9c53004574f72d32f5ed790c8563.png)


#### hosts 템플릿 파일 수정


<dx-alert infotype="explain" title="">
예를 들어 127.0.0.1 test test를 추가하면 필요에 따라 hosts 템플릿과 /etc/hosts 파일을 수정할 수 있습니다.
</dx-alert>


1. 다음 명령을 실행하여 hosts 템플릿 파일을 수정합니다.
```shellsession
vim /etc/cloud/templates/hosts.redhat.tmpl
```
2. **i**를 눌러 편집 모드로 전환합니다.
3. 파일 끝에 다음 내용을 추가합니다.
```shellsession
127.0.0.1 test test
```
4. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 닫습니다.

#### /etc/hosts 파일 수정
1. 다음 명령을 실행하여 `/etc/hosts` 파일을 수정합니다.
```shellsession
vim /etc/hosts
```
2. **i**를 눌러 편집 모드로 전환합니다.
3. 파일 끝에 다음 내용을 추가합니다.
```shellsession
127.0.0.1 test test
```
4. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 닫습니다.

