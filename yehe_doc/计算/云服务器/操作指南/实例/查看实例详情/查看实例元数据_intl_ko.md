인스턴스 메타데이터는 인스턴스 관련 데이터로, 실행 중인 인스턴스를 설정 또는 관리하는 데 사용할 수 있습니다.
>? 인스턴스 내부에서만 인스턴스 메타데이터에 액세스할 수 있으나, 데이터는 암호화로 보호되지 않습니다. 인스턴스에 액세스할 수 있는 사용자는 모두 해당 메타데이터를 조회할 수 있으므로 적절한 예방 조치를 취하여 중요 데이터를 보호하십시오.
>


## 인스턴스 메타데이터 분류
Tencent Cloud는 현재 다음과 같은 메타데이터 정보를 제공합니다.

<table>
<thead>
<tr>
<th>데이터</th>
<th width="50%">설명</th>
<th width="15%">사용 버전</th>
</tr>
</thead>
<tbody><tr>
<td>instance-id</td>
<td>인스턴스 ID</td>
<td>1.0</td>
</tr>
<tr>
<td>instance-name</td>
<td>인스턴스 이름</td>
<td>1.0</td>
</tr>
<tr>
<td>uuid</td>
<td>인스턴스 ID</td>
<td>1.0</td>
</tr>
<tr>
<td>local-ipv4</td>
<td>인스턴스 내부 IP</td>
<td>1.0</td>
</tr>
<tr>
<td>public-ipv4</td>
<td>인스턴스 공용 IP</td>
<td>1.0</td>
</tr>
<tr>
<td>mac</td>
<td>인스턴스 eth0 디바이스 mac 주소</td>
<td>1.0</td>
</tr>
<tr>
<td>placement/region</td>
<td>인스턴스가 위치한 리전 정보</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>placement/zone</td>
<td>인스턴스가 위치한 가용존 정보</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/mac</td>
<td>인스턴스 네트워크 인터페이스 디바이스 주소</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/primary-local-ipv4</td>
<td>인스턴스 네트워크 인터페이스 메인 내부 IP 주소</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/public-ipv4s</td>
<td>인스턴스 네트워크 인터페이스 공용 IP 주소</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/vpc-id</td>
<td>인스턴스 네트워크 인터페이스 VPC 네트워크 ID</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/subnet-id</td>
<td>인스턴스 네트워크 인터페이스 서브넷 ID</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/gateway</td>
<td>인스턴스 네트워크 인터페이스 게이트웨이 주소</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/local-ipv4</td>
<td>인스턴스 네트워크 인터페이스 내부 IP 주소</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/public-ipv4</td>
<td>인스턴스 네트워크 인터페이스 공용 IP 주소</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/public-ipv4-mode</td>
<td>인스턴스 네트워크 인터페이스 공용 네트워크 모드</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/subnet-mask</td>
<td>인스턴스 네트워크 인터페이스 서브넷 마스크</td>
<td>1.0</td>
</tr>
<tr>
<td>payment/charge-type</td>
<td>인스턴스 과금 유형</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>payment/create-time</td>
<td>인스턴스 생성 시간</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>payment/termination-time</td>
<td>인스턴스 폐기 시간</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>app-id</td>
<td>인스턴스 사용자 AppId</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>as-group-id</td>
<td>인스턴스가 위치한 Auto Scaling 그룹 ID</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>spot/termination-time</td>
<td>스팟 인스턴스 폐기 시간</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>instance/instance-type</td>
<td>인스턴스 사양</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>instance/image-id</td>
<td>인스턴스 이미지 ID</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>instance/security-group</td>
<td>인스턴스 바인딩 보안 그룹 정보</td>
<td>2017-09-19 업데이트</td>
</tr>
<tr>
<td>instance/bandwidth-limit-egress</td>
<td>인스턴스 내부 네트워크 아웃바운드 대역폭 제한, 단위Kbit/s</td>
<td>2019-09-29 업데이트</td>
</tr>
<tr>
<td>instance/bandwidth-limit-ingress</td>
<td>인스턴스 내부 네트워크 인바운드 대역폭 제한, 단위Kbit/s</td>
<td>2019-09-29 업데이트</td>
</tr>
<tr>
<td>cam/security-credentials/${role-name}</td>
<td>인스턴스 CAM 역할 정책에서 생성한 임시 자격 증명입니다. 인스턴스가 CAM 역할을 바인딩해야만 임시 자격 증명을 획득할 수 있습니다. ${role-name} 매개변수는 인스턴스 CAM 역할 이름으로 바꿔야 합니다. 지정하지 않는 경우 404가 반환됩니다.</td>
<td>2019-12-11 업데이트</td>
</tr>
<tr>
<td>volumes</td>
<td>인스턴스</td>
<td>1.0</td>
</tr>
</tbody></table>

