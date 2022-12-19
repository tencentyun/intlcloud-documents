COS(Cloud Object Storage)는 사전 서명된 URL을 사용하여 객체를 업로드 및 다운로드할 수 있도록 지원하며, 서명된 링크를 생성하기 위해 URL에 서명을 삽입하는 것이 원칙입니다. 서명의 유효 기간을 통해 사전 서명된 URL의 유효 기간을 제어할 수 있습니다.

사전 서명된 URL을 사용하여 다운로드할 수 있으며 임시 URL을 가져와 파일, 폴더를 공유할 수 있습니다. 또는 긴 서명 유효 기간을 설정하여 장기간 유효한 URL을 제공 받아 파일을 공유할 수도 있습니다. 세부 사항은 [파일 공유](#파일 공유)를 참고하십시오.

사전 서명된 URL로도 업로드가 가능하며, 자세한 내용은 [파일 업로드](#파일 업로드)를 참고하십시오.

<span id="파일 공유"></span>
## 파일 공유(파일 다운로드)

COS는 객체 공유를 지원하며 사전 서명된 URL을 사용하여 제한된 시간 동안 다른 사용자와 파일 및 폴더를 공유할 수 있습니다. 사전 서명된 URL의 원리는 객체 URL 뒤에 서명을 접합하는 것입니다. 서명 생성 알고리즘은 [서명 요청](https://intl.cloud.tencent.com/document/product/436/7778)을 참고하십시오.

버킷은 기본적으로 개인 읽기이며 객체 URL을 통해 직접 다운로드하면 액세스 실패 메시지가 표시됩니다. 객체 url 뒤에 유효한 서명 접합 후 **사전 서명된 URL**을 얻습니다. 서명은 신분 정보를 전달하므로 사전 서명된 URL을 사용하여 객체를 다운로드할 수 있습니다.

>?사전 서명을 생성하기 위해 영구 키를 사용해야 하는 경우 위험을 방지하기 위해 영구 키의 권한 범위를 업로드 또는 다운로드 작업으로 제한하는 것이 좋습니다. 그리고 생성된 서명의 유효 기간은 업로드 또는 다운로드 작업을 완료하는 데 필요한 가장 짧은 기간으로 설정합니다. 지정된 사전 서명된 URL의 유효 기간이 만료되면 요청이 중단되기 때문에 새 서명을 신청한 후 실패한 요청은 다시 실행해야 하며, 체크포인트 재시작을 지원하지 않습니다.

```
// 객체 URL
https://test-12345678.cos.ap-beijing.myqcloud.com/test.png

// 사전 서명된 URL(서명 값이 접합된 객체 URL)
https://test-12345678.cos.ap-beijing.myqcloud.com/test.png?q-sign-algorithm=sha1&q-ak=xxxxx&q-sign-time=1638417770;1638421370&q-key-time=1638417770;1638421370&q-header-list=host&q-url-param-list=&q-signaturexxxxxfxxxxxx6&x-cos-security-token=xxxxxxxxxxxx
```
다음 파일 공유 방법은 본질적으로 모두 자동으로 서명을 생성하고 객체 URL 뒤에 접합하며 다운로드 및 미리보기에 직접 사용할 수 있는 임시 링크를 생성합니다.


### 임시 링크 빠르게 획득(1 - 2시간 동안 유효)

콘솔 혹은 COSBrowser 툴을 통해 객체에 대한 임시 링크를 빠르게 얻을 수 있습니다.

#### 콘솔(Web 페이지)

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하여 버킷 이름을 클릭하고 ‘파일 리스트’를 입력한 다음 **세부 사항** 객체를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/aff68724b740f962e39cf1167ac2cb5b.png)
2. 객체 세부 정보 페이지로 이동하여 유효한 1시간 동안 임시 링크를 복사합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6b6b17a56e82af5c5af9143338806fc3.png)

#### COSBrowser(클라이언트)

[파일 링크 생성](https://intl.cloud.tencent.com/document/product/436/32565) 문서를 참고하여, 루트 계정 키를 사용하여 최대 2시간의 임시 링크를 획득하고, 서브 계정 키를 사용하여 최대 1.5일의 임시 링크를 획득합니다.

### 사용자 정의 시간의 임시 링크 가져오기

#### 서명 툴 사용

**시나리오에 적합: 프로그래밍에 익숙하지 않은 사용자**

작업 순서는 다음과 같습니다.
1. 파일 링크: [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인 하여 객체 세부 사항에서 서명 없이 ‘객체 주소’를 가져옵니다.
2. [API Keys 관리](https://console.cloud.tencent.com/cam/capi)에서 SecretId와 SecretKey를 가져옵니다.
3. COS 서명 툴을 클릭하여 서명 링크를 가져옵니다.
유효 기간: 초, 분, 시 및 일 레벨 설정을 지원합니다.


#### SDK를 사용하여 일괄적으로 사전 서명된 URL 가져오기

**시나리오에 적합: 임시 링크 일괄 가져오기, 프로그래밍 기반의 사용자**

콘솔과 COSBrowser에서 얻은 임시 링크는 유효 기간이 짧으며, 더 긴 임시 링크가 필요한 경우 SDK를 사용하여 사전 서명된 URL을 생성할 수도 있습니다. 이는 서명 기간을 제어하여 구현할 수 있습니다. 생성 방법은 [사전 서명된 URL을 통해 다운로드](https://intl.cloud.tencent.com/document/product/436/14116)를 참고하여 익숙한 개발 언어를 선택하십시오.

임시 키 또는 영구 키를 사용하여 사전 서명된 URL을 생성할 수 있습니다. 둘의 차이점은 임시 키는 최대 유효 기간이 36시간을 넘지 않고 영구 키는 만료되지 않는다는 점으로 이는 사전 서명된 URL의 유효 기간에 간접적인 영향을 미칩니다. 

**영구 키를 사용하여 사전 서명된 URL 생성(임의 기간)**

영구 키는 만료되지 않으며 사전 서명된 URL의 유효 기간은 설정한 서명 유효 기간에 따라 결정됩니다. SDK의 사전 서명된 URL 방법을 직접 호출할 수 있습니다. 작업 단계는 다음과 같습니다.
1. secret_id, secret_key, region 등을 입력하여 client를 초기화합니다.
2. 버킷 이름, 객체 이름 및 서명 유효 기간을 입력하여 사용자 지정 기간으로 사전 서명된 URL을 생성합니다. 자세한 내용은 다음 언어별 SDK 문서를 참고하십시오.
<table>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37680">Android SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31520">C SDK</td>
<td><a href="https://cloud.tencent.com/document/product/436/35163">C++ SDK</td>
<td><a href="https://cloud.tencent.com/document/product/436/32873">.NET SDK</a>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31528">Go SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37690">iOS SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31536">Java SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31540">JavaScript SDK</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32455">Node.js SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31544">PHP SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31548">Python SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31711">미니프로그램 SDK</a></td>
</tr>
</table>


**임시 키로 사전 서명된 URL 생성(36시간 이내)**

프런트 엔드 다이렉트 업로드 시나리오에서는 임시 키를 사용해야 하는 경우가 많습니다. 임시 키에 대한 설명 및 생성 가이드는 다음을 참고하십시오.
- [임시 키를 사용한 COS 액세스](https://intl.cloud.tencent.com/document/product/436/45242)
- [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)
- [프런트엔드에서 COS로 다이렉트 업로드 시 임시 자격 증명 사용 보안 가이드](https://intl.cloud.tencent.com/document/product/436/35265)

임시 키의 최대 유효 기간은 36시간이며, 사전 서명된 URL의 유효 기간은 귀하가 설정한 서명의 유효 기간과 임시 키의 유효 기간의 최소값입니다. 서명의 유효 기간을 X로 설정하고 임시 키의 유효 기간을 Y로, 링크의 실제 유효 시간을 T라고 가정합니다.
```
T=min(X,Y); X<=36 이므로 T<=36.
```
임시 키로 사전 서명된 URL을 생성하려면 다음 두 단계가 필요합니다.
1. [임시 키 획득](https://intl.cloud.tencent.com/document/product/436/14048#.E8.8E.B7.E5.8F.96.E4.B8.B4.E6.97.B6.E5.AF.86.E9.92.A5).
2. 임시 키 획득 후 영구 키와 유사한 함수를 사용하여 사전 서명된 URL을 생성할 수 있습니다. 임시 키로 client를 초기화하기 위해서는 SecretId, SecretKey 뿐만 아니라 token도 입력해야 하며 'x-cos-security-token' 매개변수가 전달된다는 점에 유의해야 합니다. 자세한 내용은 다음 언어별 SDK 문서를 참고하십시오.
<table>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37680">Android SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31520">C SDK</td>
<td><a href="https://cloud.tencent.com/document/product/436/35163">C++ SDK</td>
<td><a href="https://cloud.tencent.com/document/product/436/32873">.NET SDK</a>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31528">Go SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37690">iOS SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31536">Java SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31540">JavaScript SDK</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32455">Node.js SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31544">PHP SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31548">Python SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31711">미니프로그램 SDK</a></td>
</tr>
</table>

<span id="파일 업로드"></span>
## 폴더 공유

폴더는 특별한 객체이며 콘솔 또는 COSBrowser 툴을 통해 폴더를 공유할 수 있습니다. 자세한 내용은 [폴더 공유](https://intl.cloud.tencent.com/document/product/436/42387)를 참고하십시오.

## 파일 업로드
기본적으로 버킷과 객체는 개인 소유입니다. 3rd party가 버킷에 객체를 업로드할 수 있지만 CAM 계정 혹은 임시 키 사용을 원치 않는 경우 임시 업로드 작업을 완료하기 위해 URL 사전 서명을 사용해 3rd party에게 서명을 제출합니다. 유효한 서명 URL을 받은 계정은 모두 객체 업로드를 진행할 수 있습니다.

>?사전 서명을 생성하기 위해 영구 키를 사용해야 하는 경우 위험을 방지하기 위해 영구 키의 권한 범위를 업로드 또는 다운로드 작업으로 제한하는 것이 좋습니다. 그리고 생성된 서명의 유효 기간은 업로드 또는 다운로드 작업을 완료하는 데 필요한 가장 짧은 기간으로 설정합니다. 지정된 사전 서명된 URL의 유효 기간이 만료되면 요청이 중단되기 때문에 새 서명을 신청한 후 실패한 요청은 다시 실행해야 하며, 체크포인트 재시작을 지원하지 않습니다.

- 방법1: SDK를 사용하여 사전 서명된 URL 생성
각 언어 SDK는 사전 서명된 URL을 생성하고 업로드하는 방법을 제공하며, 생성 방법은 [사전 서명된 URL을 통해 업로드](https://intl.cloud.tencent.com/document/product/436/14114)를 참고하여 익숙한 개발 언어를 선택하십시오.
- 방법2: 서명 링크 자체 접합
사전 서명된 URL은 실제로 객체 URL 뒤에 접합된 서명이므로 SDK, 서명 생성 툴 등을 통해 직접 서명을 생성하고 객체 업로드를 위해 URL과 서명을 서명된 링크에 접합합니다. 그러나 서명 생성 알고리즘의 복잡성으로 인해 이 사용 방법은 일반적으로 권장되지 않습니다.
