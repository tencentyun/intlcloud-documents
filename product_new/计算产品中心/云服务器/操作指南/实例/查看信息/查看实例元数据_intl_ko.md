인스턴스 메타데이터는 사용자 인스턴스의 데이터와 연관되므로 실행하는 인스턴스를 구성 및 관리하는 데 사용될 수 있습니다.

>주의: 인스턴스 자체 내부에서만 인스턴스 데이터를 액세스할 수 있고 데이터는 암호화 보호되지 않습니다. 인스턴스를 액세스하려는 사용자는 모두 해당 메타데이터를 조회할 수 있습니다. 따라서 사용자는 적절한 예방 조치를 취하여 민감한 데이터(예를 들면 영구적인 암호화 키)를 보호할 것을 권장합니다.

## 인스턴스 meta-data
Tencent Cloud는 현재 다음과 같은 meta-data 정보를 제공합니다.

| 데이터 |설명 | 버전 |
|---------|---------|---------|
| instance-id | 인스턴스 ID | 1.0 |
| uuid | 인스턴스 ID | 1.0 |
| local-ipv4 | 인스턴스 개인 네트워크 IP | 1.0 |
| public-ipv4 | 인스턴스 공용 네트워크 IP | 1.0 |
| mac | 인스턴스 eth0 장치 mac 주소| 1.0 |
| placement/region | 인스턴스가 위치한 리전 정보| 1.1 |
| placement/zone | 인스턴스가 위치한 가용존 정보| 1.1 |
| network/network/macs/**mac**/mac | 인스턴스 네트워크 인터페이스 장치 주소 | 1.2 |
| network/network/macs/**mac**/primary-local-ipv4 | 인스턴스 네트워크 인터페이스 주요 개인 IP 주소| 1.2 |
| network/network/macs/**mac**/public-ipv4s | 인스턴스 네트워크 인터페이스 공용 네트워크 IP 주소| 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/gateway | 인스턴스 네트워크 인터페이스 게이트웨이 정보 | 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/local-ipv4 |인스턴스 네트워크 인터페이스 개인 IP 주소 | 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/public-ipv4 | 인스턴스 네트워크 인터페이스 공용 네트워크 IP 주소| 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/public-ipv4-mode | 인스턴스 네트워크 인터페이스 공용 네트워크 모드 | 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/subnet-mask | 인스턴스 네트워크 인터페이스 서브넷 마스크| 1.2 |

> 위의 표에서 굵은글씨 **mac** 및 **local-ipv4** 필드는 인스턴스가 지정한 네트워크 인터페이스의 장치 주소 및 개인 IP 주소를 표시합니다.
> 
> 요청한 목표 URL 주소는 대소문자 구분됩니다. 요청한 리턴 결과에 따라 새로 요청할 목표 URL 주소를 생성하십시오.

## 인스턴스 메타데이터 쿼리
인스턴스 메타데이터에 대한 작업은 모두**인스턴스 내부**에서 실행합니다. 먼저 인스턴스 로그인 작업을 완료하십시오. 인스턴스 로그인에 대한 더 많은 콘텐츠는 [Windows 인스턴스 로그인](/doc/product/213/5435) 및 [Linux 인스턴스 로그인](/doc/product/213/5436) 을 참조하십시오.

