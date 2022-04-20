## 작업 시나리오
본 문서는 컨테이너 클러스터에서 Node.js Hello World 서비스를 빠르게 생성하는 방법을 설명합니다. Docker 이미지를 빌드하는 방법에 대한 자세한 내용은 [How to Build a Docker Image](https://intl.cloud.tencent.com/document/product/457/9115)를 참고하십시오.

## 전제 조건

- 클러스터를 생성 완료해야 합니다. 자세한 내용은 [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637)를 참고하십시오.
- Node.js가 설치된 노드에 로그인해야 합니다.

## 작업 단계
### 이미지 생성 코드 작성
#### 애플리케이션 개발
1. 다음 명령어를 순서대로 실행하여 hellonode 디렉터리를 생성하고 이동합니다.
```shell
mkdir hellonode
```
```shell
cd hellonode/
```
2. 다음 명령을 실행하여 server.js 파일을 생성하고 엽니다.
```
vim server.js
```
3. **i**를 눌러 편집 모드로 전환하고 다음 코드를 server.js에 복사합니다.
```js
var http = require('http');
var handleRequest = function(request, response) {
  console.log('Received request for URL: ' + request.url);
  response.writeHead(200);
  response.end('Hello World!');
};
var www = http.createServer(handleRequest);
www.listen(80);
```
‘**Esc**’ 키를 누르고 ‘**:wq**’를 입력하여 파일을 저장하고 반환합니다.
4. 다음 명령어를 실행하여 server.js 파일을 실행합니다.
```shell
node server.js
```
Hello World 프로그램은 다음과 같은 방법으로 테스트할 수 있습니다.
 - 노드에 다시 로그인하고 다음 명령을 실행합니다.
```shell
curl 127.0.0.1:80
```
다음과 같은 정보가 나오면 Hello World 프로그램이 정상적으로 실행되고 있는 것입니다.
![](https://main.qcloudimg.com/raw/4b97b9e2fdaee77376b114ef92f90936.png)
 - 로컬 브라우저를 열고 주소 표시줄에 `IP 주소: 포트 번호`를 입력하여 프로그램에 액세스합니다. 여기서 포트 번호는 80입니다.
 다음과 같은 정보가 나오면 Hello World 프로그램이 정상적으로 실행되고 있는 것입니다.
![](https://main.qcloudimg.com/raw/1fb82340313ab81dcffd693f9577624d.png)


#### Docker 이미지 생성
>?Docker 이미지에 대한 자세한 내용은 [How to Build a Docker Image](https://intl.cloud.tencent.com/document/product/457/9115)를 참고하십시오.
>
1. 다음 명령어를 순차적으로 실행하여 hellonode 디렉터리에 Dockerfile 파일을 생성합니다.
```
cd hellonode
```
```
vim Dockerfile
```
2. **i**를 눌러 편집 모드로 전환하고 다음 코드를 Dockerfile 파일에 복사합니다.
```shell
FROM node:4.4
EXPOSE 80
COPY server.js .
CMD node server.js
```
‘**Esc**’ 키를 누르고 ‘**:wq**’를 입력하여 파일을 저장하고 반환합니다.
3. 다음 명령어를 실행하여 이미지를 빌드합니다.
```shell
docker build -t hello-node:v1 .
```
4. <span id="search">다음 명령어를 실행하여 빌드된 hello-node 이미지를 확인합니다.</span>
```
docker images 
```
다음 정보가 나오면 hello-node 이미지가 성공적으로 빌드된 것입니다. 다음 그림과 같이 나중에 사용할 수 있도록 IMAGE ID를 기록해 두십시오.
![](https://main.qcloudimg.com/raw/d5bf4dfa0f805d6f90399c814b3152b1.png)


#### Tencent Cloud 이미지 레지스트리에 이미지 업로드
>!이미지를 업로드하기 위한 전제 조건:
>- [My Image](https://console.cloud.tencent.com/tke2/registry/user/space)에서 네임스페이스를 생성 완료해야 합니다.
>- [Tencent Cloud Registry](https://intl.cloud.tencent.com/document/product/457/9117)에 로그인 해야합니다. 이미지 사용에 대한 자세한 내용은 [Image Registry User Guide](https://intl.cloud.tencent.com/document/product/457/9117)를 참고하십시오.

다음 명령을 순서대로 실행하여 이미지를 Tencent Cloud 이미지 레지스트리에 업로드합니다.
```shell
sudo docker tag IMAGEID ccr.ccs.tencentyun.com/네임스페이스/helloworld:v1
```
```
sudo docker push ccr.ccs.tencentyun.com/네임스페이스/helloworld:v1
```
>?
>- 명령의 IMAGEID를 4단계에서 언급한 IMAGEID로 바꿉니다.
>- 명령의 네임스페이스를 생성된 네임스페이스로 바꿉니다.
>
다음 정보가 나타나면 이미지가 성공적으로 업로드된 것입니다.
![](https://main.qcloudimg.com/raw/1aadc58e8663488200e3e34a532642c4.png)


### 이미지를 사용하여 Hello World 서비스 생성
>!Hello World 서비스를 만들고 사용하기 전에 다음을 확인하십시오.
>- Tencent Cloud 계정을 등록 완료해야 합니다. [가입 페이지](https://intl.cloud.tencent.com/register)로 이동하여 Tencent Cloud 가입에 필요한 정보를 입력합니다.
>- 클러스터를 생성 완료해야 합니다. 자세한 내용은 [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637)를 참고하십시오.
>
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. ‘Cluster Management’ 페이지에서 클러스터의 ID를 클릭하여 서비스를 생성하고 클러스터의 워크로드 ‘Deployment’ 페이지로 이동합니다. 그런 다음 다음 그림과 같이 [Create]를 클릭합니다.
![](https://main.qcloudimg.com/raw/bacaf92e14b7c342db6b3179c2ae5e8f.png)
3. ‘Create Workload’ 페이지에서 지침에 따라 워크로드의 기본 정보를 지정합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/e2d083fececab9d1f84dd82f3850537a.png)
 - **Workload Name**: 워크로드의 이름을 입력합니다. 이 예시에서 이름은 helloworld입니다.
 - **Description**: 관련 워크로드 정보를 지정합니다.
 - **Tag**: key = value 키 값 쌍을 지정합니다. 이 예시에서 기본값은 k8s-app = **helloworld**입니다.
 - **Namespace**: 필요에 따라 네임스페이스를 선택합니다.
 - **Type**: 필요에 따라 유형을 선택합니다.
 - **Volume**: 마운트할 워크로드 볼륨을 설정합니다. 자세한 내용은 [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678)를 참고하십시오.
4. 지침에 따라 ‘Containers in Pod’를 설정합니다. 아래 이미지를 참고하십시오. 
컨테이너 이름을 입력합니다. 이 예시에서 이름은 helloworld입니다.
![](https://main.qcloudimg.com/raw/27b651e922b4a3afb925326ed8393bd0.png)
[Select an image]를 클릭하고 나타나는 대화 상자에서 [My Image]를 클릭합니다. 다음 그림과 같이 검색창을 이용하여 helloworld 이미지를 찾은 후 [OK]를 클릭합니다.
![](https://main.qcloudimg.com/raw/86a18f657b75d338ab3c084710c3ba10.png)
주요 매개변수 정보는 다음과 같습니다.
 - **Image Tag**: 기본 값 v1을 사용합니다.
 - **Image Pull Policy**: 필요에 따라 사용 가능한 세 가지 정책 중 하나를 선택합니다. 이 예시에서는 기본 정책이 적용됩니다.
이미지 가져오기 정책을 설정하지 않고 이미지 태그가 `latest`이거나 비어 있는 경우 Always를 사용합니다. 그렇지 않으면 IfNotPresent를 사용합니다.
    - **Always**: 항상 원격에서 이미지를 가져옵니다.
    - **IfNotPresent**: 기본적으로 로컬 이미지를 사용합니다. 이미지를 사용할 수 없는 경우 원격 위치에서 가져옵니다.
    - **Never**: 로컬 이미지만 사용합니다. 이미지를 사용할 수 없으면 예외가 발생합니다.
5. ‘Number of Pod’ 섹션에서 지침에 따라 서비스에 대한 포드 수를 설정합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/6cc62e4c9118b83f7c4552a55f4c4cf0.png)
 - **Manual adjustment**: 포드 수를 지정합니다. 이 예에서는 1로 설정되어 있습니다. ‘+’ 또는 ‘-’를 클릭하여 포드 수를 변경할 수 있습니다.
 - **Auto Adjustment**: 설정된 조건 중 하나라도 충족되면 자동으로 pod 수를 조정합니다. 자세한 내용은 [Automatic Scaling Basic Operation](https://intl.cloud.tencent.com/document/product/457/32424)을 참고하십시오.
6.   지침에 따라 워크로드에 대한 액세스 설정(Service)을 구성합니다. 아래 이미지를 참고하십시오.   
![](https://main.qcloudimg.com/raw/57b97c8877fd3ac116c71fad4bf416f2.png)
 - **Service**: ‘Enable’을 선택합니다.
 - **Service Access**: ‘Public Network Access’를 선택합니다.
 - **Load Balancer**: 필요에 따라 로드 밸런서를 생성하거나 선택합니다.
 - **Port Mapping**: TCP 프로토콜을 선택하고 컨테이너 포트와 서비스 포트를 모두 포트 80으로 설정합니다.
 >!서비스가 속한 클러스터의 보안 그룹에 있는 노드 네트워크, 컨테이너 네트워크 및 포트 30000 - 32768은 인터넷에 개방되어 있어야 합니다. 그렇지 않으면 TKE를 사용하지 못할 수 있습니다. 자세한 내용은 [TKE 보안 그룹 설정](https://intl.cloud.tencent.com/document/product/457/9084)을 참고하십시오.
7. [Create Workload]을 클릭하여 Hello World 서비스를 생성합니다.

### Hello World 서비스에 액세스
두 가지 방법 중 하나로 Hello World 서비스에 액세스할 수 있습니다.

#### CLB IP 주소로 Hello World 서비스에 액세스
1. 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster)]를 클릭하여 ‘Cluster Management’ 페이지로 이동합니다.
2. Hello World 서비스가 속한 클러스터의 ID를 클릭하고 [Service]>[Service]를 선택합니다.
3. 서비스 관리 페이지에서 다음 그림과 같이 helloworld 서비스의 CLB IP 주소를 복사합니다.
![](https://main.qcloudimg.com/raw/96fb6f94d4d365ce4007ff7961f5e438.png)

#### 서비스 이름으로 Hello World 서비스에 액세스
클러스터의 다른 서비스 또는 컨테이너는 서비스 이름을 사용하여 직접 액세스할 수 있습니다.

### Hello World 서비스 인증
서비스 접속 시 아래와 같은 정보가 나오면 Hello World 서비스가 성공적으로 생성된 것입니다.
![](https://main.qcloudimg.com/raw/817c981526ac6297c778c1cb154a8d90.png)
컨테이너를 생성할 수 없는 경우 [Event FAQ](https://intl.cloud.tencent.com/document/product/457/8187)를 참고하십시오.
