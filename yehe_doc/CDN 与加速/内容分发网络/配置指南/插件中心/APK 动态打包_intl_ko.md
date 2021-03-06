## 기능 소개

APK 동적 패킹 플러그 인 기능은 단말 사용자 요청 URL의 특정 매개변수를 식별하고, CDN 엣지에서 해당 매개변수의 정보를 동적으로 APK에 입력하여 CDN 엣지에서 APK에 대한 동적 패킹을 구현합니다. APK 동적 패킹은 Tencent Cloud COS를 원본 서버로 사용합니다.

>? 
>-APK 동적 패킹은 알파 테스트 기능입니다. [신청 양식 제출](https://cloud.tencent.com/apply/p/1qkg1qkomyyj)을 통해 체험 신청이 가능합니다. 이미 신청을 완료한 경우, 5일(영업일) 이내에 신청 양식에 대한 심사를 진행합니다.
>- 현재 중국 내 노드에서만 APK 동적 패킹 기능을 지원합니다.


## 적용 시나리오

- App 다중 채널 전송. 예를 들어, 앱 스토어, 제휴 광고, 검색 엔진, 퍼포먼스 광고 등 다양한 채널을 수동 점검 없이 이용하려는 경우
- App 재부팅. APK 패키지에 동적으로 링크를 삽입하여 App을 처음으로 활성화하고 자동으로 지정 페이지에 리디렉션할 경우

## 사용 프로세스

1. CDN 콘솔의 플러그 인 센터에 로그인해 APK 동적 패킹 플러그 인 기능 관련 설정을 완료합니다.
2. 기존 APK를 COS 원본 서버의 지정한 업로드 디렉터리에 업로드합니다.
3. CDN 노드가 설치 패키지를 처리할 때까지 기다립니다.
4. 단말 사용자가 매개변수를 지닌 요청을 보냅니다.
5. CDN 엣지가 동적 패킹된 APK 파일을 반환합니다.

![](https://main.qcloudimg.com/raw/b26dede3d5ba4947bb5645c4db81f741.png)

## 설정 가이드

### 1단계: 동적 패킹 설정 추가
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하고 메뉴에서 [플러그 인 센터]를 선택합니다. APK 동적 패킹 플러그 인 기능 카드의 on/off 버튼을 클릭하여 APK 동적 패킹을 활성화하면 설정 추가 페이지로 이동합니다. 기능이 활성화되면 카드 하단의 [기본 설정], [용량 통계]를 통해 해당하는 설정 리스트와 용량 조회 페이지로 이동할 수 있습니다.
![](https://main.qcloudimg.com/raw/1c8a690040b028e7913376d22bf0dccd.png)
- 버킷 선택: COS 원본 서버를 선택합니다. 해당 기능은 반드시 **베이징/상하이/광저우/청두**의 COS를 원본 서버로 사용해야 합니다.
- 적용 도메인: 시스템이 자동으로 해당 COS를 원본 서버의 도메인으로 채용해 해당 도메인을 APK 배포에 사용합니다. 직접 추가하거나 삭제할 수도 있습니다.
- 업로드 디렉터리: 기존 APK의 COS 내 업로드 디렉터리를 설정합니다. 설정 후 기존 APK를 수동으로 해당 디렉터리에 업로드합니다.
- 출력 디렉터리: CDN 노드가 처리한 설치 패키지를 출력할 디렉터리를 설정합니다. 기존 APK를 업로드한 후 시스템은 자동으로 마스터 패키지를 처리 및 생성하고 해당 디렉터리에 업로드합니다. **요청 URL을 구성할 때 업로드 디렉터리가 아닌 해당 디렉터리를 지정하십시오.**
- 서명 방식: 현재 Android V1/V2 서명 방식을 채용하는 APK에 동적 패킹을 지원합니다. V2 서명은 WALLE/VASDOLLY 등 오픈 소스 다중 채널 패킹 방안을 지원합니다. 또한 지정한 사용자 정의 Block ID에 주석 정보를 입력할 수 있습니다.
- 채널 매개변수: `comment`로 고정되어 수정할 수 없습니다.
- SCF 설정: 권한 부여 후, 시스템이 설정에 따라 자동으로 SCF를 생성합니다.

>!SCF 콘솔에서 SCF를 삭제하지 마십시오!




### 2단계: 기존 APK 업로드

[COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 기존 APK를 지정한 업로드 디렉터리에 업로드합니다.

>?기존 APK 크기는 10GB를 초과할 수 없습니다.


### 3단계: 설치 패키지 처리 완료 대기

APK 동적 패킹 기능 페이지에서 [설치 패키지 상태]를 클릭하여 설치 패키지에 대한 CDN 노드 처리 상황을 조회합니다.
![](https://main.qcloudimg.com/raw/88450f16367a81e7c977a339f1de5b1f.png)

### 4단계: 동적 패킹 URL 배포

설치 패키지 처리가 끝나면 동적 패킹 URL를 배포할 수 있습니다. 구체적인 예시는 다음과 같습니다.

```
버킷: example.cos.ap-chengdu.myqcloud.com
적용 도메인: www.example.com
업로드 디렉터리: /src
출력 디렉터리: /ext
채널 매개변수: comment
채널 이름: pipeline
apk 이름: test.apk
```

해당하는 배포 URL: `https://www.example.com/ext/test.apk?comment=pipeline`

해당 URL을 요청하면 CDN 엣지가 `pipeline` 채널 정보가 입력된 APK 패킷을 가져올 수 있습니다.

## 요금 설명

- APK 동적 패킹 기능은 유료이며, 요금에 대한 자세한 내용은 Tencent Cloud 고객 매니저에게 문의하십시오.
- APK에서 SCF 트리거 설치 패키지 처리 작업을 채용해 SCF 무료 체험 한도를 초과하는 경우, SCF 요금이 발생할 수 있습니다. 자세한 내용은 [SCF 무료 한도](https://intl.cloud.tencent.com/document/product/583/12282)를 참조하십시오.

