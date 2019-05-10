클라이언트 또는 API/SDK를 통해 로그를 캡처할 수 있습니다. CLS 플랫폼에 캡처된 로그는 특정 규칙에 따라 구조화됩니다.

## 캡처 방식

### API로 로그 캡처
[CLS API](https://cloud.tencent.com/document/product/614/12445)를 호출하여 CLS에 구조화된 로그를 업로드할 수 있습니다. [로그 업로드 API](https://cloud.tencent.com/document/product/614/16873) 문서를 참조하십시오.

### SDK로 로그 캡처
현재 SDK를 사용할 수 없습니다.

### LogListener 클라이언트로 실시간 로그 캡처

LogListener는 Tencent Cloud CLS가 제공하는 로그 캡처 클라이언트입니다. LogListener를 서버에 설치하면 지정된 경로의 로그를 실시간으로 캡처하고 로그의 원본 데이터에 대해 구조화 처리를 수행할 수 있습니다. 다음 절차를 완료하기만 하면 LogListener를 사용하여 캡처할 수 있습니다.

1. 서버에 Loglistener를 설치하십시오.
2. Tencent Cloud CLS 콘솔에 서버 그룹을 생성합니다.
3. 로그 토픽에 서버 그룹을 연결하고 관련 구성을 완료하십시오.

[LogListener 작업 가이드](https://cloud.tencent.com/document/product/614/17414)를 참조하십시오.

### LogListener가 로그를 성공적으로 캡처하는지 신속하게 확인하십시오.
1. 로그 인덱스를 활성화합니다. 자세한 내용은 [인덱스 활성화](https://cloud.tencent.com/document/product/614/16981)를 참조하십시오.
2. [CLS 콘솔](https://console.cloud.tencent.com/cls)에 로그인하고 [로그 인덱스]를 클릭하여 확인하십시오(로그 캡처에 잠시 지연이 있음).

## 로그 구조화

로그 구조화는 로그 데이터가 key-value 형식으로 CLS 플랫폼에 저장되는 것을 말합니다. 로그가 구조화된 후에 구조화된 로그를 다운로드하고 키 값을 지정하여 검색하거나 구조화된 방식으로 로그를 배달할 수 있습니다.

- API 캡처를 통해 구조화된 로그 데이터를 직접적으로 업로드할 수 있습니다.
- LogListener 캡처를 통해 로그 데이터 구조화 방식을 지정하고 비구조화된 로그의 원본 데이터에 대해 구조화 구문 분석을 수행할 수 있습니다. 예를 들어, 로그의 원본 데이터가 `10002345987;write;error;topic does not exist`인 경우, 로그 구문 분석을 할 때 구분 기호를 지정할 수 있습니다. 구분 기호는 세미콜론이며, 모든 키 값은 eventid action status msg입니다. 따라서 해당 로그는 네 개의 키 값 쌍, 즉 `eventid:10002345987 action:write status error msg:topic does not exist`로 구조화됩니다.

