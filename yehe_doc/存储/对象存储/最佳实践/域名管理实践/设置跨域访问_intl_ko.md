## 동일 출처 정책

동일 출처 정책은 어떤 출처에서 불러온 파일이나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하며, 악성 위험이 있는 파일을 격리하는 핵심 보안 메커니즘에 사용됩니다. 동일한 프로토콜, 동일한 도메인(또는 IP), 동일한 포트를 동일한 출처로 보며, 한 출처 내의 스크립트는 해당 출처 내의 권한만 가집니다. 즉, 해당 출처의 스크립트는 해당 출처 내의 리소스만 읽고 쓸 수 있고 다른 출처의 리소스는 액세스할 수 없습니다. 이러한 보안 제한을 동일 출처 정책이라고 합니다. 

#### 동일 출처의 정의

두 페이지의 프로토콜, 도메인, 포트(포트를 지정한 경우)가 동일한 경우 동일 출처로 봅니다. 다음 표는 `http://www.example.com/dir/page.html`과의 동일 출처를 점검하는 예시입니다.

| **URL** | **결과** | **이유** |
|:---------:|:---------:|:---------:|
| `http://www.example.com/dir2/other.html` | 성공 | 프로토콜, 도메인, 포트 동일 |
| `http://www.example.com/dir/inner/another.html` |	성공 | 프로토콜, 도메인, 포트 동일 |
| `https://www.example.com/secure.html` |	실패	| 프로토콜 불일치(HTTPS) |
| `http://www.example.com:81/dir/etc.html` |	실패 |	포트 불일치(81) |
|`http://news.example.com/dir/other.html` |	실패 |	도메인 불일치 |

#### 크로스 도메인 액세스

Cross-Origin Resource Sharing(CORS) 메커니즘은 크로스 도메인 액세스라고도 하며, Web 애플리케이션 서버에서의 크로스 도메인 액세스 제어를 허용해 크로스 도메인 데이터 전송 시 보안을 보장합니다. CORS는 브라우저 및 서버에서 모두 지원해야 하며, 현재 모든 브라우저에서 해당 기능을 지원하고, IE 브라우저는 IE10 이상의 버전만 지원합니다.

모든 CORS 통신 프로세스는 브라우저에서 자동으로 완료하며 사용자가 개입할 필요가 없습니다. 개발자 입장에서 CORS 통신과 동일 출처의 AJAX 통신은 차이가 없으며 코드도 완전히 동일합니다. 브라우저에서 AJAX의 크로스 도메인 요청을 발견하면 자동으로 일부 헤더 정보가 추가되며, 때때로 다시 한번 부가 요청이 있게 되지만 사용자는 이를 감지할 수 없습니다.

따라서 CORS 통신 구현의 핵심은 서버입니다. 서버가 CORS 인터페이스를 구현하면 바로 크로스 도메인으로 통신됩니다.

## CORS의 주요 사용 시나리오

사용자는 브라우저를 사용하는 상황에서 CORS를 사용할 수 있으며, 서버가 아닌 브라우저가 액세스 권한을 제어하기 때문에 다른 클라이언트를 사용해도 크로스 도메인 문제를 걱정하지 않아도 됩니다.

CORS의 주요 애플리케이션은 사용자의 애플리케이션 서버를 통한 중개가 필요 없이 브라우저에서 AJAX를 사용해 직접 COS 데이터에 액세스하거나 데이터의 업로드 및 다운로드를 실현합니다. 동시에 COS와 AJAX 기술을 사용한 웹 사이트는 CORS를 사용해 COS와 직접 통신하는 것을 권장합니다.

## COS의 CORS에 대한 지원

COS에서 CORS 규칙 설정을 설정하여 필요에 따라 해당 크로스 도메인 요청을 허용하거나 거부할 수 있습니다. CORS 규칙 설정은 버킷 등급에 귀속됩니다.

CORS 요청의 통과 여부는 COS의 인증 등과 완전히 독립적입니다. 즉 COS의 CORS 규칙은 CORS 관련 Header 추가 여부를 결정하는 하나의 규칙일 뿐입니다. 해당 요청을 차단할지 여부는 완전히 브라우저에 의해 결정됩니다.

현재 COS의 모든 Object 관련 인터페이스에서 CORS 관련 인증을 제공하며, 이외에도 현재 Multipart와 관련한 인터페이스에서도 CORS 인증을 완벽하게 지원합니다.

