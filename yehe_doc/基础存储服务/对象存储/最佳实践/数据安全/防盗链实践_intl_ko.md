## 소개

Tencent Cloud COS는 링크 도용 방지 설정을 지원합니다. 사용자는 버킷에 링크 도용 방지 기능을 통해 액세스 출처에 대한 블랙리스트/화이트리스트 설정으로 리소스 도용을 방지할 수 있습니다. 본 문서에서는 버킷에 링크 도용 방지 기능을 설정하여 리소스가 도용되지 않도록 하는 방법을 자세히 소개합니다.

## 링크 도용 방지 판단 원리

링크 도용 방지는 Header의 Referer 주소를 요청하여 판단합니다.

- Referer는 Header의 일부입니다. 브라우저가 Web 서버에 요청을 발송할 때 Referer를 통해 해당 요청이 어느 페이지에서 링크된 것인지 서버에 알리면, 서버에서 특정 출처의 웹 사이트에 대한 리소스 액세스를 금지하거나 허용할 수 있습니다.
- 브라우저에서 직접 파일 링크 `https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg`를 열 경우, 요청 Header에 Referer가 존재하지 않습니다.

예를 들어, 아래 이미지와 같이 `https://127.0.0.1/test/test.html`에 이미지 `1.jpg`를 삽입하고 `https://127.0.0.1/test/test.html`에 액세스할 경우 액세스 출처를 표시하는 Referer가 존재합니다.
![](https://main.qcloudimg.com/raw/ed5d4f915132b236eb9423d81881ffd4.jpg)

<span id="fenxi"></span>
## 링크 도용 사례 분석

사용자 A가 COS에 이미지 리소스 `1.jpg`를 업로드하여 이미지 액세스 링크 `https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg`를 획득한 경우,
- 사용자 A가 해당 이미지를 자신의 웹 페이지 `https://example.com/index.html`에 삽입하면 이미지에 정상적으로 액세스할 수 있습니다.
- 사용자 B가 사용자 A의 웹 페이지에서 해당 이미지를 보고 해당 이미지를 자신의 웹 페이지 `https://b.com/test/test.html`에 삽입하면, 해당 이미지는 사용자 B의 웹 페이지에서도 정상적으로 표시됩니다.
위 사례는 사용자 A의 이미지 리소스 `1.jpg`의 링크가 사용자 B에 의해 도용된 경우입니다. 이때 사용자 A가 알지 못하는 상황에서 COS 상의 리소스가 사용자 B의 웹 페이지에서 계속 사용되는 경우, 사용자 A는 별도의 트래픽 요금을 부담하는 손실이 발생합니다. 


## 해결 방법

위 [링크 도용 사례 분석](#fenxi)의 경우 사용자 A는 링크 도용 방지 설정을 통해 사용자 B의 이미지 링크 도용을 방지할 수 있습니다. 자세한 방법은 다음과 같습니다.
1. 사용자 A가 버킷 examplebucket-1250000000에 링크 도용 방지 규칙을 설정합니다. 사용자 B의 링크 도용을 방지하는 방법은 두 가지가 있습니다.
 - 방법1: 블랙리스트 모드를 설정합니다. 도메인 설정에 `*.b.com`을 입력하고 저장하면 적용됩니다.
 - 방법2: 화이트리스트 모드를 설정합니다. 도메인 설정에 `*.example.com`을 입력하고 저장하면 적용됩니다.
2. 링크 도용 방지 설정 활성화 후,
 - `https://example.com/index.html`에 액세스하면 이미지가 정상적으로 표시됩니다.
 - `https://b.com/test/test.html`에 액세스하면 이미지가 표시되지 않으며, 다음과 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/3374bd47b5cf2eff04d15cd6d1590aae.jpg)

## 자세한 방법

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 후, 왼쪽 메뉴에서 [버킷 리스트]를 클릭해 버킷 리스트 페이지로 이동합니다.
2. 링크 도용 방지를 설정할 버킷을 선택하여 버킷으로 이동합니다.
![](https://main.qcloudimg.com/raw/66a106d2fd78632b65914f2fb6c096dc.png)
3. 왼쪽 메뉴에서 [보안 관리]>[링크 도용 방지 설정]을 클릭해 버킷 링크 도용 방지 설정 페이지로 이동합니다.
4. '링크 도용 방지 설정'에서 [편집]을 클릭해 편집 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/d726521ea58a99cfb3cf42dfae776f05.png)
5. 링크 도용 방지를 활성화하고 리스트 유형과 도메인을 설정합니다. 본 문서에서는 방법2를 예시로 설명합니다.
 - **유형**: 블랙리스트/화이트리스트 중 선택할 수 있습니다.
    - **블랙리스트**: 리스트에 있는 도메인이 버킷의 기본 액세스 주소에 액세스하는 것을 제한합니다. **리스트에 있는** 도메인이 버킷의 기본 액세스 주소에 액세스하는 경우 403을 반환합니다.
    - **화이트리스트**: 리스트에 없는 도메인이 버킷의 기본 액세스 주소에 액세스하는 것을 제한합니다. **리스트에 없는** 도메인이 버킷의 기본 액세스 주소에 액세스하는 경우 403을 반환합니다.
 - **Referer**: 도메인 설정은 최대 10개의 도메인 및 접두사 매칭이 가능하고 도메인, IP, 와일드카드 부호 `*` 등 형식의 주소를 지원합니다. 주소 1개당 한 행을 차지하며, 주소가 여러 개인 경우 줄 바꿈을 합니다. 규칙 설정에 대한 설명과 예시는 다음과 같습니다.
    - 포트가 있는 도메인 및 IP를 지원합니다(예: `example.com:8080`, `10.10.10.10:8080` 등의 주소).
    - `example.com`을 설정하면 `example.com/123`과 같이 `example.com`을 접두사로 하는 주소가 히트됩니다.
    - `example.com`을 설정하면 `https://example.com` 및 `http://example.com`을 접두사로 하는 주소가 히트됩니다.
    - `example.com`을 설정하면 포트가 있는 도메인 `example.com:8080`이 히트됩니다. 
    - `example.com:8080`을 설정하면 도메인 `example.com`이 히트되지 않습니다.
    - `*.example.com`을 설정하면 2단계, 3단계 도메인 `example.com`, `b.example.com`, `a.b.example.com`을 제한할 수 있습니다.
>!링크 도용 방지를 **활성화**하는 경우 반드시 상응하는 도메인을 입력해야 합니다.
6. 설정 완료 후 [저장]을 클릭하면 활성화됩니다.
![](https://main.qcloudimg.com/raw/ab894ac9faf520c07454d87eb10c2b37.png)

## FAQ
링크 도용 방지에 대해 궁금한 사항은 COS FAQ의 [데이터 보안](https://intl.cloud.tencent.com/document/product/436/40946) 문서에서 확인할 수 있습니다.
