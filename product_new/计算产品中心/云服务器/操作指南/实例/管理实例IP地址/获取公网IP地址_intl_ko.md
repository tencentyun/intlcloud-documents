## 작업 시나리오
본 문서는 콘솔, API 및 인스턴스 메타데이터를 통해 공인 IP를 획득하는 것을 안내합니다.


## 작업 순서

### 콘솔을 사용하여 획득하기
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
2. 인스턴스 관리 페이지에서 마우스를 주 IP 주소 열에 이동하면 <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"></img>가 나타납니다. 아래 이미지를 참조하십시오.
3. <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"></img>를 클릭하면 해당 IP 주소를 복사할 수 있습니다.	
>공인 IP 주소는 NAT를 통해 개인 IP 주소로 매핑되므로 사용자가 인스턴스 내부에서 네트워크 인터페이스 속성을 조회할 경우(예를 들면 `ifconfig (Linux)` 또는 `ipconfig (Windows)` 명령어 사용) 공인 IP 주소는 나타나지 않습니다. 인스턴스 내부에서 인스턴스의 공인 IP 주소를 확인해야 할 경우 [인스턴스 메타데이터 획득하기](#jump)를 참조하십시오.
>

### API를 사용하여 획득하기
[인스턴스 리스트 조회](https://cloud.tencent.com/document/product/213/15728)에서 관련 인터페이스를 참조하십시오.

<span id = "jump">  </span>
### 인스턴스 메타데이터를 사용하여 획득하기
1. CVM 인스턴스에 로그인하십시오.
로그인 방법은 [Linux 인스턴스 로그인](https://cloud.tencent.com/document/product/213/16515)과 [Windows 인스턴스 로그인](https://cloud.tencent.com/document/product/213/35697)을 참조하십시오.
2. cURL 툴 및 HTTP의 GET 요청을 통해 metadata에 액세스하고 공인 IP 주소를 획득합니다.
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
```
리턴값에 다음과 유사한 구성이 있으면 공인 IP 주소를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/03f603e433b7a5da09e33a8b09d731b4.png)
자세한 정보는 [인스턴스 메타데이터 조회](https://intl.cloud.tencent.com/document/product/213/4934)를 참조하십시오.