>?동일한 브라우저 상의 각 `www.a.com`와 `www.b.com` 두 페이지에서 동시에 동일한 크로스 도메인 리소스를 요청했을 때, `www.a.com`의 요청이 먼저 서버에 도달한 경우 서버는 리소스에 Access-Control-Allow-Origin 헤더를 추가하여 `www.a.com` 사용자에게 반환합니다. 이때 `www.b.com`에서 다시 요청하는 경우 서버는 Cache의 이전 요청에 대한 응답을 사용자에게 반환하여 헤더 내용과 CORS 요청이 매칭되지 않아 `www.b.com`의 요청이 실패하게 됩니다.

## CORS 설정 예시

다음은 AJAX를 사용해 COS에서 데이터를 획득할 수 있도록 설정하는 간단한 예시입니다. 예시에서 사용한 버킷(Bucket)의 권한은 공유(Public)로 설정되어 있으며, 액세스 권한이 개인 버킷(Bucket)인 경우 요청에 서명만 추가하면 되고 다른 설정은 모두 동일합니다.
다음 예시에서 사용한 버킷 이름은 corstest이며, 버킷 액세스 권한은 공개 읽기, 개인 쓰기입니다.

### 준비 과정
1. **파일에 정상적으로 액세스할 수 있는지 확인**
test.txt의 텍스트 파일을 corstest에 업로드합니다. test.txt의 액세스 주소는 `http://corstest-125xxxxxxx.cos.ap-beijing.myqcloud.com/test.txt`가 됩니다.
curl을 사용해 직접 해당 텍스트 파일에 액세스합니다. 다음 주소를 사용자의 파일 주소로 대체합니다.
```
curl http://corstest-125xxxxxxx.cos.ap-beijing.myqcloud.com/test.txt
```
test.txt 파일 반환 내용이 test이면, 해당 파일에 정상적으로 액세스할 수 있다는 의미입니다.
![](https://main.qcloudimg.com/raw/d9e4cee0e6ac49d9774bab3be46bed46.png)

2. **AJAX 기술을 사용해 파일 액세스**
이제 AJAX 기술을 사용해 직접 해당 test.txt 파일에 액세스를 시도해 봅니다.
 1. 간단한 HTML 파일을 생성하여 다음 코드를 복사한 후, 로컬에 HTML 파일로 저장하여 브라우저로 파일을 엽니다. 사용자 정의 헤더를 설정하지 않았기 때문에 해당 요청은 사전 인증이 필요 없습니다.
```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
</head>
<body>
<a href="javascript:test()">Test CORS</a>
<script>
    function test() {
        var url = 'http://corstest-125xxxxxxx.cos.ap-beijing.myqcloud.com/test.txt';
        var xhr = new XMLHttpRequest();
        xhr.open('HEAD', url);
        xhr.onload = function () {
            var headers = xhr.getAllResponseHeaders().replace(/\r\n/g, '\n');
            alert('request success, CORS allow.\n' +
                'url: ' + url + '\n' +
                'status: ' + xhr.status + '\n' +
                'headers:\n' + headers);
        };
        xhr.onerror = function () {
            alert('request error, maybe CORS error.');
        };
        xhr.send();
    }
</script>
</body>
</html>
```
 2. 브라우저에서 해당 HTML 파일을 열고 **Test CORS**를 클릭하여 요청을 발송하면 다음 오류가 나타납니다. 오류 안내: 액세스 권한이 없습니다. 오류 발생 원인은 Access-Control-Allow-Origin Header를 찾을 수 없기 때문으로, 이는 서버에서 CORS를 설정하지 않기 때문입니다.
![](https://main.qcloudimg.com/raw/db84b59f4e48ec50b3b577fa116fe7ba.jpg)
 3. 액세스에 실패한 후, 다시 Header 인터페이스로 이동해 원인을 확인하면 브라우저에서 Origin이 있는 Request를 발송했다는 것을 확인할 수 있으며, 이에 따라 해당 요청은 크로스 도메인인 것을 알 수 있습니다.
![](https://main.qcloudimg.com/raw/0ba03fd90d9e6bb59785a6ba3b17d812.jpg)
>?웹 페이지를 서버에 구축할 때 주소가 `http://127.0.0.1:8081`이면 Origin은 `http://127.0.0.1:8081`이 됩니다.

### CORS 설정
액세스 실패 원인을 확인한 후, 버킷에 관련된 CORS 설정을 하여 해당 문제를 해결할 수 있습니다. COS 콘솔에서 CORS를 설정할 수 있으며, 본 예시에서는 콘솔을 사용해 CORS를 설정하는 방법을 소개합니다. 사용자의 CORS 설정이 특별하게 복잡하지 않다면 콘솔을 사용해 CORS를 설정하는 것을 권장합니다.

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 후 **버킷 리스트**를 클릭하여 해당 버킷으로 이동하고, **보안 관리** 탭을 클릭한 뒤 페이지를 내리면 "CORS 설정"을 찾을 수 있습니다.
2. **규칙 추가**를 클릭해 첫 번째 규칙을 추가하고, 다음과 같이 가장 완화된 설정을 사용합니다.
![](https://main.qcloudimg.com/raw/6a1f4bed7f42fba69449514822759c42.png)
>! CORS 설정은 규칙 하나 하나가 모여 구성되며, 첫 번째 규칙부터 차례로 매칭하고 가장 처음에 매칭된 규칙을 기준으로 합니다.

#### 인증 결과
설정 완료 후, 다시 text.txt 텍스트 파일에 액세스를 시도합니다. 다음과 같은 결과가 나타나면 액세스 요청이 정상적으로 처리된 것입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b3725a24d973dd4799ec58ddb081dffd.jpg)

### 장애 해결 및 권장사항
크로스 도메인으로 인한 액세스 문제를 해결해야 하는 경우 CORS 설정을 다음과 같이 완화된 설정으로 설정합니다. 해당 설정은 모든 크로스 도메인 요청을 허용하며, 해당 설정 후에도 여전히 문제가 발생하는 경우 CORS가 아닌 다른 부분에서 오류가 발생한 것입니다.

가장 완화된 설정 이외에도, 더 자세한 제어 메커니즘을 설정하여 맞춤형 제어를 실현할 수 있습니다. 예를 들어, 본 예시에 다음과 같은 최소 설정을 사용해 매칭에 성공할 수 있습니다.
![](https://main.qcloudimg.com/raw/6a1f4bed7f42fba69449514822759c42.png)
따라서 대부분의 시나리오에서는 실제 필요에 따라 최소 설정을 사용해 보안성을 보장하십시오.


## CORS 설정 항목 설명

CORS 설정에는 다음과 같은 설정 항목이 있습니다.

#### 출처 Origin
크로스 도메인 요청을 허용하는 출처입니다.
- 동시에 여러 개의 출처를 지정할 수 있으며, 한 행에 하나만 입력합니다.
- `*` 설정을 지원하며, 모든 도메인을 허용한다는 의미로 권장하지 않습니다.
- `http://www.abc.com`과 같은 단일의 구체적인 도메인을 지원합니다.
- `http://*.abc.com` 형식의 두 번째 레벨 와일드카드 도메인 이름이 지원되지만 각 줄에는 `*`가 하나만 포함될 수 있습니다.
- 프로토콜명 HTTP 또는 HTTPS를 반드시 입력해야 하며, 포트가 기본값이 80이 아닌 경우 포트가 포함되어 있어야 합니다.

#### 작업 Methods
허용하는 크로스 도메인 요청 방법(1개 이상)을 열거합니다.
예시: GET, PUT, POST, DELETE, HEAD

#### Allow-Header
허용하는 크로스 도메인 요청 Header입니다.
- 동시에 여러 개의 출처를 지정할 수 있으며, 한 행에 하나만 입력합니다.
- Header는 쉽게 누락될 수 있으며, 특별히 필요한 경우가 아니라면 `*`로 설정하는 것을 장합니다. 이는 모두 허용한다는 의미입니다.
- 대소문자를 구분하지 않습니다.
- Access-Control-Request-Headers에 지정된 각 Header는 Allowed-Header의 값과 일치해야 합니다.

#### Expose-Header
브라우저에 노출되는 Header 리스트입니다. 즉, 사용자가 응용 프로그램에서 액세스하는 응답 헤더(예: Javascript의 XMLHttpRequest 객체)입니다.
- 구체적인 설정은 애플리케이션의 수요에 따라 확정되며, 기본적으로 Etag 입력을 권장합니다.
- 와일드카드 부호는 사용할 수 없으며, 대소문자를 구분하지 않고 각 행에 하나만 입력할 수 있습니다.

#### 시간 초과 Max-Age
브라우저의 특정 리소스의 선취 요청(OPTIONS 요청)에 대한 반환 결과 캐시 시간으로, 단위는 초입니다. 특별한 요구가 없는 경우 약간 크게 설정할 수 있으며(예: 60초), 해당 항목은 선택 설정 항목입니다.

