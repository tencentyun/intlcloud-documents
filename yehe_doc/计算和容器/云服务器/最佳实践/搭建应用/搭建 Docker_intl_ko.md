## 작업 시나리오
본문은 Tencent Cloud 클라우드 서비스에서 Docker를 구축하고 사용하는 방법을 소개합니다. 본문의 내용은 Linux 운영 체제에 익숙하고 Tencent Cloud 클라우드 서비스를 사용하기 시작한 개발자에게 적합합니다. Docker에 대한 자세한 내용은 [Docker 공식 홈페이지 문서](https://docs.docker.com/)를 참고하십시오.

<dx-alert infotype="explain" title="">
Windows 운영 체제의 CVM에서 Docker를 빌드 및 사용하려면 [Windows에 Docker 데스크톱 설치](https://docs.docker.com/docker-for-windows/install/)를 참고하십시오.
</dx-alert>



## 예시 운영 체제
본 문서에서는 CVM 인스턴스 운영 체제 CentOS 8.2 및 7.6을 예시로 사용합니다.
TencentOS Server 운영 체제를 사용하는 경우 실제 버전에 해당하는 작업 수행:
  - TencentOS Server 2.4: 이미지가 Docker로 미리 구성되어 있으므로 다시 설치할 필요가 없습니다. [Docker 사용하기](#userDocker)를 참고하여 직접 사용을 시작할 수 있습니다.
  - TencentOS Server 3.1 (TK4): 문서를 참고하여 구축하십시오.

## 전제 조건
구매한 Linux CVM이 있어야 합니다.
<dx-alert infotype="explain" title="">
Docker를 빌드하려면 64비트 시스템을 사용해야 하며 커널 버전은 3.10 이상이어야 합니다.
</dx-alert>



## 작업 단계

### Docker 설치

실제 운영 체제 버전에 따라 다음 단계를 수행합니다.

<dx-tabs>
::: CentOS 8.2
1. [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 다음 명령어를 실행하여 Docker 소프트웨어 보관소를 추가합니다.
```
dnf config-manager --add-repo=http://mirrors.tencent.com/docker-ce/linux/centos/docker-ce.repo
```
3. 다음 명령어를 실행하여 추가된 Docker 소프트웨어 보관소를 확인합니다.
```
dnf list docker-ce
```
4. 다음 명령어를 실행하여 Docker를 설치합니다.
```
dnf install -y docker-ce --nobest
```
5. 다음 명령어를 실행하여 Docker를 실행합니다.
```
systemctl start docker
```
6. 다음 명령어를 실행하여 설치 결과를 확인합니다.
```
docker info
```
다음 정보가 반환되면 설치가 완료된 것입니다.
![](https://main.qcloudimg.com/raw/113b820e4efc6441d88410488441291f.png)
:::
::: CentOS 7.6
1. [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 다음 명령어를 순서대로 실행하여 yum 소스를 추가합니다.
```
yum update
```
```
yum install epel-release -y
```
```
yum clean all
```
```
yum list
```
3. 다음 명령어를 실행하여 Docker를 설치합니다.
```
yum install docker-io -y
```
4. 다음 명령어를 실행하여 Docker를 실행합니다.
```
systemctl start docker
```
5. 다음 명령어를 실행하여 설치 결과를 확인합니다.
```
docker info
```
다음 정보가 반환되면 설치가 완료된 것입니다.
![](https://main.qcloudimg.com/raw/a848737e9d011f528f66dc54fca61c08.png)
:::
</dx-tabs>


### Docker[](id:userDocker) 사용
Docker의 기본 사용 명령어는 다음과 같습니다.
- Docker 데몬을 관리합니다.
 - Docker 데몬을 실행합니다.
```
systemctl start docker
```
 -  Docker 데몬을 중지합니다.
```
systemctl stop docker
```
 - Docker 데몬을 재시작합니다.
```
systemctl restart docker
```
- 이미지를 관리합니다. 본문은 Docker Hub의 Nginx 이미지를 예시로 사용합니다.
```
docker pull nginx 
```
 - 태그 수정 : 이미지 태그를 수정하여 구분을 기억할 수 있습니다.
```
docker tag docker.io/nginx:latest tencentyun/nginx:v1
```
 - 기존 이미지 보기:
```
docker images
```
 - 이미지 강제 삭제:
```
docker rmi -f tencentyun/nginx:v1
```
- 컨테이너 관리.
 - 컨테이너 입력:
```
docker run -it ImageId /bin/bash
```
이 중 `ImageId`는 `docker images` 명령어를 실행하여 얻을 수 있습니다.
 - 컨테이너 종료: 'exit' 명령어를 실행하여 현재 컨테이너를 종료합니다.
 - 백그라운드에서 실행 중인 컨테이너 입력:
```
docker exec -it 컨테이너 ID /bin/bash
```
 - 컨테이너를 이미지로 만듭니다.
```
docker commit <컨테이너 ID 또는 컨테이너 이름> [<레지스트리 이름>[:<태그>]]
```
예시:
```
docker commit 1c23456cd7**** tencentyun/nginx:v2
```

### 이미지 생성

1. 다음 명령어를 실행하여 Dockerfile 파일을 엽니다.
```
vim Dockerfile
```
2. **i**를 눌러 편집 모드로 전환하고 다음을 추가합니다.
```
FROM tencentyun/nginx:v2  #기본 이미지 출처 성명.
MAINTAINER DTSTACK #이미지 소유자 성명.
RUN mkdir /dtstact # RUN 뒤에는 컨테이너가 실행되기 전에 실행해야 하는 명령어를 입력합니다. Dockerfile은 127줄을 넘을 수 없기 때문에 명령어가 많은 경우 스크립트로 작성하여 실행할 것을 권장합니다.
ENTRYPOINT ping https://cloud.tencent.com/ #시작 실행 명령어. 여기서 마지막 명령어는 포그라운드에서 계속 실행할 수 있는 명령어이어야 합니다. 그렇지 않으면 명령어가 백그라운드에서 실행될 때 컨테이너가 종료됩니다.
```
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
4. 다음 명령어를 실행하여 이미지를 빌드합니다.
```
docker build -t nginxos:v1 .  #. Dockerfile 파일의 경로이며 무시할 수 없습니다.
```
5. 다음 명령어를 실행하여 이미지가 성공적으로 생성되었는지 확인합니다.
```
docker images
```
6. 다음 명령어를 순서대로 실행하여 컨테이너를 실행 및 확인합니다.
```
docker run -d nginxos:v1         #백그라운드에서 컨테이너를 실행합니다.
docker ps                        #현재 실행 중인 컨테이너를 확인합니다.
docker ps -a                     #실행되지 않는 컨테이너를 포함한 모든 컨테이너를 확인합니다.
docker logs CONTAINER ID/IMAGE   #방금 실행한 컨테이너가 표시되지 않으면 컨테이너 ID 또는 이름을 통해 실행 로그를 확인하고 문제를 진단합니다.
```
6. 다음 명령어를 순서대로 실행하여 이미지를 생성합니다.
```
docker commit fb2844b6**** nginxweb:v2 #commit 매개변수 뒤에 빌드할 새 이미지의 컨테이너 ID와 이름 및 버전 넘버를 추가합니다.
docker images                    #로컬(다운로드 및 로컬 생성) 이미지를 나열합니다.
```
7. 다음 명령어를 실행하여 이미지를 원격 웨어하우스로 푸시합니다.
기본적으로 Docker Hub에 푸시합니다. 먼저 Docker에 로그인하고 이미지에 연결을 바인딩하고 'Docker 사용자 이름/이미지 이름:태그' 형식으로 이미지 이름을 생성한 후 마지막으로 푸시를 완료해야 합니다.
```
docker login #실행 후 이미지 레지스트리의 사용자 이름과 비밀번호 입력
docker tag [이미지 이름]:[태그] [사용자 이름]:[태그]
docker push [사용자 이름]:[태그]
```
푸시가 완료되면 브라우저로 Docker Hub 공식 홈페이지에 로그인하여 볼 ​​수 있습니다.