>? 
>- 위 표에서 `${mac} 및 `${local-ipv4}` 필드는 각각 인스턴스가 지정한 네트워크 인터페이스의 디바이스 주소와 내부 IP 주소를 의미합니다.
>- 요청한 타깃 URL 주소는 대소문자를 구분합니다. 요청에 대한 반환 결과에 따라 새로 요청할 타깃 URL 주소를 생성하십시오.
>- 현재 버전에서 placement에 대한 반환 데이터가 변경되었습니다. 이전 버전의 데이터를 사용해야 할 경우, 이전 버전의 경로를 지정하거나 버전 경로를 지정하지 않고 버전 1.0의 데이터에 액세스할 수 있습니다. placement에 대한 반환 데이터는 [리전과 가용존](https://intl.cloud.tencent.com/document/product/213/6091)을 참조하십시오.

## 인스턴스 메타데이터 조회
인스턴스 내부에서 인스턴스 메타데이터를 통해 인스턴스 로컬 IP, 공용 IP 등 데이터에 액세스하여 외부 응용 프로그램과의 연결을 관리할 수 있습니다.
실행 인스턴스 내부에서 모든 종류의 인스턴스 메타데이터를 조회하려면 아래 URL을 사용하십시오.

```
http://metadata.tencentyun.com/latest/meta-data/
```
cURL 툴이나 HTTP의 GET 요청을 통해 metadata에 액세스할 수 있습니다. 예시:

```
curl http://metadata.tencentyun.com/latest/meta-data/
```
* 존재하지 않는 리소스인 경우 HTTP 오류 코드 404 Not Found가 반환됩니다.
* 인스턴스 메타데이터 관련 작업은 모두 **인스턴스 내부**에서 진행됩니다. 먼저 인스턴스 로그인을 하시기 바랍니다. 인스턴스 로그인에 대한 자세한 내용은 [Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5435) 및 [Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참조하십시오.

### 메타데이터 조회 예시

아래 예시는 metadata 버전 정보를 확인하는 방법을 설명합니다.
>! Tencent Cloud가 metadata의 액세스 경로나 반환 데이터를 수정할 때 신규 metadata 버전이 배포됩니다. 응용 프로그램 또는 스크립트가 이전 버전의 구조나 반환 데이터에 종속되어 있을 경우, 지정된 초기 버전으로 metadata에 액세스할 수 있습니다. 버전을 지정하지 않으면 기본적으로 1.0 버전에 액세스됩니다.
>

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/
1.0
2017-09-19
latest
meta-data
```

아래 예시는 metadata 루트 디렉터리의 조회 방법을 설명합니다. `/`로 끝나는 단어는 디렉터리를 의미하고, `/`로 끝나지 않는 단어는 액세스 데이터를 의미합니다. 액세스 데이터의 자세한 의미는 앞의 **인스턴스 metadata 분류**를 참조하십시오.

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

