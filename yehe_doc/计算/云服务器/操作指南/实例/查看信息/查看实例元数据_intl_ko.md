인스턴스 메타데이터란 인스턴스에 관련된 데이터를 나타내며, 실행 중인 인스턴스의 설정 및 관리에 사용할 수 있습니다.
> 인스턴스 자체 내부에서만 인스턴스 메타데이터에 액세스할 수 있지만, 데이터를 암호화하여 보호하지는 않아 인스턴스에 액세스할 수 있는 사용자라면 모두 해당 메타데이터를 조회할 수 있습니다. 따라서 사용자는 적합한 예방 조치로 중요 데이터를 보호하시기를 권장합니다(예: 영구 암호화 키 사용).
>


## 인스턴스 메타데이터 분류
Tencent Cloud에서는 현재 아래와 같은 메타데이터 정보를 제공합니다.

| 데이터 | 설명 | 사용 버전 |
|---------|---------|---------|
| instance-id | 인스턴스 ID | 1.0 |
| instance-name | 인스턴스 이름 | 1.0 |
| uuid | 인스턴스 ID | 1.0 |
| local-ipv4 | 인스턴스 개인 IP | 1.0 |
| public-ipv4 | 인스턴스 공인 IP | 1.0 |
| mac | 인스턴스 eth0 디바이스 mac 주소 | 1.0 |
| placement/region | 인스턴스가 위치한 리전 정보 | 2017-09-19 업데이트 |
| placement/zone | 인스턴스가 위치한 가용존 정보 | 2017-09-19 업데이트 |
| network/interfaces/macs/**${mac}**/mac | 인스턴스 네트워크 인터페이스의 디바이스 주소 | 1.0 |
| network/interfaces/macs/**${mac}**/primary-local-ipv4 | 인스턴스 네트워크 인터페이스의 주요 개인 IP 주소| 1.0 |
| network/interfaces/macs/**${mac}**/public-ipv4s | 인스턴스 네트워크 인터페이스의 공인 IP 주소 | 1.0 |
|network/interfaces/macs/**${mac}**/vpc-id| 인스턴스 네트워크 인터페이스의 VPC 네트워크 ID | 2017-09-19 업데이트 |
|network/interfaces/macs/**${mac}**/subnet-id| 인스턴스 네트워크 인터페이스의 서브넷 ID | 2017-09-19 업데이트 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/gateway | 인스턴스 네트워크 인터페이스의 게이트웨이 주소 | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/local-ipv4 | 인스턴스 네트워크 인터페이스의 개인 IP 주소 | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/public-ipv4 | 인스턴스 네트워크 인터페이스의 공인 IP 주소 | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/public-ipv4-mode | 인스턴스 네트워크 인터페이스의 공용 네트워크 모드 | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/subnet-mask | 인스턴스 네트워크 인터페이스의 서브넷 마스크 | 1.0 |
| payment/charge-type | 인스턴스 과금 유형 | 2017-09-19 업데이트 |
| payment/create-time | 인스턴스 생성 시간 | 2017-09-19 업데이트 |
| payment/termination-time | 인스턴스 폐기 시간 | 2017-09-19 업데이트 |
| app-id | 인스턴스 소속 사용자 AppId | 2017-09-19 업데이트 |
| as-group-id | 인스턴스가 위치한 Auto Scaling 그룹 ID| 2017-09-19 업데이트 |
| spot/termination-time| 스팟 인스턴스 폐기 시간 | 2017-09-19 업데이트 |
| /meta-data/instance/instance-type | 인스턴스 사양 | 2017-09-19 업데이트 |
| /instance/image-id | 인스턴스 이미지 ID | 2017-09-19 업데이트 |
| /instance/security-group | 인스턴스에 바인딩된 보안 그룹 정보 | 2017-09-19 업데이트 |


