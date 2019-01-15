CVM 공인 IP 주소가 DDoS 공격을 받았다면, 이는 현재 공인 IP 주소가 노출되었음을 의미합니다. 그렇기 때문에 고도 방어 IP에 액세스한 후, 이미 노출된 공인 IP 주소를 변경해야 공격자가 DDoS 고도 방어 IP를 피해 CVM IP 주소를 직접 공격하지 못하게 할 수 있습니다.

CVM 공인 IP 주소를 변경하려면 다음 절차를 참조하십시오.

## 1. CVM 엘라스틱 IP로 전환
현재 CVM 공인 IP 주소가 아직 엘라스틱 공인 IP가 아닌 경우, 우선 엘라스틱 공인 IP 주소로 전환해야 변경 후에도 해당 IP를 유지할 수 있습니다.
우선, [Tencent Cloud 서버 콘솔](https://console.cloud.tencent.com/cvm/overview)에 들어갑니다. “메인 IP 주소”에서 아래 화살표 위치의 “엘라스틱 IP로 전환” 버튼을 클릭하고, [전환 확인]을 클릭합니다.
![1](https://main.qcloudimg.com/raw/18d59c18c992049559da8e121559123f.png)
![2](https://main.qcloudimg.com/raw/ce5aff975b8a4fb5b100bba5250201cc.png)
>**설명:**
>현재 공인 IP가 엘라스틱 IP 주소로 전환 시, 포워딩 과정 중에는 서비스가 중단되지 않습니다.

## 2. 엘라스틱 IP를 공인 IP로 전환
“작업” 줄에서 “더 보기” 아래 “IP 작업”의 “엘라스틱 IP 언바인딩”을 선택하고, 동시에 “언바인딩 후 공인 IP 무료 할당”을 선택한 뒤, [확인]을 클릭합니다. 이때 CVM의 IP는 새로운 공인 IP 주소로 변경됩니다.
![3](https://main.qcloudimg.com/raw/8a503b56aee15271f543ce5b9039b4bb.png)
![4](https://main.qcloudimg.com/raw/af8189d0a62fda6d3415fd4f21c73afa.png)

>**주의:**
>사용자의 CVM이 이미 엘라스틱 공인 IP를 사용했다면 다른 기존의 엘라스틱 공인 IP로 바로 바인딩할 수 있습니다.

단계 1에서, [전환 확인] 대신 [기타 엘라스틱 공인 IP]를 클릭하고 “엘라스틱 공인 IP 바인딩”으로 즉시 리디렉션됩니다. 그 다음, “엘라스틱 공인 IP 선택” 상자를 클릭하여 IP를 선택하고 [확인]을 클릭하면 CVM에 새로운 공인 IP 주소가 할당됩니다.
![5](https://main.qcloudimg.com/raw/0773396549ae77e8edf69cb590f0dc84.png)
![6](https://main.qcloudimg.com/raw/b8f36a086baed36de888ee94f4aead1e.png)
