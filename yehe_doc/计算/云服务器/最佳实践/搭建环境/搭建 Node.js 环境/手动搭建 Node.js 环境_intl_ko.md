## 작업 시나리오
본문은 Tencent Cloud CVM에 Node.js 환경 수동 배포 및 샘플 프로젝트 생성 방법을 소개합니다.

Node.js 환경을 수동으로 구축하는 경우, [CentOS 환경에서 YUM을 통해 소프트웨어 설치](https://intl.cloud.tencent.com/document/product/213/2046)와 같은 상용 명령어인 Linux 명령어를 숙지해야 하며 설치된 소프트웨어의 사용, 설정 및 호환성에 대한 이해가 필요합니다.
<dx-alert infotype="explain" title="">
Tencent Cloud는 클라우드 마켓의 이미지 환경을 통해 Node.js 환경을 배포할 것을 권장하며, Node.js 환경 수동 구축은 시간이 오래 걸릴 수 있습니다.
</dx-alert>



## 소프트웨어
본문의 Node.js 환경 소프트웨어 버전과 구성은 다음과 같습니다.
- 운영 체제: Linux 시스템, CentOS 7.6.
- Node.js: JavaScript 실행 환경, Node.js 10.16.3 및 Node.js 6.9.5.
- npm: Node.js 노드 버전 관리자, 여러 Node.js 버전 관리, npm 6.9.0.

## 전제 조건
구매한 Linux CVM이 있어야 합니다.

## 작업 단계
### 1단계: Linux 인스턴스 로그인
[Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)합니다. 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수도 있습니다.
- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)


### 2단계: Node.js 설치
1. 다음 명령어를 실행하여 Node.js Linux 64비트 이진법 설치 패키지를 다운로드합니다.
```
wget https://nodejs.org/dist/v10.16.3/node-v10.16.3-linux-x64.tar.xz
```
<dx-alert infotype="explain" title="">
자세한 설치 정보는 [Node.js 공식 홈페이지](https://nodejs.org/zh-cn/download/)에서 확인하실 수 있습니다.
</dx-alert>
2. 다음 명령어를 실행하여 설치 패키지를 압축 해제합니다.
```
tar xvf node-v10.16.3-linux-x64.tar.xz
```
3. 다음 명령을 순서대로 실행하여 소프트 링크를 생성합니다.
```
ln -s /root/node-v10.16.3-linux-x64/bin/node /usr/local/bin/node
```
```
ln -s /root/node-v10.16.3-linux-x64/bin/npm /usr/local/bin/npm
```
소프트 링크를 성공적으로 생성한 후 CVM의 랜덤 디렉터리에서 node 및 npm 명령어를 사용할 수 있습니다.
4. 다음 명령어를 순서대로 실행하여 Node.js 및 npm 버전 정보를 확인합니다.
```
node -v
```
```
npm -v
```

### 3단계: Node.js 여러 버전 설치(옵션)


<dx-alert infotype="explain" title="">
이 단계는 npm을 통해 여러 버전의 Node.js를 설치하고 빠른 전환을 가능하게 합니다. 개발자에게 적합하며 실제 필요에 따라 설치할 수 있습니다.
</dx-alert>


1. 다음 명령어를 실행하여 git를 설치합니다.
```
yum install -y git
```
2. 다음 명령어를 실행하여 NVM 소스 코드를 다운로드하고 최신 버전을 확인합니다.
```
git clone git://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```
3. 다음 명령어를 실행하여 NVM 환경 변수를 설정합니다.
```
echo ". ~/.nvm/nvm.sh" >> /etc/profile
```
4. 다음 명령어를 실행하여 환경 변수를 읽습니다.
```
source /etc/profile
```
4. 다음 명령어를 실행하여 Node.js의 모든 버전을 조회합니다.
```
nvm list-remote
```
5. 다음 명령어를 순서대로 실행하여 여러 버전의 Node.js를 설치합니다.
```
nvm install v6.9.5
```
```
nvm install v10.16.3
```
6. 다음 명령어를 실행하여 설치된 Node.js 버전을 조회합니다.
```
nvm ls
```
반환 결과가 다음과 같으면 성공적으로 설치된 것입니다. 현재 버전은 Node.js 10.16.3입니다.
![](https://main.qcloudimg.com/raw/a315fe51314357fb44ec725f20c101ed.png)
7. 다음 명령어를 실행하여 Node.js 사용 버전을 전환합니다.
```
nvm use v6.9.5
```
반환 결과는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/817fd96fef77f818e65ce41a3723e5bc.png)

### 4단계: Node.js 프로젝트 생성
1. 다음 명령어를 순서대로 실행하여 루트 디렉터리에 'index.js' 프로젝트 파일을 생성합니다.
```
cd ~
```
```
vim index.js
```
2. **i**를 눌러 편집 모드로 전환하고 `index.js` 파일에 다음을 입력합니다.
```
const http = require('http');
const hostname = '0.0.0.0';
const port = 7500;
const server = http.createServer((req, res) => { 
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello World\n');
}); 
server.listen(port, hostname, () => { 
    console.log(`Server running at http://${hostname}:${port}/`);
});
```
<dx-alert infotype="explain" title="">
본문은 `index.js` 프로젝트 파일에 포트 번호 7500을 사용합니다. 실제 필요에 따라 수정할 수 있습니다.
</dx-alert>
3. **Esc**를 누르고 **:wq**를 입력한 다음, **Enter**를 눌러 파일을 저장 및 반환합니다.
4. 다음 명령어를 실행하여 Node.js 프로젝트를 실행합니다.
```
node index.js
```
5. 로컬 브라우저에서 다음 주소에 액세스하여 프로젝트가 정상적으로 작동하는지 확인합니다.
```
http://CVM 인스턴스의 공인 IP: 설정된 포트 번호
```
표시된 결과가 다음과 같으면 Node.js 환경이 성공적으로 구축된 것입니다.
![](https://main.qcloudimg.com/raw/5b72798dc9e988eee8d8186055aa45e9.png)


## FAQ
CVM 사용 도중 문제가 생겼을 경우, 아래의 문서를 참고하여 실제 상황에 따라 문제를 분석 및 해결할 수 있습니다.
- CVM 로그인 문제는 [키 관련 문제](https://intl.cloud.tencent.com/document/product/213/18120), [로그인, 원격 연결](https://intl.cloud.tencent.com/document/product/213/17278)을 참고하십시오.
- CVM 네트워크 문제는 [IP 주소 문제](https://intl.cloud.tencent.com/document/product/213/17285), [포트 관련 문제](https://intl.cloud.tencent.com/document/product/213/2502)를 참고하십시오.
- CVM 디스크 문제는 [시스템 디스크와 데이터 디스크](https://intl.cloud.tencent.com/zh/document/product/213/17351)를 참고하십시오.