>  위의 표에서 `${mac}` 및 `${local-ipv4}` 필드는 각각 인스턴스의 특정 네트워크 인터페이스의 디바이스 주소 및 개인 IP 주소를 나타냅니다.
> 
> 요청한 타깃 URL 주소는 대소문자를 구분합니다. 요청의 출력 결과에 따라 새로 요청할 타깃 URL 주소를 생성하시기 바랍니다.
>
> 현재 버전에서는 placement 리턴 데이터가 변경되었으므로, 이전 버전의 데이터가 필요하다면 이전 버전의 경로를 지정하거나, 버전 경로를 지정하지 않는 방식을 통해 버전 1.0의 데이터에 액세스할 수 있습니다. placement 반환 데이터에 관한 자세한 정보는 [리전 및 가용존](https://intl.cloud.tencent.com/document/product/213/6091)을 참조 바랍니다.

## 인스턴스 메타데이터 조회
인스턴스 내부에서 인스턴스 메타데이터의 인스턴스 로컬 IP, 공인 IP 등 데이터에 액세스하여 외부 응용 프로그램과의 연결을 관리할 수 있습니다.
실행 중인 인스턴스 내부에서 모든 종류의 인스턴스 메타데이터를 조회하려면 아래의 URI를 사용하시기 바랍니다.

```
http://metadata.tencentyun.com/latest/meta-data/
```
cURL 툴이나 HTTP의 GET 요청을 통해 메타데이터에 액세스할 수 있습니다. 예시:

```
curl http://metadata.tencentyun.com/latest/meta-data/
```
* 존재하지 않는 리소스일 경우, HTTP 오류 코드 404 - Not Found가 반환됩니다.
* 인스턴스 메타데이터 관련 작업은 모두 **인스턴스 내부**에서만 실행할 수 있으므로, 해당 조작을 위해서는 먼저 인스턴스에 로그인해야 합니다. 인스턴스 로그인에 대한 더 자세한 내용은 [Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5435) 및 [Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참조 바랍니다.

## 메타데이터 조회 예시

아래 예시는 메타데이터의 버전 정보를 확인하는 방법을 나타냅니다.
> Tencent Cloud가 메타데이터 엑세스 경로나 리턴 데이터를 변경할 경우 새로운 메타데이터 버전이 배포되며, 만약 사용 중인 응용 프로그램이나 스크립트가 이전 버전의 구조 및 반환 데이터에 종속되어 있다면 이전 버전을 사용하여 메타데이터에 액세스할 수 있습니다. 버전을 지정하지 않을 경우, 1.0 버전으로 기본 액세스됩니다.
>

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/
1.0
2017-09-19
latest
meta-data
```

아래 예시는 메타데이터의 루트 디렉터리를 조회하는 방법을 나타냅니다. 그중 `/`로 끝나는 단어는 디렉터리를 나타내며, `/`로 끝나지 않는 단어는 액세스 데이터를 나타냅니다. 액세스 데이터에 관한 자세한 의미는 이전 문서인 **인스턴스 메타데이터 분류**를 참조 바랍니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/
instance-id
instance-name
local-ipv4
mac
network/
placement/
public-ipv4
uuid
```

아래 예시는 인스턴스의 물리적 소재지 정보를 확인하는 방법을 나타냅니다. 반환 데이터 및 물리적 소재지에 관한 자세한 정보는 [리전 및 가용존](https://intl.cloud.tencent.com/document/product/213/6091)을 참조 바랍니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/region
ap-guangzhou

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/zone
ap-guangzhou-3
```

아래 예시는 인스턴스의 개인 IP를 확인하는 방법을 나타냅니다. 인스턴스에 여러 ENI가 존재할 경우, eth0 디바이스의 네트워크 주소를 반환합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/local-ipv4
10.104.13.59
```

아래 예시는 인스턴스의 공인 IP를 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/public-ipv4
139.199.11.29
```

아래 예시는 인스턴스 ID를 확인하는 방법을 나타냅니다. 인스턴스 ID는 인스턴스의 고유 표식입니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/instance-id
ins-3g445roi
```

아래 예시는 인스턴스 uuid를 확인하는 방법을 나타냅니다. 인스턴스 uuid는 인스턴스의 고유 표식이라 할 수 있으므로, 인스턴스 ID를 사용하여 인스턴스를 구분하시길 권장합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/uuid
cfac763a-7094-446b-a8a9-b995e638471a
```

아래 예시는 인스턴스 eth0 디바이스의 mac 주소를 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/mac
52:54:00:BF:B3:51
```

아래 예시는 인스턴스 ENI 정보를 확인하는 방법을 나타냅니다. 여러 ENI가 존재할 경우 여러 줄의 데이터가 반환되며, 각 줄의 데이터는 각각 한 ENI의 데이터 디렉터리를 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/
52:54:00:BF:B3:51/
```

아래 예시는 지정된 ENI 정보를 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/
local-ipv4s/
mac
vpc-id
subnet-id
owner-id
primary-local-ipv4
public-ipv4s
local-ipv4s/
```

아래 예시는 지정된 ENI 산하의 VPC 정보를 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/vpc-id
vpc-ja82n9op

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/subnet-id
subnet-ja82n9op
```

아래 예시는 지정된 ENI에 바인딩된 개인 IP 주소 리스트를 확인하는 방법을 나타냅니다. ENI에 여러 개인 IP가 바인딩되었을 경우, 여러 줄의 데이터가 반환됩니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/
10.104.13.59/
```

아래 예시는 개인 IP 정보를 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59
gateway
local-ipv4
public-ipv4
public-ipv4-mode
subnet-mask
```

아래 예시는 개인 IP의 게이트웨이를 확인하는 방법을 나타냅니다. VPC 모델만 해당 데이터를 조회할 수 있으며, VPC 모델에 관한 자세한 정보는 [VPC](https://intl.cloud.tencent.com/document/product/215)를 참조 바랍니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/gateway
10.15.1.1
```

아래 예시는 개인 IP의 공용 네트워크 액세스 모드를 확인하는 방법을 나타냅니다. VPC 모델만 해당 데이터를 조회할 수 있으며, 기본 네트워크 모델은 공용망 게이트웨이를 통해 공용 네트워크에 액세스할 수 있습니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4-mode
NAT
```

아래 예시는 개인 IP에 바인딩된 공인 IP를 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4
139.199.11.29
```

아래 예시는 개인 IP의 서브넷 마스크를 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/subnet-mask
255.255.192.0
```

아래 예시는 인스턴스 과금 유형을 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/charge-type
POSTPAID_BY_HOUR
```

아래 예시는 인스턴스 생성 시간을 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/create-time
2018-09-18 11:27:33
```

아래 예시는 스팟 인스턴스의 폐기 시간을 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/spot/termination-time
2018-08-18 12:05:33
```

아래 예시는 CVM에 소속된 AppId를 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/app-id
123456789
```

## 인스턴스 사용자 데이터 조회
인스턴스 생성 시 인스턴스 사용자 데이터를 지정할 수 있으며, cloud-init을 설정한 CVM은 해당 데이터에 액세스할 수 있습니다.

### 사용자 데이터 인덱스
CVM 내부에서 아래의 방법을 통해 사용자 데이터에 액세스할 수 있습니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/user-data
179, client, shanghai
```
