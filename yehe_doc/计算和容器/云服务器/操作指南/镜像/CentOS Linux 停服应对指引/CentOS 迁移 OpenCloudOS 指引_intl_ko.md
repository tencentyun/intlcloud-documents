## 작업 시나리오



|---------|---------|---------|


CentOS 8 인스턴스를 사용 중인 경우 본 문서를 참고하여 OpenCloudOS 8로 교체할 수 있습니다.
## 버전 설명


 
|---------|---------|
 





## 참고 사항
- 다음과 같은 경우 마이그레이션 미지원
 - 그래픽 인터페이스가 설치됨.
 - i686용 rpm 패키지가 설치됨.
- 다음과 같은 상황은 마이그레이션 후 비즈니스의 정상적인 실행에 영향을 미칠 수 있습니다.
 - 작업 프로그램을 설치했으며 타사 rpm 패키지에 종속된 경우.
 
 

- 마이그레이션은 데이터 디스크에 영향을 주지 않으며 OS 수준의 업그레이드일 뿐이며 데이터 디스크에 대한 작업은 수행하지 않습니다.

## 리소스 요구 사항
-  여유 메모리가 500MB 이상.
- 시스템 디스크 잔여 공간 10GB 이상.

## 작업 단계
[](id:Prepare)
## 마이그레이션 준비
마이그레이션 작업은 되돌릴 수 없으며 작업 데이터의 보안을 위해 마이그레이션을 수행하기 전에 [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755)을 통해 시스템 디스크 데이터를 백업하는 것이 좋습니다.


```plaintexy
# cat <<EOF | sudo tee /tmp/centos8_vault.repo
[c8_vault_baseos]
name=c8_vault - BaseOS
baseurl=https://mirrors.cloud.tencent.com/centos-vault/8.5.2111/BaseOS/\$basearch/os/
gpgcheck=0
enabled=1
[c8_vault_appstream]
name=c8_vault - AppStream
baseurl=https://mirrors.cloud.tencent.com/centos-vault/8.5.2111/AppStream/\$basearch/os/
gpgcheck=0
enabled=1
EOF
# yum -y install python3 --disablerepo=* -c /tmp/centos8_vault.repo --enablerepo=c8_vault*
```

### 마이그레이션 실행

1. 타깃 CVM에 로그인합니다. 자세한 내용은 [표준 로그인 방식으로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.

```plaintexy
yum install -y python3
```

```plaintexy
#x86 버전
wget https://mirrors.opencloudos.tech/opencloudos/8.6/AppStream/x86_64/os/Packages/migrate2opencloudos-1.0-1.oc8.noarch.rpm
#arm 버전
wget https://mirrors.opencloudos.tech/opencloudos/8/AppStream/aarch64/os/Packages/migrate2opencloudos-1.0-1.oc8.noarch.rpm 
```
4. 다음 명령을 실행하여 마이그레이션 툴을 설치합니다. 이 명령은 /usr/sbin 아래에 migrate2tencentos.py를 생성합니다.
```plaintexy
rpm -ivh migrate2opencloudos-1.0-1.oc8.noarch.rpm
```
5. 다음 명령을 실행하여 마이그레이션을 시작합니다.
```plaintexy
python3 /usr/sbin/migrate2opencloudos.py -v 8
```
마이그레이션에는 다소 시간이 소요됩니다. 잠시만 기다려 주십시오. 스크립트 실행 완료 후, 다음과 같은 정보가 출력되면 마이그레이션이 완료되었음을 알 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c0118f0b4c20ee45ace4258b44238da2.png)
6. 인스턴스 재부팅의 자세한 내용은 [인스턴스 재기동](https://intl.cloud.tencent.com/document/product/213/4928)을 참고하십시오.
7. 마이그레이션 결과를 확인합니다.
 1. 다음 명령어를 실행하여 os-release를 확인합니다.
```plaintexy
cat /etc/os-release
```
다음 이미지와 같은 정보 반환:
![](https://qcloudimg.tencent-cloud.cn/raw/c345e844566068d5035d32fd7af9401f.png)
 2. 다음 명령어를 실행하여 커널을 확인합니다.
```plaintexy
uname -r
```
다음 이미지와 같은 정보 반환:
![](https://qcloudimg.tencent-cloud.cn/raw/ed944b071b0a202763a2096ebf766533.png)
커널은 최신 버전의 yum으로 기본 설정되어 있으므로 실제 반환 결과를 참고하십시오.
 3. 다음 명령어를 실행하여 yum을 확인합니다.
```plaintexy
yum makecache
```
다음 이미지와 같은 정보 반환:
![](https://qcloudimg.tencent-cloud.cn/raw/0e5dd8b1311c7f5b6522b201233bb1f9.png)