아래 예시는 인스턴스의 물리적 소재지 정보를 확인하는 방법을 설명합니다. 반환 데이터와 물리적 소재지의 관계는 [리전과 가용존](https://intl.cloud.tencent.com/document/product/213/6091)을 참조하십시오.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/region
ap-guangzhou

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/zone
ap-guangzhou-3
```

아래 예시는 인스턴스 내부 IP를 확인하는 방법을 설명합니다. 인스턴스에 여러 ENI가 있을 경우 eth0 디바이스의 네트워크 주소가 반환됩니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/local-ipv4
10.104.13.59
```

아래 예시는 인스턴스 공용 IP를 확인하는 방법을 나타냅니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/public-ipv4
139.199.11.29
```

아래 예시는 인스턴스 ID를 확인하는 방법을 설명합니다. 인스턴스 ID는 인스턴스의 고유 식별자입니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/instance-id
ins-3g445roi
```

아래 예시는 인스턴스 uuid를 확인하는 방법을 설명합니다. 인스턴스 uuid는 인스턴스의 고유 식별자로 사용되므로, 인스턴스 구분을 위해 인스턴스 ID 사용을 권장합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/uuid
cfac763a-7094-446b-a8a9-b995e638471a
```

아래 예시는 인스턴스 eth0 디바이스 mac의 주소를 확인하는 방법을 설명합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/mac
52:54:00:BF:B3:51
```

아래 예시는 인스턴스 ENI 정보를 확인하는 방법을 설명합니다. 여러 개의 ENI는 여러 행의 데이터를 반환하며, 각 행에 하나의 ENI 데이터 디렉터리가 표시됩니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/
52:54:00:BF:B3:51/
```

아래 예시는 지정된 ENI 정보를 확인하는 방법을 설명합니다.

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

아래 예시는 지정된 ENI가 속한 VPC 정보를 확인하는 방법을 설명합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/vpc-id
vpc-ja82n9op

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/subnet-id
subnet-ja82n9op
```

아래 예시는 지정된 ENI에 바인딩된 내부 IP 주소 리스트를 확인하는 방법을 설명합니다. ENI가 다수의 내부 IP에 바인딩된 경우 여러 행의 데이터가 반환됩니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/
10.104.13.59/
```

아래 예시는 내부 IP 정보를 확인하는 방법을 설명합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59
gateway
local-ipv4
public-ipv4
public-ipv4-mode
subnet-mask
```

아래 예시는 내부 IP 게이트웨이를 확인하는 방법을 설명합니다. VPC 모델만 해당 데이터를 조회할 수 있습니다. VPC 모델은 [VPC](https://intl.cloud.tencent.com/document/product/215)를 참조하십시오.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/gateway
10.15.1.1
```

아래 예시는 내부 IP를 확인하여 공용 네트워크 모드에 액세스하는 방법을 설명합니다. VPC 모델만 해당 데이터를 조회할 수 있습니다. 기본 네트워크 모델은 공용망 게이트웨이를 통해 공용 네트워크에 액세스할 수 있습니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4-mode
NAT
```

아래 예시는 내부 IP를 확인하고 공용 IP를 바인딩하는 방법을 설명합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4
139.199.11.29
```

아래 예시는 내부 IP의 서브넷 마스크를 확인하는 방법을 설명합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/subnet-mask
255.255.192.0
```

아래 예시는 인스턴스 과금 유형을 확인하는 방법을 설명합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/charge-type
POSTPAID_BY_HOUR
```

아래 예시는 인스턴스의 생성 시간을 확인하는 방법을 설명합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/create-time
2018-09-18 11:27:33
```


아래 예시는 스팟 인스턴스의 인스턴스 폐기 시간을 확인하는 방법을 설명합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/spot/termination-time
2018-08-18 12:05:33
```

아래 예시는 CVM이 속한 계정 AppId를 확인하는 방법을 설명합니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/app-id
123456789
```

아래 예시는 인스턴스 CAM 역할이 생성한 임시 자격 증명을 확인하는 방법을 설명합니다. CVMas는 예시로 사용한 rolename입니다.
```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/cam/security-credentials/CVMas
{
  "TmpSecretId": "AKIDoQMxA6cW447p225cIt9NW8dhA1dwl5UvxxxxxxxxxUqRlEb5_",
  "TmpSecretKey": "Q9z24VucjF4xQQN1PEsH3exxxxxxxxxgA=",
  "ExpiredTime": 1615590047,
  "Expiration": "2021-03-12T23:00:47Z",
  "Token": "xxxxxxxxxxx",
  "Code": "Success"
}
```

아래 예시는 인스턴스 스토리지를 가져오는 방법을 설명합니다.
​```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/volumes
disk-xxxxxxxx
​```

## 인스턴스 사용자 데이터 조회
인스턴스 생성 시 인스턴스 사용자 데이터를 지정할 수 있으며, cloud-init이 설정된 CVM은 해당 데이터에 액세스할 수 있습니다.

### 사용자 데이터 인덱스
사용자는 CVM 내부에서 아래의 방식으로 사용자 데이터에 액세스할 수 있습니다.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/user-data
179, client, shanghai
```
