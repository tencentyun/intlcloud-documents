## 어떤 상황에서 도메인 이름 소유권 확인을 해야 합니까?
1. a.example.com과 같이 처음 도메인에 액세스하는 경우, 도메인에 액세스 후 `b.example.com`과 같은 동일한 수준의 도메인과 다음 수준의 도메인이 권한 있는 것으로 간주됩니다. 기본적으로 액세스할 수 있으며 확인이 필요하지 않습니다. 그러나 `example.com`과 같은 상위 수준의 도메인에 대한 액세스는 여전히 확인해야 합니다;
2. 다른 계정으로 서브 도메인에 액세스한 경우, 현재 도메인 이름 소유권 확인을 수행해야 하며, 확인이 통과되면 도메인 이름을 검색하여 현재 계정에 액세스할 수 있습니다;
3. 동일한 수준의 와일드카드 서브도메인에 액세스할 때 확인이 필요합니다. 예시: `a.example.com`에 액세스했고 `*.example.com`에 액세스할 때 여전히 확인이 필요합니다. `*.a.example.com`은 2차 와일드카드 서브도메인이며 확인 없이 액세스할 수 있습니다.

## 방법1: DNS 확인(권장)

1. 도메인 이름 추가 시, 해당 도메인 이름이 확인이 필요한 경우 도메인 이름 아래에 도메인 이름 소유권을 확인하라는 메시지가 표시됩니다. **확인 방법**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1c6915b095d74f4358923be2ec7740dd.png)
2. 확인 방법에서 기본값은 DNS 확인입니다.
DNS 확인 방법을 사용하려면 DNS 업체로 이동하여 기본 도메인 이름 아래에 호스트 레코드 값이 `_cdnauth`인 TXT 레코드를 추가해야 합니다.
>!추가해야 하는 도메인 이름이 `c.b.a.example.com`, `*.example.com` 또는 `test.example.com`이든 상관없이 멀티 레벨 도메인에서 호스트 레코드 값은 ​​기본 도메인 아래에 추가되어야 합니다. 예를 들어 추가한 도메인은 `c.b.a.example.com`이며, 새 DNS 레코드는 `_cdnauth.example.com`으로 추가해야 합니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/e1da0524ad0781544052fd65195d9798.png)
**Tencent Cloud DNS의 리졸브 레코드를 추가하려면 다음 작업을 수행하십시오.**
DNS 서비스 제공 업체가 Tencent Cloud인 경우 [DNSPod 콘솔](https://console.cloud.tencent.com/cns)에 로그인하고 대상 도메인 이름을 찾은 다음 DNS를 클릭하고 TXT 레코드를 추가합니다. 호스트 매개변수를 `_cdnauth`로, 레코드 유형 매개변수를 TXT로, 레코드 값 매개변수를 Tencent Cloud CDN에서 제공하는 레코드 값으로 설정합니다. 다른 매개변수에는 기본 설정을 사용하십시오.
**Alibaba Cloud DNS의 리졸브 레코드를 추가하려면 다음 작업을 수행하십시오.**
DNS 서비스 제공 업체가 Alibaba Cloud인 경우 Alibaba Cloud의 DNS 콘솔에 로그인하고 대상 도메인 이름을 찾은 다음 작업 열에서 DNS 설정을 클릭합니다. 레코드 유형 매개변수를 TXT로 설정하고 호스트 이름 및 레코드 값 매개변수를 구성하고 다른 매개변수에 대해 기본 설정을 사용하십시오.
3. 확인 버튼을 클릭하여 확인을 시작하기 전에 TXT 레코드가 적용될 때까지 기다립니다. 도메인 이름을 확인하지 못한 경우 TXT 레코드가 유효하고 DNS 서비스 제공 업체에 적용되었는지 확인하십시오. [TXT 레코드가 적용되었는지 어떻게 확인하나요?](#q1)
4. 도메인 이름이 확인되면 도메인 이름이 다른 계정으로 연결되어 있는지 확인하십시오. 그렇다면 검색을 클릭하여 도메인 이름을 검색합니다. 도메인 이름이 검색되면 다른 계정의 도메인 이름에 대해 구성된 설정이 지워집니다.


## 방법2: 파일 확인
1. 추가한 도메인 이름에 소유권 확인이 필요한 경우 도메인 이름 필드 아래에 요구 사항 세부 정보를 알려주는 메시지가 나타납니다. 확인 방법에 대한 요구 사항을 보려면 **확인 방법**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/140a8b980bd0c30c0336dcd8f8e3607e.png)
2. 파일 인증 탭을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8883258277fef3bf2e42ceffb489324a.png)
3. verification.html을 클릭하여 인증을 위한 파일을 다운로드합니다.
4. Tencent Cloud CVM(Cloud Virtual Machine) 인스턴스, Tencent Cloud Object Storage(COS) 버킷, Alibaba Cloud ECS(Elastic Compute Service) 인스턴스 또는 Alibaba Cloud OSS(Object Storage Service) 버킷과 같은 도메인 이름 서버의 루트 디렉터리에 파일을 업로드합니다. 예를 들어 도메인 이름이 `test.example.com`인 경우 파일을 `example.com/` 또는 `test.example.com/` 루트 디렉터리에 업로드해야 합니다.
>!파일 확인 방법을 사용하는 경우에만 서브 도메인 이름에 파일을 업로드하여 확인을 수행할 수 있습니다.
5. 확인을 클릭하기 전에 `http://example.com/verification.html` 또는 `http://test.example.com/verification.html`을 통해 파일에 액세스할 수 있는지 확인하십시오. 추가한 레코드가 파일 내용과 일치하면 도메인 이름이 성공적으로 확인됩니다. 도메인 이름을 확인할 수 없는 경우 레코드와 파일 내용이 일치하는지 확인하십시오.
>! 파일 확인은 도메인 이름 검색을 지원하지 않습니다. DNS 확인 방법을 사용하는 경우에만 도메인 이름을 검색할 수 있습니다.


