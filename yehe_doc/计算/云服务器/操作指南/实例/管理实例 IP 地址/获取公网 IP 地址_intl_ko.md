## 작업 시나리오
본문은 콘솔, API 및 인스턴스 메타데이터를 통해 공용 IP를 가져오는 방법을 안내합니다.

## 작업 단계
<dx-tabs>
::: 콘솔을 통해 가져오기
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작업합니다.
  - **리스트 뷰**: 아래 이미지와 같이 기본 IP 주소 열로 마우스 이동 후 <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"/>을(를) 클릭하면 IP 주소를 복사할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/de3e24445d11fca4fc194dd51462c406.png)
  - **탭 뷰**: 아래 이미지와 같이 인스턴스 페이지에서 ‘IP 주소’의 공용 네트워크 주소 옆에 있는 <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"/>을(를) 클릭하면 공용 IP를 복사할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1a719829bf4f09d9f4785a97f66abfd0.png)

<dx-alert infotype="notice" title="">
공용 IP 주소는 NAT를 통해 개인 IP 주소로 매핑되므로 사용자가 인스턴스 내부에서 네트워크 인터페이스 속성을 조회할 경우(예를 들면 `ifconfig (Linux)` 또는 `ipconfig (Windows)` 명령어 사용) 공용 IP 주소는 나타나지 않습니다. 인스턴스 내부에서 인스턴스의 공용 IP 주소를 확인해야 할 경우 [인스턴스 메타데이터를 사용하여 가져오기](#jump)를 참고하십시오.
</dx-alert>


:::
::: \sAPI\s를 통해 가져오기
[인스턴스 리스트 조회](https://intl.cloud.tencent.com/document/product/213/33258)에서 관련 인터페이스를 참고하십시오.
:::
::: 인스턴스 메타데이터를 통해 가져오기[](id:jump)
1. CVM 인스턴스에 로그인합니다.
로그인 방법은 [Linux 인스턴스 로그인](https://intl.cloud.tencent.com/zh/document/product/213/5436)과 [Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/41018)을 참고하십시오.
2. cURL 툴 및 HTTP의 GET 요청을 통해 metadata에 액세스하고 공용 IP 주소를 가져옵니다.
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
``` 리턴값에 다음과 유사한 구성이 있으면 공용 IP 주소를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/03f603e433b7a5da09e33a8b09d731b4.png)
자세한 정보는 [인스턴스 메타데이터 조회](https://intl.cloud.tencent.com/document/product/213/4934)를 참고하십시오.
:::
</dx-tabs>
