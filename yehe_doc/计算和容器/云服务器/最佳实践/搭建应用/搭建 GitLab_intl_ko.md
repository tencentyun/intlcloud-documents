## 작업 시나리오
GitLab은 Ruby를 사용하여 개발한 오픈 소스 버전의 관리 시스템으로, Git를 소스 관리 툴로 삼아, 자가 호스팅 Git 프로젝트 리포지토리를 구현할 수 있으며, Web 인터페이스를 통해 오픈 또는 개인 프로젝트에 액세스할 수 있습니다. 본 문서에서는 Tencent Cloud CVM에 GitLab을 설치하고 또한 이를 사용하는 방법에 대해 소개합니다.



## 예시 버전
- GitLab: 커뮤니티 버전 14.6.2 
- 본문의 CVM 설정은 다음과 같습니다.
	- vCPU: 듀얼코어
	- 메모리: 4GB
	- Linux 운영 체제: CentOS 8.2 및 CentOS 7.9를 예시로 사용합니다.

## 전제 조건
- Linux CVM을 구입 완료해야 합니다.
- Linux 인스턴스에 보안 그룹 규칙(80 포트 개방)이 설정되어 있어야 합니다. 자세한 내용은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하십시오.

## 작업 단계
### GitLab 설치
1. 인스턴스에 로그인합니다. 자세한 내용은 [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.
2. 실제 운영 체제에 따라 다음 명령을 실행하여 종속 패키지를 설치합니다.
<dx-tabs>
::: CentOS 8.2
```
yum install -y curl policycoreutils-python-utils openssh-server
```
:::
::: CentOS 7.9
```
yum install -y curl policycoreutils-python openssh-server
```
:::
</dx-tabs>
3. 다음 명령어를 순서대로 실행하여 부팅 시 SSH 자동 실행으로 설정하고 SSH 서비스를 실행합니다.
```
systemctl enable sshd
```
```
systemctl start sshd
```
4. 다음 명령어를 실행하여 Postfix를 설치합니다.
```
yum install -y postfix
```
5. 다음 명령어를 실행하여 부팅 시 Postfix 자동 실행으로 설정합니다.
```
systemctl enable postfix
```
6. 다음 명령어를 실행하여 Postfix의 구성 파일 main.cf를 엽니다.
```
vim /etc/postfix/main.cf
```
7. **i**를 눌러 편집 모드로 이동하고, `inet_interfaces = all` 앞의 `#`을 삭제한 다음, `inet_interfaces = localhost` 앞에 `#`을 추가합니다. 수정이 완료되면 아래 이미지와 같습니다. 
![](https://main.qcloudimg.com/raw/57fa73bdcd05343b5dcee24e47b5f09a.png)
8. **Esc**를 누르고 **:wq**를 입력하여 수정된 내용을 저장하고 종료합니다.
9. 다음 명령어를 실행하여 Postfix를 실행합니다.
```
systemctl start postfix
```
10. 다음 명령어를 실행하여 GitLab 소프트웨어 패키지의 리포지토리를 추가합니다.
```
 curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
```
11. 다음 명령어를 실행하여 GitLab을 설치합니다.
```
sudo EXTERNAL_URL="인스턴스 공인 IP 주소" yum install -y gitlab-ce
```
인스턴스의 공인 IP 획득 방법은 [공인 IP 주소 획득](https://intl.cloud.tencent.com/document/product/213/17940)을 참고하십시오.
12. 로컬 브라우저에서 획득한 공인 IP에 액세스하여 반환되는 페이지가 아래 이미지와 같다면, GitLab 설치에 성공했음을 의미합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/abaf3b700a58ed5b4a1e13e9d82eaf7e.png"/>


### 관리자 계정 비밀번호 설정
1. 관리자 계정의 기본 암호를 가져옵니다.
 인스턴스에 로그인하고 다음 명령을 실행하여 관리자 'root' 계정의 로그인 비밀번호를 가져옵니다.
```
cat /etc/gitlab/initial_root_password
```
아래 이미지와 같이 비밀번호를 가져옵니다.
![](https://qcloudimg.tencent-cloud.cn/raw/01bfa701452cc470fbdbfb82ab294237.png)
2. GitLab에 로그인합니다.
아래 이미지와 같이 로컬 브라우저에서 CVM의 공용 IP에 액세스하여 GitLab 로그인 인터페이스로 이동한 다음, `root` 계정 및 가져온 로그인 비밀번호로 로그인합니다.
3. 관리자 계정 암호를 수정합니다.
기본 비밀번호가 저장되어 있는 파일은 최초 설정 실행 후 24시간이 지나면 자동으로 삭제됩니다. 'root' 계정 로그인 비밀번호를 최대한 빨리 수정하십시오.
 1. 페이지 오른쪽 상단에서 사용자 프로필을 선택하고 팝업 메뉴에서 **Perferences**을 선택합니다.
 2. ‘User Settings’ 페이지의 왼쪽 사이드바에서 **Password**를 선택합니다.
 3. 페이지에 현재 비밀번호, 새 비밀번호를 입력하고, 새 비밀번호를 확인한 후 **Save Password**를 클릭합니다. 아래 이미지와 같습니다.
 ![](https://qcloudimg.tencent-cloud.cn/raw/25adb5b68d48873392684d1a1030bbe1.png)

### 프로젝트 생성
1. 'root' 계정과 설정된 로그인 비밀번호를 사용하여 로그인합니다.
2. 아래 이미지와 같이 페이지 안내에 따라 개인 프로젝트를 생성하며, 본 문서는 `test`를 예로 듭니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a6d85a83b86a44c1f39dbd363a3311ce.png)
3. 프로젝트 생성 완료 후 페이지 상단의 **Add SSH Key**를 클릭합니다.
4. 'SSH Keys' 페이지로 이동하여 아래의 순서에 따라 SSH Keys를 추가합니다.
 1. [키 획득](#getKey)을 통해 프로젝트 관리에 들어갈 PC의 키 정보를 획득하고 'Key'에 붙여넣습니다.
 2. 'Title'에 해당 키의 이름을 사용자가 지정합니다.
 3. 아래 이미지와 같이 **Add key**를 클릭하고 키를 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/504b7a69215471516f7ace36bb5606af.png)
아래 이미지와 같다면 키 추가에 성공했음을 의미합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2d46dcb48b51243ce4fc91b319b3ede3.png)
5. [](id:Step5) 프로젝트 메인 페이지로 돌아가 **clone**을 클릭하여 프로젝트 주소를 기록합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9edb130321b5df140cfc863c73f6837d.png)


### 프로젝트 클론
1. 관리에 들어간 PC에서 다음 명령어를 실행하여 git 리포지토리를 사용할 사용자 이름을 설정합니다.
```
git config --global user.name "username" 
```
2. 다음 명령어를 실행하여 git 리포지토리를 사용할 사용자의 메일을 설정합니다.
```
git config --global user.email "xxx@example.com" 
```
3. 다음 명령어를 실행하여 프로젝트를 클론합니다. 그 중에서 '프로젝트 주소'를 [5단계](#Step5)에서 획득한 프로젝트 주소로 교체하십시오.
```
git clone '프로젝트 주소'
```
프로젝트 클론을 완료하면 로컬에 동일한 이름의 디렉터리가 생성되며 프로젝트 안에 있는 모든 파일이 포함됩니다.

### 파일 업로드
1. 다음 명령어를 실행하여 프로젝트 디렉터리로 이동합니다.
```
cd test/
```
2. 다음 명령어를 실행하여 GitLab에 업로드할 타깃 파일을 생성합니다. 본 문서는 test.sh를 예로 듭니다.
```
echo "test" > test.sh
```
3. 다음 명령어를 실행하여 test.sh 파일을 인덱스에 추가합니다.
```
git add test.sh
```
4. 다음 명령어를 실행하여 test.sh를 로컬 리포지토리에 제출합니다.
```
git commit -m "test.sh"
```
5. 다음 명령어를 실행하여 test.sh를 GitLab 서버에 동기화합니다.
```
git push
```
아래 이미지와 같이 test 프로젝트 페이지로 돌아가면 파일 업로드에 성공했음을 바로 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0440c9a53b3a93d056119fd47f39638e.png)

## 관련 작업
### 키 가져오기[](id:getKey)
1. 프로젝트 관리에 들어갈 PC에서 다음 명령어를 실행하여 Git를 설치합니다.
```
yum install -y git
```
2. 다음 명령어를 실행하여 키 파일 .ssh/id_rsa를 생성합니다. 키 파일을 생성하는 과정에서 **Enter**를 눌러 기본 설정을 유지합니다.
```
ssh-keygen
```
3. 다음 명령어를 실행하여 키 정보를 조회 및 기록합니다.
```
cat .ssh/id_rsa.pub
```
