## 구성 시나리오

도메인 이름의 원본 서버 기본 정보, Origin-pull 프로토콜, 원본 도메인 및 기타 정보는 원본 서버 구성 모듈에서 수정할 수 있습니다.

>! 가속 리전과 동일한 리전에 원본 서버를 구성하는 것이 좋습니다. 예를 들어 가속 리전이 중국 내에 있는 경우 중국 내에서 원본 서버를 구성합니다. 중국홍콩 또는 중국 외에서 원본 서버를 구성하는 경우 Origin-pull중에 국경 간 액세스가 필요합니다. 이 경우 Origin-pull 효과가 보장되지 않을 수 있습니다.
가속 도메인 이름이 글로벌 가속으로 구성된 경우 도메인 이름의 원본 서버 구성 모듈에서 서로 다른 리전에 대해 각각 독립적인 원본 서버를 구성할 수 있습니다. 이러한 방식으로 중국 내 및 중국 외에서 시작된 Origin-pull 요청은 다른 원본 서버로 전송됩니다. 이렇게 하면 Origin-pull 효과가 보장됩니다.

## 구성 가이드

### 기본 원본 서버 구성

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 왼쪽 사이드바에서 [도메인 관리]를 선택한 뒤, 도메인 이름 오른쪽의 [관리]를 클릭하여 도메인 구성 페이지로 이동합니다. 기본 구성 탭을 열어 원본 서버 정보 섹션을 확인합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9IJQ709_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224110508.png)

**원본 서버 유형**

<table>
<thead>
<tr>
<td style="width:150px">외부 원본 서버</td>
<td>원본 서버로 실행되는 안정적인 비즈니스 서버를 사용할 수 있습니다. 해당 IP 목록 또는 도메인 이름을 원본 서버 주소로 입력합니다.</td></ul>
</tr>
</thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/products/cos">Tencent Cloud COS 원본</a></td>
<td>COS 버킷을 원본 서버로 선택할 수 있습니다. 개인 버킷 액세스를 활성화할 수 있습니다.</td>
</tr>
<tr>
<td>타사 오브젝트 스토리지	
</td>
<td>Tencent Cloud COS 이외의 타사 오브젝트 스토리지 서비스의 버킷을 원본 서버로 사용할 수 있습니다. 현재 지원되는 타사 오브젝트 스토리지 서비스에는 Amazon S3, Alibaba Cloud OSS, Huawei Cloud OBS 및 Qiniu Cloud kodo가 포함됩니다.<br/>
<strong>참고: </strong>현재 ECDN은 타사 오브젝트 스토리지 서비스를 기반으로 하는 원본 서버를 지원하지 않습니다.</td>
</tr>
</tbody></table>


**Origin-pull 프로토콜**
CDN 캐시 노드가 Origin-pull을 위해 원본 서버에 요청을 전달할 때 사용되는 프로토콜입니다. HTTP 또는 HTTPS를 선택할 수 있습니다.

<table>
<thead>
<tr>
<td style="width:150px">HTTP Origin-pull</td>
<td>CDN은 HTTPS를 통해 원본 서버에서 HTTP 또는 HTTPS 콘텐츠를 가져옵니다.</td></ul>
</tr>
</thead>
<tbody><tr>
<td>HTTPS Origin-pull</td>
<td>CDN은 HTTPS를 통해 원본 서버에서 HTTP 또는 HTTPS 콘텐츠를 가져와 낮은 CPU 사용량으로 원본 가져오기 데이터의 도난 및 변조를 방지합니다. HTTPS를 통해 원본 서버에 액세스할 수 있는지 확인하십시오.</td>
</tr>
<tr>
<td>프로토콜 따르기</td>
<td>HTTP는 HTTP 콘텐츠의 Origin-pull에 사용됩니다. HTTPS는 HTTPS 콘텐츠의 Origin-pull에 사용됩니다. HTTPS는 키에 민감한 콘텐츠를 전송할 때도 사용됩니다. 이 옵션을 선택하는 것이 좋습니다. HTTPS를 통해 원본 서버에 액세스할 수 있는지 확인하십시오.
.</td>
</tr>
</tbody></table>

> !HTTPS Origin-pull을 선택한 경우 HTTPS를 통해 원본 서버에 액세스할 수 있는지 확인합니다. 그렇지 않으면 Origin-pull이 실패할 수 있습니다.



