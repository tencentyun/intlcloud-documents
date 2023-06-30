## 작업 시나리오

본 문서에서는 TKE를 통해 간단한 Web 애플리케이션을 만드는 방법을 설명합니다.

Web 애플리케이션은 다음 부분으로 나뉩니다.
- 첫 번째 부분은 클라이언트의 쿼리 및 쓰기 요청을 처리하는 데 사용되는 프런트 엔드 서비스입니다.
- 다른 부분은 Redis를 사용하여 작성된 데이터를 redis-master에 저장하고 redis-slave에서 데이터를 읽는 데이터 저장 서비스입니다. 프라이머리/세컨더리 복제를 통해 redis-master와 redis-slave 간에 데이터를 동기화합니다.

이 애플리케이션은 Kubernetes 프로젝트와 함께 제공되는 샘플 애플리케이션입니다. 자세한 내용은 <a href="https://github.com/kubernetes/kubernetes/tree/release-1.6/examples/guestbook">Guestbook App</a>을 참고하십시오.

## 전제 조건
- [Tencent Cloud 계정 등록](https://intl.cloud.tencent.com/register)을 완료합니다.
- 클러스터를 생성 완료해야 합니다. 자세한 내용은 [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637)를 참고하십시오.

## 작업 단계
### redis-master 서비스 생성
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. 애플리케이션을 생성할 클러스터 ID를 클릭하고 Deployment 페이지로 이동합니다. [Create]를 선택합니다. 아래 그림을 참고하십시오.
![](https://main.qcloudimg.com/raw/378d95d782c5efbf9cd9061f4c708e22.png)
3. 다음 지침에 따라 ‘Create Workload’ 페이지에서 워크로드 기본 정보를 설정합니다. 아래 그림을 참고하십시오.
![](https://main.qcloudimg.com/raw/ea0ddc2df9e0b2bcc826b852cd2c1805.png)
 - **Workload Name**: 생성할 워크로드의 이름입니다. 이 예시에서는 redis-master로 설정되어 있습니다.
 - **Description**: 워크로드와 관련된 정보를 입력합니다.
 - **Label**: key = value 형식의 키 값 쌍입니다. 이 예시에서 기본 레이블은 k8s-app = **redis-master**입니다.
 - **Namespace**: 필요에 따라 값을 선택합니다.
 - **Type**: 필요에 따라 값을 선택합니다.
 - **Volume**: 워크로드가 탑재될 볼륨을 선택합니다. 자세한 내용은 [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678)를 참고하십시오.
4. 다음 지침에 따라 **Containers in Pod**를 설정합니다. 아래 그림을 참고하십시오.
![](https://main.qcloudimg.com/raw/3f7259f65a29fb5e782abb815a41835b.png)
다음은 주요 매개변수를 설명합니다. 다른 매개변수의 경우 기본값으로 그대로 두십시오.
 - **Name**: 포드에 있는 컨테이너의 이름을 입력합니다. 이 예시에서 이름은 master입니다.
 - **Image**: `ccr.ccs.tencentyun.com/library/redis`를 입력합니다.
 - **Image Tag**: latest를 입력하십시오.
 - **Image Pull Policy**: 세 가지 정책을 사용할 수 있습니다. 필요에 따라 값을 선택합니다. 이 예에서는 이 필드를 지정할 필요가 없으며 기본 정책을 사용하기만 하면 됩니다.
이미지 풀 정책을 지정하지 않으면 이미지 태그가 비어 있거나 latest인 경우 Always 정책이 사용됩니다. 그렇지 않으면 IfNotPresent 정책이 사용됩니다.
    - **Always**: 항상 원격 끝에서 이미지를 가져옵니다.
    - **IfNotPresent**: 기본적으로 로드 이미지를 사용합니다. 로컬 이미지를 사용할 수 없는 경우 원격 끝에서 이미지를 가져옵니다.
    - **Never**: 로컬 이미지만 사용합니다. 로컬 이미지를 사용할 수 없으면 예외가 발생합니다.
6. 포드 수를 설정합니다.
![](https://main.qcloudimg.com/raw/5f861ae3fb55521d738a171764a3b097.png)
 - **Manual adjustment**: 포드 수를 설정합니다. 이 예시에서 포드 수는 1입니다. ‘+’ 또는 ‘-’를 클릭하여 포드 수를 조정할 수 있습니다.
 - **Auto adjustment**: 지정된 조건이 충족되면 시스템이 자동으로 pod 수를 조정합니다. 자세한 내용은 [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424)을 참고하십시오.
7. 다음 이미지와 같이 워크로드의 액세스 모드를 지정합니다.   
![](https://main.qcloudimg.com/raw/88d2188f7746184e88fe8a4375f0d5e1.png)
 - **Service**: ‘Enable’을 선택합니다.
 - **Service Acces**: ‘Intra-cluster’를 선택합니다.
 - **Load Balancer**: 필요에 따라 값을 선택합니다.
 - **Port Mapping**: 프로토콜 드롭다운 목록에서 TCP를 선택하고 포트와 대상 포트를 모두 6379로 설정합니다. 이러한 방식으로 다른 서비스는 redis-master 서비스 이름과 6379 포트 번호를 사용하여 master 컨테이너에 액세스할 수 있습니다.
8. [Create Workload]를 클릭하여 redis-master 서비스 생성을 마칩니다.

### redis-slave 서비스 생성
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. 서비스를 생성할 클러스터의 ID를 클릭합니다. 표시되는 Deployment 페이지에서 다음 이미지와 같이 [Create]를 클릭합니다.
![](https://main.qcloudimg.com/raw/3b828dcdb219b9466af30c359c505898.png)
3. 표시되는 ‘New Workload’ 페이지에서 지침에 따라 워크로드의 기본 정보를 지정합니다.
![](https://main.qcloudimg.com/raw/5d01db06dc78bc2136ce1b185af64dce.png)
 - **Workload Name**: 생성할 워크로드의 이름을 나타냅니다. 이 예시에서 이름은 redis-slave입니다.
 - **Description**: 워크로드와 관련된 정보를 입력합니다.
 - **Label**: key = value 형식의 키 값 쌍을 나타냅니다. 이 예시에서 기본 레이블은 k8s-app = **redis-slave**입니다.
 - **Namespace**: 필요에 따라 값을 선택합니다.
 - **Type**: 필요에 따라 값을 선택합니다.
 - **Volume**: 워크로드가 탑재될 볼륨을 선택합니다. 자세한 내용은 [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678)를 참고하십시오.
4. 다음 이미지와 같이 **Containers in pod** 설정을 구성합니다.
![](https://main.qcloudimg.com/raw/16a69f993a1faf19399dcb45584de82e.png)
다음은 주요 매개변수를 설명합니다. 다른 매개변수의 경우 기본 값으로 그대로 두십시오.
 - **Name**: 포드에 있는 컨테이너의 이름을 입력합니다. 이 예시에서 이름은 slave입니다.
 - **Image**: `ccr.ccs.tencentyun.com/library/gb-redisslave`를 입력합니다.
 - **Image Tag**: latest를 입력하십시오.
 - **Image Pull Policy**: 필요에 따라 값을 선택합니다. 이 예시에서는 이 필드를 지정할 필요가 없으며 기본 정책을 사용하기만 하면 됩니다.
 - **Environment Variable**: 다음 설정 정보를 입력합니다.
GET_HOSTS_FROM = dns
5. 포드 수를 설정합니다.
![](https://main.qcloudimg.com/raw/10353f37e16c5e33a41bf71336ee93e7.png)
 - **Manual adjustment**: 포드 수를 설정합니다. 이 예시에서 포드 수는 1입니다. ‘+’ 또는 ‘-’를 클릭하여 포드 수를 조정할 수 있습니다.
 - **Auto adjustment**: 지정된 조건이 충족되면 시스템이 자동으로 pod 수를 조정합니다. 자세한 내용은 [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424)을 참고하십시오.
6. 다음 이미지와 같이 워크로드의 액세스 모드를 지정합니다.   
![](https://main.qcloudimg.com/raw/b7ce5914042e33b404fc87165e532afe.png)
 - **Service**: ‘Enable’을 선택합니다.
 - **Service Access**: ‘Intra-cluster’를 선택합니다.
 - **Load Balancer**: 필요에 따라 값을 선택합니다.
 - **Port Mapping**: 프로토콜 드롭 다운 목록에서 TCP를 선택하고 포트와 대상 포트를 모두 6379로 설정합니다. 이러한 방식으로 다른 서비스는 redis-master 서비스 이름과 6379 포트 번호를 사용하여 master 컨테이너에 액세스할 수 있습니다.
7. [Create Workload]을 클릭하여 redis-slave 서비스 생성을 마칩니다.

### frontend 서비스 생성
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. 애플리케이션을 생성할 클러스터의 ID를 클릭합니다. 표시되는 Deployment 페이지에서 다음 이미지와 같이 [Create]를 클릭합니다.
![](https://main.qcloudimg.com/raw/46a7ea3299c791e8a31e4122a0f06b97.png)
3. 표시되는 ‘New Workload’ 페이지에서 지침에 따라 워크로드의 기본 정보를 지정합니다.
![](https://main.qcloudimg.com/raw/3c4b6d6277fe6f650ea464d1060e1ee6.png)
 - **Workload Name**: 생성할 워크로드의 이름입니다. 이 예시에서 이름은 frontend입니다.
 - **Description**: 작업 부하와 관련된 정보를 입력합니다.
 - **Tag**: key = value 형식의 키 값 쌍. 이 예시에서는 k8s-app = **frontend**를 사용합니다.
 - **Namespace**: 필요에 따라 값을 선택합니다.
 - **Type**: 필요에 따라 값을 선택합니다.
 - **Volume**: 워크로드가 탑재될 볼륨을 선택합니다. 자세한 내용은 [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678)를 참고하십시오.
5. 다음 이미지와 같이 **Containers in pod** 설정을 구성합니다.
![](https://main.qcloudimg.com/raw/0b5cfc640ced656bde9c782df01880d5.png)
다음은 주요 매개변수를 설명합니다. 다른 매개변수의 경우 기본 값으로 그대로 두십시오.
 - **Name**: 포드에 있는 컨테이너의 이름을 입력합니다. 이 예시에서 이름은 frontend입니다.
 - **Image**: `ccr.ccs.tencentyun.com/library/gb-frontend`를 입력합니다.
 - **Image Tag**: latest를 입력하십시오.
 - **Image Pull Policy**: 필요에 따라 값을 선택합니다. 이 예시에서는 이 필드를 지정할 필요가 없으며 기본 정책을 사용하기만 하면 됩니다.
 - **Environment Variable**: 다음 설정 정보를 입력합니다.
GET_HOSTS_FROM = dns
6. 포드 수를 설정합니다.
![](https://main.qcloudimg.com/raw/0e1dfb010735c93cca720b7e6fce0aa8.png)
 - **Manual adjustment**: 포드 수를 설정합니다. 이 예에서 포드 수는 1입니다. ‘+’ 또는 ‘-’를 클릭하여 포드 수를 조정할 수 있습니다.
 - **Auto adjustment**: 지정된 조건이 충족되면 시스템이 자동으로 pod 수를 조정합니다. 자세한 내용은 [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424)을 참고하십시오.
7. 다음 이미지와 같이 워크로드의 액세스 모드를 지정합니다.   
![](https://main.qcloudimg.com/raw/c89da244015147adc6d11f21ceef9e8c.png)
 - **Service**: ‘Enable’을 선택합니다.
 - **Service Access**: ‘Via Internet’를 선택합니다.
 - **Load Balancer**: 필요에 따라 값을 선택합니다.
 - **Port Mapping**: 프로토콜 드롭다운 목록에서 TCP를 선택하고 포트와 대상 포트를 모두 80으로 설정합니다. 이러한 방식으로 사용자는 로드 밸런서 IP 주소를 사용하여 브라우저에서 frontend 컨테이너에 액세스할 수 있습니다.
8. [Create Workload]을 클릭하여 frontend 서비스 생성을 완료합니다.


### Web 애플리케이션 확인
1. 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster)]를 클릭하여 ‘Cluster Management’ 페이지로 이동합니다.
2. 생성된 서비스가 있는 클러스터의 ID를 클릭합니다. 표시되는 페이지에서 [Services]>[Service]를 선택합니다.
3. 서비스 관리 페이지에서 frontend 서비스의 로드 밸런서 IP 주소를 복사합니다.
![](https://main.qcloudimg.com/raw/43d09b779fd2c0844b5c70d8ef373c53.png)
>
>- redis-master 및 redis-slave 서비스를 생성할 때 **Intra-cluster** 액세스 모드를 선택했습니다. 따라서 이러한 서비스에는 사설 IP 주소가 하나만 있으며 클러스터 내의 다른 서비스에서만 액세스할 수 있습니다.
>- frontend 서비스를 생성할 때 **Via Internet** 액세스 모드를 선택했습니다. 따라서 이 서비스는 로드 밸런서 IP 주소(공용 IP 주소)와 사설 IP 주소를 갖습니다. 결과적으로 이 서비스는 클러스터의 다른 서비스에서 액세스할 수 있을 뿐만 아니라 인터넷을 통해서도 액세스할 수 있습니다.
>
4. 브라우저에서 frontend 서비스의 로드 밸런서 IP 주소에 액세스합니다. 다음 페이지가 나오면 frontend 서비스에 정상적으로 접근할 수 있습니다.
![](https://main.qcloudimg.com/raw/d168ffa008a9c91e8b0e0c2051abd5a3.png)
5. 필드에 임의의 문자열을 입력하고 [Submit]을 클릭합니다. 입력한 문자열이 저장되어 페이지 하단에 표시되는 것을 볼 수 있습니다.
브라우저 페이지를 새로고침하여 서비스의 IP 주소에 다시 액세스하십시오. 이전에 입력한 문자열이 페이지에 남아 있어 문자열이 redis에 저장되었음을 나타냅니다.

### 개발 프랙티스
다음 예시 코드는 Guestbook App의 frontend 서비스에 대한 전체 코드입니다. HTTP 요청을 수신할 때 frontend 서비스는 이것이 set 명령인지 확인합니다.
- set 명령인 경우 프론트엔드 서비스는 매개변수에서 key와 value를 가져와 redis-master 서비스에 연결하고 redis-master 서비스에 key와 value를 적용합니다.
- set 명령이 아닌 경우 프론트엔드 서비스는 redis-slave 서비스에 연결하고 key 매개변수의 value를 얻은 다음 표시할 클라이언트에 값을 반환합니다.

```php
<?php
error_reporting(E_ALL);
ini_set('display_errors', 1);
require 'Predis/Autoloader.php';
Predis\Autoloader::register();
if (isset($_GET['cmd']) === true) {
  $host = 'redis-master';
  if (getenv('GET_HOSTS_FROM') == 'env') {
    $host = getenv('REDIS_MASTER_SERVICE_HOST');
  }
  header('Content-Type: application/json');
  if ($_GET['cmd'] == 'set') {
    $client = new Predis\Client([
      'scheme' => 'tcp',
      'host'   => $host,
      'port'   => 6379,
    ]);
    $client->set($_GET['key'], $_GET['value']);
    print('{"message": "Updated"}');
  } else {
    $host = 'redis-slave';
    if (getenv('GET_HOSTS_FROM') == 'env') {
      $host = getenv('REDIS_SLAVE_SERVICE_HOST');
    }
    $client = new Predis\Client([
      'scheme' => 'tcp',
      'host'   => $host,
      'port'   => 6379,
    ]);
    $value = $client->get($_GET['key']);
    print('{"data": "' . $value . '"}');
  }
} else {
  phpinfo();
} ?>

```


### 관련 설명

- frontend 서비스는 redis-master 및 redis-slave 서비스에 액세스할 때 **Service name and port**에 연결합니다. 클러스터는 서비스 이름을 해당 서비스 IP 주소로 해석하고 이 IP 주소에 따라 로드 밸런싱을 수행하는 dns 서비스와 함께 제공됩니다.
redis-slave 서비스가 3개의 Pod를 관리한다고 가정합니다. 프론트엔드 서비스가 redis-slave 서비스와 포트 6379에 직접 연결되어 있는 경우 dns 서비스는 redis-slave 서비스를 redis-slave 서비스의 IP 주소(로드 밸런서 IP 주소와 유사한 유동 IP 주소)로 자동 해석합니다. 그러면 dns 서비스는 redis-slave 서비스의 IP 주소를 기반으로 자동으로 로드 밸런싱을 수행하고 redis-slave 서비스의 해당 Pod에 요청을 보냅니다.
- 컨테이너에 대한 환경 변수를 지정할 때 다음 사항에 유의하십시오.
 - **Default setting (recommended)**: 런타임 시 frontend 컨테이너는 사전 설정된 환경 변수 GET_HOSTS_FROM = dns를 읽은 다음 서비스 이름을 사용하여 서비스에 직접 연결합니다.
 - **Other setting**: redis-master 또는 redis-slave 서비스의 도메인 이름을 얻으려면 다른 환경 변수를 지정해야 합니다.

