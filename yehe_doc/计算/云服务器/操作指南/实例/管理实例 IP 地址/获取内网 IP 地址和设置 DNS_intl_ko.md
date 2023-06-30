## 작업 시나리오
본 문서에서는 인스턴스의 개인 IP 주소 획득과 내부 네트워크 DNS 설정과 관련된 작업에 대해 설명합니다.

## 작업 단계
### 인스턴스의 개인 IP 주소 가져오기
<dx-tabs>
::: 콘솔을 통한 가져오기
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 인스턴스 관리 페이지에서 실제 뷰 모드에 따라 작업합니다.
   - **리스트 뷰**: 아래 이미지와 같이 조회할 개인 IP의 인스턴스를 선택하고 ‘기본 IP 주소’ 열에 마우스를 이동한 후 <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: -3px 0px;">을(를) 클릭하면 개인 IP를 복사할 수 있습니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/14720408f77509b0dced407f75adbd21.png)
 - **탭 뷰**: 아래 이미지와 같이 인스턴스 페이지에서 ‘IP 주소’ 중 내부 네트워크 주소 뒤에 있는 <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: -3px 0px;">을(를) 클릭하면 내부 IP를 복사할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3a251c153caddfb6cf62bb6e6e6ff2cd.png)

:::
::: \sAPI\s를 통한 가져오기
[DescribeInstances 인터페이스](https://intl.cloud.tencent.com/zh/document/product/213/33258)를 참고하십시오.
:::
::: 인스턴스 메타데이터를 통한 가져오기
1. CVM에 로그인합니다.
2. cURL 툴 또는 HTTP의 GET 요청을 통해 인스턴스 메타데이터에 액세스합니다.
<dx-alert infotype="explain" title="">
다음 작업은 cURL 툴을 예로 들어 설명합니다.
</dx-alert>
다음 명령어를 실행하여 개인 IP를 획득합니다.
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
``` 아래 이미지와 같이 리턴된 정보가 개인 IP 주소입니다.
![](//mc.qcloudimg.com/static/img/14a13eccebc7eee6f83bc026adb30902/image.png)
인스턴스 메타데이터에 대한 자세한 정보는 [인스턴스 메타데이터 조회](https://intl.cloud.tencent.com/zh/document/product/213/4934)를 참고하십시오.
:::
</dx-tabs>

### 내부 네트워크 DNS 설정 
네트워크 분석에 오류가 발생할 경우 사용자는 CVM 운영 체제의 유형에 따라 수동으로 내부 네트워크 DNS를 설정할 수 있습니다.
<dx-tabs>
::: Linux\s 시스템
1. Linux CVM에 로그인합니다.
2. 다음 명령어를 실행하여 `/etc/resolv.conf` 파일을 엽니다.
```
vi /etc/resolv.conf
```
3. **i**를 눌러 편집 모드로 전환하고 [내부 네트워크 DNS](https://intl.cloud.tencent.com/zh/document/product/213/5225?from_cn_redirect=1#.E5.86.85.E7.BD.91-dns)에 따라 다른 리전에 해당하는 리스트는 DNS IP를 수정합니다.
예를 들어 내부 네트워크 DNS IP를 베이징 리전의 개인 네트워크 DNS 서버로 수정합니다.
```
nameserver 10.53.216.182
nameserver 10.53.216.198
options timeout:1 rotate
```
4. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
:::
::: Windows\s 시스템
1. Windows CVM에 로그인합니다.
2. 운영 체제 인터페이스에서 **제어판** > **네트워크 및 공유 센터** > **어댑터 장치 변경**을 엽니다.
3. **이더넷**을 우클릭한 후 **속성**을 선택하여 '이더넷 속성' 창을 엽니다.
4. 아래 이미지와 같이 ‘이더넷 속성’ 창에서 **Internet 프로토콜 버전 4 (TCP/IPv4)**를 더블 클릭하여 엽니다.
![](https://main.qcloudimg.com/raw/1eef10b5919ba4db272fa0fc21fb1702.png)
5. **다음 DNS 서버 주소 사용**을 선택하고 [내부 네트워크 DNS](https://intl.cloud.tencent.com/zh/document/product/213/5225?from_cn_redirect=1#.E5.86.85.E7.BD.91-dns)에 따라 다른 리전에 해당하는 리스트는 DNS IP를 수정합니다.
![](https://main.qcloudimg.com/raw/1eef10b5919ba4db272fa0fc21fb1702.png)
6. **확인**을 클릭합니다.
:::
</dx-tabs>