**원본 서버 주소**
<table>
<thead>
<tr>
<td style="width:80px">외부 원본</td>
<td style="padding-bottom:0px;padding-top:15px"><ul><li>한 줄에 한 항목씩 여러 원본 IP 또는 원본 도메인 이름을 입력할 수 있습니다.
  <br><strong>라운드 로빈 모드의 여러 원본 IP에서 Origin-pull: </strong>라운드 로빈 모드에서 이러한 IP에서 콘텐츠를 가져오려면 한 줄에 하나의 항목으로 여러 원본 IP를 입력할 수 있습니다. CDN은 기본적으로 각 원본 IP의 가용성을 확인합니다. IP에서 콘텐츠 가져오기에 실패하거나 원본 IP로 전송된 Origin-pull 요청이 1분 이내에 시간 초과된 경우 원본 IP로 더 이상 Origin-pull 요청이 전송되지 않습니다. 원본 IP는 600초 동안 차단되고 나중에 자동으로 재개됩니다. <br><strong>도메인 이름에서 Origin-pull: </strong>도메인 이름을 원본 서버 주소로 구성할 수 있습니다. 도메인 이름은 가속 도메인 이름과 달라야 합니다. IPv6 도메인 이름은 사용할 수 없습니다. <br><strong>참고: </strong>CDN에 연결되어 있고 가속 도메인 이름을 가리키는 도메인 이름은 입력할 수 없습니다. 그렇지 않으면 해결 루프가 발생하여 Origin-pull 실패로 이어집니다. <li>원본 IP 또는 도메인 이름을 입력할 때 0 - 65535 범위의 포트와 1 - 100 범위의 가중치를 원본 서버 주소:포트:가중치 또는 원본 서버 주소::가중치 형식으로 추가할 수 있습니다. 기본적으로 포트는 생략됩니다. <br><strong>참고: </strong> 가중치는 숫자의 크기를 기준으로 정렬됩니다. 숫자가 클수록 가중치가 높아지고 원본 IP 또는 도메인 이름의 우선 순위가 높아집니다. <li>원본 서버 주소는 최대 511자를 포함할 수 있습니다.</td></ul>
</tr>
</thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/products/cos">Tencent Cloud COS 원본</a></td>
<td><li>원본 서버로 COS 버킷을 선택합니다. <li>버킷 구성 및 실제 비즈니스 요구 사항에 따라 기본 도메인 이름, 정적 웹 사이트 도메인 이름 또는 글로벌 가속 도메인 이름을 버킷 주소로 선택합니다. 예를 들어 선택한 버킷에 대해 정적 웹 사이트 구성이 활성화된 경우 정적 웹 사이트 도메인 이름을 선택합니다. <li>버킷의 액세스 권한이 비공개 읽기로 설정된 경우 CDN에 버킷 액세스 권한을 부여하고 Origin-pull 인증을 활성화하여 비공개 버킷 액세스를 허용합니다.</td>
</tr>
<tr>
<td>타사 오브젝트 스토리지</td>
<td style="padding-bottom:0px;padding-top:15px"><ul><li>리소스가 타사 오브젝트 스토리지 서비스의 버킷에 저장되어 있는 경우 유효한 버킷 주소를 원본 서버 주소로 입력합니다. 현재 지원되는 타사 오브젝트 스토리지 서비스에는 Amazon S3, Alibaba Cloud OSS, Huawei Cloud OBS 및 Qiniu Cloud kodo가 포함됩니다. </br><strong>예시: <code>my-bucket.s3.ap-east-1.amazonaws.com</code> 또는 <code>my-bucket.oss-cn-beijing.aliyuncs.com</code>. </strong>버킷 주소는 <code>http://</code> 또는 <code>http://</code> 프로토콜 헤더를 포함할 수 없습니다. <li>타사 오브젝트 스토리지 서비스의 프라이빗 버킷을 원본 서버로 사용하는 경우 유효한 키를 입력하고 Origin-pull 인증을 활성화하여 프라이빗 버킷 액세스를 허용합니다.</td>
</tr></ul>
</tbody></table>




**원본 도메인**
Origin-pull 시 CDN 노드가 원본 서버에서 액세스하는 도메인 이름을 의미합니다. 원본 도메인 설정 방법에 대한 자세한 내용은 [원본 도메인 구성](#exp)을 참고하십시오.

> ?원본 서버 주소와 원본 도메인의 차이점은 다음과 같습니다.
> - 원본 서버 주소는 Origin-pull 요청을 보내는 IP 주소를 지정합니다.
> - 원본 도메인은 Origin-pull 요청을 보낸 IP 주소에 해당하는 웹 사이트를 지정합니다.

<table>
<thead>
<tr>
<td style="width:80px">외부 원본</td>
<td >가속 도메인 이름은 기본적으로 원본 도메인으로 사용됩니다. 와일드카드 도메인 이름이 연결된 경우 원본 도메인은 기본적으로 실제 액세스 도메인 이름이며 사용자 지정할 수 있습니다.</td></tr>
</thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/products/cos">Tencent Cloud COS 원본</a></td>
<td>버킷 액세스 주소는 기본적으로 원본 도메인으로 사용되며 원본 서버 주소와 동일하며 수정할 수 없습니다.</td>
</tr>
<tr>
<td>타사 오브젝트 스토리지</td>
<td>버킷 액세스 주소는 기본적으로 원본 도메인으로 사용되며 원본 서버 주소와 동일하며 수정할 수 없습니다.</td>
</tr>
</tbody></table>



### 핫 백업 원본 서버 구성

기본 원본 서버에 대한 핫 백업 원본 서버를 추가할 수 있습니다. 모든 Origin-pull 요청은 먼저 기본 원본 서버로 전달됩니다. 4XX 또는 5XX 오류 코드가 반환되거나 연결 시간 초과 또는 프로토콜 비호환성과 같은 예외가 발생하면 요청이 핫 백업 원본 서버로 전달되어 리소스를 풀링하기 때문에 Origin-pull의 고가용성이 보장됩니다.

핫 백업 원본 서버는 자체 원본 서버 주소와 원본 도메인으로 구성할 수 있습니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fBH6442_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224110649.png)