**예시:**
이 예시에서 가속 도메인 이름은 'a.test.com'이고 원본 서버는 COS입니다.
1. Verification.html 파일을 COS의 루트 디렉터리에 업로드합니다.
2. DNS 공급자에서 가속 도메인 이름에 대한 CNAME 레코드를 추가합니다. 레코드 값 매개변수를 COS 도메인 이름으로 설정합니다.
3. http(https)://가속 도메인 이름/verification.html을 통해 verification.html 파일에 액세스할 수 있는지 확인합니다. **확인** 버튼을 클릭합니다.

## 방법3: API 작업 인증
1. CreateVerifyRecord 작업을 호출하여 가속 도메인 이름에 대한 TXT 리졸브 레코드를 생성합니다.
```
{
  "Response":{
    "Record": "202009071516044acd018wf498457628cn75ba018ec9cv",
    "RecordType": "TXT"
    "RequestId": "8518c99c-a8eb-4930-a7d0-eff586d9cc37",
    "SubDomain": "_cdnauth",
   }
}
```
2. DNSPOD와 같은 DNS 공급자에서 TXT 리졸브 레코드를 추가합니다.
3. VerifyDomainRecord 작업을 호출하여 리졸브 레코드가 적용되는지 확인합니다.
```
{
  "Response":{
    "RequestId": "b6926bb2-d0b5-42bc-b17f-e4402bdb9e9b",
    "Result": "true"
   }
}
```
4. 리졸브 레코드가 적용되면 [AddCdnDomain](https://intl.cloud.tencent.com/document/product/228/34015) 작업을 호출하여 도메인 이름을 추가합니다.


## FAQ
[](id:q1)

### TXT 레코드가 적용되는지 어떻게 알 수 있나요?
**Windows 시스템 예시:**
연결한 도메인 이름이 `test.example.com`인 경우 cmd 명령 프롬프트를 열고 `nslookup-qt=txt _test.example.com` 명령을 실행합니다. 출력에 따라 TXT 레코드가 적용되는지 또는 유효한지 확인합니다.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/7VQU778_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230310151540.png" width="70%">
**Linux/Mac 시스템 예시:**
연결한 도메인 이름이 `test.example.com`인 경우 명령 프롬프트를 열고 `dig _cdnauth.example.com txt` 명령을 실행합니다. 출력에 따라 TXT 레코드가 적용되는지 또는 유효한지 확인합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6b65e488b8b52745e8a6a4431c112975.png" width="70%">

### VOD 도메인 이름에 액세스할 수 없다는 오류가 발생하는 이유는 무엇입니까?
도메인 이름이 VOD 콘솔에 이미 추가되어 있기 때문입니다. CDN 콘솔에서 도메인 이름을 관리하려면 VOD 콘솔에서 도메인 이름을 삭제하고 약 1분 정도 기다린 후 CDN 콘솔에 추가하거나 다른 서브 도메인 이름에 액세스해야 합니다. 