### 제공한 모든 meta-data 유형 쿼리
명령어:
```
curl http://metadata.tencentyun.com/
```
리턴값은 다음과 같습니다.
![](http://mccdn.qcloud.com/img56a1ebcbd924d.png)

명령어:

```
curl http://metadata.tencentyun.com/meta-data
```
리턴값은 다음과 같습니다.
![](http://mccdn.qcloud.com/img56a1ed1128bd4.png)

이 중 placement 필드에는 region과 zone 두 가지 데이터가 포함됩니다.

명령어:

```
curl http://metadata.tencentyun.com/meta-data/placement
```
리턴값은 다음과 같습니다.
![](http://mccdn.qcloud.com/img56a1edb2b1349.png)



### 인스턴스 개인 IP 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
```
리턴값은 다음과 같습니다.
![](http://mccdn.qcloud.com/img56a1eeb9557a8.png)

### 인스턴스 공용 네트워크 IP 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
```
리턴값은 다음과 같습니다.
![](http://mccdn.qcloud.com/img56a1f015c48e5.png)

### 인스턴스 ID 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/instance-id
```
또는
```
curl http://metadata.tencentyun.com/meta-data/uuid
```
리턴값은 다음과 같습니다.
![](http://mccdn.qcloud.com/img56a1f1c703176.png)
![](http://mccdn.qcloud.com/img56a1f35d0bb18.png)

### 인스턴스 eth0 장치 주소
명령어:
```
curl http://metadata.tencentyun.com/meta-data/mac
```
리턴값은 다음과 같습니다.
![](http://mccdn.qcloud.com/img56a1f2800a4e2.png)

### 인스턴스가 위치한 리전 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/placement/region
```
리턴값은 다음과 같습니다.
![](http://mccdn.qcloud.com/img56a1f3ecd50a2.png)

### 인스턴스가 위치한 가용존 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/placement/zone
```
리턴값은 다음과 같습니다.
![](http://mccdn.qcloud.com/img56a1f45687788.png)

### 인스턴스 네트워크 인터페이스 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/ca12b20583f602d75a541d1a43452c2d/8.1.jpg)

명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/ced32a2fee5e5282cd038d4034fb11a0/8.2.jpg)

### 인스턴스 네트워크 인터페이스 상세 정보 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/4ee3cd5e1bcba00e846282aab4e352a0/9.jpg)

### 인스턴스 네트워크 인터페이스 개인 IP 주소 리스트 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/8a7e0b0e41a65b683f2f530131a45d07/10.jpg)

### 인스턴스 네트워크 인터페이스 장치 주소 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/mac
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/0627af2fbc1aada52f5821f92d200f44/11.jpg)

### 인스턴스 네트워크 인터페이스 개인 IP 주소 리스트 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/primary-local-ipv4
```
리턴값은 다음과 같습니다.
![](https://mc.qcloudimg.com/static/img/5458ecf47ec14ba9151e95d7eaa2efd4/12.jpg)

### 인스턴스 네트워크 인터페이스 공용 네트워크 IP 주소 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/public-ipv4s
```
리턴값은 다음과 같습니다.
![](https://mc.qcloudimg.com/static/img/19fa044afd25b8714b38312c7b3eef6c/13.jpg)

### 인스턴스 네트워크 인터페이스 네트워크 정보 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/5c0b23aa98661c533b2ee9cfae3a79cd/14.jpg)

### 인스턴스 네트워크 인터페이스 게이트웨이 주소 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/gateway
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/d297cd00f025c845111a50ee9874612d/15.jpg)

### 인스턴스 네트워크 인터페이스 개인 IP 주소 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/local-ipv4
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/24470fccb042eb877763a03100da8a10/16.jpg)

### 인스턴스 네트워크 인터페이스 공용 네트워크 IP 주소 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/public-ipv4
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/c0344e7c89ab0643884d8ac2b859711b/17.jpg)

### 인스턴스 네트워크 인터페이스 공용 네트워크 모드 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/public-ipv4-mode
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/115617733703e99602627bb3ce1f32cc/18.jpg)

> 비고:
- NAT: Network Address Translation, 네트워크 주소 전환
- direct: 다이렉트 네트워크, 인스턴스 네트워크 인터페이스의 공용 네트워크 IP 주소를 통해 직접 공용 네트워크를 라우팅 및 액세스합니다.

### 인스턴스 네트워크 인터페이스 서브넷 마스크 쿼리
명령어:
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/subnet-mask
```
리턴값은 다음과 같습니다.
 ![](https://mc.qcloudimg.com/static/img/ca9589a75e2a04859e3004e4b72ee967/19.jpg)