>!
>- COS 버킷 또는 타사 오브젝트 스토리지 서비스의 버킷을 핫 백업 원본 서버로 사용할 수 없습니다.
>- IPv6 원본 서버를 기본 원본 서버로 사용하는 경우 핫 백업 원본 서버로 구성할 수 없습니다.
>- 핫 백업 원본 서버의 가중치를 구성할 수 없습니다.

### 리전별 구성

가속 도메인 이름이 글로벌 가속으로 구성되어 있고 국경 간 트래픽을 피하려면 **리전별 구성**을 클릭하여 가속 도메인 이름의 서비스 리전마다 다른 원본 서버를 구성합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XXa9147_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224112431.png)
다른 Origin-Pull 정책이 필요한 리전을 선택하고 해당 원본 서버 정보를 입력합니다. 자세한 내용은 [리전별 구성](#special)을 참고하십시오.

>!
>
>- 타사 오브젝트 스토리지 서비스의 버킷을 원본 서버로 사용하는 경우 리전별 구성을 추가할 수 없습니다.


## 구성 예시

### 원본 도메인 구성[](id:exp)

CDN 원본 서버와 가속 도메인 이름 'www.test.com'이 다음과 같이 구성되어 있는 경우:
![](https://main.qcloudimg.com/raw/ec2e007bb32723f7dd12aac17524c8af.png)
사용자의 액세스 경로는 다음과 같습니다.
사용자가 CDN 노드에 캐시되지 않은 리소스 `http://www.test.com/test.txt`에 액세스하면 노드는 도메인 이름 `www.abc.com`을 확인하여 원본 서버 주소 '1.1.1.1'을 가져옵니다. 그러면 CDN 노드는 서버 `1.1.1.1`에 액세스하여 웹 사이트 경로 `www.def.com`에서 test.txt 파일을 찾아 사용자에게 파일을 반환합니다.


[](id:special)
### 리전별 구성

Tencent Cloud CDN 원본 서버의 설정이 아래와 같고, 가속 도메인 `www.test.com`의 설정이 아래와 같은 경우:
![](https://main.qcloudimg.com/raw/e9104ca2b0e38c62bdffb022a933b2b9.png)
실제 Origin-pull은 다음과 같습니다.

1. 중국 내의 사용자가 `http://www.test.com/test.txt` 파일에 액세스하고 중국 내의 노드가 이 리소스를 캐시하지 않은 경우, 서버 `1.1.1.1`에 요청을 전달하고 웹사이트 경로 `1.test.com`에서 test.txt 파일을 찾으려고 시도합니다. 리소스가 존재하면 노드는 파일을 사용자에게 직접 반환합니다. 그렇지 않은 경우 2단계로 이동합니다.
2. 중국 내의 CDN 노드가 기본 원본 서버로 요청을 전달하지 못하고 리소스를 찾을 수 없으므로, 요청을 서버 `2.2.2.2`로 전달하고 웹사이트 경로 `2.test.com`에서 test.txt 파일을 찾아 캐시하고 사용자에게 반환합니다.
3. 이때 중국 외의 사용자가 `http://www.test.com/test.txt` 파일에 액세스합니다. 중국 외의 노드는 이 리소스를 캐시하지 않았기 때문에 서버 `3.3.3.3`에 요청을 전달하고 웹사이트 경로 `3.test.com`에서 test.txt 파일을 찾으려고 시도합니다. 리소스가 존재하면 노드는 파일을 사용자에게 직접 반환합니다. 그렇지 않은 경우 4단계로 이동합니다.
4. 중국 외의 CDN 노드가 중국 외의 기본 원본 서버로 요청을 전달하지 못하고 리소스를 찾을 수 없으므로,요청을 서버 `4.4.4.4`로 전달하고 웹 사이트 경로 `4.test.com`에서 test.txt 파일을 찾은 다음 캐시하여 중국 외의 사용자에게 반환합니다.
