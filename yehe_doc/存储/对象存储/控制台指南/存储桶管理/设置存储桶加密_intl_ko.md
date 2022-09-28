## 소개

COS 콘솔에서 버킷의 서버를 암호화할 수 있습니다. 서버를 암호화하면 버킷에 신규 업로드되는 객체에 대한 암호화(기본값)가 가능합니다. 버킷 암호화에 관한 자세한 내용은 [버킷 암호화 개요](https://intl.cloud.tencent.com/document/product/436/33457)를 참조하십시오.

>? 현재 지원하는 버킷 암호화 방식은 SSE-COS 암호화입니다(Cloud Object Storage(COS)가 키를 호스팅하여 관리하는 서버 암호화 방식). 서버 암호화에 관한 내용은 [서버 암호화 개요](https://intl.cloud.tencent.com/document/product/436/18145)를 참고하십시오.
>


## 작업 단계

#### 신규 버킷 생성 시 암호화 설정

[버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 시, 다음 이미지와 같이 버킷 암호화를 추가합니다.
![](https://main.qcloudimg.com/raw/cc4f781f6ffa98b3786e52cf84d5c8d4.png)


#### 이미 생성된 버킷에 암호화 설정

버킷 생성 시 암호화 설정을 하지 않은 경우, 다음 순서에 따라 버킷을 암호화할 수 있습니다.

1. [버킷 리스트](https://console.cloud.tencent.com/cos5/bucket) 페이지에서 암호화할 버킷을 찾아 버킷 이름을 클릭한 뒤 버킷 설정 페이지로 이동합니다.
2. 왼쪽 사이드바에서 **보안 관리 > 서버측 암호화**를 클릭합니다.
3. **서버측 암호화** 설정 페이지에서 **편집**을 클릭하고 상태를 ‘활성화’로 수정합니다.
![](https://main.qcloudimg.com/raw/e2863ba89860f15464870ac198b5335f.png)
4. 지정한 암호화 방식을 선택하고, **저장**을 클릭하면 버킷 암호화 설정이 완료됩니다.
![](https://main.qcloudimg.com/raw/524717e180e357eb74fa8be0b42a51a3.png)

